 1、重启docker

[root@mz-01 ~]# sudo systemctl start docker
2、列出docker中运行的容器

[root@mz-01 ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                    PORTS               NAMES
1b4671904bfa        mysql:5.6           "docker-entrypoint.s…"   2 weeks ago         Exited (0) 30 hours ago                       mymysql
 
3、启动mysql

[root@mz-01 ~]# docker restart 1b4671904bfa
1b4671904bfa

————————————————
版权声明：本文为CSDN博主「mameng1998」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/mameng1988/article/details/82947292
