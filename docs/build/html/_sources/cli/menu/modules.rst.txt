############
Modules Menu
############

The module menu context is used to interact with, and configure, a module.
Use the ``modules`` command to enter the modules menu from any other menu.

Prefix any command with ``help`` (e.g., ``help run``) to view the command's help information.
Use any of the following flags after a command name to view the help information for that command:
``help``, ``-h``, ``--help``, ``?``, ``/?``

While the help information below shows a number of commands, only the following commands are unique to just the
``modules`` menu:

* :ref:`info<info2>`
* :ref:`reload`
* :ref:`run<run2>`
* :ref:`set`
* :ref:`show`

Help menu from the root ``modules`` menu:

.. code-block:: text

    Merlin» modules
    Merlin[modules]» help

       COMMAND  |          DESCRIPTION           |             USAGE
    ------------+--------------------------------+--------------------------------
      !         | Execute a command on the local | ! command [args]
                | system                         |
      back      | Go to the main menu            | back
      banner    | Display the Merlin ASCII art   | banner
                | banner                         |
      clear     | Cancel all Agent jobs that     | clear
                | have not been sent             |
      debug     | Switch debug output to the     | debug
                | console on or off              |
      interact  | Interact with an agent or a    | interact {agentID|listenerID}
                | listener                       |
      listeners | Move to the listeners menu     | listeners
      main      | Go to the Main menu            | main
      modules   | Move to the modules menu       | modules
      quit      | Stop and exit Merlin           | quit [-y]
      sessions  | List established Agent         | sessions
                | sessions                       |
      use       | Select a protocol to create a  | use protocol
                | listener for                   |
      verbose   | Switch verbose output to the   | verbose
                | console on or off              |

Help menu from a selected module:

.. code-block:: text

    Merlin[modules]» use windows/x64/powershell/powersploit/Invoke-Mimikatz
    Merlin[modules][windows/x64/powershell/powersploit/Invoke-Mimikatz]» help

       COMMAND  |          DESCRIPTION           |             USAGE
    ------------+--------------------------------+--------------------------------
      !         | Execute a command on the local | ! command [args]
                | system                         |
      back      | Go to the main menu            | back
      banner    | Display the Merlin ASCII art   | banner
                | banner                         |
      clear     | Cancel all Agent jobs that     | clear
                | have not been sent             |
      debug     | Switch debug output to the     | debug
                | console on or off              |
      info      | Show information about the     | info
                | module                         |
      interact  | Interact with an agent or a    | interact {agentID|listenerID}
                | listener                       |
      listeners | Move to the listeners menu     | listeners
      main      | Go to the Main menu            | main
      modules   | Move to the modules menu       | modules
      quit      | Stop and exit Merlin           | quit [-y]
      reload    | reload the module to reset the | reload
                | module's state                 |
      run       | Execute the module             | run
      sessions  | List established Agent         | sessions
                | sessions                       |
      set       | set the value of a             | set key value
                | configurable module option     |
      show      | Show the module's configurable | show
                | options                        |
      verbose   | Switch verbose output to the   | verbose
                | console on or off              |

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

.. _back:

back
----

.. note::
    USAGE: ``back``

The ``back`` command is used to leave the Module menu and return back to the :doc:`main`.

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» back
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
This command will only clear jobs for the current agent.

.. code-block:: text

    Merlin[agent][c1090dbc-f2f7-4d90-a241-86e0c0217786]» clear
    [+] jobs cleared for agent c1090dbc-f2f7-4d90-a241-86e0c0217786

debug
-----

.. note::
    USAGE: ``debug``

The ``debug`` command is a switch used to enable or disable debug output to the console.

.. code-block:: text

    Merlin[agent][13f6ebee-78ec-4414-a04c-74188b95c01c]» debug
    [+] 2023-10-19T12:16:13Z Debug output enabled
    Merlin[agent][13f6ebee-78ec-4414-a04c-74188b95c01c]» debug
    [+] 2023-10-19T12:16:15Z Debug output disabled

.. _info2:

info
----

.. note::
    USAGE: ``info``

The ``info`` command command is used to print all of the information about a module to the screen.
This information includes items such as module's name, authors, credits, description, notes, and configurable options.

.. code-block:: text

    Merlin[modules][windows/x64/powershell/powersploit/Invoke-Mimikatz]» info
    [i] 2023-10-25T02:50:48Z
    'Invoke-Mimikatz' module information

    Platform:
            windows\x64\PowerShell
    Module Authors:
            Russel Van Tuyl (@Ne0nd0g)
    Credits:
            Joe Bialek (@JosephBialek)
            Benjamin Delpy (@gentilkiwi)
    Description:
            This script leverages Mimikatz 2.2.0 and Invoke-ReflectivePEInjection to reflectively load Mimikatz completely in memory. This allows you to do things such as dump credentials without ever writing the mimikatz binary to disk. The script has a ComputerName parameter which allows it to be executed against multiple computers. This script should be able to dump credentials from any version of Windows through Windows 8.1 that has PowerShell v2 or higher installed.
    Options:

          NAME     | VALUE | REQUIRED |          DESCRIPTION
    ---------------+-------+----------+---------------------------------
      Agent        |       | true     | Agent on which to run module
                   |       |          | Invoke-Mimikatz
      DumpCreds    | true  | false    | [Switch]Use mimikatz to dump
                   |       |          | credentials out of LSASS.
      DumpCerts    |       | false    | [Switch]Use mimikatz to export
                   |       |          | all private certificates
                   |       |          | (even if they are marked
                   |       |          | non-exportable).
      Command      |       | false    | Supply mimikatz a custom
                   |       |          | command line. This works
                   |       |          | exactly the same as running
                   |       |          | the mimikatz executable
                   |       |          | like this: mimikatz
                   |       |          | "privilege::debug exit" as an
                   |       |          | example.
      ComputerName |       | false    | Optional, an array of
                   |       |          | computernames to run the
                   |       |          | script on.
    Notes:
            Invoke-Mimikatz.ps1 is currently part of the Empire project https://github.com/BC-SECURITY/Empire and was originally part of the PowerSploit project https://github.com/PowerShellMafia/PowerSploit

