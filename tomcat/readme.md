# tomcat install
## 根据以下步骤安装tomcat并设置防火墙

一般是/opt/tomcat/文件夹下放入安装包

## 解压安装

tar -zxvf apache-tomcat-8.5.59.tar.gz

进入解压后的目录中的bin执行startup.sh

cd apache-tomcat-8.5.59/

cd bin/

./startup.sh

## 开启8080防火墙端口以供主机访问

firewall-cmd --permanent --add-port=8080/tcp

firewall-cmd reload

firewall-cmd --reload

firewall-cmd --query-port=8080/tcp

## 进入webapps/ROOT/创建html测试

cd ..

cd webapps/

cd ROOT/

vim lzsb.html

<h1>lzsb ok</h1>

## 母机打开网页192.168.200.131:8080/lzsb.html
