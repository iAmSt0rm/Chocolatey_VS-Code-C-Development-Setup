# Chocolatey VS Code C Development Setup
## What it is?
A Visual Studio Code configuration that allows the *.c/.cpp* files to be compiled and the *'.exe'* file to be executed, will be created with the same name as the base *.c/.cpp* file.

## Prerequisites:
1. Chocolatey Package Manager for Windows [Downlaod Chocoaley](https://chocolatey.org/).
2. VSCode


## How to get it work?
1. Install Chocolatey on Windows
2. Open Powershell/CMD (Admin) and run *choco install mingw*.
3. Once it is installed, clone the **.vscode** folder from this repo to your current C/C++ project directory.

## Manual Setup
If you want to set it manually, follow the instructions:
1. Open the folder you have/want to begin the C/CPP project in VSCode.
2. Open Power **Command Palette** (Ctrl+Shift+P) and type *'tasks'* and select **'Tasks:Configure Task'**. It will open the **'tasks.json'** file in VSCode editor.
3. Replace all the code with the following code:
        
        {            
            "version": "2.0.0",
            "tasks": [
                {
                    "label": "echo",
                    "type": "shell",
                    "command": "g++",
                    "args": [
                        "-g", "${fileBasename}", "-o", "${fileBasenameNoExtension}"
                    ],
                    "group": {
                        "kind": "build",
                        "isDefault": true
                    }
                }
            ]
        }

4. Open Power **Command Palette** (Ctrl+Shift+P) again and type *'launch'* and select **'Debug:Open launch.json'**. It will open the **'launch.json'** file in VSCode editor.
5. Replace all the code with the following code:
       
        {
            "version": "0.2.0",
            "configurations": [
                {
                    "name": "(gdb) Launch",
                    "type": "cppdbg",
                    "request": "launch",
                    "program": "${workspaceFolder}/${fileBasenameNoExtension}.exe",
                    "args": [],
                    "stopAtEntry": false,
                    "cwd": "${workspaceFolder}",
                    "environment": [],
                    "externalConsole": true,
                    "MIMode": "gdb",
                    "miDebuggerPath": "C:\\ProgramData\\chocolatey\\lib\\mingw\\tools\\install\\mingw64\\bin\\gdb.exe", //change this if you have a different installation folder.
                    "preLaunchTask": "echo",
                    "setupCommands": [
                        {
                            "description": "Enable pretty-printing for gdb",
                            "text": "-enable-pretty-printing",
                            "ignoreFailures": true
                        }
                    ]
                }
            ]
        }

6. Open Power **Command Palette (Ctrl+Shift+P)** again and type 'configurations' and select **'C/Cpp:Edit Configurations'**. It will open the **'c_cpp_properties.json'** file in VSCode editor.
7. Replace all the code with the following code:
       
        {
            "configurations": [
                {
                    "name": "Win32",
                    "includePath": [
                        "${workspaceFolder}/**"
                    ],
                    "defines": [
                        "_DEBUG",
                        "UNICODE",
                        "_UNICODE"
                    ],
                    "compilerPath": "C:\\ProgramData\\chocolatey\\lib\\mingw\\tools\\install\\mingw64\\bin\\gcc.exe", //change this if you have a different installation folder.
                    "cStandard": "c11",
                    "cppStandard": "c++17",
                    "intelliSenseMode": "clang-x64"
                }
            ],
            "version": 4
        }

These files will be created in a folder named **'.vscode'** inside the project directory.

Now you can get your C/C++ project up and running with proper file names and degugging enabled.
