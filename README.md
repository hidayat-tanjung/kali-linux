## Kali Linux Docker Container
A Docker container setup for Kali Linux with XFCE desktop environment.

## Prerequisites
- Docker installed

- X11 server running on the host (for GUI)

- Permission to access X11 server (typically run xhost +local:)

## How to Run
Clone this repository or create a docker-compose.yml file with the provided content

Start the container with:

```
docker-compose up -d
```

To access the container shell:

```
docker exec -it kali_linux bash
```

## Configuration
The docker-compose.yml file is pre-configured with:

- Persistent volume to store data in /root
- Dedicated network for the container
- GUI support via X11 forwarding

## Installing Kali Linux Tools
To automatically install Kali Linux tools when the container starts, modify the command section in docker-compose.yml:

Core packages (kali-linux-core):

```yaml
command: /bin/bash -c "apt update && apt install -y kali-linux-core xfce4 xfce4-terminal && startxfce4"
```

## All tools (kali-linux-large - ~15GB):

```yaml
command: /bin/bash -c "apt update && apt install -y kali-linux-large xfce4 xfce4-terminal && startxfce4"
```

Specific tool bundles:

- kali-tools-top10: Top 10 most popular tools
- kali-tools-web: Web penetration testing tools
- kali-tools-wireless: Wireless attack tools
- kali-tools-forensics: Forensic tools

Example:

```yaml
command: /bin/bash -c "apt update && apt install -y kali-tools-top10 xfce4 xfce4-terminal && startxfce4"
```

Notes

- For kali-linux-large, ensure your host has sufficient disk space and RAM
- First-time installation may take significant time depending on selected packages
- Data persists in a Docker volume named kali_data

Troubleshooting
If GUI doesn't appear:

- Verify X11 server is running
- Run xhost +local: before starting the container
- Check permissions on /tmp/.X11-unix

To stop the container:

```
docker-compose down
```

## Suggested Container Image Concept
For a visual representation, consider an image featuring:

- Docker whale logo with Kali dragon riding it
- Terminal window showing docker-compose commands
- Icons of popular Kali tools (Nmap, Metasploit, etc.)
- Kali's signature blue/black color scheme with neon accents

You can create this using design tools like Figma or Canva, or find suitable stock images.
