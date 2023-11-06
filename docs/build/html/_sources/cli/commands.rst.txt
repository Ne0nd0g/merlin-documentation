Command Interface
=================

Merlin CLI commands are defined in the `commands` directory. Each command is its own file.
The following top-level directory structure is used:

* **agent** - Commands that are only accessible in the ``Merlin[agent]»`` menu, used to interact with Agent
* **all** - Commands that are accessible on all menus in the CLI
* **listeners** - Commands that are only accessible in the ``Merlin[listeners]»`` menu, used to interact with listeners
* **mainMenu** - Commands that are only accessible in the ``Merlin»`` menu
* **modules** - Commands that are only accessible in the ``Merlin[modules]»`` menu, used to interact with modules
* **multi** - Commands that are accessible in multiple menus, but not all (e.g., ``info``)

.. note::
    The ``commands/template/template.go`` file can be used as a template for new commands

New commands must implement the ``Command`` interface which has the following functions:

.. code-block:: go

	// Completer returns the data that is displayed in the CLI for tab completion depending on the menu the command is for
	// Errors are not returned to ensure the CLI is not interrupted.
	// Errors are logged and can be viewed by enabling debug output in the CLI
	Completer(m menu.Menu, id uuid.UUID) readline.PrefixCompleterInterface
	// Do executes the command and returns a Response to the caller to facilitate changes in the CLI service
	// m, an optional parameter, is the Menu the command was executed from
	// id, an optional parameter, used to identify a specific Agent, Listener, or Module
	// arguments, and optional, parameter, is the full unparsed string entered on the command line to include the
	// command itself passed into command for processing
	// Errors are returned through the Error and Message fields of the embedded messages.UserMessage struct in the Response struct
	Do(m menu.Menu, id uuid.UUID, arguments string) (response Response)
	// Help returns a help.Help structure that can be used to view a command's Description, Notes, Usage, and an example
	Help(m menu.Menu) help.Help
	// Menu checks to see if the command is supported for the provided menu
	Menu(menu.Menu) bool
	// OS returns the supported operating system the command can be executed on
	OS() os.OS
	// String returns the unique name of the command as a string
	String() string

.. note::
    Once a new command file has been added to the directory, it must be added to the ``load`` function in ``commands/repository/repository.go``