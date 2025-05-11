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
get password
```
docker exec -it openvpn-as cat /usr/local/openvpn_as/init.log
```
. تعيين كلمة مرور للمستخدم admin (أو أي مستخدم أنشأته):
```

docker exec -it openvpn-as /usr/local/openvpn_as/scripts/sacli --user admin --new_pass MySecurePass123 SetLocalPassword
```
✏️ غيّر MySecurePass123 بكلمة المرور التي تريدها.
