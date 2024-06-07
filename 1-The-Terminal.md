## What is a terminal? 

A terminal or console is simply an interface where users can interact with the computer via text commands. Similar to the graphical user interface (GUI), users can issue instructions for the computer to execute - i.e. copy file, rename file, delete folder, etc. However, unlike the GUI, where interactions are conducted via mouse clicks and menu-driven interactions, when using the command line, users need to know the right text commands to issue to the computer. We will focus on the Powershell commands in this tutorial. 

### Current working directory 

Directories are separated by a backslash `\`, with the top level being the drive - i.e. `C:`. For instance, 

```Powershell
PS C:\Users\harry\Downloads>
```

indicates that my current directory is `C:\Users\harry\Downloads`, which can be accessed graphically by going from `C -> Users -> harry -> Downloads`. 

Some useful commands to remember: 

- `pwd`: get the present working directory 
- `cd <dest>`: change the directory the the destination directory. For example, running cd `C:\Users\harry` will set the current directory to `C:\Userrs\harry`

```Powershell
PS C:\Users\harry\Downloads> cd C:\Users\harry
PS C:\Users\harry>
```
- `cd ..`: change the directory the the closest parent directory. For example, the closest parent directory of `C:\Users\harry\Downloads` is `C:\Users\harry` (Without `Downloads`).

```Powershell
PS C:\Users\harry\Downloads> cd .. 
PS C:\Users\harry>
```

### Command arguments and parameters 

Most PowerShell commands, parameters to allow users to select options or provide input.

The parameters follow the command name and have the following form:


```
-<parameter_name> <parameter_value>
-<parameter_name>:<parameter_value>
```

### Workshop - command arguments

Open Powershell on your computer and follow along with the tutorial.

- Type `ni -ItemType Directory -Path newFolder`. This will create a new folder called `newFolder` in your current directory. 

- Type `ni -ItemType File -Path newFolder\firstFile.txt`. This should create a text file called `firstFile.txt` in `newFolder`. 

- Type `ni newFolder\secondFile.txt`. This should create a text file called `secondFile.txt` in `newFolder`.

- Type `ni -ItemType Directory newFolder\thirdFolder`. This should create a folder called `thirdFolder` inside `newFolder`. 

- Type `ni -ItemType Directory -Path newFolder -Name fourthFolder`. This should create a folder called `fourthFolder` inside `newFolder`.

- Type `ni -Name newFolder\fifthFile.txt`. This should create `fifthFile.txt` inside `newFolder`. 

- To confirm that all the files have been created, you will now do 
`ls newFolder`. This should show a list containing `fileFile.txt, secondFile.txt, thirdFolder, fourthFolder, and fifthFile.txt`. 

- To see only directories (folders), you can type `ls -Directory newFolder`. This should show only `thirdFolder, fourthFolder`.

- To see only files, you can type `ls -File newFolder`. This should show both `firstFile.txt, secondFile.txt, fifthFile.txt`. 

- Now, type `start newFolder`. This should open the folder `newFolder` in graphic mode. You should be able to visually check that the items `firstFile.txt, secondFile.txt, thirdFolder, fourthFolder` are there. 

- Now type `del -Recurse -Force newFolder`. This should delete `newFolder` and all of its children `firstFile.txt, secondFile.txt, thirdFolder, fourthFolder`.

- If you type `ls newFolder`. You should see an error message saying cannot find path ... because it doesn't exist. 

### Workshop explanation 

`ni` is a command to create an item in a directory. 

We use the parameter `Path` to specify the path to the new item that we want to create.
   - For `ni -ItemType Directory -Path newFolder`, `newFolder` is the new item that will be created in the current working directory.
   - For `ni -ItemType File -Path newFolder\firstItem.txt`, `firstItem.txt` will be created inside `newFolder` in the current directory. 

An item can be a directory (a folder) or a file. We use the parameter `ItemType` to specify whether the output should be a file or a folder. 
   - For `ni -ItemType Directory -Path newFolder`, `newFolder` is the new item type is a folder.
   - For `ni -ItemType File -Path newFolder\firstItem.txt`, the new item type if a file. 

Parameters have default value - i.e. we do not need to specify a value for parameters that have default values. If we don't specify the value of `Path`, it will take the default value of the current directory. This means that with the command - `ni -Name newFolder\fifthFile.txt`, the Path value is defaulted to the current path. This means `fifthFile.txt` is created inside `newFolder` in the current directory. 

Some commands accept positional arguments. This means we can specify a value without explicitly specifying the parameter associated with it. For instance, with `ni newFolder\secondFile.txt`, the value `newFolder\secondFile.txt` is associated with the parameter `Path` without us having to specify it. This is equivalent to `ni -Path newFolder\secondFile.txt`.

### To see help on specific commands:

We can use the command `help <command_name>` to read the manual on the specific command. For instance, we can access the manual of `ni`: 

```PowerShell
PS C:\Users\harry\Downloads> help ni