interact
--------

.. note::
    USAGE: ``interact {agentID|listenerID}``

The ``interact`` command takes one argument, the agent ID, and is used to switch agents and interact with a different, specified agent.

.. note::
    Use the built-in tab completion to cycle through and select the agent to interact with.

.. code-block:: text

    Merlin[module][BASH]» interact c1090dbc-f2f7-4d90-a241-86e0c0217786
    Merlin[agent][c1090dbc-f2f7-4d90-a241-86e0c0217786]»

listeners
---------

.. note::
    USAGE: ``listeners``

The ``listeners`` command moves to the Listeners menu.

.. code-block:: text

    Merlin[agent][c1090dbc-f2f7-4d90-a241-86e0c0217786]» listeners
	Merlin[listeners]»

main
----

.. note::
    USAGE: ``main``

The ``main`` command is used to leave the Agent menu and return back to the :doc:`main`. It is an alias for the back_ command.

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» main
    Merlin»

.. _reload:

reload
------

.. note::
    USAGE: ``reload``

The ``reload`` command is used to clear out all of a module's configurable options and return its settings to the default state.

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» reload
    [+] 2023-10-25T03:15:51Z The 'Invoke-Mimikatz' module was reloaded

.. _run2:

run
---

.. note::
    USAGE: ``run``

The ``run`` command is used to execute the module on the agent configured for the module's [agent](#set-agent) value.

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» run
    Merlin[module][Invoke-Mimikatz]» [-]Created job iReycchrck for agent ebf1b1d2-44d5-4f85-86f5-cae112600870
    [+]Results for job iReycchrck
    [+]
      .#####.   mimikatz 2.1 (x64) built on Nov 10 2016 15:31:14
     .## ^ ##.  "A La Vie, A L'Amour"
     ## / \ ##  /* * *
     ## \ / ##   Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
     '## v ##'   http://blog.gentilkiwi.com/mimikatz             (oe.eo)
      '#####'                                     with 20 modules * * */
    <snip>
    Merlin[module][Invoke-Mimikatz]»

sessions
--------

.. note::
    USAGE: ``sessions``

The ``sessions`` command is used to quickly list information about established agents from the module menu to include their status.
The sessions command is available from any menu in the CLI.

.. code-block:: text

    Merlin[module][BASH]» sessions

                   AGENT GUID              |    TRANSPORT    |   PLATFORM    |      HOST       |        USER         |                 PROCESS                  | STATUS | LAST CHECKIN |      NOTE
    +--------------------------------------+-----------------+---------------+-----------------+---------------------+------------------------------------------+--------+--------------+-----------------+
      d07edfda-e119-4be2-a20f-918ab701fa3c | HTTP/2 over TLS | linux/amd64   | ubuntu          | rastley             | main(200769)                             | Active | 0:00:08 ago  | Demo Agent Here

.. _set:

set
---

The ``set`` command is used to set the value for one of the module's configurable options.
This command is used by specifying the name of the option that should be set followed by a value.
Tab completion is enabled and provides a list of all configurable options.

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» set DumpCerts true
    [+]DumpCerts set to true
    Merlin[module][Invoke-Mimikatz]»

.. _set-agent:

set Agent
^^^^^^^^^

The `Agent` *option* for every module must be set in order for it have a target to execute on.
By default, the module is configured with a blank value of ``00000000-0000-0000-0000-000000000000``.
To set an agent, provide the agent's ID (tab completion enabled).

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» set Agent c1090dbc-f2f7-4d90-a241-86e0c0217786
    [+]agent set to c1090dbc-f2f7-4d90-a241-86e0c0217786
    Merlin[module][Invoke-Mimikatz]»


The special value ``all`` can be provided and instructs Merlin to execute the module on all agents.
When this value is provided, the module's agent option is set to all F's like: ``ffffffff-ffff-ffff-ffff-ffffffffffff``

.. code-block:: text

    Merlin[module][Invoke-Mimikatz]» set Agent all
    [+] 2023-10-25T03:20:59Z set 'Agent' to: all

.. _show:

show
----

.. note::
    USAGE: ``show``

The ``show`` command is used to show the module's configurable options

.. code-block:: text

    Merlin[modules][windows/x64/powershell/powersploit/Invoke-Mimikatz]» show
    [i] 2023-10-25T03:24:12Z
    'Invoke-Mimikatz' module options

          NAME     | VALUE | REQUIRED |          DESCRIPTION
    ---------------+-------+----------+---------------------------------
      Agent        |       | true     | Agent on which to run module
                   |       |          | Invoke-Mimikatz
                   |       | false    |
                   |       | false    |
                   |       | false    |
                   |       | false    |
      DumpCreds    | true  | false    | [Switch]Use mimikatz to dump
                   |       |          | credentials out of LSASS.
      DumpCerts    |       | false    | [Switch]Use mimikatz to export
                   |       |          | all private certificates
                   |       |          | (even if they are marked
                   |       |          | non-exportable).
      Command      |       | false    | Supply mimikatz a custom
                   |       |          | command line. This works
                   |       |          | exactly the same as running
                   |       |          | the mimikatz executable
                   |       |          | like this: mimikatz
                   |       |          | "privilege::debug exit" as an
                   |       |          | example.
      ComputerName |       | false    | Optional, an array of
                   |       |          | computernames to run the
                   |       |          | script on.

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
