##################
Command Line Flags
##################

The following command line flags can be used when executing Merlin agent:

.. code-block:: text

    Merlin Agent
      -addr string
            The address in interface:port format the agent will use for communications (default "127.0.0.1:7777")
      -auth string
            The Agent's authentication method (e.g, OPAQUE (default "opaque")
      -debug
            Enable debug output
      -headers string
            A new line separated (e.g., \n) list of additional HTTP headers to use
      -host string
            HTTP Host header
      -ja3 string
            JA3 signature string (not the MD5 hash). Overrides -proto flag
      -killdate string
            The date, as a Unix EPOCH timestamp, that the agent will quit running (default "0")
      -listener string
            The uuid of the peer-to-peer listener this agent should connect to
      -maxretry string
            The maximum amount of failed checkins before the agent will quit running (default "7")
      -padding string
            The maximum amount of data that will be randomly selected and appended to every message (default "4096")
      -parrot string
        parrot or mimic a specific browser from github.com/refraction-networking/utls (e.g., HelloChrome_Auto)
      -proto string
            Protocol for the agent to connect with [https (HTTP/1.1), http (HTTP/1.1 Clear-Text), h2 (HTTP/2), h2c (HTTP/2 Clear-Text), http3 (QUIC or HTTP/3.0), tcp-bind, tcp-reverse, udp-bind, udp-reverse, smb-bind] (default "h2")
      -proxy string
            Hardcoded proxy to use for http/1.1 traffic only that will override host configuration
      -psk string
            Pre-Shared Key used to encrypt initial communications (default "merlin")
      -secure string
            Require TLS certificate validation for HTTP communications (default "false")
      -skew string
            Amount of skew, or variance, between agent checkins (default "3000")
      -sleep string
            Time for agent to sleep (default "30s")
      -transforms string
            Ordered CSV of transforms to construct a message (default "jwe,gob-base")
      -url string
            A comma separated list of the full URLs for the agent to connect to (default "https://127.0.0.1:443")
      -useragent string
            The HTTP User-Agent header string that the Agent will use while sending traffic (default "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.85 Safari/537.36")
      -v    Enable verbose output
      -version
            Print the agent version and exit

addr
====

The ``-addr`` flag is only used for peer-to-peer agents to specify what network address they should connect or bind to,
depending on the selected protocol. For example, ``tcp-bind`` will bind to the specified address and
``tcp-reverse`` will connect to the specified address.

auth
====

The ``-auth`` flag specifies what authentication protocol the Merlin Agent will use to communicate with the server.
The default value is ``opaque``.
The ``none`` value can be used to disable Agent authentication.

.. note::
    This value must match the listener's configuration on the server

debug
=====

By default, the Merlin Agent will not write anything to STDOUT while it is running.
The ``-debug`` flag enables debug output and facilitates troubleshooting to identify the source of a problem.

.. note::
    Windows Agents must have been compiled with debug enabled or else there will be no console window to see

headers
=======

The ``-headers`` flag is used to additional HTTP headers to add to every message.
The headers are provided as a string and must be separated by a new line (``\n``).
For example, ``-headers "X-Header1: Value1\nX-Header2: Value2"``.

host
====

The ``-host`` flag is used to specify the HTTP *Host:* header when communicating with the server.
This feature is predominately used for `Domain Fronting <https://attack.mitre.org/techniques/T1090/004/>`_.

ja3
===

`JA3 is a method for fingerprinting TLS clients on the wire <https://engineering.salesforce.com/tls-fingerprinting-with-ja3-and-ja3s-247362855967>`_.
Every TLS client has a unique signature depending on its configuration of the following TLS options:
``SSLVersion,Ciphers,Extensions,EllipticCurves,EllipticCurvePointFormats``.

The ``-ja3`` flag allows the agent to create a TLS client based on the provided JA3 hash signature.
This is useful to evade detections based on a JA3 hash for a known tool (i.e. Merlin).
`This <https://engineering.salesforce.com/gquic-protocol-analysis-and-fingerprinting-in-zeek-a4178855d75f>`_ article
documents a JA3 fingerprint for Merlin. Known JA3 signatures can be downloaded from https://ja3er.com/

