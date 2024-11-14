
This repository was created to remember me regarding the powershell and its commands. 
## What is PowerShell 
[Microsoft learning platform](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.4) stated that PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework. PowerShell runs on Windows, Linux, and macOS. It is used in many IT-related job roles for tasks that require system management, automation, and scripting.

## who will need PowerShell
Cloud Engineers / DevOps Engineers, System Administrators, Network Administrators, Information Security Analysts, Database Administrators (DBAs),  Software Engineers, and Data Engineers

## 1. How to open PowerShell
- **PowerShell in Windows**: Go to the Start menu, type “PowerShell,” and select **Windows PowerShell** or **Windows PowerShell ISE** (the Integrated Scripting Environment).
- **Run as Administrator**: Right-click on PowerShell and choose "Run as Administrator" if elevated permissions are needed.

## 2. Basic PowerShell Commands
Here are some basic commands to help you get familiar with PowerShell.

| Command             | Description                                           |
|---------------------|-------------------------------------------------------|
| `Get-Help`          | Displays help about commands and syntax.              |
| `Get-Command`       | Lists all available commands in PowerShell.           |
| `Get-Process`       | Displays currently running processes.                 |
| `Get-Service`       | Lists all services on the computer.                   |
| `Get-Location`      | Shows the current directory.                          |
| `Set-Location`      | Changes the current directory (similar to `cd`).      |
| `Clear-Host` (or `cls`) | Clears the console screen.                     |
| `Get-Content`       | Reads the contents of a file.                         |

**Example**:
```powershell
Get-Help Get-Process
```
This displays information on how to use the `Get-Process` command.

## 3. Navigating the File System

PowerShell allows you to navigate the file system, just like you would in a traditional command line:
- **Change directory**: `Set-Location` or `cd`
  ```powershell
  Set-Location "C:\path\to\your\directory"
  ```
- **List files and folders**: `Get-ChildItem` or `ls`
  ```powershell
  Get-ChildItem
  ```

## 4. Managing Files and Folders

PowerShell provides simple commands to create, copy, move, and delete files and directories.

| Command                  | Description                                   |
|--------------------------|-----------------------------------------------|
| `New-Item`               | Creates a new file or folder.                 |
| `Copy-Item`              | Copies a file or folder.                      |
| `Move-Item`              | Moves a file or folder.                       |
| `Remove-Item`            | Deletes a file or folder.                     |

**Examples**:
```powershell
# Create a new text file
New-Item -Path "C:\path\to\your\file.txt" -ItemType File

# Copy a file
Copy-Item -Path "C:\path\to\your\file.txt" -Destination "C:\path\to\new\location\"

# Move a file
Move-Item -Path "C:\path\to\your\file.txt" -Destination "C:\path\to\new\location\"

# Delete a file
Remove-Item -Path "C:\path\to\your\file.txt"
```

## 5. Viewing and Filtering Data

PowerShell is highly effective for viewing and filtering data, especially for system information and file content.

- **Filter with `Where-Object`**:
  ```powershell
  Get-Process | Where-Object { $_.CPU -gt 100 }
  ```
  This shows only processes using more than 100 units of CPU time.

- **Select specific properties** with `Select-Object`:
  ```powershell
  Get-Process | Select-Object -Property Name, CPU
  ```
  This displays only the `Name` and `CPU` columns of each process.

## 6. Using Variables

You can store data in variables for later use in PowerShell by prefixing the variable name with `$`.

```powershell
$myVariable = "Hello, PowerShell!"
$number = 42
```

To print a variable’s value:
```powershell
Write-Output $myVariable
```

## 7. Writing and Reading Text Files

PowerShell makes it easy to create, write, and read text files.

- **Write text to a file**:
  ```powershell
  "Hello, PowerShell!" | Out-File -FilePath "C:\path\to\your\file.txt"
  ```
- **Read text from a file**:
  ```powershell
  Get-Content -Path "C:\path\to\your\file.txt"
  ```

## 8. Running Loops and Conditional Statements

PowerShell supports loops (`for`, `foreach`, `while`) and conditional statements (`if`, `else`) for automating tasks.

