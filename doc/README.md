## MikTeX Installation (Windows)
- Download MikTeX: Visit the MikTeX website at https://miktex.org/download.
- Click on the "Download" button to download the installer.
- Run the Installer: Double-click the downloaded installer (miktex-*.exe) and follow the on-screen instructions to complete the installation.
- Configuration: During installation, you can choose various settings for MikTeX. The default options are usually sufficient for most users.
- Updating Package Database: After installation, launch the MikTeX Console from the Start menu. Click on "Tasks" and then "Refresh file name database" to update your installed packages.

## Installing GNU Make with Chocolatey (Windows)
- Install Chocolatey (if not already installed):
Open a Command Prompt or PowerShell with administrative privileges and run the following command:
```sh
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

- Install GNU Make:
Open a new Command Prompt or PowerShell with administrative privileges and run the following command:
```sh
choco install make
```

## Compiling the LaTeX Document using `make`

To compile the document run the following command:
```sh
make
```

## Cleaning the Project using `make clean`
To clean the project and remove the intermediate files generated during compilation, run the following command in the Command Prompt or PowerShell:
```sh
make clean
```