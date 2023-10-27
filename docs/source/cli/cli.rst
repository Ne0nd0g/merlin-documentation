Command Line Flags
==================

Merlin is composed of the following components:

* Merlin Server - The program that receives and handles Agent traffic and operator CLI commands to control the server and Agents
* Merlin Agent - The post-exploitation command and control Agent that runs on a compromised host
* Merlin CLI - The command line interface that allows operators to interact with the Merlin Server and Agents

.. note::
    This page cover the Merlin Command Line Interface (CLI) program

The CLI uses Google RPC (gRPC) protocol buffers over TLS to communicate with the Merlin Server.
All API calls require a password to authenticate to the server.

.. code-block:: text

    $ ./merlin-cli -h
    Usage of merlin-cli:
      -addr string
            The address of the Merlin server to connect to (default "127.0.0.1:50051")
      -password string
            the password to connect to the Merlin server (default "merlin")
      -secure
            Require server TLS certificate verification
      -tlsCA string
            TLS Certificate Authority file path
      -tlsCert string
            TLS certificate file path
      -tlsKey string
            TLS private key file path
      -version
            Print the version number and exit

addr
----

.. note::
    The default address is ``127.0.0.1:50051``

The ``addr`` flag specifies the address of the Merlin Server to connect to. The connection uses gRPC over TLS.

password
--------

.. warning::
    The default password is ``merlin`` and should always be changed to prevent unauthorized access

The ``password`` flag sets the password needed to authenticate all gRPC requests.

secure
------

.. note::
    By default, the Merlin Server will generate a self-signed TLS certificate that will not be trusted by the CLI if this flag is enabled.

The ``secure`` flag enables TLS certificate verification. When this flag is set, the CLI will verify the Server's TLS certificate.

tlsCA
-----

The ``tlsCA`` flag specifies a custom CA certificate file to validate and trust the Server's certificate.

tlsCert
-------

The ``tlsCert`` flag specifies the certificate file the Merlin CLI will use for mutual TLS authentication with the Merlin Server.

tlsKey

The ``tlsKey`` flag specifies the private key file for the ``tlsCert``.

version
-------

The ``version`` flag prints the version number of the Merlin Server and exits.

.. code-block:: text

    $ ./merlin-cli -version
    Merlin Version: 1.0.0, Build: nonRelease
