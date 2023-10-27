Command Line Flags
==================

Merlin is composed of the following components:

* Merlin Server - The program that receives and handles Agent traffic and operator CLI commands to control the server and Agents
* Merlin Agent - The post-exploitation command and control Agent that runs on a compromised host
* Merlin CLI - The command line interface that allows operators to interact with the Merlin Server and Agents

.. note::
    This page cover the Merlin Server program


Command Line Flags
------------------

.. code-block:: text

    $ ./merlin-server -h
    Usage of merlin-server:
      -addr string
            The address to listen on for client connections (default "127.0.0.1:50051")
      -debug
            Enable debug logging
      -extra
            Enable extra debug logging
      -password string
            the password to for CLI RPC clients to connect to this server (default "merlin")
      -secure
            Require client TLS certificate verification
      -tlsCA string
            TLS Certificate Authority file path to verify client certificates
      -tlsCert string
            TLS certificate file path
      -tlsKey string
            TLS private key file path
      -trace
            Enable trace logging
      -version
            Print the version number and exit

addr
^^^^

.. note::
    The default address is ``127.0.0.1:50051``

The ``addr`` flag specifies the address to listen on for Merlin CLI connections. This **IS NOT** the interface for Merlin
Agents to connect to. The Merlin Server uses gRPC for over TLS for CLI connections.

debug
^^^^^

The ``debug`` flag enables the ``debug`` log level for the Merlin Server and writes debug logs to the log file at
``data/log/merlinServerLog.txt``.

.. code-block:: text

    {"time":"2023-10-17T14:43:27.333763628-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/authenticators/opaque.(*Authenticator).Authenticate","file":"/merlin/pkg/authenticators/opaque/opaque.go","line":78},"msg":"Received OPAQUE message","OPAQUE type":1,"Agent":"6b25e714-93fb-45e6-85c8-38963efd09d9"}
    {"time":"2023-10-17T14:43:27.333886943-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/authenticators/opaque.(*Authenticator).registrationInit","file":"/merlin/pkg/authenticators/opaque/opaque.go","line":128},"msg":"Received new agent OPAQUE user registration initialization from 6b25e714-93fb-45e6-85c8-38963efd09d9"}

extra
^^^^^

The ``extra`` flag enables the ``extra`` log level for the Merlin Server and writes extra debug logs to the log file at
``data/log/merlinServerLog.txt``. The ``extra`` level inherently enables the ``debug`` and ``trace`` levels as well.
This level is primarily used to log HTTP requests and responses that contain a lot of data.

.. code-block:: text

    {"time":"2023-10-18T21:04:12.653012066-04:00","level":"DEBUG-8","source":{"function":"github.com/Ne0nd0g/merlin/pkg/servers/http.(*Handler).agentHandler","file":"/merlin/pkg/servers/http/handler.go","line":60},"msg":"HTTP Connection Details","host":"127.0.0.1:443","uri":"/","method":"POST","protocol":"HTTP/2.0","headers":{"Accept-Encoding":["gzip"],"Authorization":["Bearer eyJhbGciOiJkaXIiLCJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwidHlwIjoiSldUIn0..71SU4sj_ilrDyCCJ.lQxvax0K4U1rcIBWAk8tF2rZ_9Jxw_hyatTMkXWAO1YKtr8F9IdNEnlK8tJE0TwnKxK0UGd5KzuwpKBvfkyJIaTPxMELRTqW71CxRgnRlsFt8GvJrnY2E8_btJthKmZAaCl3DJEPocZuYDp0rB5VQSufsG0FPoJAuCw_p-cZAJntSGzlJqrjjIHi6z_ZI60vpz4N-sQrJWbOc2et07ULute2UVKuOcDNMH5MRMOATZqyFJUJlwkw9HVsml4.gH1Z6HrchxY_9DlRMfR_NA"],"Content-Length":["735"],"Content-Type":["application/octet-stream; charset=utf-8"],"User-Agent":["Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.85 Safari/537.36"]},"content length":735,"tls negotiated protocol":"h2","tls cipher suite":4865,"tls server name":""}
    {"time":"2023-10-18T21:04:12.663746773-04:00","level":"DEBUG-8","source":{"function":"github.com/Ne0nd0g/merlin/pkg/servers/http.(*Handler).agentHandler","file":"/merlin/pkg/servers/http/handler.go","line":60},"msg":"HTTP Connection Details","host":"127.0.0.1:443","uri":"/","method":"POST","protocol":"HTTP/2.0","headers":{"Accept-Encoding":["gzip"],"Authorization":["Bearer eyJhbGciOiJkaXIiLCJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwidHlwIjoiSldUIn0..71SU4sj_ilrDyCCJ.lQxvax0K4U1rcIBWAk8tF2rZ_9Jxw_hyatTMkXWAO1YKtr8F9IdNEnlK8tJE0TwnKxK0UGd5KzuwpKBvfkyJIaTPxMELRTqW71CxRgnRlsFt8GvJrnY2E8_btJthKmZAaCl3DJEPocZuYDp0rB5VQSufsG0FPoJAuCw_p-cZAJntSGzlJqrjjIHi6z_ZI60vpz4N-sQrJWbOc2et07ULute2UVKuOcDNMH5MRMOATZqyFJUJlwkw9HVsml4.gH1Z6HrchxY_9DlRMfR_NA"],"Content-Length":["883"],"Content-Type":["application/octet-stream; charset=utf-8"],"User-Agent":["Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.85 Safari/537.36"]},"content length":883,"tls negotiated protocol":"h2","tls cipher suite":4865,"tls server name":""}