- **For loop**:
  ```powershell
  for ($i = 1; $i -le 5; $i++) {
      Write-Output "Number: $i"
  }
  ```

- **If statement**:
  ```powershell
  $num = 5
  if ($num -gt 3) {
      Write-Output "$num is greater than 3"
  } else {
      Write-Output "$num is less than or equal to 3"
  }
  ```

## 9. Working with Processes and Services

- **List running processes**:
  ```powershell
  Get-Process
  ```

- **Stop a process**:
  ```powershell
  Stop-Process -Name "notepad" -Force
  ```

- **List services**:
  ```powershell
  Get-Service
  ```

- **Start or stop a service**:
  ```powershell
  Start-Service -Name "wuauserv"   # Start Windows Update service
  Stop-Service -Name "wuauserv"    # Stop Windows Update service
  ```

## 10. Using PowerShell to Automate Tasks

PowerShell’s scripting capabilities let you automate complex tasks by writing scripts (`.ps1` files) that run a series of commands.

- **Create a Script**:
  1. Open a text editor (such as Notepad) and write your commands.
  2. Save the file with a `.ps1` extension, such as `MyScript.ps1`.

- **Run a Script**:
  ```powershell
  .\MyScript.ps1
  ```
  Ensure that PowerShell’s execution policy allows scripts to run:
  ```powershell
  Set-ExecutionPolicy RemoteSigned
  ```
## 11 monitor a text file for new lines
- to get all lines in txt file
```powershell
Get-Content -Path "C:\path\to\your\file.txt" -Wait
```
- to append text to a file
```powershell
Add-Content -Path "C:\path\to\your\file.txt" -Value "Your text to append"
```
- to replace text in a file
```powershell
(Get-Content -Path "C:\path\to\your\file.txt") -replace 'old text', 'new text' | Set-Content -Path "C:\path\to\your\file.txt"
```
- to edit specific line
```powershell
# Read the file into an array, where each line is an element
$file = Get-Content -Path "C:\path\to\your\file.txt"

# Modify a specific line (e.g., line 2)
$file[1] = "This is the new content for line 2"

# Write the modified content back to the file
$file | Set-Content -Path "C:\path\to\your\file.txt"
```
- to insert Text at a Specific Line
```powershell
$file = Get-Content -Path "C:\path\to\your\file.txt"

# Insert text at a specific line (e.g., insert after line 2)
$newContent = @("Inserted line")
$file = $file[0..1] + $newContent + $file[2..($file.Count - 1)]

# Write the modified content back to the file
$file | Set-Content -Path "C:\path\to\your\file.txt"
```
- to remove Lines from a File
```powershell
$file = Get-Content -Path "C:\path\to\your\file.txt"

# Remove line 2 (e.g., by omitting index 1)
$file = $file | Where-Object { $_ -ne $file[1] }

# Write the updated content back to the file
$file | Set-Content -Path "C:\path\to\your\file.txt"
```
- to monitor a File for Real-Time Updates
```powershell
Get-Content -Path "C:\path\to\your\file.txt" -Tail 10 -Wait
```


## 12. Tips and Best Practices

- **Use Aliases**: Many common PowerShell commands have aliases (`ls` for `Get-ChildItem`, `cd` for `Set-Location`, `cat` for `Get-Content`). Use them for quicker access.
- **Piping (`|`)**: Use the pipeline to chain commands together for efficient processing.
- **Error Handling**: Use `Try` and `Catch` blocks to manage errors in scripts.

## Example Script: Automate Backup

To copy files from one folder to another, then create a backup:

```powershell
$source = "C:\path\to\source\folder"
$destination = "C:\path\to\backup\folder"

# Create the backup folder if it doesn't exist
if (!(Test-Path -Path $destination)) {
    New-Item -ItemType Directory -Path $destination
}

# Copy files
Copy-Item -Path "$source\*" -Destination $destination -Recurse
Write-Output "Backup completed successfully!"
```

## Further Learning

- **Explore cmdlets**: Use `Get-Command` and `Get-Help` to discover and learn new cmdlets.
- **Microsoft PowerShell Documentation**: Microsoft offers comprehensive documentation, tutorials, and example scripts.