**NOTE:** Make sure the input JA3 hash will enable communications with the Server. For example, if you leverage a JA3
hash that only supports SSLv2 and the server does not support that protocol, then they will not be able to communicate.
The ``-ja3`` flag will override the the ``-proto`` flag and will cause the agent to use the protocol provided in the JA3 hash.

killdate
========

The ``-killdate`` flag is used to specify the date, as an Unix epoch timestamp, that the agent should quit running.
`EpochConverter <https://www.epochconverter.com>`_ is a good resource to generate or convert a timestamp.
The default value is ``0`` which means the Agent does not have a killdate.

listener
========

The ``-listener`` flag is used to specify the UUID of the **LISTENER** that the peer-to-peer Agent is configured to connect to.
The Agent's configuration must match the Listener's configuration on the server.

.. warning::
    If the listener's UUID is not provided, the Agent will not run

maxretry
========

The ``-maxretry`` flag is the maximum amount of failed checkins before the agent will quit running. The default value is 7.

padding
=======

The ``-padding`` flag is maximum amount of data that will be randomly selected and appended to every message.
The default value is 4096 bytes. The data padding is intended to increase the detection difficulty for idle checkin
behavior when the message size was fixed everytime.

parrot
======

The ``-parrot`` flag is used to configure the HTTP TLS client to parrot or mimic a specific browser.
This setting will override the ``-ja3`` flag.
Examples of some supported values are:

* ``HelloChrome_Auto``
* ``HelloChrome_102``
* ``HelloGolang``
* ``HelloFirefox_Auto``
* ``HelloIOS_Auto``
* ``HelloEdge_Auto``
* ``HelloSafari_Auto``
* ``Hello360_Auto``
* ``HelloQQ_Auto``

A full list of options can be found in the ``u_common.go`` file in the `utls library <https://github.com/refraction-networking/utls/tree/master>`_.

proto
=====

The ``-proto`` flag specifies what protocol the Merlin Agent will use to communicate with the server

* ``http`` protocol communicates using the clear-text HTTP/1.1 protocol. This can be useful when leveraging Domain Fronting on a CDN that does not allow both fronting and TLS encrypted traffic.
* ``https`` protocol communicates using SSL/TLS encrypted HTTP/1.1 protocol.
* ``h2c`` protocol communicates using the clear-text HTTP/2 protocol. This clear-text version is not used by web browsers like Chrome and may stand out during traffic analysis. However, it also has the potential to evade detections if allowed out of the network and no network defenses are able to parse the traffic.
* ``h2`` protocol communicates using the TLS encrypted HTTP/2 protocol. This will start the connection with prior knowledge and will not negotiate from HTTP/1.1 to HTTP/2. Some web proxies will not allow HTTP/2 communications. In this case you should use ``https``. Alternatively, the HTTP/2 protocol *might* bypass network defenses or detections.
* ``http3`` protocol communicates using HTTP/2 transported over `QUIC <https://tools.ietf.org/html/draft-ietf-quic-transport-28>`_ known as `HTTP/3 <https://tools.ietf.org/html/draft-ietf-quic-http-29>`_. It is important to note that QUIC is a UDP protocol and may not be allowed of the network depending on egress filtering. QUIC uses TLS transport encryption.
* ``tcp-bind`` protocol is for peer-to-peer agents to bind to a TCP port and wait for a connection from a parent Agent
* ``tcp-reverse`` protocol is for peer-to-peer agents to connect to a TCP port on a parent Agent
* ``udp-bind`` protocol is for peer-to-peer agents to bind to a UDP port and wait for a connection from a parent Agent
* ``udp-reverse`` protocol is for peer-to-peer agents to connect to a UDP port on a parent Agent
* ``smb-bind`` protocol is for peer-to-peer agents to bind to a SMB named pipe and wait for a connection from a parent Agent
* ``smb-reverse`` protocol is for peer-to-peer agents to connect to a SMB named pipe on a parent Agent

proxy
=====

The ``-proxy`` flag is used to force HTTP/1.1 communications to go through a known proxy.
At this time the Merlin Agent **WILL NOT** automatically detect if a host is configured to use a proxy.
The HTTP/2 protocol does not support using a proxy. If a proxy is required to egress a network,
use the ``http`` or ``https`` protocols.

