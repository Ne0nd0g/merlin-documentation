Main Menu
=========

After executing the Merlin server binary, interaction continues from the Merlin prompt ``Merlin»``.
This is the default menu presented when starting the Merlin server.
To view available commands for this menu, type `help` and press enter.
Tab completion can be used at any time to provide the user a list of commands that can be selected.

| Merlin is equipped with a tab completion system that can be used to see what commands are available at any given time.
Hit double tab to get a list of all available commands for the current menu context.

.. code-block:: text

    Merlin» help

       COMMAND  |          DESCRIPTION           |             USAGE
    ------------+--------------------------------+---------------------------------
      !         | Execute a command on the local | ! command [args]
                | system                         |
      back      | Go to the main menu            | back
      banner    | Display the Merlin ASCII art   | banner
                | banner                         |
      clear     | Cancel all Agent jobs that     | clear
                | have not been sent             |
      debug     | Switch debug output to the     | debug
                | console on or off              |
      group     | Add, list, or remove Agent     | group {add agentID groupName
                | groupings                      | | list [groupName] |remove
                |                                | agentID groupName}
      interact  | Interact with an agent or a    | interact {agentID|listenerID}
                | listener                       |
      jobs      | Display all unfinished jobs    | jobs
      listeners | Move to the listeners menu     | listeners
      main      | Go to the Main menu            | main
      modules   | Move to the modules menu       | modules
      queue     | Queue up commands for one,     | queue {agentID|groupName}
                | multiple, unknown agents, or a | command [args]
                | group                          |
      quit      | Stop and exit Merlin           | quit [-y]
      reconnect | reconnect the CLI to a Merlin  | reconnect
                | server                         |
      remove    | Remove or delete an agent from | remove agentID
                | the server so that it will     |
                | not show up in the list of     |
                | available agents.              |
      sessions  | List established Agent         | sessions
                | sessions                       |

      socks     | Start, stop, or list a SOCKS5  | socks {list | start
                | server on the Merlin server    | [interface:]port agentID |stop
                |                                | [interface:]port agentID}
      verbose   | Switch verbose output to the   | verbose
                | console on or off              |
      version   | Display the Merlin version     | version

    Visit the wiki for additional information https://merlin-c2.readthedocs.io/en/latest/server/menu/main.html

!
-

.. note::
    USAGE: ``! command [args]``

Any command that begins with a ``!`` (a.k.a bang or exclamation point) will be executed on host itself where the Merlin
server is running. This is useful when you want simple information, such as your interface address, without having to
open a new terminal.

.. note::
    There must be a space after the ``!`` for the command to be executed.

.. code-block:: text

    Merlin» ! ip a show ens32

    [i] Executing system command...

    [+] 2: ens32: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 00:0c:29:z3:ff:91 brd ff:ff:ff:ff:ff:ff
        inet 192.168.211.221/24 brd 192.168.211.255 scope global dynamic noprefixroute ens32
           valid_lft 1227sec preferred_lft 1227sec
        inet6 fe80::a71d:1f6a:a0d1:7985/64 scope link noprefixroute
           valid_lft forever preferred_lft forever

    Merlin»

back
----

.. note::
    USAGE: ``back``

The ``back`` command go to the parent menu, typically the main menu. When the ``back`` command is executed from the
main menu, nothing will happen.

.. code-block:: text

    Merlin» back
    Merlin»

banner
------

.. note::
    USAGE: ``banner``

The ``banner`` command is used too print the super cool ascii art banner along with the version and build numbers.

.. code-block:: text

    Merlin» banner
    Merlin»


                                   &&&&&&&&
                                 &&&&&&&&&&&&
                                &&&&&&&&&&&&&&&
                              &&&&&&&&&&& &&&&
                             &&&&&&&&&&&&&  &&&&
                            &&&&&&&&&&&& &  &&&&
                           &&&&&&&&&&&&&     &&&&
                          &&&&&&&&&&&&&&&     &&&
                         &&&&&&&&&&&&&&&&&     &&&
                        &&&&&&&&&&&&&&&&&&&     &&&
                       &&&&&&&&&&&&&&&&&&&&&
                      &&&&&&&&&&&&&&&&&&&&&&&
                      &&&&&&&&&&&&&&&&&&&&&&&
                     &&&&&&&&&&&&&&&&&&&&&&&&&
                    &&&&&&&&&&&&&&&&&&&&&&&&&&&
                   &&&&&&&&&&&&&&&&&&&&&&&&&&&&&
                  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
                 &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
           &&&&  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&   &&&
        &&&&&&  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&  &&&&&&
      &&&&&&&   &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&   &&&&&&&
    &&&&&&&&&  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&  &&&&&&&&&
    &&&&&&&&&&  &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&  &&&&&&&&&&
    &&&&&&&&&&&   &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&   &&&&&&&&&&&
    &&&&&&&&&&&&&     &&&&&&&&&&&&&&&&&&&&&&&     &&&&&&&&&&&&&
      &&&&&&&&&&&&&&&          MERLIN         &&&&&&&&&&&&&&&
        &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
           &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
               &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
                       Version: 2.0.0
                       Build: nonRelease

