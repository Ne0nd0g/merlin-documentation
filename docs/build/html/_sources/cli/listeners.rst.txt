#########
Listeners
#########

This page covers information about listener configurations

Introduction
============

Listeners are instantiated on the Merlin Server and are how Merlin Agents communicate with the server.
Listeners are configured through the Merlin CLI.
Listeners contain the configuration that the Merlin Server uses to understand Merlin Agent traffic.
Some Listeners have an associated associated server, like an HTTP server, not to be confused with the Merlin Server.
Peer-to-peer Listeners do not have a server because traffic is passed to them through delegate messages, they don't
actually bind to a network interface.

Available Listener types are:

* **HTTP** - Uses the HTTP/1.1 protocol to communicate with Merlin Agents without TLS
* **HTTPS** - Uses the HTTP/1.1 protocol to communicate with Merlin Agents with TLS
* **H2C** - Uses the HTTP/2 clear-text protocol to communicate with Merlin Agents without TLS
* **HTTP2** - Uses the HTTP/2 protocol to communicate with Merlin Agents with TLS
* **HTTP3** - Uses the UDP-based HTTP/3 protocol (HTTP/2 over QUIC) to communicate with Merlin Agents with TLS
* **SMB** - Processes messages for SMB-based peer-to-peer Agents but does not listen for traffic itself, just handling
* **TCP** - Processes messages for TCP-based peer-to-peer Agents but does not listen for traffic itself, just handling
* **UDP** - Processes messages for UDP-based peer-to-peer Agents but does not listen for traffic itself, just handling

Core Configuration Options
==========================

The following configuration options are standard across all Listener types:

* :ref:`Authenticator`
* :ref:`Description`
* :ref:`ID`
* :ref:`Name<Listener Name>`
* :ref:`Protocol`
* :ref:`PSK`
* :ref:`Transforms`

.. _Authenticator:

Authenticator
--------------

The ``Authenticator`` configuration option is used to set what method of authentication is used by the Merlin Agent to
authenticate to the server.

The following options are available:

* **OPAQUE** - This is the default option and uses the `OPAQUE <https://datatracker.ietf.org/doc/draft-irtf-cfrg-opaque/>`_ Asymmetric Password Authenticated Key Exchange (PAKE)
* **None** - This option disables authentication and allows any Merlin Agent to connect to the Listener

.. _Description:

Description
-----------

The ``Description`` configuration option is used to set a description for the Listener.
Mainly used by operators to describe the purpose of the Listener.

.. _ID:

ID
--

The ``ID`` is a UUID for the instantiated listener tracked on the Merlin Server.
If this value is not set, a random one will be generated when the Listener is created.

The ``ID`` field can be set to a specific UUID before it is created.
This is useful when the Server is restarted and the Listener needs to be recreated.
It is also useful when a peer-to-peer Agent was configured to communicat with a specific Listener ID does not exist.

.. _Listener Name:

Name
----

The ``Name`` configuration option is used to set a name for the Listener.
Mainly used by operators to identify the listener in tables displayed in the Merlin CLI.

.. _Protocol:

Protocol
--------

The ``Protocol`` configuration option is used to set what protocol the Listener will use to communicate with the Merlin Agent.

.. note::
    Because peer-to-peer listeners do not have an associated server, there are not separate types for bind and reverse

The following options are available:

* **HTTP** - Uses the HTTP/1.1 protocol to communicate with Merlin Agents without TLS
* **HTTPS** - Uses the HTTP/1.1 protocol to communicate with Merlin Agents with TLS
* **H2C** - Uses the HTTP/2 clear-text protocol to communicate with Merlin Agents without TLS
* **HTTP2** - Uses the HTTP/2 protocol to communicate with Merlin Agents with TLS
* **HTTP3** - Uses the UDP-based HTTP/3 protocol (HTTP/2 over QUIC) to communicate with Merlin Agents with TLS
* **SMB** - Processes messages for SMB-based peer-to-peer Agents but does not listen for traffic itself, just handling
* **TCP** - Processes messages for TCP-based peer-to-peer Agents but does not listen for traffic itself, just handling
* **UDP** - Processes messages for UDP-based peer-to-peer Agents but does not listen for traffic itself, just handling

.. _PSK:

PSK
---

.. warning::
    The default PSK is ``merlin`` and should not be used

