FAQ
===

* :ref:`How do I see help information for a command in the CLI?<help>`
* :ref:`How do I reconnect to the Merlin Server without restarting the CLI?<reconnect faq>`

.. _help:

help
----

How do I see help information for a command in the CLI?

The help information for any command can be retrieved by prefixing the command with `help`.
Alternatively, the following flags can be used after the command to retrieve help information:
``help``, ``-h``, ``--help``, ``?``, ``/?``

.. code-block:: text

    Merlin» help socks
    [i] 2023-10-19T12:45:35Z 'socks' command help

    Description:
            Start, stop, or list a SOCKS5 server on the Merlin server
    Usage:
            socks {list | start [interface:]port agentID |stop [interface:]port agentID}
    Example:

    Notes:
            There can only be one SOCKS5 listener per agent.
            SOCKS5 listeners do not require authentication. Control access accordingly using firewall rules or SSH tunnels.

.. code-block:: text

    Merlin» socks /?
    [i] 2023-10-19T12:46:00Z 'socks' command help

    Description:
            Start, stop, or list a SOCKS5 server on the Merlin server
    Usage:
            socks {list | start [interface:]port agentID |stop [interface:]port agentID}
    Example:

    Notes:
            There can only be one SOCKS5 listener per agent.
            SOCKS5 listeners do not require authentication. Control access accordingly using firewall rules or SSH tunnels.

.. _reconnect faq:

reconnect
---------

How do I reconnect to the Merlin Server without restarting the CLI?

Use the ``reconnect`` command to re-establish a connection to the Merlin Server.

.. code-block:: text

    Merlin»
    [!] 2023-10-19T12:49:14Z there was an error receiving a message from the server stream: rpc error: code = Unavailable desc = error reading from server: EOF
    Merlin» reconnect
    [+] 2023-10-19T12:49:41Z Successfully reconnected to the server at 127.0.0.1:50051
