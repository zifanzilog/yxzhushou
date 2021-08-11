# Vscode 更新日志
[插件下载](https://gitee.com/lua_development/yxzhushou/blob/master/vscode插件安装包)
<!-- 已知bug：-->
<!-- lua.exe会被360当作木马删除 需要重新编译lua,dll分离-->
<!-- 不允许终端修改为cmd启动，只能pshell 技术原因，无法获取当前终端类型-->
## 1.0.0
日期：2021.8.4

新增：
+ 启动时进行 main.lua 检查
+ 支持多项目结构开发
+ 支持外部 main.lua 启动调试
+ 优化逻辑 当前活跃窗口为项目窗口
+ 抓图工具 ‘载入’ 只允许读取 png
+ 增加取色代码生成 ‘<编辑>’ 功能 
+ lua.exe 检查是否存在

bug：
+ 修复 vscode路径名称有空格时无法识别
+ 修复 vscode插件路径名称有空格时无法识别
+ 修复 用户路径名称有空格时无法识别

## 0.0.23
日期：2021.7.27

新增：
+ data.lua 格式化自定义 
+ 优化 代码生成 逻辑判断
+ 优化 选择范围 随鼠标移动

## 0.0.22
日期：2021.7.21

新增：
+ 添加 \[终端\] 显示 \[系统日志\]
+ 优化 设备连接模式
+ 优化 鱼叉助手 API 树视图
+ 添加 选择范围 功能键
+ 优化 取色器 逻辑判断
+ 优化 二值化 逻辑判断

## 0.0.16
日期：2021.5.5

新增：
+ 添加 App 接口
+ 添加 [luacheck](https://github.com/mpeterv/luacheck) 诊断器（0.19.0）
+ 优化 [luacheck](https://github.com/mpeterv/luacheck) 支持中文诊断

## 0.0.15
日期：2021.4.5

新增：
+ 添加 抓图工具
+ 添加 [Luapanda](https://github.com/Tencent/LuaPanda) 调试器（3.2.0）