# neos-ts
《游戏王》对战平台[YGOPro](https://github.com/Fluorohydride/ygopro)的网页版。

## 开发动机
网页版YGOPro存在以下优势：
- 便利性：玩家无需下载，即可进行游戏王对战；
- 跨平台性：一套代码适配Windows，MacOS，Linux平台；
- 版本实时性：新版本更新后，无需玩家操作，版本自动迭代；
- 后发优势：可以针对单机版的一些缺点，比如缺失用户系统和卡组无法云端同步等，
进行针对性优化.

## 开发目标
对网页版YGOPro的开发目标暂定为：
- 一套新的灵活，扩展性强的UI界面；
- 兼容[233服务器](https://ygo233.com/)，能和单机版YGOPro联机；
- 一套新的用户系统，实现卡组云端同步；
- 特效和动画；
- （可选）竞技天梯榜；
- （可选）实时语音功能。

## 开发进度
- [调研文档](./doc/investigation)；
- [讨论文档](./doc/discuss)
- （WIP）[协议文档](./doc/investigation/protocol.md)；
- 重新实现的[客户端Demo](https://github.com/DarkNeos/ygopro-client-rs)；
- （WIP）用于ygopro的[websocket协议代理](https://github.com/DarkNeos/ygopro-proxy)
- （fork项目）用于测试的[服务端实现](https://github.com/DarkNeos/srvpro)
- 用于参考的[ygopro2客户端](https://code.mycard.moe/mycard/YGOProUnity_V2)

## 后续计划：
- 调研技术框架[three.js](https://threejs.org/)和[react](https://reactjs.org/)；
- 完成[代理服务](https://github.com/DarkNeos/ygopro-proxy)的基本框架实现，将ygopro的数据协议转成[protobuf](https://developers.google.com/protocol-buffers)格式；
- 基于[react](https://reactjs.org/)编写小型Demo，确认基础功能的实现可行和数据协议的具体细节；
- 设计整体的软件架构，包括游戏对局和用户系统，包括前端和后端；
- 代码开撸。

## 招募决斗者

**我们认为这个项目是一个难度/复杂度适中的前端&游戏开发练手项目，也是能给简历充实内容的项目。
最重要的是，这是个有价值的项目，能服务于国内外许多游戏王爱好者。**

对此项目开发感兴趣的同仁，可以通过邮箱：linuxgnulover@gmail.com 联系我，
或者加入QQ群进行交流：<img src="./assets/ygo_qq.png" width=300 high=300>

此外，我们非常希望得到YGOPro单机版开发者们，特别是YGOPro服务端[srvpro](https://github.com/mycard/srvpro)和[ygopro](https://github.com/mycard/ygopro/tree/server)
还有移动端[ygomobile](https://github.com/mycard/ygomobile)，PC端[YGOProUnity_V2](https://code.mycard.moe/mycard/YGOProUnity_V2)开发者们的帮助，
若开发者们有幸看到了这个repo，还请在空余时间通过上面的联系方式联系我们，十分感谢。

## LICENSE
                    GNU GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007

 Copyright (C) 2007 Free Software Foundation, Inc. <https://fsf.org/>
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.
