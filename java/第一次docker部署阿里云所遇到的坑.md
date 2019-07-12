### 第一次docker部署阿里云所遇到的坑

- docker 要按照官网写

- 开放内部端口

  > #Firewall configuration written by system-config-firewall  

  > #Manual customization of this file is not recommended.  
  >
  > *filter  
  > :INPUT ACCEPT [0:0]  
  > :FORWARD ACCEPT [0:0]  
  > :OUTPUT ACCEPT [0:0]  
  > -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT  
  > -A INPUT -p icmp -j ACCEPT  
  > -A INPUT -i lo -j ACCEPT  
  > -A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT  
  > -A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT  
  > -A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT  
  > -A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT  
  > -A INPUT -j REJECT --reject-with icmp-host-prohibited  
  > -A FORWARD -j REJECT --reject-with icmp-host-prohibited  
  > COMMIT  

- mysql 安装8.0 

  1. mysql 中设置不区分大小写
  2. mysql 设置utf-8
  3. mysql 设置远程链接
  4. 宿主主机的ip是172.17.0.1

  > docker run -di --name=mysql \
  > -v /usr/local/src/mysql/data:/var/lib/mysql \
  > -v /usr/local/src/mysql/conf/my.cnf:/etc/mysql/my.cnf \
  > --privileged=true \
  > -p 3306:3306 \
  > -e MYSQL_ROOT_PASSWORD=123456 mysql \
  > --lower_case_table_names=1
  >
  > 
  >
  > [client]
  > default-character-set=utf8
  >
  > [mysql]
  > default-character-set=utf8
  >
  > [mysqld]
  > pid-file        = /var/run/mysqld/mysqld.pid
  > socket          = /var/run/mysqld/mysqld.sock
  > datadir         = /var/lib/mysql
  > secure-file-priv= NULL
  >
  > #Disabling symbolic-links is recommended to prevent assorted security risks
  >
  > symbolic-links=0
  > max_connections=10000
  > default-time_zone='+8:00'
  > character-set-client-handshake=FALSE
  > character_set_server=utf8
  > collation-server=utf8_unicode_ci
  > init_connect='SET NAMES utf8 COLLATE utf8_unicode_ci'
  >
  > #Custom config should go here
  >
  > !includedir /etc/mysql/conf.d/
  >
  >
  > docker exec -it mysql /bin/bash
  >
  > mysql -uroot -p123456
  >
  > 远程 root  password
  > ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

- tomcat下以war包方式运行文件

  > docker run -d -p 8080:8080 tomcat
  >
  > docker exec -it mytomcat bash
  > docker cp ymall.war tomcat:/usr/local/tomcat/webapps
  > docker restart mytomcat



