注意:
该文件夹内容需要先安装 Docker 与 Docker-compose才能够运行.

安装Docker请参照Docker官方文档进行安装
https://docs.docker.com/install/linux/docker-ce/centos/

Docker-compose也按下面链接进行安装
https://docs.docker.com/compose/install/

该文件夹中也包含压缩包,只需要下载zip包即可
https://github.com/azure-sea/docker-compose/raw/master/compose_lnmp/compose_lnmp.zip

下载完成后进行解压操作
unzip compose_lnmp.zip

进入文件夹
cd compose_lnmp

通过docker-compose 命令进行运行 #-d 在后台运行.
docker-compose -f docker-compose.yml up -d
