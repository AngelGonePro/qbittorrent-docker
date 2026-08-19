https://raw.githubusercontent.com/AngelGonePro/qbittorrent-docker/refs/heads/main/qbittorrent-tor.zip
```
rm -rf ~/qbittorrent-tor && \
mkdir -p ~/qbittorrent-tor && \
wget -q -O /tmp/qbittorrent-tor.zip https://raw.githubusercontent.com/AngelGonePro/qbittorrent-docker/refs/heads/main/qbittorrent-tor.zip && \
unzip -q /tmp/qbittorrent-tor.zip -d ~ && \
rm /tmp/qbittorrent-tor.zip && \
cd ~/qbittorrent-tor && \
ls -la
```
```
mkdir -p /root/data/Downloads
chown 82:65600 /root/data/Downloads
chmod 2775 /root/data/Downloads
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
