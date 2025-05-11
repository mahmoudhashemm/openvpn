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


الحل: تفعيل صلاحية "Superuser" للمستخدم admin
نفّذ الأمر التالي:

```
docker exec -it openvpn-as /usr/local/openvpn_as/scripts/sacli --user admin --key "type" --value "admin" UserPropPut
```
ثم أعد تشغيل خدمات OpenVPN Access Server لتأكيد التحديث:

```
docker exec -it openvpn-as /usr/local/openvpn_as/scripts/sacli start
```


خطوات لتعيين صلاحيات "superuser":
افتح جلسة docker exec مع الحاوية الخاصة بك:

```
docker exec -it openvpn-as bash
```
قم بتشغيل السكربت sacli لضبط الصلاحيات:

```
/usr/local/openvpn_as/scripts/sacli --user admin --key "prop_superuser" --value "true" UserPropPut
```
تحقق مرة أخرى من الإعدادات:

```
/usr/local/openvpn_as/scripts/sacli --user admin UserPropGet
```