clear
-----

.. note::
    USAGE: ``clear``

The ``clear`` command will cancel all jobs in the queue that have not been sent to the agent yet.
This command will only clear jobs for ALL agents.

.. code-block:: text

    Merlin» clear
    Merlin»
    [+] All unsent jobs cleared at 2021-08-03T01:10:09Z

debug
-----

.. note::
    USAGE: ``debug``

The ``debug`` command is a switch used to enable or disable debug output to the console.

.. code-block:: text

    Merlin» debug
    [+] 2023-10-19T12:16:13Z Debug output enabled
    Merlin» debug
    Merlin»
    [+] 2023-10-19T12:16:15Z Debug output disabled


group
-----

.. note::
    USAGE: ``group {add agentID groupName | list [groupName] |remove agentID groupName}``

The ``group`` command interacts with server-side groups that agents can be added to and removed from.
Arbitrary agent commands and modules can be executed against an entire group at one time.

* :ref:`group add`
* :ref:`group list`
* :ref:`group remove`

.. _group add:

add
^^^

.. note::
    USAGE: ``group add agentID groupName``

The ``group add`` command adds an agent to a named group. If the group name does not exist, it will be created.
The list of available agents can be tab completed.

.. code-block:: text

    Merlin» group add 99dbe632-984c-4c98-8f38-11535cb5d937 EvilCorp

    [i] Agent 99dbe632-984c-4c98-8f38-11535cb5d937 added to group EvilCorp

    Merlin» group add d07edfda-e119-4be2-a20f-918ab701fa3c EvilCorp

    [i] Agent d07edfda-e119-4be2-a20f-918ab701fa3c added to group EvilCorp

.. _group list:

list
^^^^

.. note::
    USAGE: ``group list``

The ``group list`` command displays all existing group names to include agents that are members of a group.
The ``all`` group always exists and is used to task every known agent.

.. code-block:: text

    Merlin» group list
    +----------+--------------------------------------+
    |  GROUP   |               AGENT ID               |
    +----------+--------------------------------------+
    | all      | ffffffff-ffff-ffff-ffff-ffffffffffff |
    | EvilCorp | 99dbe632-984c-4c98-8f38-11535cb5d937 |
    | EvilCorp | d07edfda-e119-4be2-a20f-918ab701fa3c |
    +----------+--------------------------------------+

.. _group remove:

remove
^^^^^^

.. note::
    USAGE: ``group remove agentID groupName``

The ``group remove`` command is used to remove an agent from a named group. The list of ALL agents is tab completable
but does not mean the agent is in the group. The list of existing groups can also be tab completed.

.. code-block:: text

    Merlin» group remove 99dbe632-984c-4c98-8f38-11535cb5d937 EvilCorp
    Merlin»
    [i] Agent 99dbe632-984c-4c98-8f38-11535cb5d937 removed from group EvilCorp

interact
--------

.. note::
    USAGE: ``interact {agentID|listenerID}``

The ``interact`` command takes one argument, the agent or listener ID. The current menu determines what type of entity
the command will interact with. The default is to interact with Agents across all menus. To interact with a Listener,
use the 'listeners' menu." Use tab completion to cycle through and select available Agents or Listeners.

.. code-block:: text

    Merlin» interact c22c435f-f7c4-445b-bcd4-0d4e020645af
    Merlin[agent][c22c435f-f7c4-445b-bcd4-0d4e020645af]»

.. code-block:: text

    Merlin» listeners
    Merlin[listeners]» interact ae0c47c8-a1ca-4d65-9627-88843be8ddbc
    Merlin[listeners][ae0c47c8-a1ca-4d65-9627-88843be8ddbc]»

jobs
----

.. note::
    USAGE: ``jobs``

The ``jobs`` command displays unfinished jobs for ALL agents when executed from the main menu.

.. code-block:: text

    Merlin» jobs

                     AGENT                 |     ID     |  COMMAND   | STATUS  |       CREATED        |         SENT
    +--------------------------------------+------------+------------+---------+----------------------+----------------------+
      d07edfda-e119-4be2-a20f-918ab701fa3c | UjNoTALgcn | pwd        | Created | 2021-08-03T01:39:57Z |
      99dbe632-984c-4c98-8f38-11535cb5d937 | UHOddpFQTm | run whoami | Sent    | 2021-08-03T01:40:11Z | 2021-08-03T01:40:17Z

