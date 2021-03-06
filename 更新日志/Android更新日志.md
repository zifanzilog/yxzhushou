# Android App更新日志

## v1.0.6
日期：2020/11/11

bug：
+ 修复 [touchMove](../鱼叉助手API文档.md/#touchMove) 移动函数,重置算法
+ 修复 手机发热严重问题(录屏算法优化)

## v1.0.5
日期：2020/11/10

新增：
+ 后台保活无声音乐暂时改成有声音乐,方便测试是否后台进程被杀.

bug：
+ 修复App主界面无法向下滑动问题.(反馈作者:8068884)
+ 修复悬浮窗显示多个的问题.(反馈作者:357339600)

## v1.0.4
日期：2020/11/10

新增：(反馈作者:506465336)
+ 新增物联设备运行时,自动连接功能.每隔5秒检测一次连接状态

## v1.0.3
日期：2020/11/9

bug：(反馈作者:357339600)
+ 修复控制台占用内存的问题(运行3小时内存爆炸),现在手机端控制台只显示最多1000个字符后自动清空.如果需要查看更多信息,请打开发送控制台信息到电脑,在PC端查看.
+ 修改发送图片jpg格式为png格式,试图解决识别率不准的问题(有待下一步测试)

## v1.0.2
日期：2020/11/8

新增：
+ 可在手机端查看App更新日志功能
+ 函数：[keepScreen](../鱼叉助手API文档.md/#keepScreen)、[getColor](../鱼叉助手API文档.md/#getColor)、[getColorRGB](../鱼叉助手API文档.md/#getColorRGB)

bug：
+ 修复热更新无法下载的问题
+ 修复保存配置无法正常保存的问题

## v1.0.1
日期：2020/11/8

bug：(反馈作者:506465336)
+ 修复无法调用 [findColor](../鱼叉助手API文档.md/#findColor)、[touchDown](../鱼叉助手API文档.md/#touchDown)、[touchMove](../鱼叉助手API文档.md/#touchMove)、[touchUp](../鱼叉助手API文档.md/#touchUp) 等函数问题

## v1.0.0
日期：2020/11/7

新增：
+ 开启录屏服务
+ 开启悬浮窗服务
+ 开启读写本地文件服务
+ 开启后台播放无声音乐保活
+ 开启socket服务
+ 可搜索已连接手机的热点设备ip地址，mac地址
+ 支持物联设备连接（默认4444端口）
+ 支持github热更新，zip解压，保存到手机本地(暂时不允许中文文件名称下载)
+ 支持读取本地目录，运行Lua文件
+ 支持运行Lua期间，可随意暂停Lua程序
+ 支持发送图片到电脑（默认8888端口）
+ 支持发送控制台信息到电脑（默认端口9999）
+ 支持手机内查看控制台信息
+ 支持保存图片到手机
+ 函数：[findColor](../鱼叉助手API文档.md/#findColor)、[touchDown](../鱼叉助手API文档.md/#touchDown)、[touchMove](../鱼叉助手API文档.md/#touchMove)、[touchUp](../鱼叉助手API文档.md/#touchUp)、[getScreenSize](../鱼叉助手API文档.md/#getScreenSize)、[mSleep](../鱼叉助手API文档.md/#mSleep)