password
^^^^^^^^

.. warning::
    The default password is ``merlin`` and should always be changed to prevent unauthorized access

The ``password`` flag sets the password that Merlin CLI clients need in order to authenticate all gRPC requests.

secure
^^^^^^

The ``secure`` flag enables mutual TLS authentication requiring Merlin CLI clients to authenticate to the server.
Use the ``tlsCA`` flag to provide a Certificate Authority file to verify client certificates.

tlsCA
^^^^^

The ``tlsCA`` flag specifies the path to a Certificate Authority file to verify client certificates when the ``secure`` flag is set.

tlsCert
^^^^^^^

.. note::
    The Server will auto generate a self-signed TLS certificate if one is not provided

The ``tlsCert`` flag specifies the path to a TLS certificate file for the Server to use for TLS connections.

tlsKey
^^^^^^

The ``tlsKey`` flag specifies the path to a TLS private key file for the Server to use for TLS connections.

trace
^^^^^

The ``trace`` flag enables the ``trace`` log level for the Merlin Server and writes trace logs to the log file at
``data/log/merlinServerLog.txt``. The ``trace`` level inherently enables the ``debug`` level as well.
This level is primarily used to log the entry and exit of functions to troubleshoot.

.. code-block:: text

    {"time":"2023-10-19T07:03:44.030764364-04:00","level":"DEBUG-4","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Service).Run","file":"/merlin/pkg/services/rpc/rpc.go","line":331},"msg":"entering into function","addr":"127.0.0.1:50051"}
    {"time":"2023-10-19T07:03:44.031342997-04:00","level":"INFO","msg":"Starting gRPC server on 127.0.0.1:50051"}
    {"time":"2023-10-19T07:03:52.609812218-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Service).authenticationStream","file":"/merlin/pkg/services/rpc/rpc.go","line":325},"msg":"authentication successful","Method":"/rpc.Merlin/Listen","Client":"127.0.0.1:39536"}
    {"time":"2023-10-19T07:03:52.610193878-04:00","level":"DEBUG-4","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Server).Listen","file":"/merlin/pkg/services/rpc/rpc.go","line":129},"msg":"entering into function","in":{"id":"a07b33cd-5b46-4e5c-81bb-38d06f91f5ee"}}
    {"time":"2023-10-19T07:04:06.235845947-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Service).authentication","file":"/merlin/pkg/services/rpc/rpc.go","line":296},"msg":"authentication successful","Method":"/rpc.Merlin/GetListenerTypes","Client":"127.0.0.1:39536"}
    {"time":"2023-10-19T07:04:06.236009755-04:00","level":"DEBUG-4","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Server).GetListenerTypes","file":"/merlin/pkg/services/rpc/listener.go","line":163},"msg":"entering into function","context":{"Context":{"Context":{"Context":{"Context":{"Context":{}}}}}},"empty":{}}
    {"time":"2023-10-19T07:04:06.236749705-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Service).authentication","file":"/merlin/pkg/services/rpc/rpc.go","line":296},"msg":"authentication successful","Method":"/rpc.Merlin/GetListenerDefaultOptions","Client":"127.0.0.1:39536"}
    {"time":"2023-10-19T07:04:06.236834196-04:00","level":"DEBUG-4","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Server).GetListenerDefaultOptions","file":"/merlin/pkg/services/rpc/listener.go","line":59},"msg":"entering into function","context":{"Context":{"Context":{"Context":{"Context":{"Context":{}}}}}},"in":{"data":"HTTPS"}}
    {"time":"2023-10-19T07:04:07.968606945-04:00","level":"DEBUG","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Service).authentication","file":"/merlin/pkg/services/rpc/rpc.go","line":296},"msg":"authentication successful","Method":"/rpc.Merlin/CreateListener","Client":"127.0.0.1:39536"}
    {"time":"2023-10-19T07:04:07.968773738-04:00","level":"DEBUG-4","source":{"function":"github.com/Ne0nd0g/merlin/pkg/services/rpc.(*Server).CreateListener","file":"/merlin/pkg/services/rpc/listener.go","line":44},"msg":"entering into function","context":{"Context":{"Context":{"Context":{"Context":{"Context":{}}}}}},"in":{"options":{"Authenticator":"OPAQUE","Description":"Default HTTP Listener","Interface":"127.0.0.1","JWTKey":"ZVdxdlFUVnJhcXNQV0doRkRoV2pwWk5PSk1mRXBLTkY=","JWTLeeway":"1m","Name":"My HTTP Listener","PSK":"merlin","Port":"443","Protocol":"HTTPS","Transforms":"jwe,gob-base","URLS":"/","X509Cert":"/merlin/data/x509/server.crt","X509Key":"/merlin/data/x509/server.key"}}}