modules
-------

.. note::
    USAGE: ``modules``

The ``modules`` command will move into the Modules menu.

.. code-block:: text

    Merlin» modules
    Merlin[modules]»

queue
-----

.. note::
    USAGE: ``queue {agentID|groupName} command [args]``

The ``queue`` command can be used to pre-load, or queue, arbitrary commands/jobs against an agent or a group.
Additionally, the agent does not have to exist for this command to be used.
When an agent with that ID checks in, it will receive the job.

Queue a command for one agent:

.. code-block:: text

    Merlin» queue 99dbe632-984c-4c98-8f38-11535cb5d937 run ping 8.8.8.8
    [-] Created job LumWveIkKe for agent 99dbe632-984c-4c98-8f38-11535cb5d937
    [-] Results job LumWveIkKe for agent 99dbe632-984c-4c98-8f38-11535cb5d937

    [+]
    Pinging 8.8.8.8 with 32 bytes of data:
    Reply from 8.8.8.8: bytes=32 time=42ms TTL=128
    Reply from 8.8.8.8: bytes=32 time=63ms TTL=128
    Reply from 8.8.8.8: bytes=32 time=35ms TTL=128
    Reply from 8.8.8.8: bytes=32 time=48ms TTL=128

    Ping statistics for 8.8.8.8:
        Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
    Approximate round trip times in milli-seconds:
        Minimum = 35ms, Maximum = 63ms, Average = 47ms

Queue a command for a group:

.. code-block:: text

    Merlin» queue EvilCorp run whoami

    [-] Created job lkvozuKJLW for agent d07edfda-e119-4be2-a20f-918ab701fa3c

    [-] Created job xKAgunnKTF for agent 99dbe632-984c-4c98-8f38-11535cb5d937
    Merlin»
    [-] Results job xKAgunnKTF for agent 99dbe632-984c-4c98-8f38-11535cb5d937

    [+] DESKTOP-H39FR21\bob


    [-] Results job lkvozuKJLW for agent d07edfda-e119-4be2-a20f-918ab701fa3c

    [+] rastley

Queue a command for an agent that has never checked in before and is currently unknown to the server:

.. code-block:: text

    Merlin» queue c1090dbc-f2f7-4d90-a241-86e0c0217786 run whoami
    [-] Created job rJVyZTuHkm for agent c1090dbc-f2f7-4d90-a241-86e0c0217786

.. warning::
    Some agent control commands such as ``sleep`` can not be queued because the agent structure must exist on the server to calculate the JWT

quit
----

.. note::
    USAGE: ``quit [-y]``

The ``quit`` command is used to stop and exit the Merlin server. The user will be prompted for confirmation to prevent
from accidentally quitting the program. The confirmation prompt can be skipped with ``quit -y``.

.. code-block:: text

    Merlin» quit

    Are you sure you want to exit? [yes/NO]:
    yes
    [!]Quitting...

listeners
---------

.. note::
    USAGE: ``listeners``

The ``listeners`` command will move into the Listeners menu.

.. code-block:: text

    Merlin» listeners
    Merlin[listeners]»


remove
------

.. note::
    USAGE: ``remove agentID``

The ``remove`` command is used to remove or delete an agent from the server so that it will not show up in the list of available agents.

.. note::
    Removing an active agent will cause that agent to fail to check in and it will eventually exit.

.. code-block:: text

    Merlin» sessions

    +--------------------------------------+-------------+------+--------+-----------------+--------+
    |              AGENT GUID              |  PLATFORM   | USER |  HOST  |    TRANSPORT    | STATUS |
    +--------------------------------------+-------------+------+--------+-----------------+--------+
    | c62ac059-e54d-4204-82a4-d5c054b63ac3 | linux/amd64 | joe  | DEV001 | HTTP/2 over TLS |  Dead  |
    +--------------------------------------+-------------+------+--------+-----------------+--------+

    Merlin» remove c62ac059-e54d-4204-82a4-d5c054b63ac3
    Merlin»
    [i] Agent c62ac059-e54d-4204-82a4-d5c054b63ac3 was removed from the server
    Merlin» sessions

    +------------+----------+------+------+-----------+--------+
    | AGENT GUID | PLATFORM | USER | HOST | TRANSPORT | STATUS |
    +------------+----------+------+------+-----------+--------+
    +------------+----------+------+------+-----------+--------+

    Merlin»

