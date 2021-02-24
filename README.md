## 说明
基于 python3.7 + django 2.2.3 实现的 django-webshell，参考 https://github.com/huyuan1999/django-webssh 。在参考项目的基础上做了一些优化：新增前端页面刷新确认页面（刷新会导致 websocket 连接断开）、后端 paramiko 线程创建代码优化、记录命令记录以及结果、支持 zmodem 上传下载文件(rz, sz)。有兴趣的同学可以在此基础上稍作修改集成到自己的堡垒机中。

### 所需技术: 
- websocket 目前市面上大多数的 webssh 都是基于 websocket 协议完成的
- django-channels django 的第三方插件, 为 django 提供 websocket 支持
- xterm.js 前端模拟 shell 终端的一个库
- paramiko python 下对 ssh2 封装的一个库

### 如何将所需技术整合起来？
1. xterm.js 在浏览器端模拟 shell 终端, 监听用户输入通过 websocket 将用户输入的内容上传到 django
2. django 接受到用户上传的内容, 将用户在前端页面输入的内容通过 paramiko 建立的 ssh 通道上传到远程服务器执行
3. paramiko 将远程服务器的处理结果返回给 django
4. django 将 paramiko 返回的结果通过 websocket 返回给用户
5. xterm.js 接收 django 返回的数据并将其写入前端页面

### 流程图
![](https://github.com/leffss/django-webssh/blob/master/screenshots/0.png?raw=true)

## 启动
```
pip3 install -r requirements.txt
cd django-webssh/webssh/
python3 manage.py runserver 0.0.0.0:8000
```	
访问：http://127.0.0.1:8000

## 预览
![](https://github.com/leffss/django-webssh/blob/master/screenshots/1.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/2.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/3.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/4.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/5.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/6.PNG?raw=true)
![](https://github.com/leffss/django-webssh/blob/master/screenshots/7.PNG?raw=true)
