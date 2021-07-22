# iOS App更新日志
<!-- ## v1.0.0(*) 正在修复
日期：2021/

新增：
+ 新增API函数（需求作者：79324158）
+ aes加密解密

待解决的bug：
+ 搜索设备，搜索不到时出现卡死问题（反馈作者：79324158） -->

## v1.0.0(28)
日期：2021/04/18

新增：（需求作者：79324158）
+ 函数 [http](./鱼叉助手API文档.md/#http) HTTPget/HTTPpost 网络请求
+ 函数 [base64encode](./鱼叉助手API文档.md/#base64encode) base64编码
+ 函数 [base64decode](./鱼叉助手API文档.md/#base64decode) base64解码

## v1.0.0(27)
日期：2021/04/18

核心优化：
+ 函数 [findColor](./鱼叉助手API文档.md/#findColor)、[findColors](./鱼叉助手API文档.md/#findColors) 新增模糊找色算法，提高16倍以上识别速度。

新增：
+ 函数 [mTime](./鱼叉助手API文档.md/#mTime) 毫秒级时间戳

bug：
+ 修复 一键运行 自动下载失败的bug（对应 智图学院PC端（1.0.5版本）开发模式）

## v1.0.0(26) 重要更新
日期：2021/04/16

新增：
+ 找色算法深度优化，并增加更多丰富功能
+ 升级函数 [findColor](./鱼叉助手API文档.md/#findColor) 区域多点找色（支持偏色、精度值、找色方向设置）
+ 函数 [keepScreen](./鱼叉助手API文档.md/#keepScreen) 保持屏幕
+ 函数 [getColorRGB](./鱼叉助手API文档.md/#getColorRGB) 获取颜色RGB值
+ 升级函数 [findColors](./鱼叉助手API文档.md/#findColors) 高级区域多点找色（支持偏色、精度值、找色方向设置）
+ 对应 智图学院PC端（1.0.5版本）

删除：
+ 函数 ~~[findColor_vs](./鱼叉助手API文档.md/#findColor_vs) 固定位置找色~~（ 推荐 [getColorRGB](./鱼叉助手API文档.md/#getColorRGB) ）

## v1.0.0(25)
日期：2021/04/15

bug：
+ 修复 App UI 项目列表 添加 删除 序号错乱问题
+ 增加 App UI 项目列表 删除功能
+ 对应 智图学院PC端（1.0.5版本）

## v1.0.0(24)
日期：2021/04/13

新增：（需求作者：79324158）
+ 函数 [lua_exit](./鱼叉助手API文档.md/#lua_exit) 退出脚本程序

bug：
+ 修复函数 [touchDown](./鱼叉助手API文档.md/#touchDown) 自动连接设备失败 死循环导致开发模式无法停止运行的问题
+ 修复函数 [mSleep](./鱼叉助手API文档.md/#mSleep) 延时 开发模式无法停止运行的问题
+ UI刘海自动适配代码重写
+ 对应 智图学院PC端（1.0.5版本）

## v1.0.0(23)
日期：2021/04/12

新增：(需求作者：357339600)
+ 开发模式支持一键运行、一键下载、一键截图
+ 开发模式自动解压缩
+ 对应 智图学院PC端（1.0.5版本）

## v1.0.0(15)
日期：2021/03/16

bug：
+ 修复下载地址无法保存的bug.(反馈作者：357339600)

## v1.0.0(10) 重要更新
日期：2021/01/31

bug：
+ 修复运行时长2小时就iOS后台杀掉的bug，新版测试稳定超过24小时。

## v1.0.0(9)
日期：2021/01/29

新增：
+ 主页UI增加 测试鼠标 功能，测试设备是否连接正常。
+ [showUI](./鱼叉助手API文档.md/#showUI) 页面优化，新增单选框，支持背景图片，支持读取叉叉json文件

bug：
1. Lua API [UIshow](./鱼叉助手API文档.md/#UIshow) 更名为 [showUI](./鱼叉助手API文档.md/#showUI) ,兼容叉叉
2. [findColor_vs](./鱼叉助手API文档.md/#findColor_vs) 比色函数逻辑增强

## v1.0.0(8)
日期：2021/01/22

新增：
+ 自动下载功能会提前删除旧版本目录，保证程序运行最新程序，解决Lua代码没有更新的bug。

bug：
+ 程序下载成功，但Lua代码没有更新的bug。
+ 修复鼠标初始化，只有移动函数才会激活鼠标初始化，不使用移动不会进行初始化。

## v1.0.0(6)
日期：2021/01/20

新增：
+ [findColor_vs](./鱼叉助手API文档.md/#findColor_vs) 多点比色函数
+ [init](./鱼叉助手API文档.md/#init) 初始化方向函数，允许横屏取色,横屏点击
+ App UI 增加开发者发送图片可选项

## v1.0.0(4)
日期：2021/01/20

新增：
+ [教程](https://www.bilibili.com/video/BV1qt4y1z7Rw)
+ 启动直播录屏会先调用touchUp函数进行物联设备连接一次
+ 使用了touchMove,touchup内部会调用touchinit鼠标位置初始化(左下角)