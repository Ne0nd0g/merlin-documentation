TLS
===

.. warning::
    By default, the Merlin CLI will trust any TLS certificate presented by the Merlin Server.


The CLI will communicate with the Merlin Server over TLS. When the ``secure`` flag is set, the CLI will
verify the Server's TLS certificate. If the Server's certificate is not signed by a trusted CA, the CLI will fail to
connect. Use the ``tlsCA`` flag to specify a custom CA certificate file to validate and trust the Server's certificate.

Mutual TLS
----------

The CLI can also use mutual TLS to authenticate to the Merlin Server. The CLI must use certificates that the Server will
trust. Use the ``tlsCert`` and ``tlsKey`` flags to specify the certificate and private key files to use for mutual TLS.
The provided TLS certificate should be signed by a CA that the Server trusts.