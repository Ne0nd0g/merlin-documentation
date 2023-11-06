#######
Logging
#######

The Merlin CLI program creates a log file in the current working directory named `merlinClientLog.txt`.
This file contains log data about the CLI program itself along with the executed commands and their output.

.. code-block:: text

    {"time":"2023-10-26T09:46:50.660713487-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).Run","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":143},"msg":"Starting Merlin version: 0.0.0, build: nonRelease, client ID: 891bf3bc-2474-43c8-8ee0-072427b4ecbc"}
    {"time":"2023-10-26T09:46:50.700554795-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).displayUserMessages.func1","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":558},"msg":"[+] 2023-10-26T13:46:50Z Succesfully connected to Merlin server at 127.0.0.1:50051"}
    {"time":"2023-10-26T09:47:07.157172376-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).handle","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":201},"msg":"Command entered: listeners"}
    {"time":"2023-10-26T09:47:12.776028985-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).handle","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":201},"msg":"Command entered: interact dc61d4c9-9114-4482-a09e-f33e13aa8541"}
    {"time":"2023-10-26T09:47:15.236683208-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).handle","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":201},"msg":"Command entered: main"}
    {"time":"2023-10-26T09:47:17.430615308-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).handle","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":201},"msg":"Command entered: interact 617d2d8f-5349-4532-8d7e-12b342589897"}
    {"time":"2023-10-26T09:47:19.725450154-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).handle","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":201},"msg":"Command entered: run whoami"}
    {"time":"2023-10-26T09:47:19.75005658-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).displayUserMessages.func1","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":544},"msg":"[-] 2023-10-26T13:47:19Z Created job oHcHIcojhs for agent 617d2d8f-5349-4532-8d7e-12b342589897 at 2023-10-26T13:47:19Z"}
    {"time":"2023-10-26T09:47:44.849542612-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).displayUserMessages.func1","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":544},"msg":"[-] 2023-10-26T13:47:44Z Results of job oHcHIcojhs for agent 617d2d8f-5349-4532-8d7e-12b342589897 at 2023-10-26T13:47:44Z"}
    {"time":"2023-10-26T09:47:44.849670815-04:00","level":"INFO","source":{"function":"github.com/Ne0nd0g/merlin-cli/services/cli.(*Service).displayUserMessages.func1","file":"/home/rastley/Dev/merlin-cli/services/cli/cli.go","line":558},"msg":"[+] 2023-10-26T13:47:44Z Created whoami process with an ID of 353566\nrastley\n"}