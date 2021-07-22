# 鱼叉助手 API(内部测试..尚未开放)

### iOS/Android 通用函数
* 说明：删除线表示正在内测，尚未开放，请勿使用
* 反馈问题使用 [码云issues](https://gitee.com/lua_development/yxzhushou/issues) 留言，我们会关注和回复。

**触摸函数**
* [init](#init) 初始化屏幕方向
* [touchDown](#touchDown) 触摸按下
* [touchMove](#touchMove) 移动
* [touchUp](#touchUp) 触摸抬起

**图像函数**
* [findColor](#findColor) 区域多点找色<font color=#ffff00>（推荐使用）</font>
* [findColors](#findColors) 高级区域多点找色<font color=#ffff00>（推荐使用）</font>
* ~~[getColor](#getColorRGB) 获取屏幕某点颜色值~~
* [getColorRGB](#getColorRGB) 获取颜色RGB值
* ~~[findImageInRegionFuzzy](#findImageInRegionFuzzy) 模糊区域找图~~
* ~~[snapshot](#snapshot) 截图~~
* [keepScreen](#keepScreen) 保持屏幕
* ~~[binarizeImage](#binarizeImage) 二值化图片转换为table~~

**功能函数**
* [http](#http) HTTPget/HTTPpost 网络请求
* [base64encode](#base64encode) base64编码
* [base64decode](#base64decode) base64解码

**其他函数**
* [mSleep](#mSleep) 延时
* [sysLog](#sysLog) 系统日志
* [lua_exit](#lua_exit) 退出脚本执行

**UI界面函数**
* ~~[showUI](#showUI) 显示自定义脚本界面~~
* ~~[getUIContent](#getUIContent) 获取UI文件信息~~
* ~~[resetUIConfig](#resetUIConfig) 重置UI默认选项~~

**设备函数**
* [getScreenSize](#getScreenSize) 获取屏幕竖屏分辨率
* [getScreenDirection](#getScreenDirection) 获取屏幕方向
* ~~[setScreenScale](#setScreenScale) 设置屏幕等比例自动缩放~~
* ~~[setScreenAllScale](#setScreenAllScale) 设置屏幕全分辨率自动缩放~~
* [mTime](#mTime) 获取本地时间戳（毫秒）
* ~~[getNetTime](#getNetTime) 获取网络时间~~
* [getOSType](#getOSType) 获取系统类型
* [isPriviateMode](#isPriviateMode) 获取系统环境类型
* [getMobilephoneType](#getMobilephoneType) 获取系统型号
* ~~[getLocalInfo](#getLocalInfo) 获取系统语言属性~~

**仅支持Android函数**
* ~~[toast](#toast) 提示~~
* [createHUD](#createHUD) 创建HUD内容
* [showHUD](#showHUD) 显示HUD内容
* [hideHUD](#hideHUD) 隐藏HUD内容
* ~~[dialog](#dialog) 提示框~~
* ~~[dialogRet](#dialogRet) 带按钮的对话框~~
* ~~[dialogInput](#dialogInput) 带参数的对话框~~

# init
初始化屏幕方向

参数|类型|说明
-|-|-
appid|<font color=#FF8C00>string</font>|兼容叉叉，暂时无用
rotate|<font color=#00FFFF>number</font>|0 - 竖屏，1 - Home在右，~~2 - Home在左~~

返回值|类型|说明
-|-|-
nil|nil|nil

语法：
```lua
init(appid, rotate)
```

脚本示例：
```lua
--[[说明：假如使用竖屏对截图进行取色，需要告诉脚本 init("0",0) 开发取色方向为竖屏，如果实际运行时，当前为横屏与开发不一致，系统会对每个受影响函数的坐标参数转换为横屏坐标点，当前为竖屏则不作修改。]]

--竖屏
init("0", 0);

--横屏 home 在右
init("0", 1);
```
受 [init](#init) 影响函数：
+ [touchDown](#touchDown) 触摸按下 | [touchMove](#touchMove) 触摸移动 | [touchUp](#touchUp) 触摸抬起
+ [findColor](#findColor) 区域多点找色 | [getColorRGB](#getColorRGB) 获取单点RGB

# touchDown 
触摸按下

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

语法：
```lua
touchDown(id, x, y)
```

脚本示例：
```lua
--单击
touchDown(1, 100, 100)
mSleep(50)
touchMove(1, 100, 100)
mSleep(50)
touchUp(1, 100, 100)
```

# touchMove 
移动

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

语法：
```lua
touchMove(id, x, y)
```

脚本示例：
```lua
--移动距离过远，需要分段使用
touchDown(1, 100, 100)
mSleep(50)
--移动每次坐标值不能过大，与实际位置小于50以内最稳定
touchMove(1, 150, 150)
--移动需要时间，延时越大越稳定
mSleep(100)
touchMove(1, 200, 200)
mSleep(100)
touchUp(1, 200, 200)
```

# touchUp 
触摸抬起

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

语法：
```lua
touchUp(id, x, y)
```

脚本示例：
```lua
--单击
touchDown(1, 100, 100)
mSleep(50)
touchUp(1, 100, 100)
```

# findColor
区域多点找色<font color=#ffff00>（推荐使用）</font>

参数|类型|说明
-|-|-
left, top|<font color=#00FFFF>number</font>|`[必填]` 寻找区域左上角顶点屏幕坐标
right, bottom|<font color=#00FFFF>number</font>|`[必填]` 寻找区域右下角顶点屏幕坐标
x0,y0|<font color=#00FFFF>number</font>|`[必填]` 起始点坐标值，填写0,0时使用相对坐标体系，填非0,0的绝对坐标自动换算为相对坐标
color|<font color=#00FFFF>number</font>|`[必填]` 起始点颜色的十六进制颜色值
x1,y1|<font color=#00FFFF>number</font>|`[必填]` 偏移位置的坐标值
color1|<font color=#00FFFF>number</font>|`[必填]` 偏移位置需要匹配颜色的十六进制颜色值
degree|<font color=#00FFFF>number</font>|`[必填]` 全局找色精度，范围：1 ~ 100，当是100时为完全匹配
hdir|<font color=#00FFFF>number</font>|\[选填\] 水平搜索方向，0表示从左到右，1表示从右到左，默认为0
vdir|<font color=#00FFFF>number</font>|\[选填\] 垂直搜索方向，0表示从上到下，1表示从下到上，默认为0
priority|<font color=#00FFFF>number</font>|\[选填\] 搜索优先级，0表示水平优先，1表示垂直优先，默认为0

返回值|类型|说明
-|-|-
x，y|<font color=#00FFFF>number</font>|`[成功]` 返回第一个坐标，`[失败]` 返回 -1，-1

语法：
```lua
--[[说明：第一种和第二种最终都会自动转换成第三种语法]]

--第一种语法:
local x, y = findColor(
    {left, top, right, bottom},
    "x0|y0|color0,x1|y1|color1,x2|y2|color2,...",
    degree,
    hdir,
    vdir,
    priority
    )

--第二种语法:
local x, y = findColor(
    {left, top, right, bottom},
    "x0|y0|color0,x1|y1|color1(|degree1),x2|y2|color2(-offset2),...",
    degree,
    hdir,
    vdir,
    priority
    )

--第三种语法:
local x, y = findColor(
    {left, top, right, bottom},
    {
        {x = x0,y = y0,color = color0},
        {x = x1,y = y1,color = color1,(degree = degree1)},
        {x = x2,y = y2,color = color2,(offset = offset2)},
        ...
    },
    degree,
    hdir,
    vdir,
    priority
    )
```
脚本示例：
```lua
--开启保持屏幕
keepScreen(true);

--相对坐标写法：
--[[说明：第一个坐标(0,0)，系统则判断为相对坐标]]
local x, y = findColor(
    {0, 0, 639, 959},
    "0|0|0x181F85,29|1|0x00BBFE|90,103|-4|0x0B6BBE-0x050505,65|9|0x150972"
    )
local x, y = findColor(
    {0, 0, 639, 959},
    {
        {x = 0, y = 0, color = 0x181F85},
        {x = 29, y = 1, color = 0x00BBFE, degree = 90},
        {x = 103, y = -4, color = 0x0B6BBE, offset = 0x050505},
        {x = 65, y = 9, color = 0x150972}
    })

--绝对坐标写法：
--[[说明：第一个坐标(268,802)非(0,0)则系统判断为绝对坐标，会自动转换成(0,0)，再根据第一个坐标对其他位置进行相对坐标转换]]
local x, y = findColor(
    {0, 0, 639, 959},
    "268|802|0x181F85,297|803|0x00BBFE|90,371|798|0x0B6BBE-050505,333|811|0x150972"
)
local x, y = findColor(
    {0, 0, 639, 959},
    {
        {x = 268, y = 802, color = 0x181F85},
        {x = 297, y = 803 color = 0x00BBFE, degree = 90},
        {x = 371, y = 798 color = 0x0B6BBE, offset = 0x050505},
        {x = 333, y = 811 color = 0x150972}
    })

--单点偏色的写法：
--[[说明：默认为95，如果设置偏色，会优先使用偏色值作为相似度]]
local x, y = findColor(
    {0, 0, 749, 1333}, 
    "0|0|0xf12735-0x202002,387|-553|0x3eeb5d-0x555555,268|-148|0x2178fa",
    95, 0, 0, 0)

--单点相似度的写法：
--[[说明：默认为95，如果设置单点80，会优先使用80]]
local x, y = findColor(
    {0, 0, 749, 1333}, 
    "0|0|0xf12735|80,387|-553|0x3eeb5d|75,268|-148|0x2178fa",
    95, 0, 0, 0)

--关闭保持屏幕
keepScreen(false);
```
提高 [findColor](#findColor) 函数找色效率：
+ [keepScreen]() 保持屏幕

# getMobilephoneType
获取手机型号
```lua
local var = getMobilephoneType()
--安卓
var = "xiaomi 8"
--iOS
var = "iPhone 8"/"iPhone 7 Plus"
```

# getOSType
获取系统类型
```lua
local var = getOSType()
--安卓
var = "android"
--iOS
var = "iOS"
```

# isPriviateMode
获取系统环境类型

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

语法：
```lua
touchUp(id, x, y)
```

```lua
local var = isPriviateMode()
--越狱/ROOT
var = "1"
--免越狱/免ROOT
var = "0"
```