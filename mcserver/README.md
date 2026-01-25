# How to make a Minecraft Server in Termux with Cross-Play Support (Without Root)

## Introduction
Setting up a Minecraft server on your Android device using Termux is a great way to host a multiplayer world without needing a dedicated computer or rooting your phone. Termux is a powerful terminal emulator that runs a Linux environment on Android, and it doesn't require root access. This guide focuses on setting up a Java Edition server, which supports cross-play on Bedrock Edition.

## Requirements
- **Android Device:** Any Android phone or tablet running Android 7.0 or higher.
- **Termux App:** Download and install Termux from F-Droid or the official website (Google Play Store version may have limitations).
- **Storage Space:** At least 1-2 GB free space for the server files.
- **Internet Connection:** Stable Wi-Fi or mobile data for downloading and hosting.


## Step-by-Step Guide

### Step 1: Install and Update Termux
1. Install Termux from F-Droid (recommended) or the official source.
2. Open Termux and update the package list:
   ```
   pkg update && pkg upgrade
   ```
3. Install essential package:
   ```
   pkg install  wget 
   ```

### Step 2: Install Java
We need to install Java first. Below are the supported Java versions for running a Minecraft server in Termux:

```sh
pkg install openjdk-17
pkg install openjdk-21
```
`Note: if you are you using an  older Android versions then  use openjdk-17 because older versions does not support openjdk-21`

Verify the installation of java:
```
java -version
```

### Step 3: Download and Set Up Server 
1. Create a directory for the server:
   ```
   mkdir mcserver && cd mcserver
   ```
2. Choose Minecraft Version Based on Java Version (IMPORTANT)

   `Note: The Minecraft server version you can run **depends entirely on the Java version installed**.`
---
### Java Version Compatibility
- **openjdk-17**
  - Supports Minecraft **1.17 – 1.20.4**
  - Best choice for **older or low-end phones**
- **openjdk-21**
  - Required for Minecraft **1.20.5+**
  - Needed to run **latest versions like 1.21.11**

> ⚠️ Using the wrong Java version will cause the server to crash or fail to start.
---
 3. Download and Install the Server (PaperMC)
 ### What is PaperMC?
- PaperMC is a high-performance Minecraft Java Edition server software. It is more optimized and uses less RAM than the official Mojang server, making it suitable - for running on Android devices using Termux.

### For openjdk-17 users (Minecraft 1.20.4)
``` 
wget https://api.papermc.io/v2/projects/paper/versions/1.20.1/builds/196/downloads/paper-1.20.1-196.jar
```

### For openjdk-21 users (Minecraft 1.21.11)
```
wget https://api.papermc.io/v2/projects/paper/versions/1.21.11/builds/1/downloads/paper-1.21.11-1.jar
```
### Note
- If you want to download **other Minecraft versions**, you can visit the **PaperMC version list** on the official PaperMC website and copy the download link for your desired version.
- If you want to use **other server software** (such as **Vanilla**, **Spigot**, **Fabric**, or **Forge**), you can download their server `.jar` file from their official websites and install it in the same way using `wget` with the provided download link.
### Rename the Server File (Step by Step)

After downloading the PaperMC server file, you should rename it to `server.jar`.  
This avoids confusion and makes it easier to run the server later.

#### Step 1: List the files in the directory
Use the `ls` command to see the downloaded file name. You will see a file name similar to one of these:
- `paper-1.20.1-196.jar`
- `paper-1.21.11-1.jar`

#### Step 2: Rename the file using `mv`
Copy the exact file name shown by `ls`, then use the `mv` command to rename it.

**Example for Minecraft 1.20.1 (openjdk-17):**
```
mv paper-1.20.1-196.jar server.jar
```
**Example for Minecraft 1.21.11 (openjdk-21):**
```
mv paper-1.21.11-1.jar server.jar
```
#### Step 3: Confirm the rename
Run `ls` again You should now see: ```server.jar``` 
