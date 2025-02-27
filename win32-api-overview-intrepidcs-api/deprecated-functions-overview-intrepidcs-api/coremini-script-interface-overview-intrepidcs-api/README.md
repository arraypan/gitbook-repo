# CoreMini Script interface Overview - intrepidcs API

The CoreMini Script Interface is a way to use functionality from Vehicle Spy in your own application.  When a CoreMini file is created in Vehicle Spy 3 it creates header files for the functions in the file and giving access to basic parameters in the script.

This section includes commands to load and interact with CoreMini scripts for Intrepid Control Systems 3G hardware.  CoreMini scripts are created using Vehicle Spy 3.  For information on creating CoreMini scripts see the help documents for Vehicle Spy 3.  The table below lists the different script interface commands and gives a short description of the command.

| Function              | Description                                                                  |
| --------------------- | ---------------------------------------------------------------------------- |
| ScriptStart           | Starts execution of a script that has been downloaded to a neoVI device      |
| ScriptStop            | Stops execution of a script running on a neoVI device                        |
| ScriptLoad            | Downloads a script to a connected neoVI device into a specified location     |
| ScriptClear           | Clears a script from a specific location on a neoVI device                   |
| ScriptStartFBlock     | Starts a function block within a script on a neoVI device                    |
| ScriptGetFBlockStatus | Returns the run status of a function block within a script on a neoVI device |
| ScriptStopFBlock      | Stops the execution of a function block within a script on a neoVI device    |
| ScriptGetScriptStatus | Stops the execution of a function block within a script on a neoVI device    |
| ScriptReadAppSignal   | Read an application signal from a script running on a neoVI device           |
| ScriptWriteAppSignal  | Set the value of an application signal in a script running on a neoVI device |
