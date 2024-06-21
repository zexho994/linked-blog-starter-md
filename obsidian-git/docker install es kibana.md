参考：
https://blog.csdn.net/weixin_45056780/article/details/125408524?spm=1001.2014.3001.5501



创建network：


## 启动ES
![[Pasted image 20240523101716.png]]


### 生产管理员密码和token

生成管理员密码
docker exec -it es /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic

gnvRODm5yyGHSqcuVkRI
![[Pasted image 20240523101814.png]]



生成token
docker exec -it es /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana

eyJ2ZXIiOiI4LjEwLjEiLCJhZHIiOlsiMTcyLjE3LjAuMjo5MjAwIl0sImZnciI6IjdhMGVjYzcwMWYwMjgxNTBhOWQ5ZjcyMjJlZmExNGY0ODc0ZGQ2NzM1ZDZjMDQ4ZDczYWU4YTUwYTFiODk1YjIiLCJrZXkiOiJGeGFPcEk4Qi1pWVNHRUc1Q0haUDpWNGZWaEdUcFIxdTZPWHl4dnMyR2ZBIn0=
![[Pasted image 20240523101857.png]]


!! 记得保存

```
xOE*ZtIVLoEw_Tj_kNBe
```

```
eyJ2ZXIiOiI4LjEzLjAiLCJhZHIiOlsiMTcyLjE3LjAuMjo5MjAwIl0sImZnciI6IjNhYjIxMjFjZTg4Yjc1MmVmNjAwZmMwNDIxN2FhN2ZlYTVhYjBjMDcyYTM4NTQxMWI4MTVhZWMzOTBhNjIwODYiLCJrZXkiOiIwbmJDbTQ4QjJocVpCSlpXcDBmdjpoUmtZWW51SlR3V1pFQmJGVDQ0NW1BIn0=
```


### 修改ssl配置和跨域

docker cp es:/usr/share/elasticsearch/config/elasticsearch.yml C:\Users\邹志浩\OneDrive\桌面\es.yml

docker cp C:\Users\邹志浩\OneDrive\桌面\es.yml es:/usr/share/elasticsearch/config/elasticsearch.yml

![[es.yml]]


```
http.cors.enabled: true
http.cors.allow-origin: "*"

xpack.security.enabled: false
xpack.security.http.ssl:
  enabled: false
```


es启动成功, 浏览器输入 localhost:9200
![[Pasted image 20240523102521.png]]


## 启动 kibana
![[Pasted image 20240523102422.png]]
![[Pasted image 20240523102640.png]]

![[Pasted image 20240523102718.png]]

![[Pasted image 20240523102720.png]]

![[Pasted image 20240523102742.png]]


记得修改https成http
![[Pasted image 20240523102811.png]]
