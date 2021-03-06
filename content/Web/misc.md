---
title: 杂项
date: 2017-03-22
---

**没有银弹**：没有任何一项技术或方法能让软件工程的生产力在十年内提高十倍。\[百度百科]
**粒度**：指数据仓库的数据单位中保存数据的细化或综合程度的级别。细化程度越高，粒度级就越小；相反，细化程度越低，粒度级就越大。数据的粒度一直是一个设计问题。在数据仓库环境中粒度之所以是主要的设计问题，是因为它**深深地影响存放在数据仓库中的数据量的大小，同时影响数据仓库所能回答的查询类型**。在数据仓库中的数据量大小与查询的详细程度之间要作出权衡。\[百度百科]

IaaS - Infrastructure as a Service [基础设施即服务]，是消费者使用处理、储存、网络以及各种基础运算资源，部署与执行操作系统或应用程序等各种软件。
PaaS - Platform as a Service [平台即服务]，提供运算平台与解决方案堆栈，介于软件即服务与基础设施即服务之间。
SaaS - Software as a Service [软件即服务]，通俗可以称为“即需即用软件”，是一种软件交互模式。在这种交互模式中云端集中式托管软件及相关的数据，软件仅需透过互联网，而不须透过安装即可使用。用户通常使用精简客户端经由一个网页浏览器来访问软件即服务。
IoT - Internet of Things [物联网]，让所有能行使独立功能的普通物体实现互联互通的网络。
SOA - Service-oriented architecture [面向服务的体系结构]，是构造分布式计算的应用程序的方法，它将应用程序功能作为服务发送给最终用户或者其他服务。

# Chrome Dev Summit 2016

Progressive Web Apps (PWA)，能够提供类似 Native app 一样体验的 Web app。主要有几个特点：
- 可添加至桌面（可安装）
- 离线能力
- 消息推送
- 安全
- 响应式

Darin Fisher（选择我感兴趣的点）
- 移动端的挑战：分辨率，cpu，内存，电池，网络
- 印度 2.3 亿，美国 4.6 亿，中国 7.6 亿的网民
- **超过 3 秒的网页，53% 的用户选择离开**
- 在 3G 环境下，要确保页面 5 秒内加载完成
- “添加到主屏幕”这个功能提高了用户 4 倍的浏览频率
- Lighthouse 是个测试 PWA 的工具
- [browser-issue-tracker-search] 为开发者提供的网站，包括bug，w3c 标准，API 建议等

Alex
- 手机网页打开的平均时间在 19s
- Motion Mark 测试，PC 要比手机端快 25 倍
- **使用真机 Debug**
- **重视低端设备**
- 硬件限制以至于手机不能比 PC 块
- [High Performance Browser Networking]
- 少加载 code，在合适的时间执行合适的代码
- Service Worker 不仅仅是离线，更重要的是提升效率

Paul - 关于 Web 未来发展方向
- **Web 一定会赶超 Native APIs**
- 手机游戏会与 Native 平起平坐，并带来更高的利润
- 现有 API：定位（Geolocation），相机（Camera），麦克风（Microphone），电池（Battery），权限（Permissions），网络状况（Network），自动填充（Autofill），用户授权（Credential Management API），支付（PaymentRequest API），消息推送（Push notifications），离线（Offline），可安装（Installability）
- SLICE（Secure，Linkable，Indexable，Composable，Ephemeral）
- [Doing Science On The Web]
- **新的交互方式**：Physical Web. Web Bluetooth. WebUSB. WebVR.
