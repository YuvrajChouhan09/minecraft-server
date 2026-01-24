# How to Set Up a Minecraft Server in Termux with Cross-Play Support (No Rooting Required)

## Introduction
Setting up a Minecraft server on your Android device using Termux is a great way to host a multiplayer world without needing a dedicated computer or rooting your phone. Termux is a powerful terminal emulator that runs a Linux environment on Android, and it doesn't require root access. This guide focuses on setting up a Bedrock Edition server, which supports cross-play across platforms like PC, Xbox, PlayStation, Nintendo Switch, and mobile devices.

**Note:** Cross-play is available with Minecraft Bedrock Edition. Java Edition does not support cross-play natively, so we'll use Bedrock Dedicated Server (BDS) for this setup.

## Prerequisites
- **Android Device:** Any Android phone or tablet running Android 7.0 or higher.
- **Termux App:** Download and install Termux from F-Droid or the official website (Google Play Store version may have limitations).
- **Storage Space:** At least 1-2 GB free space for the server files.
- **Internet Connection:** Stable Wi-Fi or mobile data for downloading and hosting.
- **Minecraft Account:** Optional, but useful for testing. Players joining need their own Minecraft accounts.
- **No Rooting Needed:** Termux works without root access.

## Step-by-Step Guide

### Step 1: Install and Update Termux
1. Install Termux from F-Droid (recommended) or the official source.
2. Open Termux and update the package list:
   ```
   pkg update && pkg upgrade
   ```
3. Install essential packages:
   ```
   pkg install curl wget unzip
   ```

### Step 2: Install Java (Required for BDS)
Bedrock Dedicated Server requires Java. Install OpenJDK:
```
pkg install openjdk-17
```
Verify the installation:
```
java -version
```

### Step 3: Download and Set Up Bedrock Dedicated Server (BDS)
1. Create a directory for the server:
   ```
   mkdir minecraft-server && cd minecraft-server
   ```
2. Download the latest BDS from Mojang's official site. Check the current version on the [Minecraft website](https://www.minecraft.net/en-us/download/server/bedrock).
   ```
   wget https://piston-data.mojang.com/v1/objects/8f3112a1049751cc472ec13e397eade5336ca7ae/server.jar
   ```
   (Replace the URL with the latest download link if needed.)

3. Extract or prepare the server files. BDS comes as a JAR file, but you may need to download additional scripts or use a wrapper for easier management.

   For simplicity, you can use a script to automate setup. Download a BDS setup script:
   ```
   wget https://raw.githubusercontent.com/TheRemote/MinecraftBedrockServer/master/SetupMinecraft.sh
   chmod +x SetupMinecraft.sh
   ./SetupMinecraft.sh
   ```
   This script will download and configure BDS automatically.

### Step 4: Configure the Server
1. After setup, navigate to the server directory (usually `~/minecraft-server`).
2. Edit the server properties file:
   ```
   nano server.properties
   ```
   Key settings to modify:
   - `server-name`: Set your server's name.
   - `gamemode`: Choose survival, creative, etc.
   - `difficulty`: Set to easy, normal, hard.
   - `max-players`: Limit the number of players (e.g., 10).
   - `online-mode`: Set to true for security (requires Xbox Live accounts for cross-play).
   - `allow-cheats`: false (unless you want cheats).
   - `level-name`: Name your world.

   Save and exit (Ctrl+X, Y, Enter in nano).

3. For cross-play, ensure `online-mode` is true. This allows players from different platforms to join using their Minecraft accounts.

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

