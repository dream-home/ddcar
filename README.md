
# 祺迹车管客户端接入协议 v2.4.0

## 目录
* [目录](#目录)
* [概述](#概述)
* [协议说明](#协议说明)
 * [业务说明](#业务说明)
* [规范说明](#规范说明)
 * [status公共状态](#status公共状态)
 * [字段类型说明](#字段类型说明)
 * [HTTP基本方法说明](#http基本方法说明)
 * [API请求规则](#api请求规则)
* [协议内容](#协议内容)
 * [获取图片验证码](#获取图片验证码)
 * [验证用户输入的图片验证码](#验证用户输入的图片验证码)
 * [获取短信验证码](#获取短信验证码)
 * [验证用户输入的短信验证码](#验证用户输入的短信验证码)
 * [注册](#注册)
 * [登录](#登录)
 * [验证用户存在](#验证用户存在)
 * [修改密码](#修改密码)
 * [集团信息](#集团信息)
 * [上传车辆批量修改的excel](#上传车辆批量修改的excel)
 * [批量修改车辆](#批量修改车辆)
 * [组和车辆列表信息](#组和车辆列表信息)
 * [车辆信息](#车辆信息)
 * [新建、修改、删除车队（组）](#新建修改删除车队组)
 * [上传添加设备excel](#上传添加设备excel)
 * [设备批量添加](#设备批量添加)
 * [添加单个设备](#添加单个设备)
 * [实时定位](#实时定位)
 * [进入紧急模式时间](#进入紧急模式时间)
 * [修改设备模式（紧急模式,普通模式）](#修改设备模式紧急模式普通模式)
 * [轨迹查询](#轨迹查询)
 * [管理员信息](#管理员信息)
 * [退出登录](#退出登录)
 * [注册wspush](#注册wspush)
 * [重置密码](#重置密码)
 * [分级查询组和车辆列表信息](#分级查询组和车辆列表信息)
 * [搜索车辆或者组](#搜索车辆或者组)
 * ~~[车辆进入远程追踪](#车辆进入远程追踪)~~
 * [警告设置信息获取设置](#警告设置信息获取设置)
 * [警告历史的查询功能](#警告历史的查询功能)
 * [用户反馈](#用户反馈)
 * [未读告警的数据条数](#未读告警的数据条数)
 * [告警信息列表](#告警信息列表)
 * [查询获取用户集团车架号](#查询获取用户集团车架号)
 * [子账号管理](#子账号管理)
 * [导出管理员账号下车辆信息excel](#导出管理员账号下车辆信息excel)
 * [app下载跳转地址](#app下载跳转地址)
 * [车辆下所有终端最新位置](#车辆下所有终端最新位置)
 * [终端配对历史](#终端配对历史)
 * [根据sn同步获取终端最新状态](#根据sn同步获取终端最新状态)
 * [终端详细信息](#终端详细信息)
 * [终端历史位置信息](#终端历史位置信息)
 * [终端开关状态设置](#终端开关状态设置)
 * [终端设备历史](#终端设备历史)
 * [终端通讯时间](#终端通讯时间)

## 概述

* 本协议为祺迹客户端与服务端通信协议。为了方便和快速开发,客户端和服务端按照协议可以同时开发,以协议作为开发规范。如需要有修改,请先修改协议,再按照协议进行开发,以降低开发耦合度。

## 协议说明

#### 业务说明

* 所有的时间戳均采用UTC时间,用Epoch表示,精确到秒
* location的经纬度全部为整数,精确到毫秒。(经纬度均除以3600000来获取真实值)。
* 如果相关字为空,提供相应的缺省值。比如一个类型为str的字段为 空, 提供空字符串; 一个类型为int的字段为空, 提供 0。

## 规范说明

* 所有参数一律小写
* 所有页面名称一律小写
* 数据交换传输用json格式,已标注除外,json格式如下
```json
{
    "status": "服务器响应状态",
    "message": "服务器响应消息",
    "data":{}
}
```

* 所有服务器传入json格式参数必须是object对象

#### status公共状态
* 999 未登录或登陆超时,请重新登录。

#### 字段类型说明

* object: json对象,default:｛｝
* array:数组,default :[]
* string:字符串 default: ""(空字符串)
* number: 数字类型
* data:封装返回的数据,default:{}

#### HTTP基本方法说明

* GET: 向服务器查询数据请求,返回请求数据或错误码。
* POST: 向服务器请求添加新条目,返回处理状态值
* PUT:向服务器发送修改条目请求,返回处理状态值
* DELETE:向服务器发送删除条目请求,返回处理状态值

#### API请求规则
* GET: 请求统一使用restful风格,请求参数依次使用`\`隔开
* POST: 统一使用body中的json格式字符串进行提交
* PUT: 提交方式同POST
* DELETE: 请求方式同GET

## 协议内容

#### 获取图片验证码

URL: /captcha

Table: 无

支持方法:GET

支持客户端:Web , Android, IOS

* GET方法

 功能描述:获取图片验证码。

 请求参数:无

 返回结果:

 直接返回验证码的图片地址

Example调用格式:

```html
<img src=" /captcha?rand=0.231456789"/>
```

注:rand为0-1之间的一个随机数

#### 验证用户输入的图片验证码

URL: /checkcaptcha

Table: 无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:验证用户输入的图片验证码是否正确

请求参数:

| 参数    | 类型   | 描述       | 默认值 | 是否必填 |
|---------|--------|------------|--------|-------|
| captcha | string | 图片验证码 | ""    | Yes     |

返回结果:

| 参数名称 | 参数类型 | 描述                                    |
|----------|----------|--------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                       |
| data     | object     | 返回的数据                            |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

注:其他状态信息

* 203:图片验证码错误

#### 获取短信验证码

URL: /smscaptcha

Table: 暂无

支持方法:POST

支持客户端:Web , Android, IOS

* POST方法

功能描述:获取短信验证码, 短信验证码发送到用户手机。

请求参数:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| mobile   | string   | 手机号  |
| type    | string   | 短信类型 (register:注册用户时, resetpass:找回密码时) |

Example:
```json
{
    "mobile": "15982463820",
    "type": "register"
}
```

返回结果:

| 参数名称    | 参数类型 | 描述                                      |
|-------------|----------|-------------------------------------------|
| status      | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message     | string   | 处理结果描述消息                          |
| data        | object     | 包含下列参数                              |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

注:其他状态信息

* 228:该手机号已经注册
* 223:该用户不存在
* 134:短信获取类型不存在
* 918:每日获取验证码不可超过5次
* 917:短信服务器繁忙,请稍后重试

#### 验证用户输入的短信验证码

URL: /checksmscaptcha

Table: 暂无

支持方法:POST

支持客户端:Web , Android, IOS

* POST方法

功能描述:验证用户输入的短信验证码是否正确

请求参数:

| 参数        | 类型   | 描述       | 默认值 | 是否必填 |
|-------------|--------|------------|--------|----------|
| sms_captcha | string | 短信验证码 | ""     | Yes      |

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object     | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

注:其他状态信息

202:验证码错误，请重新输入。

104:短信验证码已失效，请重新获取。

#### 注册

URL: /register

Table: 暂无

支持方法:POST

支持客户端:Web , Android, IOS

* POST方法

功能描述:用户通过填写用户名,密码,验证码完成注册。

* 密码加密规则如下:
* md5(md5(原密码)+salt)

请求参数:

| 参数        | 类型   | 描述                                 | 默认值 | 是否必填 |
|-------------|--------|--------------------------------------|--------|----------|
| username    | string | 手机号                               |  ""    | Yes      |
| password    | string | 用户密码md5加密后的值,长度32位       |  ""    | Yes      |
| from        | int    | 客户端类型:0:Web, 1:Android, 2:IOS   | 0      | Yes      |

Example:
```json
{
    "username": "15882081234",
    "password": "MD5('123456')",
    "from": 0
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object     | 返回的数据                                |
| user_id  | string   | （无用）加密后的用户唯一标识（登录成功才有）      |
| user_type| int      | （无用）用户类型 1-管理员 2-监控员(无效，跟其他接口不一致) 3-子账号  |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "user_id": "12234255ddfa34",
        "user_type": 1
    }
}
```

注:其他状态信息

131:非法的手机号
228:该手机号已经注册


#### 登录

URL: /login

Table: 暂无

支持方法:GET, POST

支持客户端:Web, Android, IOS (GET 方法只支持Web)

* GET方法

功能描述:体验帐号登录

请求参数:无

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

* POST方法

功能描述:注册用户登录
请求参数: 以json格式提交

| 参数         | 类型   | 描述                                                      | 默认值 | 是否必填 |
|--------------|--------|-----------------------------------------------------------|--------|-------|
| username     | string | 注册手机号                                                |    ""    | Yes  |
| password     | string | 用户密码,范围:6-20位                                    |      ""  | Yes   |
| captcha      | string | 用户输入验证码,范围:4位 (用户名或密码错误3次后才有)     |      ""  | Yes      |
| from         | int    | 客户端类型:0:Web, 1:Android, 2:IOS                      | 0    | Yes     |
| remember_me  | int    | 登录时选择是否记住我,0:没有勾选"记住我"1:已经勾选"记住我" | 0     | Yes      |

Example:
```json
{
    "username":"15882081234",
    "password": "111111",
    "captcha": "1234",
    "from": 0,
    "remember_me": 0
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                 |
|----------|----------|--------------------------------------|
| status   | string   | 状态                                 |
| message  | string   | 用户名、密码的错误消息               |
| data     |  object    | 包含下列参数                         |
| user_id  | string   | 加密后的用户唯一标识（登录成功才有） |
| user_type| int      | 用户类型 1-管理员 2-子账号 3-监控员（无效）  |
| privilege| string   | [子账号权限类型定义](#子账号权限类型) |
| name_show | int | 集团下车辆名优先显示模式<br/>1-车架号<br/>2-车牌号 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "user_id": "12234255ddfa34",
        "user_type": 1,
        "privilege": "1,2,3,4",
        "name_show": 1
    }
}
```

#### 验证用户存在

URL: /checkuserexists

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:验证用户名

请求参数:

| 参数     | 类型   | 描述   | 默认值 | 是否必填 |
|----------|--------|--------|--------|----------|
| username | string | 手机号 |    ""    | Yes      |

Example:
```json
{
    "username": "15882081234",
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 用户名、密码的错误消息                    |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功！",
    "data": {}
}
```

注:其他状态信息

* 223:该用户不存在

#### 修改密码

URL: /updatepassword

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:修改密码（已经登录）

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| oldpassword | string | 当前密码         |   ""     | Yes     |
| password | string | 新密码 |    ""    | Yes      |

Example:
```json
{
    "oldpassword": "12345645",
    "password": "123456"
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 错误信息                                  |
| data     | object     | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message":"密码修改成功",
    "data": {}
}
```

注:其他状态信息

205:当前密码错误,请重新输入

#### 集团信息

URL: /corpinfo

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:修改集团信息

请求参数:

| 参数      | 类型   | 描述     | 默认值 | 是否必填 |
|-----------|--------|----------|--------|----------|
| corp_name | string | 集团名称 |    ""  | Yes      |
| name_show | int | 集团下车辆名优先显示模式<br/>1-车架号<br/>2-车牌号 |    ""  | No      |

Example:
```json
{
    "corp_name": "红光集团",
    "name_show": 1
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### 上传车辆批量修改的excel

URL: /updatecarsexcel

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:上传车辆批量修改的excel

请求参数:

| 参数       | 类型 | 描述            | 默认值 | 是否必填 |
|------------|------|-----------------|--------|----------|
| upload_file | string | 上传的excel文件名 | ""   | Yes      |
| *file* | File | 上传的excel文件 | ""   | Yes      |

备注： 这里使用的是`multipart/form-data`的 content-type

返回结果:

| 参数名称   | 参数类型 | 描述                                         |
|------------|----------|----------------------------------------------|
| status     | int      | 处理结果状态值（0表示成功, 其他表示错误）    |
| message    | string   | 处理结果描述消息                             |
| data       | object     | 包含下列参数                                 |
| res        | array     | 数据的检测结果（如果没有错误不返回下列数据） |
| row_no     | int      | 错误数据的行号                               |
| sn         | string   | 设备标识                                     |
| vin        | string   | 车辆标识                                     |
| cnum       | string   | 车牌号                                       |
| icon       | int      | 图标                                         |
| group_name | string   | 组名                                         |
| message    | array    | 错误原因信息数组                             |

Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
            "res":[
            {
                "row_no": "156",
                "sn": "SN123456",
                "vin": "123",
                "cnum": "川A88888",
                "icon": 1,
                "group_name": "test",
                "message": ["SN设备号不存在", "车辆不存在"]
            }
        ]
    }
}
```

#### 批量修改车辆

URL: /batchupdatecars

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:批量修改车辆

请求参数:无

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

注:左侧树的改变用push推送。上传车辆批量修改

#### 组和车辆列表信息

URL: /cartree

Table: 暂无

支持方法:GET,POST

支持客户端:Web, Android, IOS

* GET方法

功能描述:获取集团,车队,车辆,终端信息

请求参数:无

返回结果:

| 参数名称     | 参数类型 | 描述                                    |
|--------------|----------|-----------------------------------------|
| status       | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                        |
| data         | object     | 包含下列参数                       |
| id         | string     | 数据id                              |
| pid         | string   | 父id                              |
| name       | string     | 名称                             |
| type     | string      | 包括:group,car,terminal   |
| info       | object     | 详细信息                             |
| cid      | string   | 集团id                                    |
| create_time  | int      | 创建时间                            |
| group_id     | string   | 组id              |
| team_name     | string   | 组名                                 |
| car_id          | string   | 车辆id                          |
| vin       | string   | 车辆唯一标识                                   |
| cnum         | string      | 车牌号                                |
| icon         | int      | 车辆图标                                |
| position      | object     | 位置信息,包含下列参数                    |
| latitude     | int      | 加密前纬度                              |
| longitude    | int      | 加密前经度                              |
| clatitude    | int      | 加密后纬度                              |
| clongitude   | int      | 加密后经度                              |
| altitude    | int      | 高度                                    |
| degree       | string   | 方向                                        |
| address      | string   | [deprecated] 位置描述                         |
| locate_time  | int      | 取点时间                                |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位, 2: 未知-刚绑定未发送过报文的情况  ）      |
| speed        | float    | 速度                                    |
| locate_error | int      | 定位误差                                |
| tid          | string   | 终端id                                  |
| sn           | string   | 终端sn                                  |
| activate_code | string   | 激活码                                  |
| type         | string      | ZJ210,ZJ211,ZJ300                       |
| mode         | object   | 工作模式                                |
| firmware_version|string|固件版本 F: 全功能ZJ210, E: 简易版ZJ210, S: 长待机版ZJ210(车管一期), T: 全功能版ZJ211, U: 简易版ZJ211, V:带WiFi功能的ZJ300|
| terminal_mode | object   | 0：ZJ211/ZJ300 待机模式，1：ZJ211/ZJ300 唤起模式，2：ZJ210或ZJ211/ZJ300 配对模式 3：ZJ210 单独模式 |
| param_interval | string   | 终端请求参数的间隔（例如：30  表示 30分钟）                               |
| device_mode   | int   | 0:普通模式，1:待紧急模式，2:紧急模式|
| gps_status     | string   | 终端GPS状态（0：关闭  1：打开）                             |
| gsm   | int   | GSM信号强度                         |
| gps   | int   | GPS信号的SNR值                        |
| pbat   | int   | 剩余电量百分比                         |
| login   | int   | 登录状态,1 = 登录,0 = 未登录, 2 = 待机             |
| login_time   | int   | 终端最近一次登录时间                      |
| battery_voltage   | int   | 210外接电瓶电压值                      |
| status   | int   | 终端状态,0 = 未知状态 1 = 停留,2 = 行驶,3 = 熄火,4 = 怠速  |
| charge_status   | int   | 终端充电状态,0 = 未连接外部电源正在放电, 1 = 连接外部电源正在充电, 2 = 连接外部电源但不在充电|
| emergency_status   | int   | [deprecated] 0:未开启进入紧急模式,1:待进入紧急模式,2:已经进入紧急模式|
| emergentable   | int   | [deprecated] 0:不能进入紧急模式,1:能进入紧急模式|
| light   | int   | 终端感光开关 0：关闭 1：开启 |
| light_status   | int   | ZJ300设备的感光状态<br/>-1 - 未知（默认值）<br/>0 - 感光功能关闭<br/>1 - 无光   <br/>2 - 有光 |
| wifi   | int   | 终端wifi热点开关 0：关闭 1：开启 |
| wifi_status   | int   | ZJ300的wifi热点状态<br/>-1 - 未知（默认值）<br/>0 - wifi功能关闭<br/>1 - wifi热点开启   <br/>2 - wifi热点关闭 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":[
        {
            "id": "1",
            "pid": "0",
            "cid": "1",
            "name": "集团名称",
            "type": "group",
            "info": {
                "group_id": "11",
                "team_name": "顶级组名称",
                "create_time": 123435233
            }
        },
        {
            "id": "11",
            "pid": "1",
            "name": "车队1",
            "type": "group",
            "info":{
                "group_id": "11",
                "team_name": "车队1",
                "create_time": 123435233
            }
        },
        {
            "id": "111",
            "pid": "11",
            "name": "车辆1",
            "type": "car",
            "cid": "1",
            "info":{
                "car_id": "111",
                "vin": "1111",
                "cnum": "川A88888",
                "icon": 1,
                "emergency_status": 1,
                "emergentable": 1,
                "position":{
                    "latitude": 80551404,
                    "longitude": 408851028,
                    "clatitude": 80560938,
                    "clongitude": 408892892,
                    "altitude": 36,
                    "degree": 120,
                    "address":" 广东省珠海市香洲区s111",
                    "locate_time": 1427277564,
                    "speed": 8,
                    "locate_error": 20,
                    "locate_type": 1
                }
            }
        },
        {
            "id": "1111",
            "pid": "111",
            "name": "设备1-1",
            "type": "terminal",
            "cid": "1",
            "group_id": "111",
            "info": {
                "tid": 1111,
                "sn": 47487879,
                "activate_code": "Asce234d",
                "type": "ZJ211",
                "firmware_version": "F",
                "login_time":1449387449,
                "mode": {
                    "terminal_mode": "1",
                    "param_interval": "30",
                    "gps_status": "0"
                },
                "device_mode": 0,
                "gsm": 4,
                "gps" : 40,
                "pbat": 60,
                "login" : 1,
                "status": 0,
                "battery_voltage": 12000,
                "charge_status": 0
            }
        }
    ]
}
```

* POST方法

功能描述:修改组和车辆的位置

请求参数:

| 参数      | 类型   | 描述     | 默认值 | 是否必填 |
|-----------|--------|----------|--------|----------|
| pid       | string | 要将车辆或组拖到哪个组下面   |   ""     | Yes      |
| id        | string | 操作的车辆id或组id |    ""    | Yes      |
| type      | int | 车辆为1,组为2 |    ""    | Yes      |


Example:
```json
{
    "pid": "1",
    "id": "2",
    "type": 1
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 错误信息                                  |
| data     | object     | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message":"密码修改成功",
    "data":{}
}
```

#### 车辆信息

URL: /carinfo

Table: 暂无

支持方法:GET, POST

支持客户端:Web, Android, IOS

* GET方法

功能描述:返回车辆和车辆下的终端信息

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| car_id   | string |  车辆id,手机客户端传空的（可以但不推荐不传）时候返回一辆集团下车辆   |   ""     | No(不推荐不传字段)     |

返回结果:

| 参数名称     | 参数类型 | 描述                                    |
|--------------|----------|-----------------------------------------|
| status       | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                        |
| data         | object     | 包含下列参数                       |
| id         | string     | 数据id                              |
| cid       | string     | 集团id                         |
| create_time  | int      | 创建时间                            |
| group_id     | string   | 组id                             |
| vin       | string   | 车辆唯一标识                                   |
| name       | string     | 名称                             |
| cnum         | string      | 车牌号                                |
| icon         | int      | 车辆图标                                |
| position      | object     | 位置信息,包含下列参数                    |
| latitude     | int      | 加密前纬度                              |
| longitude    | int      | 加密前经度                              |
| clatitude    | int      | 加密后纬度                              |
| clongitude   | int      | 加密后经度                              |
| altitude    | int      | 高度                                    |
| degree       | string   | 方向                                        |
| address      | string   | 位置描述                                |
| locate_time  | int      | 取点时间                                |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位  ）      |
| speed        | float    | 速度                                    |
| locate_error | int      | 定位误差                                |
| tid          | string   | 终端id                                  |
| sn           | string   | 终端sn                                  |
| activate_code | string   | 激活码                                  |
| type         | string      | ZJ210,ZJ211,ZJ300                       |
| mode         | object   | 工作模式                                |
| terminal_mode | string   | 0：ZJ211/ZJ300 待机模式，1：ZJ211/ZJ300 唤起模式，2：ZJ210或ZJ211/ZJ300 配对模式 3：ZJ210 单独模式 |
| param_interval | string   | 终端请求参数的间隔（例如：30  表示 30分钟）   |
| gps_status     | string   | 终端GPS状态（0：关闭  1：打开）         |
| activate_time   | int   | 终端激活时间                          |
| gsm   | int   | GSM信号强度                                   |
| gps   | int   | GPS信号的SNR值                                   |
| pbat   | int   | 剩余电量百分比                                  |
| login   | int   | 登录状态,1 = 登录,0 = 未登录, 2 = 待机         |
| login_time   | int   | 终端最近一次登录时间                           |
| status   | int   | 终端状态,0 = 未知状态 1 = 停留,2 = 行驶,3 = 熄火,4 = 怠速  |
| charge_status   | int   | 终端充电状态,0 = 未连接外部电源正在放电, 1 = 连接外部电源正在充电, 2 = 连接外部电源但不在充电|
| emergency_status   | int   | [deprecated] 0:未开启进入紧急模式,1:待进入紧急模式,2:已经进入紧急模式|
| emergency_time   | int   | 终端进入紧急模式的(即将)开始时间|
| emergentable   | int   | [deprecated] 0:不能进入紧急模式,1:能进入紧急模式|
| device_mode   | int   | 0:普通模式，1:待紧急模式，2:紧急模式|
| battery_voltage   | int   | 210终端的外接电源电压mv |
| firmware_version   | string   | 固件版本 F: 全功能ZJ210, E: 简易版ZJ210, S: 长待机版ZJ210(车管一期), T: 全功能版ZJ211, U: 简易版ZJ211, V:ZJ300 |
| light   | int   | 终端感光开关 0：关闭 1：开启 |
| light_status   | int   | ZJ300设备的感光状态<br/>-1 - 未知（默认值）<br/>0 - 感光功能关闭<br/>1 - 无光   <br/>2 - 有光 |
| wifi   | int   | 终端wifi热点开关 0：关闭 1：开启 |
| wifi_status   | int   | ZJ300的wifi热点状态<br/>-1 - 未知（默认值）<br/>0 - wifi功能关闭<br/>1 - wifi热点开启   <br/>2 - wifi热点关闭 |


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "id": "20",
        "vin": "1111",
        "name": "1111",
        "cnum": "川A88888",
        "icon": 1,
        "cid": "1",
        "group_id": "11",
        "create_time": 123435283,
        "emergency_status": 1,
        "emergentable": 1,
        "position": {
            "latitude": 80551404,
            "longitude": 408851028,
            "clatitude": 80560938,
            "clongitude": 408892892,
            "altitude": 36,
            "degree": 120,
            "address":"广东省珠海市香洲区s111",
            "locate_time": 1427277564,
            "speed": 8,
            "locate_error": 20,
            "locate_type": 1
        },
        "terminals":[{
            "tid": "1111",
            "sn": "47487879",
            "activate_code": "Asce234d",
            "type": "ZJ211",
            "mode": {
                "terminal_mode": "1",
                "param_interval": "30",
                "gps_status": "0"
            },
            "device_mode": 0,
            "activate_time": 212342323,
            "emergency_time": 1435687458,
            "gsm": 4,
            "gps" : 40,
            "pbat": 60,
            "login" : 1,
            "login" : 1449387449,
            "status": 0,
            "battery_voltage":12000,
            "charge_status": 0,
            "firmware_version": "F",
            "position": {
	            "latitude": 80551404,
	            "longitude": 408851028,
	            "clatitude": 80560938,
	            "clongitude": 408892892,
	            "altitude": 36,
	            "degree": 120,
	            "address":" 广东省珠海市香洲区s111",
	            "locate_time": 1427277564,
	            "speed": 8,
	            "locate_error": 20,
	            "locate_type": 1
	        }
        }
        ]
    }
}
```

* POST方法

功能描述:修改车辆信息

请求参数:

| 参数          | 类型     | 描述                          | 默认值 | 是否必填 |
|---------------|--------|-----------------------------|-----|------|
| car_id        | string | 车辆id(如果将车辆标识作为车辆id,则该参数不需要) | ""  | Yes  |
| vin           | string | 车辆标识                        | ""  | Yes  |
| cnum          | string | 车牌号                         | ""  | No   |
| icon          | int    | 图标                          | 1   | Yes  |
| 210           | string | 配对的210 tid                  | ""  | No   |
| 211           | array  | [配对的211 tid]                | ""  | No   |
| light_setting | object | 形如 { s24s5d4fsdfsf: true }  | ""  | No   |


Example:

```json
{
    "car_id": "11",
    "vin": "11",
    "cnum": "test",
    "icon": 1,
    "210": "21215442198fdsfewrf",
    "211": ["4rgd151h1514521225151"],
    "light_setting": {
        "4rgd151h1514521225151": true
    }
}
```
返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### 新建、修改、删除车队（组）

URL: /group

Table: 暂无

支持方法:GET,POST,PUT,DELETE

支持客户端:Web, Android, IOS

* GET方法

功能描述:查询车队信息

请求参数:

| 参数       | 类型   | 描述   | 默认值 | 是否必填 |
|------------|--------|--------|--------|----------|
| gid | string | 组id   | ""     | Yes      |

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                  |
| id     | string   | 组id                                 |
| pid     | string  | 父组id                                  |
| name     | string   | 组名                                  |
| create_time     | int   | 组创建时间                                 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {
        "id":"123",
        "pid":"1234",
        "name":"test",
        "create_time":123423412
    }
}
```

* POST方法

功能描述:新建车队

请求参数:

| 参数       | 类型   | 描述   | 默认值 | 是否必填 |
|------------|--------|--------|--------|----------|
| group_name | string | 组名   | ""       | Yes      |
| pgid       | string | 父组id | ""      | Yes      |

Example:

```json
{
    "pgid": "11",
    "group_name": "test"
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                      |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

* PUT方法

功能描述:修改组名
请求参数:

| 参数       | 类型   | 描述 | 默认值 | 是否必填 |
|------------|--------|------|--------|----------|
| gid        | string    | 组id |  ""      | Yes      |
| group_name | string | 组名 | ""     | Yes      |

Example:

```json
{
    "gid": "11",
    "group_name": "test"
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}

}
```

* DELETE方法

功能描述:删除组
请求参数:组id

| 参数 | 类型 | 描述 | 默认值 | 是否必填 |
|------|------|------|--------|----------|
| gid  | string  | 组id |  ""     | Yes      |


返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### 上传添加设备excel

URL: /addterminalexcel

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:上传要添加设备信息的excel

请求参数:

| 参数       | 类型 | 描述            | 默认值 | 是否必填 |
|------------|------|-----------------|--------|----------|
| gid        | string | 当前组id       | "     | Yes      |
| upload_file | string | 上传的excel文件名 | ""   | Yes      |
| *file* | File | 上传的excel文件 | ""   | Yes      |

备注： 这里使用的是`multipart/form-data`的 content-type

Example:
```json
{
    "gid": "111",
    "upload_file": ""
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                             |
|----------|----------|--------------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误）        |
| message  | string   | 处理结果描述消息                                 |
| data     | object     | 包含下列参数                                |
| res      | array     | 每条数据的检测结果（如果excel没有错误不返回下列数据） |
| row_no   | int      | 错误数据的行号                                   |
| status   | int      | 每条数据的状态                                   |
| message  | string   | 每条数据的错误信息                                             |
| activate_code   | string      | 激活码                                   |
| vin   | string      | 车辆标识                                 |
| cnum  | string   | 车牌号                                             |
| icon   | int      | 车辆图标                                   |
| group_name   | string      | 车队名称                                 |


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "res":[
            {
                "row_no": "156",
                "status": -1,
                "message": "激活码不存在",
                "activate_code": "sdewrw2",
                "vin": "1",
                "cnum": "川A88888",
                "icon": 1,
                "group_name": "test"
            }
        ]
    }
}
```

#### 设备批量添加

URL: /batchaddterminal

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:设备批量添加

请求参数:无

返回结果:

| 参数名称   | 参数类型 | 描述                                      |
|------------|----------|-------------------------------------------|
| status     | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message    | string   | 处理结果描述消息                          |
| data       | object     | 返回的结果                     |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### 添加单个设备

URL: /addterminal

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:添加单个设备
请求参数:

| 参数          | 类型   | 描述     | 默认值 | 是否必填 |
|---------------|--------|----------|--------|----------|
| group_id      | string | 组id    |  ""     | Yes      |
| activate_code | string | 激活码   |   ""   | Yes      |
| vin           | string | 车辆标识 | ""     | No       |
| cnum        | string | 车牌号   | ""     | No       |
| icon          | int    | 图标     | 1      | Yes      |
| safe_mode   | int    | 安全新增<br/>0-强制添加(不传此参数或者传0都是为0)<br/>1-安全添加(车辆在不同分组下会提示信息) | 0 | No |

Example:
```json
{
    "group_id": "",
    "activate_code":" TYB93CEAZJ",
    "vin": "1111",
    "cnum": "川A88888",
    "icon": 1,
    "safe_mode": 1
}
```

**safe_mode开启时,提示返回数据**

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的信息                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

**safe_mode开启时,提示返回数据**
```json
{
    "status": 1510,
    "message": "车辆存在于另一分组下",
    "data": {
        "group_id": "另一分组id",
        "group_name": "另一分组",
        "car_name": "目标车名"
    }
}
```

#### 实时定位

URL: /realtimeposition

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:显示当前车辆的最新位置信息
请求参数:

| 参数   | 类型 | 描述   | 默认值 | 是否必填 |
|--------|------|--------|--------|----------|
| car_id | string|array | 车辆id |   ""     | Yes      |

Example:
```json
{
    "car_id": "11"
}
```

```json
{
    "car_id": ["e1415c5c56f042a097c6311e0fcb01e7", "152ae75a0c6947aeb0ee304f98c585b6"]
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-------------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                          |
| data         | object     | 包含下列参数                              |
| car_id       | string   | 车辆id                                  |
| vin          | string   | 车辆标识                                  |
| latitude     | int      | 加密前纬度                                |
| longitude    | int      | 加密前经度                                |
| clatitude    | int      | 加密后纬度                                |
| clongitude   | int      | 加密后经度                                |
| altitude    | int      | 高度                                      |
| address      | string   | 位置描述                                  |
| locate_time  | int      | 取点时间                                  |
| speed        | float    | 速度                                      |
| locate_error | int      | 定位误差                                  |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位, 2: 未知-刚绑定未发送过报文的情况  ）      |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {
        "car_id": "11",
        "vin": "330A0000CB",
        "latitude": 144091162,
        "longitude": 144091162,
        "clatitude": 144117196,
        "clongitude": 418749577,
        "altitude": 0,
        "address": "北京上地",
        "locate_time": 1349858699,
        "speed": 20.0,
        "locate_error": 0,
        "locate_type": 1
    }
}
```

```json
{
    "status": 0,
    "message": "操作成功。",
    "data": [
        {
            "car_id": "e1415c5c56f042a097c6311e0fcb01e7",
            "vin": "330A0000CB",
            "latitude": 144091162,
            "longitude": 144091162,
            "clatitude": 144117196,
            "clongitude": 418749577,
            "altitude": 0,
            "address": "北京上地",
            "locate_time": 1349858699,
            "speed": 20.0,
            "locate_error": 0,
            "locate_type": 1
        },
        {
            "car_id": "152ae75a0c6947aeb0ee304f98c585b6",
            "vin": "330A0000CB",
            "latitude": 144091162,
            "longitude": 144091162,
            "clatitude": 144117196,
            "clongitude": 418749577,
            "altitude": 0,
            "address": "北京上地",
            "locate_time": 1349858699,
            "speed": 20.0,
            "locate_error": 0,
            "locate_type": 1
        }
    ]
}
```

#### 进入紧急模式时间

URL: /enteremergencymodetime

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

*  POST方法

功能描述:计算进入紧急模式时间

请求参数:

| 参数   | 类型   | 描述         | 默认值 | 是否必填 |
|--------|--------|--------------|--------|----------|
| car_id | string | 车辆id       | ""   | No      |
| tids | array | 车辆id       | ""   | No      |

Example:
```json
{
    "car_id":"152ae75a0c6947aeb0ee304f98c585b6",
    "tids": ["t123", "t234"]
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的信息                                |
| emergency_time   | int   | 进入紧急模式的时间|

Example:
传参为car_id
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "emergency_time": 123434,
    }
}
```

传参为tids
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "emergency_time": [12345, 23456],
    }
}
```

#### 修改设备模式（紧急模式,普通模式）

URL: /changemode

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

*  POST方法

功能描述:修改设备的模式

请求参数:

| 参数   | 类型   | 描述         | 默认值 | 是否必填 |
|--------|--------|--------------|--------|----------|
| car_id | string | 车辆id       | ""   | No      |
| tid    | string | 终端id       | ""   | No      |
| status | int | 0:退出紧急模式，1：进入紧急模式 | 0   | Yes      |

Example:
```json
{
    "car_id": "c123",
    "tid": "t123",
    "status": 1
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的信息                                |


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 轨迹查询

URL: /track

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:查询车辆的轨迹信息。多个终端的情况下,会将各终端融合在一起,返回融合后的位置点列表。
请求参数:

| 参数       | 类型   | 描述     | 默认值 | 是否必填 |
|------------|--------|----------|--------|----------|
| car_id     | string | 车辆id   | ""   | Yes      |
| start_time | int    | 开始时间 | 0   | Yes      |
| end_time   | int    | 结束时间 | 0     | Yes      |

Example:
```json
{
    "car_id": "c123",
    "start_time": 111112123,
    "end_time": 112122122
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-----------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误）    |
| message      | string   | 处理结果描述消息                          |
| data         | object     | 包含下列参数                              |
| track        | array     | 轨迹点 （包含所有停留点）                 |
| lid          | int      | (没用)轨迹点的id                               |
| tid          | string   | 终端唯一标识                              |
| dev_type     | string   | 终端设备类型                              |
| point_type   | int      | 停留点类型 (1: 移动点 2: 停留点 |
| latitude     | int      | 加密前纬度                                |
| longitude    | int      | 加密前经度                                |
| clatitude    | int      | 加密后纬度                                |
| clongitude   | int      | 加密后经度                                |
| degree       | int      | 方向                                     |
| address      | string   | 位置描述                                  |
| timestamp    | int      | 取点时间                                  |
| speed        | float    | 速度                                     |
| locate_error | int      | 定位误差                                  |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位  ）      |
| mileage      | strint   | 里程                                     |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {
        "track":[
            {
                "clatitude": 80481884,
                "clongitude": 408962940,
                "degree": 210,
                "lid": 40745,
                "tid": "终端id",
                "tid": "TYB93CEAZJ",
                "dev_type": "ZJ210",
                "point_type": 1,
                "latitude": 80472096,
                "locate_error": 14,
                "locate_type": 1,
                "longitude": 408921156,
                "mileage": 28760,
                "address": "广东省珠海市香洲区S111(港湾大道),帝景湾山庄附近",
                "speed": 28,
                "timestamp": 1436782999
            },
            {
                "clatitude": 80481884,
                "clongitude": 408962940,
                "degree": 210,
                "lid": 40745,
                "tid": "终端id",
                "tid": "TYB93CEAZJ",
                "dev_type": "ZJ210",
                "point_type": "2",
                "latitude": 80472096,
                "locate_error": 14,
                "locate_type": 1,
                "longitude": 408921156,
                "mileage": 28760,
                "address": "广东省珠海市香洲区S111(港湾大道),帝景湾山庄附近",
                "speed": 28,
                "timestamp": 1436782999
            }
        ]
    }
}
```

#### 管理员信息

URL: /userinfo

Table: 暂无

支持方法: GET,POST

支持客户端:Web, Android, IOS

* GET方法

功能描述:查询用户信息

请求参数:无

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     |  object    | 包含下列参数                              |
| alias    | string   | 别名                                      |
| username | string   | 用户名                                    |
| user_type| int      | 用户类型 1-管理员 2-子账号 3-监控员（无效）  |
| privilege| string   | [子账号权限类型定义](#子账号权限类型) |
| name_show | int | 集团下车辆名优先显示模式<br/>1-车架号<br/>2-车牌号 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "alias": "笨小孩",
        "username": "15882081234",
        "privilege": "1,2,3",
        "user_type": 1
    }
}
```
* POST方法

功能描述:修改管理员信息

请求参数:

| 参数  | 类型   | 描述     | 默认值 | 是否必填 |
|-------|--------|----------|--------|----------|
| alias | string | 用户别名 | ""     | Yes      |

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 退出登录

URL: /logout

支持方法:GET

支持客户端:Web, Android, IOS

* GET方法

功能描述:完成Web登录用户的注销,推出登录状态。清除本次HTTP请求的cookie

请求参数:无

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的信息                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 注册wspush

URL: /wspush

支持方法:POST

支持客户端:Web, Android, IOS

* POST 方法

功能描述:为登录的用户注册push

请求参数:

| 参数  | 类型   | 描述     | 默认值 | 是否必填 |
|-------|--------|----------|--------|----------|
| devid       | string | 设备编号。（Android,IOS 才有） |      ""  | Yes      |
| from        | int    | 客户端类型:0:Web, 1:Android, 2:IOS | 0      | Yes      |

Example:
```json
{
    "devid": "111",
    "from": 0
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object     | 返回的数据                                |
| wspush   | object     | push数据,包含id和key                                |
| id       | string   | push的id                                |
| key      | string   | push的key                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "wspush":{
            "id": "polly",
            "key": "sfswrefrdofjoldjfo"
        }
    }
}
```

#### 重置密码

URL: /resetpassword

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:重置密码（未登录）

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| username | string | 手机号         |   ""     | Yes      |
| password | string | 用户输入新密码 |    ""    | Yes      |

Example:
```json
{
    "username": "1582082014",
    "password": "123456"
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 错误信息                                  |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 1,
    "message": "服务异常",
    "data":{}
}
```

#### 分级查询组和车辆列表信息

URL: /grouplist

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:分级获取集团,车队,车辆,终端信息

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| gid | string | 组id(gid"",请求集团下的第一层车队信息)          |   ""     | Yes     |

返回结果:

| 参数名称     | 参数类型 | 描述                                    |
|--------------|----------|-----------------------------------------|
| status       | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                        |
| data         | object     | 包含下列参数                       |
| id         | string     | 数据id                              |
| pid         | string   | 父id                              |
| cid       | string     | 集团id                         |
| cname       | string     | 集团名称                             |
| name       | string     | 名称                             |
| create_time  | int      | 创建时间                            |
| group_id     | string   | 组id              |
| group_quantity   | int  | 车队数量            |
| car_quantity   | int  | 车辆数量            |
| vin       | string   | 车辆唯一标识                                   |
| cnum         | string      | 车牌号                                |
| icon         | int      | 车辆图标                                |
| position      | object     | 位置信息,包含下列参数                    |
| latitude     | int      | 加密前纬度                              |
| longitude    | int      | 加密前经度                              |
| clatitude    | int      | 加密后纬度                              |
| clongitude   | int      | 加密后经度                              |
| altitude    | int      | 高度                                    |
| degree       | string   | 方向                                        |
| address      | string   | 位置描述                                |
| locate_time  | int      | 取点时间                                |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位  ）      |
| speed        | float    | 速度                                    |
| locate_error | int      | 定位误差                                |
| tid          | string   | 终端id                                  |
| sn           | string   | 终端sn                                  |
| activate_code | string   | 激活码                                  |
| type         | string      | Zj210,ZJ211,ZJ300                       |
| mode         | object   | 工作模式                                |
| terminal_mode | string   | 0：ZJ211/ZJ300 待机模式，1：ZJ211/ZJ300 唤起模式，2：ZJ210或ZJ211/ZJ300 配对模式 3：ZJ210 单独模式 |
| param_interval | string   | 终端请求参数的间隔（例如：30  表示 30分钟）                               |
| device_mode   | int   | 0:普通模式，1:待紧急模式，2:紧急模式|
| gps_status     | string   | 终端GPS状态（0：关闭  1：打开）                             |
| activate_time   | int   | 终端激活时间                         |
| gsm   | int   | GSM信号强度                         |
| gps   | int   | GPS信号的SNR值                        |
| pbat   | int   | 剩余电量百分比                         |
| login   | int   | 登录状态,1 = 登录,0 = 未登录, 2 = 待机              |
| login_time   | int   | 上次登录时间                        |
| status   | int   | 终端状态,0 = 未知状态 1 = 停留,2 = 行驶,3 = 熄火,4 = 怠速  |
| charge_status   | int   |终端充电状态,0 = 未连接外部电源正在放电, 1 = 连接外部电源正在充电, 2 = 连接外部电源但不在充电|
| emergency_status   | int   | 0:未开启进入紧急模式,1:待进入紧急模式,2:已经进入紧急模式|
|firmware_version|string|固件大版本号 F: 全功能ZJ210, E: 简易版ZJ210, S: 长待机版ZJ210(车管一期), T: 全功能版ZJ211, U: 简易版ZJ211, V:ZJ300|
| emergentable   | int   | 0:不能进入紧急模式,1:能进入紧急模式|
| light   | int   | 终端感光开关 0：关闭 1：开启 |
| light_status   | int   | ZJ300设备的感光状态<br/>-1 - 未知（默认值）<br/>0 - 感光功能关闭<br/>1 - 无光   <br/>2 - 有光 |
| wifi   | int   | 终端wifi热点开关 0：关闭 1：开启 |
| wifi_status   | int   | ZJ300的wifi热点状态<br/>-1 - 未知（默认值）<br/>0 - wifi功能关闭<br/>1 - wifi热点开启   <br/>2 - wifi热点关闭 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "corp":{
            "pid": "0",
            "cid": "1",
            "cname":"集团名称",
            "id": "1",
            "name":"顶级组名称",
            "create_time":123435233,
            "group_quantity":20,
            "car_quantity":100
        },
        "groups":[
            {
                "pid": "1",
                "cid":"1",
                "id": "11",
                "name": "车队1",
                "create_time":123435233,
                "group_quantity":10,
                "car_quantity":40
            }
        ],
        "cars":[
            {
                "pid": "15",
                "cid": "1",
                "id": "20",
                "vin": "1111",
                "cnum": "川A88888",
                "icon": 1,
                "group_id": "11",
                "create_time":123435283,
                "emergency_status": 1,
                "emergentable": 1,
                "position":{
                    "latitude": 80551404,
                    "longitude": 408851028,
                    "clatitude": 80560938,
                    "clongitude": 408892892,
                    "altitude": 36,
                    "degree": 120,
                    "address": "广东省珠海市香洲区s111",
                    "locate_time": 1427277564,
                    "speed": 8,
                    "locate_error": 20,
                    "locate_type": 1
                },
                "terminals":[
                    {
                        "tid": "1111",
                        "sn": 47487879,
                        "activate_code": "Asce234d",
                        "type": "ZJ211",
                        "mode": {
                            "terminal_mode":"1",
                            "param_interval":"30",
                            "gps_status":"0"
                        },
                        "device_mode": 0
                        "activate_time": 212342323,
                        "gsm": 4,
                        "gps" : 40,
                        "pbat": 60,
                        "login" : 1,
                        "login_time":123435233,
                        "status": 0,
                        "charge_status": 0,
                        "firmware_version": "F"
                    }
                ]
            }
        ]
    }
}
```

#### 搜索车辆或者组

URL: /search

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:搜索车辆信息或者组信息

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| keywords    | string |  搜索的关键字   |   ""     | Yes     |
| type    | int |  1=只搜索车辆,2=搜索车辆和组   |   ""     | Yes     |

Example:
```json
{
    "keywords": "车辆",
    "type": 1
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                    |
|--------------|----------|-----------------------------------------|
| status       | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                        |
| data         | object     | 包含下列参数                       |
| keywords     | string     | 搜索的关键字                 |
| id         | string     | 数据id                              |
| cid       | string     | 集团id                         |
| create_time  | int      | 创建时间                            |
| group_id     | string   | 组id              |
| vin       | string   | 车辆唯一标识                                   |
| cnum         | string      | 车牌号                                |
| icon         | int      | 车辆图标                                |
| position      | object     | 位置信息,包含下列参数                    |
| latitude     | int      | 加密前纬度                              |
| longitude    | int      | 加密前经度                              |
| clatitude    | int      | 加密后纬度                              |
| clongitude   | int      | 加密后经度                              |
| altitude    | int      | 高度                                    |
| degree       | string   | 方向                                        |
| address      | string   | 位置描述                                |
| locate_time  | int      | 取点时间                                |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位  ）      |
| speed        | float    | 速度                                    |
| locate_error | int      | 定位误差                                |
| tid          | string   | 终端id                                  |
| sn           | string   | 终端sn                                  |
| activate_code | string   | 激活码                                  |
| type         | string      | ZJ210,ZJ211,ZJ300                       |
| mode         | object   | 工作模式                                |
| terminal_mode | string   | 0：ZJ211/ZJ300 待机模式，1：ZJ211/ZJ300 唤起模式，2：ZJ210或ZJ211/ZJ300 配对模式 3：ZJ210 单独模式 |
| param_interval | string   | 终端请求参数的间隔（例如：30  表示 30分钟）                               |
| device_mode   | int   | 0:普通模式，1:待紧急模式，2:紧急模式|
| gps_status     | string   | 终端GPS状态（0：关闭  1：打开）                             |
| activate_time   | int   | 终端激活时间                         |
| gsm   | int   | GSM信号强度                         |
| gps   | int   | GPS信号的SNR值                        |
| pbat   | int   | 剩余电量百分比                         |
| login   | int   | 登录状态,1 = 登录,0 = 未登录, 2 = 待机             |
| status   | int   | 终端状态,0 = 未知状态 1 = 停留,2 = 行驶,3 = 熄火,4 = 怠速  |
| charge_status   | int   | 终端充电状态,0 = 未连接外部电源正在放电, 1 = 连接外部电源正在充电, 2 = 连接外部电源但不在充电|
| firmware_version   | string   |固件版本 F: 全功能ZJ210, E: 简易版ZJ210, S: 长待机版ZJ210(车管一期), T: 全功能版ZJ211, U: 简易版ZJ211, V: ZJ300 |
| track_time   | int   | -1:不能进入紧急模式,0:已经进入紧急模式,其他:还有多长时间进入紧急模式|
| groups   | array   | 组信息|
| pid     | string   | 父组id|
| cid   | string   | 集团id|
| id   | string   | 组id|
| name   | string   |组名|
| group_quantity | int   | 子组的数量|
| car_quantity   | int   | 车辆数量|
| emergency_status   | int   | 0:未开启进入紧急模式,1:待进入紧急模式,2:已经进入紧急模式|
| emergentable   | int   | 0:不能进入紧急模式,1:能进入紧急模式|
| light   | int   | 终端感光开关 0：关闭 1：开启 |
| light_status   | int   | ZJ300设备的感光状态<br/>-1 - 未知（默认值）<br/>0 - 感光功能关闭<br/>1 - 无光   <br/>2 - 有光 |
| wifi   | int   | 终端wifi热点开关 0：关闭 1：开启 |
| wifi_status   | int   | ZJ300的wifi热点状态<br/>-1 - 未知（默认值）<br/>0 - wifi功能关闭<br/>1 - wifi热点开启   <br/>2 - wifi热点关闭 |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "keywords": "车辆",
        "cars":[
            {
                "id":"20",
                "vin": "1111",
                "cnum": "川A88888",
                "icon": 1,
                "cid": "1",
                "group_id":"11",
                "create_time":123435283,
                "emergency_status":1,
                "emergentable":1,
                "position":{
                    "latitude": 80551404,
                    "longitude": 408851028,
                    "clatitude": 80560938,
                    "clongitude": 408892892,
                    "altitude": 36,
                    "degree":120,
                    "address":" 广东省珠海市香洲区s111",
                    "locate_time": 1427277564,
                    "speed":8,
                    "locate_error":20,
                    "locate_type":1
                },
                "terminals":[
                    {
                        "tid": "1111",
                        "sn": "47487879",
                        "activate_code": "Asce234d",
                        "type":"zj211",
                        "mode": {
                            "terminal_mode": "1",
                            "param_interval": "30",
                            "gps_status": "0"
                        },
                        "device_mode": 0,
                        "activate_time": 212342323,
                        "gsm": 4,
                        "gps" : 40,
                        "pbat": 60,
                        "login" : 1,
                        "status": 0,
                        "charge_status": 0,
                        "firmware_version": "F"
                    }
                ]
            }
        ],
        "groups":[
            {
                "pid":"123d",
                "cid":"213dd",
                "id":"111",
                "name":"车队1",
                "create_time":1232342,
                "group_quantity":10,
                "car_quantity":40
            }
        ]
    }
}
```

~~#### 车辆进入远程追踪~~

URL: /remotetrack

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述:车辆进入或退出远程追踪

请求参数: 以json格式提交

| 参数     | 类型   | 描述           | 默认值 | 是否必填 |
|----------|--------|----------------|--------|----------|
| tid      | string |  要追踪的终端id|   ""    | Yes     |
|gps_status| string | gps开关 1.开 0.关   |   -    | Yes     |


Example:
```json
{
    "tid": "b8ed0924fdba4017a5a9b343c77c05eb",
    "gps_status": "1"
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 错误信息                                  |
| data     | object   | 返回的数据                                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 警告设置信息获取/设置

URL: /warningset

支持方法:GET,POST

支持客户端:Web, Android, IOS

* GET 方法

功能描述:查询当前用户的告警推送服务设置情况

请求参数:
    无

返回结果:'on'返回值true表示开启，false表示关闭; 'limit'表示阈值
Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "voice": {"on":false},
    	"offline": {"on":true},
    	"over_speed": {"on":true, "limit":120},
	"long_stop":{"on":false, "limit":[12,72]}
    }
}
```

* POST 方法

功能描述:用户设置那些警告需要推送到前端

请求参数:

| 参数  | 类型   | 描述     | 默认值 | 是否必填 |
|-------|--------|----------|--------|----------|
| voice  | boolean   | 提示音 |   无 | No      |
| offline| boolean   | 异常离线 | 无 | No      |
|low_power| boolean  | 低电警告 | 无 | No      |
|pull_out | boolean  | 设备拔出 |无  | No      |
|emergency|boolean   | 紧急模式 | 无 | No      |
|wait4emergency|boolean |待进入紧急模式|无|No  |
|full_power| boolean |满电|无|No |
|self_test_error|boolean|自检异常|无|No |
|low_voltage|boolean |电瓶低电|无|No |
|long_stop|boolean |长时间停留|无|No |
|over_speed|boolean |超速|无|No  |
|light_sensed|boolean | 感光设备拔除 | 无|No |

Example:
```json
{
   "voice": {"on":false},
   "offline": {"on":true},
   "over_speed": {"on":true, "limit":120},
   "long_stop":{"on":false, "limit":[12,72]}
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
    }
}
```

#### 警告历史的查询功能

URL: /warningsearch

支持方法:POST

支持客户端:Web, Android, IOS

* POST 方法

功能描述:用户查询一段时间内曾推送的警告

请求参数:

| 参数  | 类型   | 描述     | 默认值 | 是否必填 |
|-------|--------|----------|--------|----------|
| search\_type | string | 搜索警告类型<br/>all: '全部',<br/>off_line: '离线',<br/>low_power: '低电状态',<br/>pull_out: '设备拔出',<br/>in_emergency_mode: '紧急模式',<br/>wait_4_emergency: '待紧急模式',<br/>low_voltage: '电瓶低电',<br/>long_stop: '长时间停留',<br/>over_speed: '超速',<br/>full_power: 满电,<br/>self_test_error: 自检异常 <br/> light_sensed:光感设备拔除|  无 | No  |
| car_id      | array  | 车辆ID         |  无 | Yes |
| begintime   | int    | 开始时间       |  无 | Yes |
| endtime     | int    | 结束时间       |  无 | Yes |

Example:
```json
{
    "search_type": "1",
    "car_id": ["48417fes5f45e6gh"],
    "begintime": 1445785648,
    "endtime": 1445934585
}
```

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 包含下列参数                       |
| list      | int      |  事件列表   |
| car_id      | string     |  车辆id   |
| name | string | 车辆名称（车架号或车牌号) |
| dev_type  | string   |  sn和设备类型          |
| eid       | string   | 事件id                 |
| w_type    | int    | 警告类型<br/> 1.离线;2.低电;3.设备拔出;4.紧急模式;5.待紧急模式;6.满电;7.自检异常;8.电瓶低电;9.长时间停留;10.超速;11.光感设备拔除|
| w_content | int      |  提醒内容      |
| timestamp | int      |  提醒发生的时间  |
| latitude  | int    | 纬度                 |
| longitude | int    | 经度                 |
| clatitude  | int    | 加密后纬度                 |
| clongitude | int    | 加密后经度                 |
| total     | int      |  数据总条数  |
| remark    | object | 包含下列参数   |
| stop_begin | int | 长时间停留开始时间|

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":[
            {
                "name": "川ACGD56",
                "dev_type":"ZJ210",
                "w_type":3,
                "eid": 1231546546,
                "car_id": "xxxxxxxxxxxxxxxxx",
                "w_content":"设备拔出",
                "timestamp":1442202728,
                "latitude": 14587778778,
                "longitude": 14342342425,
                "clatitude": 14587778778,
                "clongitude": 14342342425,
		"remark":{"stop_begin": 1223423242}
            },
            {
                "name": "川ACGD56",
                "dev_type":"S1N5D756ED(ZJ210W)",
                "w_type":2,
                "eid: 1231546545,
                "car_id": "xxxxxxxxxxxxxxxxx",
                "w_content":"电量耗尽",
                "timestamp":1442203728,
                 "latitude": 14587778778,
                "longitude": 14342342425,
                "clatitude": 14587778778,
                "clongitude": 14342342425
            }
    ]
}
```

#### 用户反馈

URL: /feedback

支持方法:POST

支持客户端:Web, Android, IOS

* POST 方法

功能描述:用户提交反馈信息

请求参数:

| 参数        | 类型   | 描述                         | 默认值 | 是否必填 |
|-------------|--------|------------------------------|--------|----------|
| contact     | string | 联系人                       |  无    | Yes      |
| contact_info| string | 联系方式                     |  无    | Yes      |
| type        | int    | 联系方式类型 1-手机号 2-邮箱 |  1     | Yes      |
| num         | int    | 车队规模(辆)                 |  无    | Yes      |

Example:
```json
{
    "contact": "刘先生",
    "contact_info": "15982463820",
    "type": 1,
    "num": 100
}
```

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 返回的数据                              |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 未读告警的数据条数

URL: /warningnum

支持方法:GET

支持客户端:Web, Android, IOS

* GET 方法

功能描述:用户未读告警消息的条数

请求参数:无

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 返回的数据                              |
| unread| int     | 设备异常未读告警条数                     |
| undeleted | int     | 未被标记为删除的告警条数                |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
        "unread":30,
        "undeleted":30
    }
}
```

#### 告警信息列表

URL: /warninglist

支持方法:GET，PUT，DELETE

支持客户端:Web, Android, IOS

* GET 方法

功能描述:用户未删除的告警消息，最多返回50条数据

请求参数:

| 参数        | 类型   | 描述                         | 默认值 | 是否必填 |
|-------------|--------|------------------------------|--------|----------|
| timestamp   | int    | 时间（不传的话默认获取最新50条数据） |  无    | NO      |

Example:
```json
{
    "timestamp": 1442202728
}
```

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 返回的数据                              |
| warnings  | array     | 返回的告警数据集合                              |
| eid       | string   |告警数据的id                              |
| car_id     | string |车辆id              |
| name | string | 车辆名称（车架号或车牌号) |
| dev_type  | string | sn和终端类型    |
| w_type    | int    | 警告类型<br/> 1.离线;2.低电;3.设备拔出;4.紧急模式;5.待紧急模式;6.满电;7.自检异常;8.电瓶低电;9.长时间停留;10.超速;11.光感设备拔除|
| w_content | string | 警告内容             |
| timestamp | int    | 时间戳		    |
| latitude  | int    | 纬度                 |
| longitude | int    | 经度                 |
| clatitude  | int    | 加密后纬度                 |
| clongitude | int    | 加密后经度                 |
| remark    | object | 包含下列参数   |
| stop_begin | int | 长时间停留开始时间|


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
		"warnings":[
			{
			"eid": "18ddb67cbeaf444b9e23a1a155d4c96a",
			"car_id": "18ddb67cbeaf444b9e23a1a155d4c967"
            "dev_type":"S1N5D756ED(ZJ210W)",
            "w_type":3,
            "w_content":"设备拔出",
            "timestamp":1442202728,
            "latitude": 14587778778,
            "longitude": 14342342425,
            "clatitude": 14587778778,
            "clongitude": 14342342425
	    "remark":{"stop_begin":112312312}
			}
		]
	}
}
```

* PUT 方法

功能描述: 将告警信息标记为已读，如果没有传eid则将所有告警设置为已读

请求参数:

| 参数        | 类型   | 描述                         | 默认值 | 是否必填 |
|------------|--------|------------------------------|--------|----------|
| eid        | string | 告警id（如果没有传eid，将所有告警设置为已读） |  ""    | Yes      |

Example:
```json
{
    "eid": "18ddb67cbeaf444b9e23a1a155d4c96a"
}
```

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 返回的数据                              |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

* DELETE 方法

功能描述: 将告警信息标记为删除状态，如果没有传eid则将所有告警设置为删除状态

请求参数:

| 参数       | 类型   | 描述                         | 默认值 | 是否必填 |
|------------|--------|------------------------------|--------|----------|
| eid        | string | 告警id                       |  ""    | Yes      |

返回结果:

| 参数名称  |  参数类型  |   描述   |
|-----------|------------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误） |
| message   | string   | 处理结果描述消息                        |
| data      | object     | 返回的数据                              |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{}
}
```

#### 查询获取用户集团车架号

URL: /uservins

支持方法:POST

支持客户端:Android, IOS

* POST 方法

功能描述:增量获取用户集团下车架号数据信息

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填 |
|-------------|--------|----------------------------|--------|----------|
| date        | int    | 客户端保存的最新车架号时间 | 0      | YES       |

**注:如果客户端没有时间则可以传date为0,此时获取所有车架号信息,如果有指定时间戳则增量获取指定时间戳之后的车架号信息**

Example:
```json
{
    "date": 1450074132
}
```

返回结果:

| 参数名称  | 参数类型 |   描述   |
|-----------|----------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误）   |
| message   | string   | 处理结果描述消息                          |
| data      | object     | 返回的数据                                |
| vins      | array    | 车架号列表                                |

**注:如果管理员集团下没有对应的车架号信息,返回的counts和newest_time都为0**

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
    	"newest_time": 1450074132,
    	"counts": 2346,
    	"vins": [
    	    "FFFFF01234",
    	    "FFFFF01235"
    	]
    }
}
```

#### 子账号管理

URL: /subusers

支持方法: GET, POST, DELETE

支持客户端: Web, Android, IOS

* GET 方法

功能描述: 查询集团下子账号列表

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填 |
|-------------|--------|----------------------------|--------|----------|

Example:

返回结果:

| 参数名称  | 参数类型 |   描述   |
|-----------|----------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误）   |
| message   | string   | 处理结果描述消息                          |
| data      | array    | 返回的数据                                |
| oid       | string   | 用户唯一id                                |
| mobile    | string   | 手机号(账号)                              |
| name      | string   | 子账号用户                                |
| privilege| string   | [子账号权限类型定义](#子账号权限类型) |
| groups    | array    | 组列表数据                                |
| gid       | string   | 子账号被分配的顶级组id                    |
| cars      | array    | 车辆列表数据                              |
| carid     | string   | 子账号被分配的车辆id                      |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": [
        {
            "oid": "26a322871a4943ffafead42f7d7cdcd9",
            "mobile": "18013014718",
            "name": "一嗨租车",
            "privilege": "1,2,3,4",
            "groups": ["455ac4604a174991a4324f02aca5ae19", "455ac4604a174991a4324f02aca5ae20"],
            "cars": ["4551c10d1ec749e190347cd52b0093cd", "9b67f9ef08a34a6992b0684e37781ab5"]
        }
    ]
}
```

* POST 方法

功能描述: 新增或修改子账号信息

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填  |
|-------------|--------|----------------------------|--------|-----------|
| oid       | string   | 用户唯一id                 |        | NO        |
| mobile    | string   | 手机号(账号)               |        | NO        |
| name      | string   | 子账号用户                 |        | NO        |
| user_type| int      | 用户类型 1-管理员 2-子账号 3-监控员  |        | NO   |
| privilege| string   | [子账号权限类型定义](#子账号权限类型) |        | NO   |
| groups    | array    | 组列表数据                 |        | NO        |
| gid       | string   | 子账号被分配的顶级组id     |
| cars      | array    | 车辆列表数据               |
| carid     | string   | 子账号被分配的车辆id       |

Example:
```json
{
    "oid": "26a322871a4943ffafead42f7d7cdcd9",
    "mobile": "18013014718",
    "name": "一嗨租车",
    "privilege": "1,2,3,4",
    "groups": ["455ac4604a174991a4324f02aca5ae19", "455ac4604a174991a4324f02aca5ae19"],
    "cars": ["4551c10d1ec749e190347cd52b0093cd", "9b67f9ef08a34a6992b0684e37781ab5"]
}
```

返回结果:

| 参数名称  | 参数类型 |   描述   |
|-----------|----------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误）   |
| message   | string   | 处理结果描述消息                          |
| data      | object     | 返回的数据                                |


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

* DELETE 方法

功能描述: 删除子账号信息

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填  |
|-------------|--------|----------------------------|--------|-----------|
| oid       | string   | 用户唯一id                 |        | YES       |

Example:
```json
{
    "oid": "26a322871a4943ffafead42f7d7cdcd9"
}
```

返回结果:

| 参数名称  | 参数类型 |   描述   |
|-----------|----------|----------|
| status    | string   | 处理结果状态值0表示成功, 其他表示错误）   |
| message   | string   | 处理结果描述消息                          |
| data      | object     | 返回的数据                                |


Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### 导出管理员账号下车辆信息excel
(to be split into two interface!!!)

URL: /exportallcars

支持方法: GET

支持客户端: Web, Android, IOS

* GET 方法

功能描述: 异步导出管理员账号下车辆信息excel

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填 |
|-------------|--------|----------------------------|--------|----------|
|  start_time  |   int  |           开始时间         |        |    YES   |
|  end_time    |   int  |           结束时间         |        |    YES   |
|  type    |   string  |       可能值：  abnormal，normal，all        |   "abnormal"   |    YES  |
|  export\_fields   |  array |  导出字段:<br/> sn-设备sn, vin-车架号, cnum-车牌号, <br/>activate_time-激活时间, group_name-组名, terminal_status-终端状态, <br/>current_location-位置信息, locate_time-定位时间, bind_time-绑定时间, <br/>install_time-安装时间  |        |    YES   |

Example:
```json
{
  "start_time": 1453875495,
  "end_time": 1454386005,
  "export_fields": [
    "sn",
    "vin",
    "cnum",
    "activate_time",
    "group_name",
    "terminal_status",
    "current_location",
    "locate_time"
  ]
}
```

返回结果:
1.返回url地址用于下载文件
2.返回无url则表示后台还未准备好文件,需要等一会儿再次询问。
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {
        "url": "http://oss.aliyun.com/232323?accesskey=ue32t23232sddw",
	"filename": "我的集团2016.xls"
    }
}
```

或者无url（文件还未准备好）
```json
{
    "status": 0,
    "message": "操作成功",
    "data": {}
}
```

#### app下载跳转地址
URL: /download/{target}(/{device})?

支持方法: GET

支持客户端: Web, Android, IOS

* GET 方法

功能描述: app下载跳转地址,地址为restful风格,target为admin平台定义的target标识

请求参数:

| 参数        | 类型   | 描述                       | 默认值 | 是否必填 |
|-------------|--------|----------------------------|--------|----------|
| target      | string | 为admin平台定义的target标识| ""     | 是       |
| device      | string | 强制设备类型,ios,android   | ""     | 否       |

Example:

返回结果: 后台 Http 重定向到发布平台

#### 车辆下所有终端最新位置

URL: /carterminallastpos

Table: 暂无

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述: 显示当前车辆下所有终端的最新位置信息
请求参数:

| 参数   | 类型 | 描述   | 默认值 | 是否必填 |
|--------|------|--------|--------|----------|
| carids | array| 车辆id列表 |   []   | Yes      |

Example:
```json
{
    "carids": ["e1415c5c56f042a097c6311e0fcb01e7", "152ae75a0c6947aeb0ee304f98c585b6"]
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-------------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                          |
| data         | object     | 包含下列参数                              |
| tid          | string   | 终端tid                                   |
| latitude     | int      | 加密前纬度                                |
| longitude    | int      | 加密前经度                                |
| clatitude    | int      | 加密后纬度                                |
| clongitude   | int      | 加密后经度                                |
| altitude     | int      | 高度                                      |
| address      | string   | 位置描述                                  |
| locate_time  | int      | 取点时间                                  |
| speed        | float    | 速度                                      |
| locate_error | int      | 定位误差                                  |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位, 2: 未知-刚绑定未发送过报文的情况）|

Example:
```json
{
    "status": 0,
    "message": "操作成功。",
    "data": [
        {
            "tid": "e1415c5c56f042a097c6311e0fcb01e7",
            "latitude": 144091162,
            "longitude": 144091162,
            "clatitude": 144117196,
            "clongitude": 418749577,
            "altitude": 0,
            "address": "北京上地",
            "locate_time": 1349858699,
            "speed": 20.0,
            "locate_error": 0,
            "locate_type": 1
        },
        {
            "tid": "152ae75a0c6947aeb0ee304f98c585b6",
            "latitude": 144091162,
            "longitude": 144091162,
            "clatitude": 144117196,
            "clongitude": 418749577,
            "altitude": 0,
            "address": "北京上地",
            "locate_time": 1349858699,
            "speed": 20.0,
            "locate_error": 0,
            "locate_type": 1
        }
    ]
}
```

#### 终端配对历史

URL: /terminalpairlog

Table: t_terminal_pairlog

支持方法:POST

支持客户端:Web, Android, IOS

* POST方法

功能描述: 获取终端配对历史信息,指定时间戳之前的10条最新记录,按照时间倒序排列
请求参数:

| 参数   | 类型 | 描述   | 默认值 | 是否必填 |
|--------|------|--------|--------|----------|
| tid    |string| 终端id |   ""   | Yes      |
| timestamp | int  | 时间戳(不传则默认使用请求服务器的时间) |  0   | No   |
| type | string  | 终端类型 `210 or 211` |  0   | Yes   |

Example:
```json
{
    "tid": "152ae75a0c6947aeb0ee304f98c585b6",
    "timestamp": 1349858699,
    "type": "210"
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-------------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                          |
| data         | array    | 包含下列参数                              |
| tid          | string   | 配对终端tid                               |
| sn           | string   | 配对终端sn                                |
| type         | int      | 配对历史事件类型<br/>1-配对成功<br/>2-配对失联 |
| pair_time    | int      | 配对历史事件发生时间                      |

Example:
```json
{
    "status": 0,
    "message": "操作成功。",
    "data": [
        {
            "tid": "2805c1b53ad24fd7975c07aada95b8bf",
            "sn": "3D4C3000A5",
            "type": 1,
            "pair_time": 1349851699
        },
    ]
}
```

#### 根据sn同步获取终端最新状态

URL: /open/syncsn

Table: 暂无

支持方法:POST

支持客户端:Web , Android, IOS

* POST方法

功能描述:用户通过填写主账号手机号，和sn数组获取各个sn的当前情况，一次支持最大500个。


请求参数:

| 参数        | 类型   | 描述                                 | 默认值 | 是否必填 |
|-------------|--------|--------------------------------------|--------|----------|
| mobile      | string | 手机号                               |  ""    | Yes      |
|     sns     | array  |                sn数组                |  []    | Yes      |

Example:
```json
{
    "mobile": "15882081234",
    "sns": ["2222222220"]
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object     | 返回的数据                                |
|    sn    | string   | 设备号      |
| offline_time | int      | 最后一次离线时间  |
| login_time | int      | 最近一次登录时间  |
|   login  | int      | 登录情况： 0=离线  1=在线  |
|   type   | int      | 设备类型 0=接线设备 1=无线设备  |

Example:
```json
{
    "status": 0,
    "message": "操作成功",
    "data":[
      {
        "sn": "2222222220",
        "offline_time": 1472045412,
        "login": 0,
        "type": 0,
        "login_time": 1473823410
      },
      {
        "sn": "CD02054952",
        "offline_time": 1474425106,
        "login": 1,
        "type": 0,
        "login_time": 1473823410
      }
    ]
}
```

#### 终端详细信息

URL: /terminaldetail

Table: 无

支持方法: POST

支持客户端: Web, Android, IOS

* POST方法

功能描述: 获取终端详细信息
请求参数:

| 参数   | 类型 | 描述   | 默认值 | 是否必填 |
|--------|------|--------|--------|----------|
| tid    |string| 终端id |   ""   | Yes      |

Example:
```json
{
    "tid": "152ae75a0c6947aeb0ee304f98c585b6"
}
```
返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-------------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message      | string   | 处理结果描述消息                          |
| data         | object   | 包含下列参数                              |
| activate_time| int      | 终端激活时间                              |
| begintime    | int      | 终端绑定时间                              |
| hb_time      | int      | 终端最近一次心跳时间                      |
| last_pkt_time| int      | 终端最后一个报文时间                      |
| install_time | int      | 终端安装时间                             |

Example:
```json
{
    "status": 0,
    "message": "操作成功。",
    "data": {
        "activate_time": 212342323,
        "begintime": 1423547589,
        "hb_time": 1437547589,
        "last_pkt_time": 1437547589,
        "install_time": 1437547589
    }
}
```

#### 终端历史位置信息

URL: /terminalposhistory

Table: 无

支持方法: POST

支持客户端: Web, Android, IOS

* POST方法

功能描述: 获取终端位置历史信息,指定时间戳之前的10条最新记录,按照时间倒序排列
请求参数:

| 参数   | 类型 | 描述   | 默认值 | 是否必填 |
|--------|------|--------|--------|----------|
| tid    |string| 终端id |   ""   | Yes      |
| timestamp | int  | 时间戳(不传则默认使用请求服务器的时间) |  0   | No   |

Example:
```json
{
    "tid": "152ae75a0c6947aeb0ee304f98c585b6",
    "timestamp": 1349858699
}
```

返回结果:

| 参数名称     | 参数类型 | 描述                                      |
|--------------|----------|-------------------------------------------|
| status       | int      | 处理结果状态值（0表示成功, 其他表示错误）  |
| message      | string   | 处理结果描述消息                         |
| data         | array    | 包含下列参数                            |
| locate_type  | int      | 定位类型（0：基站定位, 1：gps定位, 2: 未知-刚绑定未发送过报文的情况）|
| locate_time  | int      | 取点时间                                |
| gsm          | int      | GSM信号强度                             |
| gps          | int      | GPS信号的SNR值                          |
| latitude     | int      | 加密前纬度                              |
| longitude    | int      | 加密前经度                              |
| clatitude    | int      | 加密后纬度                              |
| clongitude   | int      | 加密后经度                              |

Example:
```json
{
    "status": 0,
    "message": "操作成功。",
    "data": [
        {
            "locate_type": 1,
            "locate_time": 1427277564,
            "gsm": 4,
            "gps": 40,
            "latitude": 80551404,
            "longitude": 408851028,
            "clatitude": 80560938,
            "clongitude": 408892892
        },
    ]
}
```

#### 终端开关状态设置
URL: /switch_setting

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

*  POST方法

功能描述: 终端开关状态设置

请求参数:

| 参数   | 类型   | 描述         | 默认值 | 是否必填 |
|--------|--------|--------------|--------|----------|
| settings | array | 开关设置对象数组 | []   | Yes      |
| tid | string | 终端id | "" | Yes      |
| mode | array | 开关名：开关状态 开关名列表 light,wifi,gps <br/>开关状态 1: 开启 0: 关闭 | []   | Yes      |

Example:

```json
{
  "settings": [
    {
      "tid": "t123",
      "mode": {
        "wifi": 0,
        "light": 1
      }
    },
    {
      "tid": "t234",
      "mode": {
        "light": 0
      }
    }
  ]
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | object   | 返回的信息                                |


Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data":{
    }
}
```

#### 终端设备历史
URL: /device_history

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

*  POST方法

功能描述: 终端设备历史

请求参数:

| 参数   | 类型   | 描述         | 默认值 | 是否必填 |
|--------|--------|--------------|--------|----------|
| tid    | string | 终端id       | "" | Yes  |
| begintime | int | 开始时间     |  0 | Yes |
| endtime   | int | 结束时间     |  0 | Yes |


Example:

```json
{
    "tid": "48417fes5f45e6gh",
    "begintime": 1445785648,
    "endtime": 1445934585
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | array   | 返回的信息                                |
| event_type | int   | 设备事件类型                              |
| create_at  | int   | 设备事件发生时间                          |
| name    | string   | 设备事件名称                             |
| remark  | string   | 设备事件详情说明                          |


Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data": [
        {
            "event_type": 1,
            "create_at": 1445934500,
            "name": "设备登录",
            "remark": ""
        },
        {
            "event_type": 2,
            "create_at": 1445934520,
            "name": "更换设备",
            "remark": "替换为SN：1A2B3C4D5E"
        },
    ]
}
```

#### 终端通讯时间
URL: /communicate_time

Table: 暂无

支持方法: POST

支持客户端:Web, Android, IOS

*  POST方法

功能描述: 终端通讯时间 **不支持ZJ210设备的时间获取**

请求参数:

| 参数   | 类型   | 描述         | 默认值 | 是否必填 |
|--------|--------|--------------|--------|----------|
| tids    | array | 终端id数组，不支持ZJ210设备的时间获取    | "" | Yes  |


Example:

```json
{
    "tids": ["t123", "t234"]
}
```

返回结果:

| 参数名称 | 参数类型 | 描述                                      |
|----------|----------|-------------------------------------------|
| status   | int      | 处理结果状态值（0表示成功, 其他表示错误） |
| message  | string   | 处理结果描述消息                          |
| data     | array   | 返回的信息                                |
| tid | string   | 终端id                            |
| last_time | int   | 终端上次通讯时间                            |
| next_time  | int   | 预计终端下次通讯时间                        |


Example:

```json
{
    "status": 0,
    "message": "操作成功",
    "data": [
        {
            "tid": "t123",
            "last_time": 554894542,
            "next_time": 586516548
        },
        {
            "tid": "t234",
            "last_time": 554894542,
            "next_time": 586516548
        }
    ]
}
```

## 子账号权限类型

子账号权限数据<br/>
使用逗号隔开;<br/>
1-车辆定位;<br/>
2-车辆活动回放;<br/>
3-车辆跟踪;<br/>
4-提醒查询;<br/>
5-设置紧急模式;<br/>
6-显示设备;<br/>
7-显示定位方式;<br/>
8-控制GPS开关;</br>
默认都有1权限