NAME
    New-Item

SYNTAX
    New-Item [-Path] <string[]> [-ItemType <string>] [-Value <Object>] [-Force] [-Credential <pscredential>] [-WhatIf] [-Confirm] [-UseTransaction]  [<CommonParameters>]

    New-Item [[-Path] <string[]>] -Name <string> [-ItemType <string>] [-Value <Object>] [-Force] [-Credential <pscredential>] [-WhatIf] [-Confirm] [-UseTransaction]
    [<CommonParameters>]


ALIASES
    ni


REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help New-Item -Online" or
           go to https://go.microsoft.com/fwlink/?LinkID=113353.

PS C:\Users\harry\Downloads>
```

### Understanding the output of help 

`NAME` is the official name of the command. `ALIAS` is the alternative name or the mnemonic version of the command. To Powershell, the two commands are equivalent, and the outputs of `New-Item newFile` and `ni newFile` are the same. 

`SYNTAX` describe the structure of the command and the parameters that you can provide to the command. In the `ni` example, the parameters are: 

- Path 
- ItemType 
- Name 
- Value
- Force 
- Credential
- WhatIf
- Confirm 
- UseTransaction 
- CommonParameters - other parameters. 

Items enclosed with `<string>` means that you should provide a value to it. For instance, in `ni` example, one part of the syntax was 

```
New-Item -Name <string>
```

This means the syntax accept 

```
New-Item -Name newFile.txt
``` 

where `newFile.txt` is the string value associated with the parameter `Name`. 

Parameters enclosed with `[]` means that they are optional - i.e you can call the command without having to specify the parameter. 

For instance, in the following command: 

```
New-Item -Name <string> [-Confirm]
```

the confirm parameter is optional. This means that you can invoke the command 

```
New-Item -Name newFile
```

or 

```
New-Item -Name newFile -Confirm
```

Try them to see the difference. 




To see a detailed explanation of what each parameter does, their default values and so on, you can use the command 

```Powershell
help ni -Online
```

For instance, this is the parameter write-up about `Path`: 

```
-Path
Specifies the path of the location of the new item. The default is the current location when Path is omitted. You can specify the name of the new item in Name, or include it in Path. Items names passed using the Name parameter are created relative to the value of the Path parameter.

...

Type:	String[]
Position:	0
Default value:	Current location
Required:	False
```

We see that the default value of path is the current location and its position is 0. This means that if we don't provide the value of Path, it will use the default value. If we don't associate a value with the parameter Path, the first free value is associated with the path value. 

This explains the behaviour of the commands that we use in the exercise: 

-  `ni -ItemType Directory -Path newFolder\thirdFolder` - here we specify the path for the new item which is `newFolder\thirdFolder`.
- `ni -Name newFolder\fifthFile.txt`-  here, Path is ommitted, and it takes the default value which is the current location. Here we create a file named `newFolder\fifthFile.txt` in the current location. 
- `ni -ItemType Directory -Path newFolder -Name fourthFolder` - here we specify the item name `fourthFolder` and a path `newFolder`. The item `fourthFolder` is created inside `newFolder`. 
- `ni newFolder\secondFile.txt` - here we don't specify the Path value, so the free value - i.e. value not associated with any parameter (`newFoler\secondFile.txt`) is associated with Path. 

### Some other useful commands 

- `pwd`: get present working directory 
- `cd`: to change directory 
- `ls`: list all files in the current directory
- `ni`: create a new item in the current directory 
- `del`: delete a file/directory in the current directory 
- `rni`: rename item 
- `cp`: copy item from one place to another.
- `help`: to see command syntax 
- `cat`: to read content of a file 
- `echo`: to print to the console 
- `clear`: to clear the current console 


### Exercise 

1/ Use only the terminal, in the current directory, create a new file called `greetings.txt` with the file content `print("Hello World")` - use `ni` with parameter `Value`. Use `cat` to view the content of the file. Change the file name to `greetings.py`. Run `python greetings.py` and see the output. This should print `Hello World to the screen`. Delete the file `greetings.py`. 

2/ 