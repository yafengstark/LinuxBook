
## java 命令

方式一：

 
java -jar shareniu.jar
特点：当前ssh窗口被锁定，可按CTRL + C打断程序运行，或直接关闭窗口，程序退出

那如何让窗口不锁定？

方式二

 
java -jar shareniu.jar &
&代表在后台运行。

特定：当前ssh窗口不被锁定，但是当窗口关闭时，程序中止运行。

继续改进，如何让窗口关闭时，程序仍然运行？

方式三


nohup java -jar wxdev.jar >temp.txt &

nohup 意思是不挂断运行命令,当账户退出或终端关闭时,程序仍然运行
