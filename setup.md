## Setting up a minecraft server

Here are my notes on setting up a minecraft server with [Spigot](https://www.spigotmc.org) and
[Raspberry Juice](https://dev.bukkit.org/projects/raspberryjuice).

I'm following the raspberry pi instructions in
[this post](http://lemire.me/blog/2016/04/02/setting-up-a-robust-minecraft-server-on-a-raspberry-pi/).

### On a Mac

- Make a directory for the server, for example
  `~/Documents/MinecraftServer` and change into that directory

  ```
  mkdir ~/Documents/MinecraftServer
  cd ~/Documents/MinecraftServer
  ```

- Download the build file for Spigot

  ```
  wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
  ```

- Make sure you have Java version 8

  ```
  javac -version
  java -version
  ```

  They should be like `1.8.0_91`.

- Build the server stuff

  ```
  java -jar BuildTools.jar
  ```

  It will download and build a bunch of stuff. This takes a while.
  On my Mac Book Pro this took 10 minutes.

- There should be a file in there called something like
  `spigot-1.11.2.jar`. You now want to fire up the server for the
  first time:

  ```
  java -jar -Xms512M -Xmx1024M spigot-1.11.2.jar
  ```

- It will create a file `eula.txt` halt. You need to edit that file
  and change the line `eula=false` to `eula=true`. By doing so, you're
  saying you agree to the "End user license agreement" (EULA).

- Now you can fire up the server again, and it will fully run.

  ```
  java -jar -Xms512M -Xmx1024M spigot-1.11.2.jar
  ```

  You can stop the server by typing `stop`. Start it again by running
  the same `java` command.

- Edit the file `server.properties`, changing the following settings
  to put you in "peaceful" (`difficulty=0`) and "creative"
  (`gamemode=1`) modes, and to force players into these default modes
  (otherwise they'll be in whatever mode they were in last).
  You can also set `motd` to some description of your server.

  ```
  force-gamemode=true
  gamemode=1
  difficulty=0
  motd=My very own minecraft server
  ```

- Create a shell script to start the server, say `start_server.sh`:

  ```
  #!/bin/sh

  cd ~/Documents/MinecraftServer
  java -Xms512M -Xmx1024M -jar spigot-1.11.2.jar
  ```

- Make that file executable

  ```
  chmod +x start_server.sh
  ```

- Give yourself and other players "op" status:

  ```
  op [username]
  ```

- Start Minecraft and select "MultiPlayer". Click "Add Server" and
  give it a name. Server address could be `localhost` if it's running
  on the same computer that your using to run Minecraft.

- Download
  [RaspberryJuice](https://dev.bukkit.org/projects/raspberryjuice) by
  visiting [its site](https://dev.bukkit.org/projects/raspberryjuice)
  and clicking the blue "Download" button in the upper right. You'll
  get a file like `rasberryjuice-1.9.jar`. Put this in your `plugins/`
  folder.

- Stop and start the server again. In the first dozen or so lines
  printed, you should see something like:

  ```
  [22:33:02 INFO]: [RaspberryJuice] Loading RaspberryJuice v1.9
  ```

  This indicates that the RaspberryJuice plugin is running.
