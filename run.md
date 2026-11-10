sudo lsof -tiTCP:511 -sTCP:LISTEN | xargs sudo kill
sudo -n nohup python3 -m http.server 511 --bind 127.0.0.1 > /tmp/portfolio-511.log 2>&1 < /dev/null &