The ``PSK`` configuration option is used to set the pre-shared key that is used to encrypt traffic between the Merlin Agent and the Listener.

.. _Transforms:

Transforms
----------

The ``Transforms`` option is used to specify the ordered list of transforms that will be used to construct/deconstruct a message.
The default value is ``jwe,gob-base``. The transforms are applied in the order they are specified.

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

.. _HTTP:

HTTP Configuration Options
==========================

The following configuration options are specific to HTTP-based Listeners:

* :ref:`Interface<HTTP Interface>`
* :ref:`JWTKey`
* :ref:`JWTLeeway`
* :ref:`Port<HTTP Port>`
* :ref:`URLS`
* :ref:`X509Cert`
* :ref:`X509Key`

.. _HTTP Interface:

Interface
---------

The ``Interface`` configuration option is used to set the network interface that the Listener will bind to.
The default is the loopback adapter at ``127.0.0.1``.

.. note::
    Use ``0.0.0.0`` as a shortcut for all interfaces

.. _JWTKey:

JWTKey
------

The ``JWTKey`` configuration option is used to set the key that is used to sign & encrypt the JWTs that Merlin Agents
use to authenticate to the HTTP server. The key is represented as a base64 encoded string.

This is useful when the Merlin Server has restarted but existing Merlin Agents are still using the old key.
However, Merlin Agent's can recover if a new JWTKey is used so long as the PSK matches.

If a JWTKey is excluded, or set to an empty value, then JWTs will not be used by the HTTP server to authenticate Merlin Agents.
This is useful to disable using JWTs all together.

.. _JWTLeeway:

JWTLeeway
---------

The ``JWTLeeway`` configuration option is used to set the leeway for JWTs that are used to authenticate Merlin Agents.
The Leeway is the amount of time difference, or skew, that is allowed between the Merlin Agent and the Merlin Server.
This is very common for systems that are not synchronized with NTP such as virtual machines.

If the time between the Server and the Agent is greater than the leeway, the JWT will be rejected and the Agent message will be rejected.

.. _HTTP Port:

Port
----

The ``Port`` configuration option is used to set the port that the Listener will bind to.

.. _URLS:

URLS
----

The ``URLS`` configuration option is used to set the URLs that the HTTP server can receive Merlin Agent traffic on.
Provide a comma separated list of URLs as a string.
The HTTP server will reject Agent messages that are received on URLs not in the list.

.. _X509Cert:

X509Cert
--------

The ``X509Cert`` configuration option is used to set the X509 certificate that the HTTP server will use server TLS connections.

.. note::
    If a valid certificate path is not provided, the server will generate a self-signed certificate

.. _X509Key:

X509Key
-------

The ``X509Key`` configuration option is used to set the X509 key that the HTTP server will use to encrypt traffic.

.. _SMB:

SMB Configuration Options
=========================

.. _Pipe:

Pipe
----

The ``Pipe`` configuration option is used to set the named pipe that peer-to-peer SMB communications will occur on.
Only include the name of the pipe. Do not include the UNC path or the interface.

The SMB listener does not have an associated server, so the listener itself does not create or listen on the named pipe.
It is just used to identify the configuration the Agent will use.

.. _TCP:

TCP Configuration Options
=========================

.. _TCP Interface:

Interface
---------

The ``Interface`` configuration option is used to set the network interface that peer-to-peer Agents will bind or connect to.

The TCP listener does not have an associated server, so the listener itself does not create or listen on the named pipe.
It is just used to identify the configuration the Agent will use.

.. _TCP Port:

Port
----

The ``Port`` configuration option is used to set the port that peer-to-peer Agents will bind or connect to.

The TCP listener does not have an associated server, so the listener itself does not create or listen on the named pipe.
It is just used to identify the configuration the Agent will use.

.. _UDP:

UDP Configuration Options
=========================

.. _UDP Interface:

Interface
---------

The ``Interface`` configuration option is used to set the network interface that peer-to-peer Agents will bind or connect to.

The UDP listener does not have an associated server, so the listener itself does not create or listen on the named pipe.
It is just used to identify the configuration the Agent will use.

.. _UDP Port:

Port
----

The ``Port`` configuration option is used to set the port that peer-to-peer Agents will bind or connect to.

The UDP listener does not have an associated server, so the listener itself does not create or listen on the named pipe.
It is just used to identify the configuration the Agent will use.
