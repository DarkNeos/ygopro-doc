# YGOPro服务端前期调研

## 大致整体架构

<img src="../../assets/ygopro-server.drawio.svg" width=300 high=300>

## 部署方法
### 云服务器部署
- 第一步：下载`srvpro`项目
  - `git clone git@github.com:mycard/srvpro.git`
  - `cd srvpro`
  - `npm install`
- 第二步：编译`ygopro`项目
  - `git clone git@github.com:mycard/ygopro.git`(在srvpro目录下)
  - `cd ygopro`
  - `git checkout server`(切换到server分支)
  - `git submodule update --init --recursive`(初始化git子项目)
  - `wget -O - https://github.com/premake/premake-core/releases/download/v5.0.0-beta1/premake-5.0.0-beta1-linux.tar.gz | tar zfx -`(下载premake5)
  - `wget -O - https://www.lua.org/ftp/lua-5.3.6.tar.gz | tar zfx -; cd lua-5.3.6; sudo make linux install; cd ..`(下载lua)
  - `mv lua-5.3.6 lua`
  - `cp ./premake/lua/premake5.lua ./lua`
  - `./premake5 gmake`(生成makefile)
    - mac平台下是`./premake5 gmake --cc=clang`
    - M1平台下是`./premake5 gmake --cc=clang --mac-arm`
  - `cd build && make config=release && cd..`(编译，这步完成后ygopro/bin/release目录下会生成ygopro可执行文件)
  - `ln -s bin/release/ygopro ./`(创建软链接)
  - `strip ygopro && cd ..`(ygopro编译完成，返回srvpro目录)
- 第三步：创建`config/config.json`文件
  - `mkdir config`
  - `cp data/default_config.json config/config.json`
- 第四步：运行`ygopro-server.js`
  - `node ygopro-server.js`

以上四步完成后，就可以在ygopro客户端上连接部署的服务了。

查看云服务器公网ip：
```bash
curl ifconfig.me
```

运行`ygopro-server.js`后，控制台输出日志中会显示ygopro服务端监听的端口，默认是`7911`。

在ygopro客户端中点击`联机模式`，然后在弹出的窗口中将对应的ip地址和端口输入，即可进入房间了。
如果成功进入了房间，则表示成功在云服务器中部署了ygopro服务端。


### 本机部署
流程和云服务器部署一样。

在本机部署后，本机启动的ygopro客户端可以通过ip地址`127.0.0.1`连接部署好的服务。

### docker部署
- 第一步：下载docker
  - [docker菜鸟教程](https://www.runoob.com/docker/docker-tutorial.html)
- 第二步：拉取srvpro镜像
  - `docker pull git-registry.mycard.moe/mycard/srvpro:lite`
- 第三步：运行docker容器，并完成端口映射
  - 如何运行docker容器和什么是端口映射可以参考[docker菜鸟教程](https://www.runoob.com/docker/docker-container-usage.html)
  - 下图将docker内的`7911`端口映射到了本机的`8080`端口：<img src="../../assets/docker-port-map.png" width=600 high=600>

完成以上三步后即可在ygopro客户端上连接ygopro服务端了，ip地址为本机ip地址，端口为映射后的本机端口（`8080`）。
  
## 数据协议

## 代码导读
