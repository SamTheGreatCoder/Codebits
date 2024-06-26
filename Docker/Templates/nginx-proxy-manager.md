# Nginx Proxy Manager
https://nginxproxymanager.com/guide/#quick-setup
``` yaml
version: '3.8'
services:
  nginx-proxy-manager:
    container_name: nginx-proxy-manager
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP
    # Uncomment the next line if you uncomment anything in the section
    # environment:
      # Uncomment this if you want to change the location of
      # the SQLite DB file within the container
      # DB_SQLITE_FILE: "/data/database.sqlite"
      # Uncomment this if IPv6 is not enabled on your host
      # DISABLE_IPV6: 'true'
    volumes:
      - /opt/pve/nginx-proxy-manager/data:/data
      - /opt/pve/nginx-proxy-manager/letsencrypt:/etc/letsencrypt
    networks:
      - frontend
      - backend
# Personal addition for homelab
networks:
  frontend:
    external:
      name: "frontend"
  backend:
    external:
      name: "backend"
```