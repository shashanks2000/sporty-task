# Windows Setup Reference Guide

This is a reference guide for setting up Docker Desktop with WSL2 on Windows. The purpose is to share the essential steps for installing WSL2, enabling necessary features, using Chocolatey package manager, downloading Docker, and ensuring proper configuration.

## Step 1: Enable WSL2 (Windows Subsystem for Linux)

### Automatic Installation (Recommended)

1. Open **PowerShell** as Administrator
2. Run the following command:

   ```powershell
   wsl --install
   ```

3. Restart your computer when prompted
4. After restart, a Ubuntu terminal will open automatically to complete the setup

### Manual Installation (if automatic fails)

1. Open **PowerShell** as Administrator
2. Enable WSL feature:

   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```

3. Enable Virtual Machine Platform:

   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

4. Restart your computer
5. Download and install the [WSL2 Linux kernel update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
6. Set WSL2 as default:

   ```powershell
   wsl --set-default-version 2
   ```

7. Install Ubuntu:

   ```powershell
   wsl --install -d Ubuntu
   ```

## Step 2: Install Chocolatey Package Manager

1. Open **PowerShell** as Administrator
2. Install Chocolatey:

   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
   ```

3. Close and reopen PowerShell as Administrator
4. Verify installation:

   ```powershell
   choco --version
   ```

## Step 3: Install Docker Desktop

Using Chocolatey in **PowerShell** as Administrator:

```powershell
choco install docker-desktop -y
```

## Step 4: Install Make

```powershell
choco install make -y
```

## Step 5: Configure Docker Desktop

1. Start Docker Desktop from the Start menu
2. Go to **Settings** → **General**
3. Ensure "Use the WSL 2 based engine" is checked
4. Go to **Settings** → **Resources** → **WSL Integration**
5. Enable integration with your default WSL distro (Ubuntu)
6. Click **Apply & Restart**

## Step 6: Run the Project

Navigate to the project directory in PowerShell and use Chocolatey's make:

```powershell
cd path\to\data_analyst
make up
```

## Common Issues

- **Check if Hyper-V is disabled** (Docker Desktop with WSL2 doesn't need Hyper-V)
- **Ensure Docker Desktop is running** before executing make commands

## Verification

To verify everything is working correctly:

1. Check Docker is running:

   ```powershell
   docker --version
   docker ps
   ```

2. Check make is available through Chocolatey:

   ```powershell
   make --version
   ```

3. Test project startup:

   ```powershell
   cd path\to\data_analyst
   make up
   ```

If you see the application logs and can access the intended port, your setup is complete!

---

We hope this reference guide helps you get your development environment up and running smoothly. Wishing you the best of luck with your setup