# BenMAP_batchmode_for_MAC

This repo provides python script to run BenMAP on a MacBook using Wine. 

Author: Yunha Lee

Date: March 13, 2025

### 1. Install WINE and Winetricks on Your MacBook
First, install WINE and Winetricks using Homebrew. Run the following commands in Terminal:

```bash
brew install wine-stable
brew install winetricks
```

### 2. Install .NET Framework 4.5.2 with Winetricks
WINE requires the .NET Framework to run BenMAP. Use Winetricks to install .NET Framework 4.5.2:

```bash
winetricks dotnet452
```

### 3. Create a WINE Prefix
A WINE prefix is a directory that mimics a Windows environment. Set up a WINE prefix for BenMAP:

```bash
export WINEPREFIX=~/wine-benmap
```

### 4. Configure the WINE Environment
Run the WINE configuration tool. You can customize the environment if needed, but the default settings might be sufficient:

```bash
winecfg
```

### 5. Download the BenMAP Installer
Download the BenMAP installer from the US EPA website.

### 6. Install BenMAP with WINE
Run the BenMAP installer using WINE. This process is similar to installing BenMAP on a Windows machine. For example, install it under `C:\Program Files (x86)`:

```bash
wine ~/Downloads/BenMAP-CE-Installer_x64_1.5.8.29.exe
```

### 7. Running BenMAP with WINE
To open the BenMAP GUI program, use the following command:

```bash
wine ~/wine-benmap/drive_c/Program\ Files\ \(x86\)/BenMAP-CE/BenMAP.exe
```

### 8. Running BenMAP from the Command Line
If you want to run BenMAP from the command line, you need to adjust the `.ctlx` file paths to use WINE's directory format. Here's an example:

```plaintext
VARIABLES

COMMANDS

SETACTIVESETUP -ActiveSetup United States

CREATE AQG

-Filename Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/batchmode/AQG/control_co_ccs_county_inmap_2020_pm25.aqgx
-GridType County
-Pollutant PM2.5

ModelDirect

-ModelFilename Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/inmap_output/county_case/control_CO_CCS_county_inmap_2020_PM25.csv
-DSNName "Text Files"

GENERATE REPORT AuditTrail

-InputFile  Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/batchmode/AQG/control_co_ccs_county_inmap_2020_pm25.aqgx
-ReportFile Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/batchmode/AQG/control_co_ccs_county_inmap_2020_pm25.txt
```

### 9. Run BenMAP from the Command Line
To execute the `.ctlx` file via the command line, use:

```bash
wine "C:\Program Files (x86)\BenMAP-CE\BenMAP.exe" "Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/batchmode/CFG/control_co_ccs_wo_NH3_VOC_county_inmap_2020_pm25_wine.ctlx"
```

### 10. Run BenMAP from python
I wrote a jupyter notebook script to run BenMAP batchmode: ./batchmode/run_benmap_Wine.ipynb
This script will run BenMAP all mode (AQG, CFG, and APV) for multiple control runs. Note the script uses "county" level. 


### Summary
- **Install WINE**: Use Homebrew to install WINE and Winetricks.
- **Set Up WINE**: Configure WINE with `winecfg` and create a WINE prefix for BenMAP.
- **Install BenMAP**: Run the BenMAP installer using WINE.
- **Run BenMAP**: Start BenMAP using WINE, either through the GUI or command line. 


### Important note
If wine benmap batchmode return "error", it can be due to .NET installation issue. 
In that case, re-try "winetricks dotnet452" to install .NET program correctly and rerun the wine batchmode command. 
```bash
winetricks dotnet452
```

You can also debug wine batchmode by running this: 
```bash
WINEDEBUG=+file wine "C:\Program Files (x86)\BenMAP-CE\BenMAP.exe" "Z:/Users/yunhalee/Documents/LOCAETA/RCM/BenMAP/batchmode/AQG/control_co_ccs_county_inmap_2020_pm25_wine.ctlx" 
```