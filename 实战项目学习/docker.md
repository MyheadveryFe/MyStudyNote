```
systemctl start docker
docker version
docker images
docker info
docker search 镜像名 --filter=STARS=3000
docker pull 镜像名:[tag]
docker rmi -f 镜像id
docker rmi -f $(docker images -aq)
docker run [参数] 镜像名
	--name="容器名"
	-d
	-it
	-p ip:主机端口:容器端口
	-p 主机端口:容器端口
	-p 容器端口
exit
docker ps
docker ps -a
docker ps -n=1
docker ps -aq
docker run centos /bin/bash
ctrl+p+q
docker rm 容器id
docker rm -f($docker ps -aq)
docker ps -a -q|xargs docker rm
docker start 容器id
docker restart
docker stop
docker kill
docker run -d centos
docker logs [参数] 容器id
	-f
	-t
	--tail 行数
docker logs -tf --tail 10 容器id
docker top 容器id
docker inspect 容器id
docker exec -it 容器id 命令
docker attach 容器id
docker cp 容器id:/容器路径 /主机路径
docker run -d --name nginx01 -p 3344:80 nginx
docker exec -it nginx01 /bin/bash
docer run -it --rm tomcat:9.0
docker run -d --name tomcat01 -p 9090:8080 tomcat
docker exec -it tomcat01 /bin/bash
docker stats
	-e ES_JAVA_OPTS="-Xms64m -Xmx512m"
docker run -d -p 8080:9000 --restart=alays -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
docker commit -m "描述" -a="作者" 容器id 目标镜像名:[tag]
docker run -it -v /主机目录:/容器目录 镜像名 /bin/bash
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
	-v 名字:/容器内路径
	-v /容器内路径
	-v /主机路径:/容器内路径
docker volume ls
docker volume inspect 具体容器名
	-v /容器内路径:ro
	-v /容器内路径:rw
docker build -f 脚本文件名 -t 名/名:[tag] .
docker run -it --name docker02 --volumes-from docker01 kuangshen/centos:1.0
docker push
docker history 镜像id
docker login -u 用户名
docker push 名/名:[tag]


## 脚本
FROM
MAINTAINER
RUN
ADD
WORKDIR
VOLUME
EXPOSE
CMD
ENTRYPOINT
ONBUILD
COPY
ENV


```