sessions
--------

.. note::
    USAGE: ``sessions``

The ``sessions`` command is used to quickly list information about established agents from the main menu to include their status.
The sessions command is available from any menu in the CLI.

* **AGENT GUID**: A unique identifier for every running instance
* **TRANSPORT**: The protocol the agent is communicating over
* **PLATFORM**: The operating system and architecture the agent is running on
* **HOST**: The hostname where the agent is running
* **USER**: The username that hte agent is running as
* **PROCESS**: The Agent's process name followed by its Process ID (PID) in parenthesis
* **STATUS**: The Agent's communiction status of either active, delayed, or dead
* **LAST CHECKIN**: The amount of time that has passed since the agent last checked in
* **NOTE**: A free-form text area for operators to record notes about a specific agent; tracked server-side only

.. code-block:: text

    Merlin» sessions

                   AGENT GUID              |    TRANSPORT    |   PLATFORM    |      HOST       |        USER         |                 PROCESS                  | STATUS | LAST CHECKIN |      NOTE
    +--------------------------------------+-----------------+---------------+-----------------+---------------------+------------------------------------------+--------+--------------+-----------------+
      d07edfda-e119-4be2-a20f-918ab701fa3c | HTTP/2 over TLS | linux/amd64   | ubuntu          | rastley             | main(200769)                             | Active | 0:00:08 ago  | Demo Agent Here

socks
-----

.. note::
    USAGE: ``socks {list | start [interface:]port agentID |stop [interface:]port agentID}``

The ``socks`` command is used to start, stop, or list SOCKS5 listeners. There can only be one SOCKS5 listener per agent.

* :ref:`socks2 list`
* :ref:`socks2 start`
* :ref:`socks2 stop`

.. _socks2 list:

list
^^^^

.. note::
    USAGE: ``socks list``

The ``list`` command will list active SOCKS5 listeners per agent. If the SOCKS5 listener was configured to listen on
all interfaces (e.g., 0.0.0.0), then the interface will be listed as ``[::]:``.

.. code-block:: text

    Merlin» socks list
    [i]
            Agent                           Interface:Port
    ==========================================================
    c1090dbc-f2f7-4d90-a241-86e0c0217786    127.0.0.1:9050
    7be9defd-29b8-46ee-8d38-0f3805e9233f    [::]:9051
    6d8a3a59-e484-40b3-977b-530b351106a6    192.168.1.100:9053

.. _socks2 start:

start
^^^^^

.. note::
    USAGE: ``socks start [interface:]port agentID``

.. warning::
    SOCKS5 listeners do not require authentication. Control access accordingly using firewall rules or SSH tunnels.

.. note::
    In most cases you should only bind to the loopback adapter, 127.0.0.1, to prevent unintentionally exposing the port.

The ``start`` command will start a SOCKS5 listener for the current agent. This command **requires four arguments**.
The third argument is the interface and port, or just the port, that you want to bind the listener to.
The fourth argument is the agent (tab completable) that you want to start the SOCKS5 listener for.

.. code-block:: text

    Merlin» socks start 9050 c1090dbc-f2f7-4d90-a241-86e0c0217786
    [-] Started SOCKS listener for agent c1090dbc-f2f7-4d90-a241-86e0c0217786] on 127.0.0.1:9050

.. _socks2 stop:

stop
^^^^

.. note::
    USAGE: ``socks stop [interface:]port agentID``

The ``stop`` command will stop and remove the SOCKS5 listener for the current agent. This command **requires four arguments**.
The third argument is the interface and port, or just the port, that you want to bind the listener to.
This value doesn't really matter, but it is need for consistency to keep the agent ID in the fourth spot.
The fourth argument is the agent (tab completable) that you want to start the SOCKS5 listener for.

.. code-block:: text

    Merlin» socks stop 9050 c1090dbc-f2f7-4d90-a241-86e0c0217786
    [-] Successfully stopped SOCKS listener for agent c1090dbc-f2f7-4d90-a241-86e0c0217786 on 127.0.0.1:9055

verbose
-------

.. note::
    USAGE: ``verbose``

The ``verbose`` command is a switch used to enable or disable verbose output to the console.

.. code-block::

    Merlin» verbose
    [+] 2023-10-19T12:40:44Z Verbose output enabled
    Merlin» verbose
    [+] 2023-10-19T12:40:46Z Verbose output disabled
    Merlin»

version
-------

.. note::
    USAGE: ``version``

The ``version`` command is used to simply print the version numbers of the running Merlin server.

.. code-block:: text

    Merlin» version

    Merlin version: 1.0.0.

    Merlin»

