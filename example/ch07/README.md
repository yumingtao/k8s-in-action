# 7.4.6
# 7.4.6
## 从文件夹创建一个configmap
```
$ k create configmap fortune-config-1 --from-file=configmap-files
$ k port-forward fortune-configmap-volume 8080:80 &
curl -H 'Accept-Encoding: gzip' -I localhost:8080
```

# 7.4.7
```
$ k edit cm fortune-config-1
$ k exec fortune-configmap-volume -c web-server cat /tmp/whole-fortune-config-volume/my-nginx-config.conf
$ k exec fortune-configmap-volume -c web-server -- nginx -s reload
```

# 7.5.2
```
$ k exec fortune-configmap-volume ls /var/run/secrets/kubernetes.io/serviceaccount
```

# 7.5.3
## 生成证书及私钥文件
```
$ openssl genrsa -out https.key 2048
$ openssl req -new -x509 -key https.key -out https.cert -days 3650 -subj /CN=www.kubia-example.com
$ k create secret generic fortune-https --from-file=https.key --from-file=https.cert --from-file=foo
```


# 7.5.5
```
$ k create configmap fortune-config-2 --from-file=my-nginx-config-https.conf --from-file=configmap-files/sleep-interval
$ k create -f fortune-pod-https.yaml
$ k port-forward fortune-https 8443:443 &
$ k exec fortune-https -c web-server -- mount | grep certs
$ k create secret docker-registry mydockerhubsecret --docker-username=yumingtao --docker-password=xxxxxxxxx --docker-email=yumingtao2008@gmail.com
$ k create -f fortune-pod-with-private-image.yaml
$ k port-forward fortunep 8080:80 &
$ curl http://localhost:8080
```