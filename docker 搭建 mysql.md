# docker 搭建 mysql

1. 获取镜像

   ```shell
   docker pull mysql # 拉取最新的 mysql 镜像
   ```
   
2. 执行`docker run`

   ```shell
   # 因为 mysql不是 root 用户执行 所以挂在目录没有访问权限需要以特定用户执行
   mkdir data
   ls -lnd data
   drwxr-xr-x  5 501  20  170 11 27 00:00 .
   
   sudo docker run -p 3306:3306 --name mysql \  
   -v ~/Desktop/docker/mysqlmysql/logs:/var/log/mysql \
   -v ~/Desktop/docker/mysql/mysql/data:/var/lib/mysql \
   -e MYSQL_ROOT_PASSWORD=123456 \
   --user 5:501 \
   mysql
   
   #当然也可以简单粗暴
   sudo docker run -d  -p  3306:3306 --name mysql \
      -v ~/Desktop/docker/mysql/volum/mysql/logs:/var/log/mysql \
      -v ~/Desktop/docker/mysql/volum/data:/var/lib/mysql-files \
      -e MYSQL_ROOT_PASSWORD=123456 \
      --user root  mysql
   ```

3. 本地使用 mysqlcli
```shel
	sudo docker exec -it mysql bash
  mysql -uroot -p123456l
```

