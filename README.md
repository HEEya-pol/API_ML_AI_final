
# 项目名称：宠物管家

| Title | Content |
| --- | --- |
## 背景
随着经济的发展，人们对精神层面的追求越来越高，越来越多的人开始饲养宠物，人们饲养宠物成为精神、生活伴侣。近年来宠物经济火爆，各市场领域规模激增，人们对宠物以及宠物周边服务的需求在持续不断增长着，但是宠物饲养趋势不断攀升，市面上的宠物app仍就不多，还处于探索阶段。
## 产品定位
“PET”是一款宠物管家软件，旨在于帮助宠物主人了解以及护理爱宠。
## 产品功能
- 识别宠物类型
- 附近宠物医院/宠物中心
- 社区交流养宠心得
- 提醒对爱宠进行护理
## 加值宣言
- 百度动物识别
识别近八千种动物，接口返回动物名称，并获取百科信息
- 高德地图api
多种搜索方式，高德提供了千万级别的POI，通过POI搜索，可以完成找宠物医院、找宠物中心等等的功能
## 核心价值
-  动物识别：拍照／上传宠物图片，检测该图片，返回识别结果的百科信息。
- 高德地图api：搜索出附近相关宠物地点，并规划出路线。
## 用户痛点
- 用户不了解爱宠习性和宠物护理，很难系统地收集到宠物信息
- 宠物异常行动现象会让大多数用户感到很可恼，无从下手
- 用户找不到一款合适的宠物软件
## 用户需求		
| 用户案例| 对应接口|   重要程度|
| --- | --- |--- |
| 用户希望了解爱宠品种和习性| 动物识别|重要|
| 用户想要知道附近的宠物医院/宠物中心及路径| 高德地图|  特别重要|
| 用户希望可以有一个平台发布爱宠动态，并且与他人交流养宠新心得|    | 重要|
##### 具体运用场景：
- 场景一：用户a捡了一只流浪猫，他想知道这只猫的品种，于是打开识别功能，通过上传这只猫的图片，得到这只猫的品种信息
- 场景二：用户b的爱宠生病了，他想知道附近的宠物医院及路径，于是打开搜索功能，得到了附近宠物医院的信息和地图路径
## 产品目标
###### 前期：
- 识别宠物品种及相关信息
- 地图搜索
- 通过投放宠物用品广告，实现盈利
###### 后期：
- 建立宠物交流社区
- 上线商城功能和上门服务，增加产品盈利
## 产品原型
1. 宠物识别
![ ](https://github.com/HEEya-pol/API_ML_AI_final/blob/master/image/1a5d11b7eb9142b92c5457a894aa487.png)
2. 宠物场所搜索
![ ](https://github.com/HEEya-pol/API_ML_AI_final/blob/master/image/8e385e07d599db9eed5bcdf18ce4e31.png)
## 产品架构图
## 原型文档
## API的调用
###### 接口描述：
识别近八千种动物，接口返回动物名称，支持获取识别结果的百科信息，接口返回百科词条URL、图片和描述，支持自定义返回词条数
###### 请求地址：https://aip.baidubce.com/rest/2.0/image-classify/v1/animal
###### 服务示例：
- 输入内容：
```
# encoding:utf-8
import base64
import urllib.parse
import urllib.request
 
'''
动物识别
'''
 
request_url = "https://aip.baidubce.com/rest/2.0/image-classify/v1/animal"
 
# 二进制方式打开图片文件
f = open('C:/Users/Alyfu/Desktop/f.png', 'rb')
img = base64.b64encode(f.read())
 
params = {"image":img,"top_num":6}
params = urllib.parse.urlencode(params).encode(encoding='UTF8')
 
access_token = '[调用鉴权接口获取的token]'
request_url = request_url + "?access_token=" + access_token
request = urllib.request.Request(url=request_url, data=params)
request.add_header('Content-Type', 'application/x-www-form-urlencoded')
response = urllib.request.urlopen(request)
content = response.read()
if content:
    print(bytes(content).decode('utf-8'))
```
- 返回结果
```HTTP/1.1 200 OK
x-bce-request-id: 73c4e74c-3101-4a00-bf44-fe246959c05e
Cache-Control: no-cache
Server: BWS
Date: Tue, 18 Oct 2016 02:21:01 GMT
Content-Type: application/json;charset=UTF-8
{
    "log_id": "3833028759661534105",
   "result": [
     {
        "score": "0.208929",
            "name": "美国短毛猫"
       },
     {
       "score": "0.139112",
        "name": "家猫"
        },
      {
       "score": "0.0580069",
      "name": "布偶猫"
     },
      {
       "score": "0.0542856",
      "name": "波米拉猫"
      },
          {
         "score": "0.0482468",
         "name": "英国短毛猫"
         },
         {
            "score": "0.0471158",
            "name": "欧洲短毛猫"
       }
    ]
} 
```