version
^^^^^^^

The ``version`` flag prints the version number of the Merlin Server and exits.

.. code-block:: text

    $ ./merlin-server -version
    Merlin Version: 2.0.0, Build: nonRelease


Logging
-------

.. note::
    The Server typically requires administrative privileges so that it can bind to an interface and TCP port.
    The log file will be created with the permissions of the user that started the Merlin Server.

The Merlin Server creates a log file in the ``data/log`` directory called ``merlinServerLog.txt`` and **ALSO** writes
messages to STDOUT where the server was executed. The default logging level is ``INFO``. Use the ``debug``, ``trace``,
and ``extra`` flags to enable more verbose logging.

.. code-block:: text

    {"time":"2023-10-17T15:37:38.91950926-04:00","level":"INFO","msg":"Created new TLS certificate","Serial":142904993534574102007199776395950920709,"Subject":["Merlin"],"NotBefore":"2023-10-17T15:37:38.91050229-04:00","NotAfter":"2024-10-22T15:37:38.910516592-04:00"}
    {"time":"2023-10-17T15:37:38.921245266-04:00","level":"INFO","msg":"Starting gRPC server on 127.0.0.1:50051"}
    {"time":"2023-10-17T15:39:27.784636096-04:00","level":"INFO","msg":"Registered new RPC client with ID 9d9a3e2a-ecee-49d5-bbc8-c95a6d5c54d6"}
    {"time":"2023-10-17T15:39:34.801648979-04:00","level":"INFO","msg":"Create new listener","protocol":"HTTPS","address":"127.0.0.1:443","name":"My HTTP Listener","id":"f726d4b2-fd2f-44aa-bb60-ea8ab3731440","authenticator":"OPAQUE","transforms":"[jwe gob-base]"}
    {"time":"2023-10-17T15:39:34.803925949-04:00","level":"INFO","msg":"Certificate was not found at: /merlin/data/x509/server.crt. Creating in-memory x.509 certificate used for this session only"}
    {"time":"2023-10-17T15:39:48.885672042-04:00","level":"INFO","msg":"New authenticated agent checkin for 0db4203d-1b5a-40cb-9800-8e75cdf04013"}

Mutual TLS
----------

The Merlin Server can be configured to use mutual TLS authentication with the Merlin CLI (not for Merlin Agent connections).
Use the ``secure`` flag to enable mutual TLS authentication and the ``tlsCA`` flag to provide a Certificate Authority
file that was used to sign the client certificates.
