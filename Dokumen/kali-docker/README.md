# Kali Linux Docker Container

A Docker container setup for Kali Linux with XFCE desktop environment and GUI support.

---

## Prerequisites

- Docker installed ([Install Docker](https://docs.docker.com/get-docker/))
- X11 server running on the host (for GUI)
- Permission to access X11 server (typically run: `xhost +local:`)
- (Optional) [VcXsrv](https://sourceforge.net/projects/vcxsrv/) or [XQuartz](https://www.xquartz.org/) for Windows/macOS

---

## Getting Started

1. **Clone this repository** or create a `docker-compose.yaml` file with the provided content.

2. **Start the container:**

   ```sh
   docker-compose up -d
   ```

3. **Access the container shell:**

   ```sh
   docker exec -it kali_linux bash
   ```

4. **(Optional) Access the XFCE desktop:**
   - Ensure your X11 server is running and accessible.
   - Run `startxfce4` inside the container if not started automatically.

---

## Configuration

The `docker-compose.yaml` file is pre-configured with:

- Persistent volume to store data in `/root`
- Dedicated network for the container
- GUI support via X11 forwarding
- Container name: `kali_linux`
- Data persists in a Docker volume named `kali_data`

---

## Installing Kali Linux Tools

To automatically install Kali Linux tools when the container starts, modify the `command` section in `docker-compose.yaml`:

**Core packages (kali-linux-core):**

```yaml
command: /bin/bash -c "apt update && apt install -y kali-linux-core xfce4 xfce4-terminal && startxfce4"
```

**All tools (kali-linux-large ~15GB):**

```yaml
command: /bin/bash -c "apt update && apt install -y kali-linux-large xfce4 xfce4-terminal && startxfce4"
```

**Specific tool bundles:**

- `kali-tools-top10`: Top 10 most popular tools
- `kali-tools-web`: Web penetration testing tools
- `kali-tools-wireless`: Wireless attack tools
- `kali-tools-forensics`: Forensic tools

**Example:**

```yaml
command: /bin/bash -c "apt update && apt install -y kali-tools-top10 xfce4 xfce4-terminal && startxfce4"
```

---

## Notes

- For `kali-linux-large`, ensure your host has sufficient disk space and RAM.
- First-time installation may take significant time depending on selected packages.
- Data persists in a Docker volume named `kali_data`.

---

## Troubleshooting

If GUI doesn't appear:

- Verify X11 server is running.
- Run `xhost +local:` before starting the container.
- Check permissions on `/tmp/.X11-unix`.
- Ensure your firewall allows X11 connections.

To stop the container:

```sh
docker-compose down
```

---

## Updating the Container

To update packages inside the container:

```sh
docker exec -it kali_linux bash
apt update && apt upgrade -y
```

---

## Suggested Container Image Concept

For a visual representation, consider an image featuring:

- Docker whale logo with Kali dragon riding it
- Terminal window showing docker-compose commands
- Icons of popular Kali tools (Nmap, Metasploit, etc.)
- Kali's signature blue/black color scheme with neon accents

You can create this using design tools like Figma or Canva, or find suitable stock images.

---

## References

- [Kali Linux Documentation](https://www.kali.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Kali Docker Images](https://hub.docker.com/r/kalilinux/kali-linux-docker)
