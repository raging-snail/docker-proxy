# docker-proxy

# 部署步骤

### step1.拉取代码
``` bash
git clone https://github.com/raging-snail/docker-proxy.git
```

### step2.部署pages
+ 登录Cloudflare，创建pages
+ 上传文件，选择刚刚拉取的代码，只需要index.html文件，其它内容不需要
+ 如果有域名，可以设置自定义域，即访问链接。如果不设置，Cloudflare会自动给你分配一个访问链接

### step3.部署worker
+ 登录Cloudflare，创建worker
+ 将woker.js中的代码粘贴到woker中
+ 将第一行代码的链接修改为你刚刚部署的pages访问链接
  ``` js
  const readme = `https://xxxx.pages.dev/`;
  ```
+ 如果有域名，可以设置触发器，例如：docker.xxxxxx.xyz。如果不设置，Cloudflare会自动给你分配一个访问链接（国内访问非常慢）

# 使用

### 方式1：直接使用

#### 原拉取镜像方式
``` bash
docker pull library/alpine:latest
```
#### 加速拉取镜像命令
``` bash
# 将前缀改为你自己部署的worker链接
docker pull docker.xxxxxx.xyz/library/alpine:latest
```

### 方式2：设置镜像源
``` bash
# 设置镜像源
sudo tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": ["https://docker.xxxxxx.xyz"]
}
EOF
# 重新加载
sudo systemctl daemon-reload
# 重启docker
sudo systemctl restart docker
```
