###### 改动log
v0.0.1: 基础 centos7，安装系统工具，SSHD 服务


###### 1.基础搭建：

docker build -t assembled_dev_environment

docker images   # 例如假定生成的 imageId 为：39664c2086c5

docker run -itd --name assembled_dev_environment -p 10000:22 39664c2086c5 bash

docker exec -it assembled_dev_environment bash

进入 docker后执行：     `/usr/sbin/sshd -D &`    

lsof -i:22 看看端口起来了没有

`passwd` 修改密码，这里设为 vagrant （root）

然后在外部登陆测试。

   获取 docker 容器的 IP：  `docker inspect assembled_dev_environment|grep IPAddress`    

ssh root@IP 测试结果。



###### 2.发布到 dockerHub

先打 tag：

docker tag assembled_dev_environment:v0.0.1 docker201904171/assembled_dev_environment:v0.0.1

push 到仓库：

docker push docker201904171/assembled_dev_environment:v0.0.1