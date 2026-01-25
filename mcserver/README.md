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


### Step 5: Run the Server
1. Start the server:
   ```
   ./start.sh
   ```
   Or directly:
   ```
   java -Xmx1024M -Xms1024M -jar server.jar nogui
   ```
   (Adjust memory as needed; 1024M is 1GB.)

2. The server will generate world files and start. You'll see output like "Server started" with the IP address.

3. To stop the server, type `stop` in the console.

### Step 6: Port Forwarding and Access
- **Local Access:** Players on the same Wi-Fi can join using your device's IP (check with `ifconfig` or `ip addr show`).
- **External Access:** For players outside your network, set up port forwarding on your router (port 19132 UDP for Bedrock). Use tools like ngrok for temporary tunneling if needed:
  ```
  pkg install ngrok
  ngrok tcp 19132
  ```
  Share the ngrok URL with friends.

- **Firewall:** Termux doesn't have a built-in firewall, but ensure your Android's firewall allows connections.

## Notes on Cross-Play
- **Bedrock Edition Only:** Cross-play works seamlessly with BDS. Players on Windows 10/11, Xbox, PlayStation, Switch, iOS, and Android can join the same server.
- **No Rooting:** This entire setup runs without root access, making it safe and easy.
- **Performance:** Android devices may not handle large servers well due to hardware limits. Start small (2-5 players) and monitor CPU/ram usage.
- **Updates:** Regularly check for BDS updates and backup your world files.
- **Troubleshooting:** If the server doesn't start, check Java installation and permissions. Use `chmod +x` on scripts if needed.

## Additional Tips
- **Backup:** Copy the `worlds` folder regularly.
- **Mods/Addons:** Bedrock supports addons; download from trusted sources.
- **Security:** Use strong passwords and monitor player activity.
- **Alternatives:** If BDS is complex, consider third-party tools like MCPE Master or apps, but Termux provides full control.

Enjoy hosting your Minecraft server on the go! If you encounter issues, check Termux forums or Minecraft communities for help.

