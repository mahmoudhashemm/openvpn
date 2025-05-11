# openvpn
```
docker run -d \
  --name openvpn-as \
  --restart unless-stopped \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_MODULE \
  --privileged \
  -p 943:943 \
  -p 9443:9443 \
  -p 1194:1194/udp \
  -v /opt/openvpn-as-data:/config \
  openvpn/openvpn-as
```