psk
===

The ``-psk`` flag is used to specify the Pre-Shared Key (PSK) that the Merlin Agent uses to initiate communication with
the Merlin Server. The first message is encrypted with the PSK and subsequent messages establish a new session based
encryption key using the `OPAQUE protocol <https://eprint.iacr.org/2018/163.pdf>`_ from
`this <https://tools.ietf.org/html/draft-krawczyk-cfrg-opaque-03>`__ IETF draft.
Additional information about OPAQUE can be found here:
`Merlin Goes OPAQUE for Key Exchange <https://posts.specterops.io/merlin-goes-opaque-for-key-exchange-420db3a58713>`_.

skew
====

The ``-skew`` flag is the amount of skew, or variance, between agent checkins. The default value is 3000

sleep
=====

.. note::
    You must include the unit of measurement after the number (e.g. 30s or 1m)

The ``-sleep`` flag is used to specify how long the agent will sleep between checkin attempts.
For example, ``30s`` is for thirty seconds and ``1m`` is for one minute.

Peer-to-peer bind and reverse Agents can be configured with a negative sleep value (e.g., -10s).
The actual amount doesn't matter, just that it is negative.
A negative sleep value prevents the peer-to-peer Agent from communicating on the network UNLESS it has a job.
This means there are no status checkin messages back to the Server at a fixed interval.

transforms
==========

The ``-transforms`` flag is used to specify the ordered list of transforms that will be used to construct/deconstruct a message.
The default value is ``jwe,gob-base``. The transforms are applied in the order they are specified.
The value provided to the ``-transforms`` flag **MUST** match the listener's configuration or the Agent will fail to connect.

.. note::
    The ``gob-base`` transform must be the last transform in the list to unmarshall into a Go structure

Available transforms consist of encoders and encrypters:

* ``aes`` - AES encrypt/decrypt the data
* ``base64-byte`` - Encode/decode the data to/from base64 as bytes using the `EncodeLen() <https://pkg.go.dev/encoding/base64#Encoding.EncodedLen>`_ function
* ``base64-string`` - Encode/decode the data to/from base64 as a string using the `EncodeToString() <https://pkg.go.dev/encoding/base64#Encoding.EncodeToString>`_ function
* ``hex-byte`` - Encode/decode the data to/from hex as bytes using the `EncodeLen <https://pkg.go.dev/encoding/hex#EncodedLen>`_ function
* ``hex-string`` - Encode/decode the data to/from hex as a string using the `EncodeToString <https://pkg.go.dev/encoding/hex#EncodeToString>`_ function
* ``gob-base`` - Gob encode/decode the message in to a `Merlin Base <https://github.com/Ne0nd0g/merlin-message/blob/main/messages.go>`_ message structure
* ``gob-string`` - Gob encode/decode the message in to a string
* ``jwe`` - Encode/decode the data into a `JSON Web Encryption (RFC 7516) <https://www.rfc-editor.org/info/rfc7516>`_ structure
* ``rc4`` - Encode/decode the data using the RC4 stream cipher
* ``xor`` - Encode/decode the data using the XOR cipher

The JWE transform uses the following configuration:

* Encrypter: ``A256GCM``
* Algorithm: ``PBES2_HS512_A256KW``
* PBES2Count: ``3000``

url
===

The ``-url`` flag is used to specify the Uniformed Resource Locator (URL) that the agent will attempt to communicate with.
Include the protocol (i.e. ``https``), the host (i.e. ``127.0.0.1``), the page (i.e ``/`` or ``/news.php``),
and optionally port (i.e. ``:443``).
This will result in ``https://127.0.0.1:443/``.
**NOTE:** By default the Merlin agent will communicate on the loopback adapter.

useragent
=========

The ``-useragent`` flag is the HTTP User-Agent header string that the Agent will use while sending traffic.
The default value is: ``Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.85 Safari/537.36``.

verbose
=======

The ``-v`` flag enables verbose output. By default a running Merlin Agent will not write any information to STDOUT.
This can be used to see what the agent is doing along with what commands it is receiving.

version
=======

The ``-version`` flag will print the Agent version to the screen and then exit.
