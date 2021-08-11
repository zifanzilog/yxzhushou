# 鱼叉助手 API(内部测试..尚未开放)

#### iOS/Android 通用函数
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
* [getColor](#getColorRGB) 获取屏幕某点颜色值
* [getColorRGB](#getColorRGB) 获取屏幕某点颜色R,G,B值
* ~~[findImageInRegionFuzzy](#findImageInRegionFuzzy) 模糊区域找图~~
* ~~[snapshot](#snapshot) 截图~~
* [keepScreen](#keepScreen) 保持屏幕
* [binarizeImage](#binarizeImage) 二值化图片转换为table

**功能函数**
* ~~[http](#http) HTTPget/HTTPpost 网络请求~~
* ~~[base64encode](#base64encode) base64编码~~
* ~~[base64decode](#base64decode) base64解码~~

**其他函数**
* [mSleep](#mSleep) 延时
* [sysLog](#sysLog) 系统日志
* [lua_exit](#lua_exit) 退出脚本执行

**界面函数**
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

**安卓函数**

仅支持Android使用

* ~~[toast](#toast) 提示~~
* [createHUD](#createHUD) 创建HUD内容
* [showHUD](#showHUD) 显示HUD内容
* [hideHUD](#hideHUD) 隐藏HUD内容
* ~~[dialog](#dialog) 提示框~~
* ~~[dialogRet](#dialogRet) 带按钮的对话框~~
* ~~[dialogInput](#dialogInput) 带参数的对话框~~

# init
### **初始化屏幕方向**

参数|类型|说明
-|-|-
appid|<font color=#FF8C00>string</font>|兼容叉叉，暂时无用
rotate|<font color=#00FFFF>number</font>|0 - 竖屏，1 - Home在右，~~2 - Home在左~~

**说明：**
+ 假如使用竖屏对截图进行取色，需要告诉脚本 init("0",0) 开发取色方向为竖屏，如果实际运行时，当前为横屏与开发不一致，系统会对每个受影响函数的坐标参数转换为横屏坐标点，当前屏幕方向与开发方向一致则不作修改。

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
init(appid, rotate)
```

**脚本示例：**
```lua

--开发方向为竖屏
init("0", 0);

--开发方向为横屏 home 在右
init("0", 1);
```
受 [init](#init) 函数影响的函数：
+ [touchDown](#touchDown) 触摸按下
+ [touchMove](#touchMove) 触摸移动
+ [touchUp](#touchUp) 触摸抬起
+ [findColor](#findColor) 区域多点找色
+ [findColors](#findColors) 区域多点找色
+ [getColor](#getColor) 获取屏幕某点颜色值
+ [getColorRGB](#getColorRGB) 获取屏幕某点颜色R,G,B值

# touchDown 
### **触摸按下**

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
touchDown(id, x, y)
```

**脚本示例：**
```lua
touchDown(1, 100, 100) --单击
mSleep(50)
touchMove(1, 100, 100)
mSleep(50)
touchUp(1, 100, 100)
```

# touchMove 
### **移动**

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
touchMove(id, x, y)
```

**脚本示例：**
```lua
touchDown(1, 100, 100) --移动距离过远，需要分段使用
mSleep(50)
touchMove(1, 150, 150) --移动每次坐标值不能过大，与实际位置小于50以内最稳定
mSleep(100)            --移动需要时间，延时越大越稳定
touchMove(1, 200, 200)
mSleep(100)
touchUp(1, 200, 200)
```

# touchUp 
### **触摸抬起**

参数|类型|说明
-|-|-
id|<font color=#00FFFF>number</font>|手指 id，Root/越狱支持多指操作 1 - 10，免越狱/免Root 设置 1
x, y|<font color=#00FFFF>number</font>|坐标

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
touchUp(id, x, y)
```

**脚本示例：**
```lua
touchDown(1, 100, 100) --单击
mSleep(50)
touchUp(1, 100, 100)
```

# findColor
### **区域多点找色<font color=#ffff00>（推荐使用）</font>**

参数|类型|说明
-|-|-
left, top|<font color=#00FFFF>number</font>|`[必填]` 寻找区域左上角顶点屏幕坐标
right, bottom|<font color=#00FFFF>number</font>|`[必填]` 寻找区域右下角顶点屏幕坐标
x0,y0|<font color=#00FFFF>number</font>|`[必填]` 起始点坐标值，填写0,0时使用相对坐标体系，填非0,0的绝对坐标自动换算为相对坐标
color|<font color=#00FFFF>number</font>|`[必填]` 起始点颜色的十六进制颜色值
x1,y1|<font color=#00FFFF>number</font>|`[必填]` 偏移位置的坐标值
color1|<font color=#00FFFF>number</font>|`[必填]` 偏移位置需要匹配颜色的十六进制颜色值
degree1|<font color=#00FFFF>number</font>|\[选填\] 偏移位置找色相似度，范围：1 ~ 100，当是100时为完全匹配
offset1|<font color=#00FFFF>number</font>|\[选填\] 偏移位置找色偏色值，十六进制颜色值，当是0x000000时为完全匹配，当大于0时degree1自动设置为100
degree|<font color=#00FFFF>number</font>|`[必填]` 全局找色相似度，范围：1 ~ 100，当是100时为完全匹配
hdir|<font color=#00FFFF>number</font>|\[选填\] 水平搜索方向，0表示从左到右，1表示从右到左，默认为0
vdir|<font color=#00FFFF>number</font>|\[选填\] 垂直搜索方向，0表示从上到下，1表示从下到上，默认为0
priority|<font color=#00FFFF>number</font>|\[选填\] 搜索优先级，0表示水平优先，1表示垂直优先，默认为0

**说明：**
* 起始点坐标值填写0,0时，偏移位置坐标值使用相对坐标；填写为非0,0的坐标时，则认为偏移位置坐标为绝对坐标，找色时，将根据填写的绝对坐标换算出的相对坐标进行寻找。
* 偏移位置颜色的偏色值或相似度可任意选用，同时填写了偏色值和相似度时，将以偏色为准，忽略相似度值。
* 个别偏移位置颜色偏色值或相似度优先于全局找色相似度，全局找色相似度对未指定偏色或相似度的颜色有效。

返回值|类型|说明
-|-|-
x, y|<font color=#00FFFF>number</font>|`[成功]` 返回颜色第一个坐标，`[失败]` 返回 -1，-1

**关于搜索方向：**
hdir|vdir|priority|<center>区域搜索路径</center>
-|-|-|-
0|0|0|左上角 → 右上角 → 左下角 → 右下角
0|0|1|左上角 → 左下角 → 右上角 → 右下角
0|1|0|左下角 → 右下角 → 左上角 → 右上角
0|1|1|左下角 → 左上角 → 右下角 → 右上角
1|0|0|右上角 → 左上角 → 右下角 → 左下角
1|0|1|右上角 → 右下角 → 左上角 → 左下角
1|1|0|右下角 → 左下角 → 右上角 → 左上角
1|1|1|右下角 → 右上角 → 左下角 → 左上角

**语法：**
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
**脚本示例：**
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

# findColors
### **高级区域多点找色<font color=#ffff00>（推荐使用）</font>**

**说明：**

[findColor](#findColor) 扩展函数

返回值|类型|说明
-|-|-
point|<font color=#FFFF00>table</font>|`[成功]` 返回所有符合条件的参照点的坐标，最多99个 `[失败]` 返回空表 { }

**返回的 table 为key-value的形式，如下：**
```lua
--成功
local point = {
 {x = 100,y = 110},
 {x = 200,y = 210},
 {x = 300,y = 310},
 ...
}
--失败
local point = {}
```

提高 [findColors](#findColors) 函数找色效率：
+ [keepScreen]() 保持屏幕

# getColor
### **获取屏幕某点颜色值**

参数|类型|说明
-|-|-
x，y|<font color=#00FFFF>number</font>|获取颜色值的屏幕坐标

返回值|类型|说明
-|-|-
color|<font color=#00FFFF>number</font>|该点的十进制颜色值RGB

**语法：**
```lua
local color = getColor(x, y)
```

**脚本示例：**
```lua
--如果某点符合某颜色则点击
if getColor(100, 100) == 0xffffff then 
   touchDown(1, 100, 100)
   mSleep(50)
   touchUp(1, 100, 100)
end
```
**注意事项：**
* [getColor](#getColor) 函数获得的颜色值十六进制文本中，实际顺序为RGB

# getColorRGB
### **获取屏幕某点颜色R,G,B值**

参数|类型|说明
-|-|-
x，y|<font color=#00FFFF>number</font>|获取颜色值的屏幕坐标

返回值|类型|说明
-|-|-
r，g，b |<font color=#00FFFF>number</font>|该点的十进制颜色值RGB

**语法：**
```lua
local r, g, b = getColorRGB(x, y)
```

**脚本示例：**
+ 判断某点的颜色与某颜色相似：
```lua
local r,g,b = getColorRGB(100,100); --获取该点的R,G,B值
if r > 200 and b < 150 then   --判断颜色强度
    touchDown(1,100,100)
    mSleep(50)
    touchUp(1,100,100)
end
```
+ 封装一个单点模糊比色函数：
```lua
function isColor(x,y,c,s)   --x,y为坐标值，c为颜色值，s为相似度，范围0~100。
    local fl,abs = math.floor,math.abs
    s = fl(0xff*(100-s)*0.01)
    local r,g,b = fl(c/0x10000),fl(c%0x10000/0x100),fl(c%0x100)
    local rr,gg,bb = getColorRGB(x,y)
    if abs(r-rr)<s and abs(g-gg)<s and abs(b-bb)<s then
        return true
    end
    return false
end
if isColor(963,  961, 0x7b593f,90) then     
    touchDown(963, 961)
    mSleep(50)
    touchUp(963, 961)
end
```
+ 封装一个多点比色函数：
```lua
function isColors(color,s) --固定坐标 多点比色
	s = s or 95  --相似度
	s = math.floor(0xff*(100-s)*0.01)    --浮点数
	for var = 1, #color do
		local lr,lg,lb = getColorRGB(color[var][1],color[var][2])   --游戏颜色
		local rgb = color[var][3]   --脚本颜色
		local r = math.floor(rgb/0x10000)    --脚本颜色RGB
		local g = math.floor(rgb%0x10000/0x100)
		local b = math.floor(rgb%0x100)
		if math.abs(lr-r) > s or math.abs(lg-g) > s or math.abs(lb-b) > s then  --绝对值
			return false
		end
	end
	return true
end

--使用
local color = {
  {540,498,0xffffff},
  {519,235,0x0a67c9},
  {607,238,0x0d6fd2}
}
keepScreen(true);--开  搭配保持屏幕，可提高效率
if isColors(color,95) then
  print("找到")
end
keepScreen(false);--关
```

**注意事项：**
* [getColorRGB](#getColorRGB) 函数获得的颜色值十六进制文本中，实际顺序为RGB

# keepScreen
### **保持屏幕**

参数|类型|说明
-|-|-
bool|<font color=#00FF00>boolean</font>| 启动 = true ，关闭 = false

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
keepScreen(bool)
```

**脚本示例：**
```lua
keepScreen(true); --停止截图，保留第一次截图
for y = 1, 640, 10 do
    for x = 1, 960, 10 do
        --格式化颜色为十六进制文本
        local color = string.format("%X", getColor(x, y));
        --输出
        print("("..x..", "..y..") Color: "..color..".");
    end
end
keepScreen(false); --恢复截图
```
受 [keepScreen](#keepScreen) 影响函数：
+ [findColor](#findColor) 区域多点找色
+ [findColors](#findColors) 高级区域多点找色
+ [getColor](#getColor) 获取屏幕某点颜色值
+ [getColorRGB](#getColorRGB) 获取屏幕某点颜色R,G,B值

# binarizeImage
### **二值化图片转换为table**

参数|类型|说明
-|-|-
rect|<font color=#FFFF00>table</font>|`[必填]` {x1, y1, x2, y2} 屏幕二值化的识别范围，越准确越好
diff|<font color=#FFFF00>table</font>|`[必填]` {"颜色1-偏色1", "颜色-偏色2", ...} 色值范围，可以提供多个，供二值化使用

返回值|类型|说明
-|-|-
colorTbl|<font color=#FFFF00>table</font>|图像二值化后的table，0 代表黑色，1 代表白色

**语法：**
```lua
 local colorTbl = binarizeImage({
   rect = {x1, y1, x2, y2},
   diff = {diff}
  })
```

**脚本示例：**
```lua
local colorTbl = binarizeImage({
  rect = {30, 80, 53, 101},
  diff = {"0xf7d363-0x1f1f1f", "0xefaa29-0x1f1f1f"}
})
-- 使用打印表函数输出colorTbl结果
ptable(colorTbl)
--[[
colorTbl格式类似这样：
{
    {0,0,0,0,1,0,0,0,0,0,0,0,0,0},
    {0,0,0,1,0,1,0,0,0,0,0,0,0,0},
    {0,0,0,0,1,0,0,0,0,0,0,0,0,0},
    {0,0,0,1,0,0,0,0,0,0,0,0,0,0},
    {0,0,0,1,0,0,0,0,0,0,0,0,0,0},
    {0,0,1,1,0,0,0,0,0,0,0,0,0,0},
    {0,1,0,1,0,0,0,0,0,0,0,0,0,0},
    {0,1,1,1,1,1,0,1,1,0,0,0,0,0},
    {1,0,1,1,0,0,0,0,1,1,1,0,0,0},
    {0,1,0,1,0,0,0,0,0,0,1,1,0,0},
    {1,1,1,0,0,0,0,0,0,0,1,1,0,0},
    {1,0,0,0,0,0,0,0,0,0,1,0,1,0},
    {1,0,0,0,0,0,0,0,0,0,0,1,1,0},
    {1,0,0,0,0,0,0,0,0,0,0,1,0,1},
    {1,0,0,0,0,0,0,0,0,0,0,0,1,0},
    {1,0,0,0,0,0,0,0,0,0,0,1,1,1},
    {1,0,0,0,0,0,0,0,0,0,0,1,0,1},
    {1,1,0,0,0,0,0,0,0,0,0,1,1,0},
    {1,0,1,0,0,0,0,0,0,0,1,0,0,0},
    {0,1,1,1,0,1,0,0,1,1,1,0,0,0},
    {0,0,0,1,1,1,0,1,1,0,0,0,0,0},
    {0,0,0,0,0,0,1,0,1,0,0,0,0,0}
}
]]
```

# mSleep
### **延时**

参数|类型|说明
-|-|-
interval|<font color=#00FFFF>number</font>|单位为毫秒，脚本暂停执行的时间长度

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
mSleep(interval)
```

**脚本示例：**
```lua
--延迟5秒
mSleep(5000)

--长按 3 秒
touchDown(1, 200, 300); --按下
mSleep(3000);           --延迟 3 秒
touchUp(1, 200, 300);   --抬起
```

**注意事项：**
* 延迟函数一般是用来模拟人在界面上的操作，因此要考虑人在各种情况下的延迟、界面加载时的响应时间。
* 延迟间隔不可过短，当 interval <= 50 ms 时，延迟精确度大幅下降，当 interval <= 16 ms 时，实际延迟约在16 ms左右。
* 请勿将此函数用于长时间的精确计时。
* 1 秒 (s) = 1000 毫秒 (ms)。

# sysLog
### **系统日志**

参数|类型|说明
-|-|-
content|<font color=#FF8C00>string</font>|需要显示的日志内容

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
sysLog(contents)
```

**注意事项：**
+ 该函数将日志输出到对应平台的开发窗口
+ 该函数可通过 [setSysConfig](#setSysConfig) 设置项"isFileLog"设置为写入日志到文件，详情查看“[setSysConfig](#setSysConfig) 设置系统参数”条目

# lua_exit
### **退出脚本执行**

**脚本示例：**
```lua
print("1")
lua_exit() --结束
print("2") --无法到达
```

# getMobilephoneType
### **获取手机型号**

参数|类型|说明
-|-|-
var|<font color=#FF8C00>string</font>|手机型号

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
getMobilephoneType()
```

**脚本示例：**
```lua
local var = getMobilephoneType()
--安卓
var = "xiaomi 8"
--iOS
var = "iPhone 8"/"iPhone 7 Plus"
```

# getOSType
### **获取系统类型**

参数|类型|说明
-|-|-
var|<font color=#FF8C00>string</font>|系统类型

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
getOSType()
```

**脚本示例：**
```lua
local var = getOSType()
--安卓
var = "android"
--iOS
var = "iOS"
```

# isPriviateMode
### **获取系统环境类型**

参数|类型|说明
-|-|-
var|<font color=#FF8C00>string</font>|系统环境类型

返回值|类型|说明
-|-|-
nil|nil|nil

**语法：**
```lua
isPriviateMode()
```

**脚本示例：**
```lua
local var = isPriviateMode()
--越狱/ROOT
var = "1"
--免越狱/免ROOT
var = "0"
```