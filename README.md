
# QUCS Installation on Linux Ubuntu Using Wine

This guide provides step-by-step instructions on how to install and run **QUCS** (Quite Universal Circuit Simulator) on Ubuntu 22.04 using **Wine**. Wine allows running Windows applications on Linux-based systems.

---

## Steps to Install QUCS on Ubuntu

### 1. Install Wine on Ubuntu

First, you need to install **Wine** on your system. Wine will allow you to run the Windows version of QUCS.

#### Add WineHQ Repository
```bash
sudo dpkg --add-architecture i386
sudo mkdir -p /etc/apt/keyrings
sudo wget -nc https://dl.winehq.org/wine-builds/winehq.key -O /etc/apt/keyrings/winehq.gpg
echo "deb [signed-by=/etc/apt/keyrings/winehq.gpg] https://dl.winehq.org/wine-builds/ubuntu/ jammy main" | sudo tee /etc/apt/sources.list.d/winehq.list
sudo apt update
```

#### Install Wine Stable Version
```bash
sudo apt install --install-recommends winehq-stable
```

#### Verify Wine Installation
```bash
wine --version
```

You should see the Wine version installed on your system.

---

### 2. Download and Extract QUCS

Now, download the QUCS Windows Portable Package from the [QUCS SourceForge page](https://sourceforge.net/projects/qucs/files/qucs-binary/).

#### Steps:
1. Download the QUCS Package (e.g., `qucs-<version>-win32-mingw482-asco-freehdl-adms.zip`): Download the latest version of the QUCS Windows portable package from SourceForge.
2. Create a directory to store the QUCS files:
   ```bash
   mkdir ~/qucs
   ```
3. Extract the downloaded file: Assuming the file is in the `~/Downloads` folder:
   ```bash
   cd ~/Downloads
   unzip qucs-<version>-win32-mingw482-asco-freehdl-adms.zip -d ~/qucs
   ```

---

### 3. Run QUCS Using Wine

To run QUCS, navigate to the extracted folder and execute the `qucs.bat` file using Wine.

#### Steps:
1. Navigate to the extracted folder:
   ```bash
   cd ~/qucs
   ```
2. Run the QUCS `.bat` file using Wine:
   ```bash
   wine qucs.bat
   ```

Wine will now execute the `qucs.bat` file, and QUCS should launch.

---

### 4. Automate Launching QUCS

For convenience, you can create a shortcut to launch QUCS from anywhere easily.

#### a. Create a Shell Script
1. Create a script in `~/bin` to make launching QUCS easier:
   ```bash
   mkdir -p ~/bin
   echo 'wine /path/to/qucs.bat' > ~/bin/qucs
   chmod +x ~/bin/qucs
   ```
2. Add `~/bin` to your `PATH`:
   ```bash
   export PATH=$PATH:~/bin
   ```
3. Add this to your `~/.bashrc` or `~/.zshrc` to make it permanent:
   ```bash
   echo 'export PATH=$PATH:~/bin' >> ~/.bashrc
   source ~/.bashrc
   ```

Now you can launch QUCS by simply typing:
```bash
qucs
```

#### b. Create a Desktop Shortcut
1. Create a `.desktop` file on your Desktop:
   ```bash
   nano ~/Desktop/QUCS.desktop
   ```
2. Add the following content to the file:
   ```ini
   [Desktop Entry]
   Name=QUCS
   Exec=wine /path/to/qucs.bat
   Path=/path/to/qucs
   Icon=/path/to/qucs/icon.png
   Terminal=false
   ```
3. Make the `.desktop` file executable:
   ```bash
   chmod +x ~/Desktop/QUCS.desktop
   ```

Now you should be able to launch QUCS either by clicking the desktop shortcut or typing `qucs` in the terminal.

---

### 5. Final Steps

Once these steps are complete, you can launch QUCS either from the terminal by typing `qucs` or by clicking the desktop shortcut.

---

## Troubleshooting

- **Wine Issues:** Ensure you have installed Wine correctly
- **Permissions:** If QUCS is not launching, check the permissions for the `qucs.bat` file and ensure Wine has access to it.
