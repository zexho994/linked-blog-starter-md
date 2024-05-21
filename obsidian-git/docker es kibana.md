
## 生产管理员密码和token

生成管理员密码
docker exec -it es /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic

生成token
docker exec -it es /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

!! 记得保存

```
xOE*ZtIVLoEw_Tj_kNBe
```

```
eyJ2ZXIiOiI4LjEzLjAiLCJhZHIiOlsiMTcyLjE3LjAuMjo5MjAwIl0sImZnciI6IjNhYjIxMjFjZTg4Yjc1MmVmNjAwZmMwNDIxN2FhN2ZlYTVhYjBjMDcyYTM4NTQxMWI4MTVhZWMzOTBhNjIwODYiLCJrZXkiOiIwbmJDbTQ4QjJocVpCSlpXcDBmdjpoUmtZWW51SlR3V1pFQmJGVDQ0NW1BIn0=
```


## 修改ssl配置和跨域

docker cp es:/usr/share/elasticsearch/config/elasticsearch.yml C:\Users\admin\OneDrive\桌面\es.yml

docker cp C:\Users\admin\OneDrive\桌面\es.yml es:/usr/share/elasticsearch/config/elasticsearch.yml


![[es.yml]]


```
http.cors.enabled: true
http.cors.allow-origin: "*"

xpack.security.enabled: false
xpack.security.http.ssl:
  enabled: false
```

https://blog.csdn.net/mengo1234/article/details/104989382


开启kibana