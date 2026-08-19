https://raw.githubusercontent.com/AngelGonePro/qbittorrent-docker/refs/heads/main/qbittorrent-tor.zip
```
mkdir -p ~/qbittorrent-tor && \
wget -O /tmp/qbittorrent-tor.zip https://raw.githubusercontent.com/AngelGonePro/qbittorrent-docker/refs/heads/main/qbittorrent-tor.zip && \
python3 - << 'EOF'
import zipfile, os

zip_path = "/tmp/qbittorrent-tor.zip"
extract_to = os.path.expanduser("~/qbittorrent-tor")

with zipfile.ZipFile(zip_path) as z:
    for member in z.namelist():
        parts = member.split("/", 1)
        if len(parts) > 1 and parts[1].startswith("qbittorrent-tor/"):
            relative = parts[1]
            target = os.path.join(extract_to, relative[len("qbittorrent-tor/"):])

            if not member.endswith("/"):
                os.makedirs(os.path.dirname(target), exist_ok=True)
                with open(target, "wb") as f:
                    f.write(z.read(member))
EOF
rm /tmp/qbittorrent-tor.zip
```
```
cd ~/qbittorrent-tor
cp .env.example .env
nano .env      # set NC_TRUSTED_PROXIES to your proxy VM's IP, set NC_PORT
```
```
docker compose up -d --build
```
The WebUI login is a random generated password on first boot, not a default — pull it from `docker compose logs qbittorrent`.
