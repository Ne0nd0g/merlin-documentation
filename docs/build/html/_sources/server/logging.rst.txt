Logging
=======


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