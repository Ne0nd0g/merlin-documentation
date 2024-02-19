############
Custom Build
############

This section details how to build custom build a Merlin Agent using the Make file.

**NOTE:** Merlin is distributed with pre-compiled agent binaries for all major platforms in the ``data/bin`` directory.

Basic
-----

The provided Make file can be used to build a new agent from **source**. It is recommended that you first use
``go get github.com/Ne0nd0g/merlin-agent`` to pull a copy of the Merlin source code to the host. Move into the Merlin root
directory where the Make file is located.

* Windows agent: ``make windows``
* Linux agent: ``make linux``
* macOS agent: ``make darwin``
* MIPS agent: ``make mips``
* ARM agent: ``make arm``

Advanced
--------

Use the provided Make file to build a Merlin Agent with hard coded values. This removes the need for an operator to use
commandline arguments and allows the Agent to simply be executed. The table below shows configurable compile options

View the :doc:`Listeners </cli/listeners>` page for additional information on specific listener configurable options.

.. csv-table:: Build Options
   :header: "Option", "Description", "Notes"
   :widths: auto

    ADDR, The interface and port for peer-to-peer agents to bind or connect to, Overrides the ``-addr`` flag
    AUTH, The method of Agent authentication to the server, Overrides the ``-auth`` flag
    HEADERS, Comma Separated list of HTTP headers to send with every HTTP request., Overrides the ``-headers`` flag
    HOST, HTTP Host header, Overrides the ``-host`` commandline flag
    HTTPCLIENT, "The type of HTTP client (or driver) to use (e.g., go or winhttp)", Overrides the ``-http-client`` commandline flag
    JA3, JA3 signature string (not the MD5 hash), Overrides the ``-ja3`` commandline flag
    KILLDATE, "The date, as a Unix EPOCH timestamp, that the agent will quit running", Overrides the ``-killdate`` commandline flag
    LISTENER, The UUID of the listener that the peer-to-peer agent is configured to communicate with., Overrides the ``-listener`` flag
    RETRY, The maximum amount of failed checkins before the agent will quit running, Overrides the ``-maxretry`` commandline flag
    PAD, The maximum amount of data that will be randomly selected and appended to every message, Overrides the ``-padding`` commandline flag
    PARROT, Configure the HTTP client's TLS configuration to match the provided browser string, Overrides the ``-parrot`` commandline flag
    PROTO, "Protocol for the agent to connect with [https (HTTP/1.1), http (HTTP/1.1 Clear-Text), h2 (HTTP/2), h2c (HTTP/2 Clear-Text), http3 (QUIC or HTTP/3.0)] (default 'h2')", Overrides the ``-proto`` commandline flag
    PROXY, Hardcoded proxy to use for http/1.1 traffic only that will override host configuration, Overrides the ``-proxy`` commandline flag
    PSK, Pre-Shared Key used to encrypt initial communications (default "merlin"), Overrides the ``-psk`` commandline flag
    SECURE, Require TLS certificate validation for HTTP communications, Overrides the ``-secure`` commandline flag
    SKEW, "Amount of skew, or variance, between agent checkins", Overrides the ``-skew`` commandline flag
    SLEEP, "The amount of time the Agent will sleep between checkins Must use golang time notation (e.g., ``10s`` for ten seconds)", Overrides the ``-sleep`` command line flag
    TAGS, Comma separated list of Go build tags for compiling the agent, Overrides Go's ``-tags`` commandline flag
    TRANSFORMS, Ordered CSV of transforms to construct a message with, Overrides the ``-transforms`` commandline flag
    URL, Full URL for agent to connect to (default "https://127.0.0.1:443"), Overrides the ``-url`` commandline flag
    USERAGENT, The HTTP User-Agent header string that Agent will use while sending traffic, Overrides the ``-useragent`` commandline flag

An example of creating a new Linux HTTP agent that is using domain fronting through ``https://merlin.com/c2endpoint.php`` using a PSK of ``SecurePassword1``:

``make linux URL=https://merlin.com:443/c2endpoint.php HOST=myendpoint.azureedge.net PROTO=https PSK=SecurePassword1``

Build Tags
----------

By default, the Merlin Agent is built with all available features and components compiled in.
Build tags can be used to control what features are compiled into the agent to reduce the size of the binary or to
restrict the agent's capabilities.

When any build tag is included, the agent will ONLY include that feature and nothing else.
For example, if ONLY the ``http`` tag is provided, the SMB, TCP, and UDP clients will not be included.

The following build tags are available:

.. csv-table:: Build Tags
   :header: "Tag", "Description", "Notes"
   :widths: auto

    http, Include ALL HTTP clients,
    http1, Include Go's built-in HTTP/1.1 client, Used with the ``-proto`` flag's ``http`` & ``https`` options
    http2, Include the HTTP/2 client, Used with the ``-proto`` flag's ``http2`` & ``h2c`` options
    http3, Include the HTTP/3 UDP client, Used with the ``-proto`` flag's ``http3`` option
    mythic, Include the Mythic C2 client, Used with the Mythic C2 Framework's `http <https://github.com/MythicC2Profiles/http>`_ profile
    smb, Include the SMB client, Used with the ``-proto`` flag's ``smb-bind`` & ``smb-reverse`` options
    tcp, Include the TCP client, Used with the ``-proto`` flag's ``tcp-bind`` & ``tcp-reverse`` options
    udp, Include the UDP client, Used with the ``-proto`` flag's ``udp-bind`` & ``udp-reverse`` options

Windows Agent
-------------

The Windows Merlin Agent executable is compiled as a GUI application instead of console application. The Merlin Agent
does not have a GUI component. The reason this is used is so that the Merlin Agent window disappears after it is executed.
This behavior is intentional so that the user will not see the application window. This is done with the LDFLAGS when
building the agent using the ``-H=windowsgui`` option as shown `here <https://golang.org/cmd/link/>`_

This causes problems when a user **WANTS** to see the Merlin Agent verbose or debug output. To view Merlin verbose/debug
output, use the Makefile ``windows-debug`` target (e.g., ``make windows-debug``)

Cross-Compiling
---------------

The Merlin agent and server can be cross-compiled to any operating system or architecture.
A list of golang supported operating systems and architectures can be found here: https://golang.org/doc/install/source#environment

.. csv-table:: Supported Platforms
   :header: "$GOOS", "$GOARCH"
   :widths: auto

    android,arm
    darwin,386
    darwin,amd64
    darwin,arm
    darwin,arm64
    dragonfly,amd64
    freebsd,386
    freebsd,amd64
    freebsd,arm
    linux,386
    linux,amd64
    linux,arm
    linux,arm64
    linux,ppc64
    linux,ppc64le
    linux,mips
    linux,mipsle
    linux,mips64
    linux,mips64le
    netbsd,386
    netbsd,amd64
    netbsd,arm
    openbsd,386
    openbsd,amd64
    openbsd,arm
    plan9,386
    plan9,amd64
    solaris,amd64
    windows,386
    windows,amd64
