# Setting Up Your Work Environment

## Downloads for Your Work Environment

Download the following tools for your work environment:
- [Python](https://www.python.org/downloads/release/python-3913/), version 3.10 is also acceptable
- [Anaconda](https://www.anaconda.com/download) (email required)
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

1. Request administrative access via the user support portal or contact Rok Andolšek/Ares Osrednikar on Microsoft Teams.
2. Use the username (AD\Workstationadmin) and password during installation when prompted for credentials. If the installation doesn't start, right-click > Run as Administrator.
3. Install all programs in `C:\Programi\` and check "ADD to path" during Python installation. For Anaconda, you can do the same thing or add the PATH manually later under system variables.

![Python Add to Path](screenshots\python_setup.png)
![Environment Variables](screenshots\anaconda_setup.png)


## Running Code

Run the code in a folder that is not on OneDrive; otherwise, you will get an error stating that you do not have access in the terminal. We suggest `C:\Programi\`.

## Database Access

You need to request permission to connect to the Datawarehouse, which contains a collection of data from multiple databases.

Blaž Dobravec manages permissions and submits access requests through Einformatik, considering NDA due to GDPR to ensure data is not exported to personal computers.

Open SSMS and connect to the server `SRVEGBIDB01p` with the default user `EGXXXX`. Under databases, find `DW.star`. Access to other databases is restricted. For more information on `DW.star`, see [sql_dwh_basics.md](06_sql_dwh_basics.md).

## Python Libraries

The use of `pip install` only works outside the corporate network; otherwise, you will get an SSL error. Therefore, use WiFi.

## Github

Inform Blaž Dobravec of your Github username so you can be added to different repositories from [EG-ResearchAndDevelopment](https://github.com/EG-ResearchAndDevelopment).
