# Setting Up Your Work Environment

## Downloads for Your Work Environment

Download the following tools for your work environment:
- [Python](https://www.python.org/downloads/release/python-3913/), version 3.10 is also acceptable (optional python also comes with Anaconda),
- [Anaconda](https://www.anaconda.com/download) (Skip email registration, right bottom corner),
- [VSCode](https://code.visualstudio.com/download) (IDE)
- [Git](https://git-scm.com/downloads) (version control)
- [Notepad++](https://notepad-plus-plus.org/downloads/) (QOL text editor)

## Available Software on Your Computer

The Software Center includes:
- SSMS/SQL Management Studio, for database access
- QGIS, an open-source GIS program
- Greenshot, for screenshots
- ABBYY FineReader PDF, for editing PDFs
- Adobe Acrobat, for PDFs
- 7-Zip, for zip files

## Already Installed

- Microsoft Office
- Microsoft Outlook
- Microsoft Teams

## Installation

###### Disclaimer: Most likely you will still have to add all the PATH-s into system variables manually!

1. Request administrative access via the user support portal or contact Rok Andolšek/Ares Osrednikar on Microsoft Teams.
2. Use the username (AD\Workstationadmin) and password during installation when prompted for credentials. If the installation doesn't start, right-click > Run as Administrator.
3. Install all programs in `C:\Programi\`, select to install for all users and check "ADD to path" where it is possible. For Anaconda, you can do the same thing or add the PATH manually later under system variables.


![Python Add to Path](screenshots\python_setup.png)
![Environment Variables](screenshots\anaconda_setup.png)

## Anaconda configuration

###### Disclaimer: Conda only works with powershell and not CMD because of group policies

After the installation you have to complete the following steps:

1. Add The following PATH-s into your system variables (Urejanje spremenljivk delovnega okolja):

* C:\Programi\anaconda
* C:\Programi\anaconda\Scripts
* C:\Programi\anaconda\Library\bin
* C:\Programi\anaconda\python.exe

![Anaconda Add to Path](screenshots\conda_system_variables.png)

2. Add additional rights to your C:\Programi\anaconda folder (Right-click on the folder > properties > security tab) read/write and change/execute - the ones under full contol

3. Open C:\Programi\anaconda folder in your vscode and in etc > conda create 'condarc' file which serves as a global configuration file for your computer. Paste the following files into the file:

```
channels:
  - defaults
envs_dirs:
  - C:\Programi\anaconda\envs
pkgs_dirs:
  - C:\Programi\anaconda\pkgs
``` 
![condarc](screenshots\condarc.png)

4. Add condarc as a system variable into system variables as in the pitcure below 

![condarc sys variable](screenshots\condarc_sys_var.png)

5. Firstly run ```conda init``` in powershell CLI , create test environment with your python version from anaconda```conda create --name test_env python=3.11```, afterward use ```conda activate test_env ``` and check that ```pip install pandas``` in powershell works. 

## Git configuration

Add The following PATH-s into your system variables (Urejanje spremenljivk delovnega okolja):

 * C:\Programi\Git\bin
 * C:\Programi\Git\cmd

![git config](screenshots\git_config.png)

## Running Code

Run the code in a folder that is not on OneDrive; otherwise, you will get an error stating that you do not have access in the terminal. We suggest `C:\Programi\projects`.

## Database Access

You need to request permission to connect to the Datawarehouse, which contains a collection of data from multiple databases.

Blaž Dobravec manages permissions and submits access requests through Einformatik, considering NDA due to GDPR to ensure data is not exported to personal computers.

Open SSMS and connect to the server `SRVEGBIDB01p` with the default user `EGXXXX`. Under databases, find `DW.star`. Access to other databases is restricted. For more information on `DW.star`, see [sql_dwh_basics.md](06_sql_dwh_basics.md).

## Python Libraries

The use of `pip install` only works outside the corporate network; otherwise, you will get an SSL error. Therefore, use WiFi.

## Github

Inform Blaž Dobravec of your Github username so you can be added to different repositories from [EG-ResearchAndDevelopment](https://github.com/EG-ResearchAndDevelopment).
