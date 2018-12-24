# 文档说明

|发布日期|2018.12.09|
| ---------- | --- |
|产品名称|绿植计划|
|文件现状|进行中|
|文件的主人|陈文娟|
|更新|2018.12.23|
# 1. 产品说明
## a) 产品定位
> 绿植计划—每个植物都应该有个好名字

绿植计划是一款识别植物小游戏的微信小程序，不仅能认识各种植物还能在线上虚拟种植，用户在体验游戏的乐趣的同时还能获取植物科普知识。
## b) 用户痛点

- 遇到植物不认识，需要识别工具
- 不懂栽培知识，导致植物生长受阻/致死
- 懒得阅读百科信息

## c)产品核心目标
- 识别图片中的植物，得出植物百科信息。
- 植物百科信息语音读取，解放双眼，语音播报植物百科。

## d）产品核心功能举例

花园主游戏模块
辨认植物模块
#### AR识别植物模块
个人模块

## e)价值宣言
市场上已有的通过花果叶等特征部位图片识别各种植物花卉的产品，没有语音播报功能。用户在扫描完植物时，焦点更应该放在大自然，而不是手机上，因此基于此用户痛点，结合百度语音合成技术，制作出这款产品。

## f)产品概述(最小可行性产品）
绿植计划以拍照识别图片中的植物为基础功能，用户拍照上传植物图片，可获得植物百科信息，一键点击语音播报植物百科信息。

## g）人工智能概率性
花伴侣智能植物识别API使用中科院权威图库识别数量包括杂草一万一，准确率>95%。

形色植物识别API包括中国常见4000种植物，准确率>98%。


# 2. 用户分析
## a) 目标用户群体
- 年龄：13-30岁 
- 学历：初中及以上
- 地区：城市
- 以学生、白领为主要用户
- 主要集中在90、00后
- 居住在三四线城市
- 游戏爱好者、植物爱好者、花艺爱好者、孩子家长、教育者、旅行者


## b) 用户需求
|.|功能|应用|技术|
| --- | --- |--- | --- |
|1| 植物花卉识别|看到不认识的植物拍照识别|图像识别
|2| 常见杂草识别|即使是杂草也想知道是怎么草|图像识别
|3|植物百科信息|想进一步了解植物信息，获取植物养护资料|图像识别
|4|语音播报|不想看太多的文字|语音合成

## c) 使用的API
- 花伴侣智能植物识别API
- 形色植物识别API
- 百度语音合成API

# 3.可行性分析
https://github.com/ccwwen/try/tree/master

调用花伴侣智能植物识别API

1.识别清晰的植物图片
![杜鹃.jpeg](https://upload-images.jianshu.io/upload_images/9130153-c795a559701a8cb8.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
调用API


```python
import base64
import requests
url_host = "http://plantgw.nongbangzhu.cn"
app_code = '38ef43ff3c704a7c8bc5f934185b3a3d' #这里替换为你购买的AppCode
# 植物花卉识别接口_v2的请求示例
def recognize2():
    url_path = '/plant/recognize2'

    with open("./pics/杜鹃.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + '38ef43ff3c704a7c8bc5f934185b3a3d'}
        response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
recognize2()
# 植物百科信息获取
def info():
    url_path = '/plant/info'

    code = "gRznEHlcJyg46Tpd" # 这个植物代号是调用recognize2()时获得的InfoCode字段
    body = {'code': code}
    headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + app_code}
    response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
    print(response.text)

    return
info()
```


返回结果
![@ZH`97D%VMZX8}1UG(L[YHO.png](https://upload-images.jianshu.io/upload_images/9130153-c9c05a2a4c5c0abe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.识别杂草
![狗尾草.jpg](https://upload-images.jianshu.io/upload_images/9130153-0662418171084be3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```python
def weed():
    url_path = '/plant/recognize_weed'

    with open("./pics/狗尾草.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + app_code}
        response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
weed()

```

```json
{"Status":0,"Message":"OK","Result":[{"Score":"71.10","AliasList":[],"Genus":"狗尾草属","InfoCode":"lxBYUeDkinFIebDN","AliasName":"","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E9%87%91%E8%89%B2%E7%8B%97%E5%B0%BE%E8%8D%89/57b22cd5eee20ca7a42052f2c295ec24bee56743bf4082d8b386d0fb1f22a51e.jpeg","LatinName":"Setaria pumila",
"Name":"金色狗尾草"},{"Score":"26.63","AliasList":["谷莠子","莠"],"Genus":"狗尾草属","InfoCode":"Ldky3VBXkBXT1gk1","AliasName":"谷莠子、莠","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%8B%97%E5%B0%BE%E8%8D%89/3eb25266b9522aa0c4579c4cee8509ffe595f981c0792c5881a77087a353ce99.jpeg","LatinName":"Setaria viridis",
"Name":"狗尾草"},{"Score":"2.04","AliasList":["法氏狗尾草"],"Genus":"狗尾草属","InfoCode":"LTRjFvZfKKGC42gA","AliasName":"法氏狗尾草","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%A4%A7%E7%8B%97%E5%B0%BE%E8%8D%89/3c685666212f4bcddabc866372f6261d3e53e770a2e8c0a14904c5a85b8e2d03.jpeg","LatinName":"Setaria faberi",
"Name":"大狗尾草"},{"Score":"0.01","AliasList":["荠菜","菱角菜"],"Genus":"荠属","InfoCode":"O0OUVuZnuRzsdf6E","AliasName":"荠菜、菱角菜","Family":"十字花科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E8%8D%A0/eb35c6ecc963232588968eb2efa297f81ab84f0171c3a008bb71adb85fa8bf05.jpeg","LatinName":"Capsella bursa-pastoris",
"Name":"荠"},{"Score":"0.01","AliasList":[],"Genus":"菵草属","InfoCode":"hMKVHhUAV4entqJr","AliasName":"","Family":"禾本科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E8%8F%B5%E8%8D%89/2a3064175a9d0506a4b4fec259ad40044bdb4a93a6b3a26d521d0e32d0941d04.jpeg","LatinName":"Beckmannia syzigachne",
"Name":"菵草"}]}
```




3.识别模糊的植物图片

![image](https://upload-images.jianshu.io/upload_images/9130153-685ad592134f1e13.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

输出
![60QN)DG[AWX6HM}Y)SZ{GAQ.png](https://upload-images.jianshu.io/upload_images/9130153-df3f0f29d4c5438a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```json
{"Status":0,"Message":"OK","Result":[{"Score":"68.33","AliasList":["蟑螂花","龙爪花"],"Genus":"石蒜属","InfoCode":"b7bK68TQkpSYFWQy","AliasName":"蟑螂花、龙爪花","Family":"石蒜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%9F%B3%E8%92%9C/a57f668fc68e5576ecd5629079b2f62a7883a7981a98d43c84ea8ee12f734fe0.jpeg","LatinName":"Lycoris radiata",
"Name":"石蒜"},{"Score":"10.90","AliasList":[],"Genus":"虎耳兰属","InfoCode":"YYsDD68zEX3S5IJA","AliasName":"","Family":"石蒜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%BD%91%E7%90%83%E8%8A%B1/326d5acf43296dcfea5403c200090b10553ffe018cc05ff8801072d334d4c326.jpeg","LatinName":"Haemanthus multiflorus",
"Name":"网球花"},{"Score":"3.47","AliasList":["宽苞茅膏菜"],"Genus":"茅膏菜属","InfoCode":"r7GxejtzIogOxTAh","AliasName":"宽苞茅膏菜","Family":"茅膏菜科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%8C%99%E5%8F%B6%E8%8C%85%E8%86%8F%E8%8F%9C/b0ed070faf73d9ceda1c7b5fd787947e2b1563adb89033e373f47e721d13625f.jpeg","LatinName":"Drosera spatulata",
"Name":"匙叶茅膏菜"},{"Score":"1.56","AliasList":["灯笼花","假西藏红花"],"Genus":"木槿属","InfoCode":"aSYfLGuDxcY7KUCr","AliasName":"灯笼花、假西藏红花","Family":"锦葵科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E5%90%8A%E7%81%AF%E8%8A%99%E6%A1%91/bb0a9452a68edf55a1e43e3facde2c1d67088ffdc41b7af0a7ee418a06137986.jpeg","LatinName":"Hibiscus schizopetalus",
"Name":"吊灯芙桑"},{"Score":"0.75","AliasList":[],"Genus":"","InfoCode":"qvguYOtMzX26EKoS","AliasName":"","Family":"","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%9C%B1%E7%A0%82%E6%A2%85/32ca46e12651f98ad9c8fb729f64f9a39df403a2859ccaae2bbacdf49a019457.jpeg","LatinName":"Turpinia pomifera var. pomifera",
"Name":"朱砂梅"}]}
```

4.百度语音合成API

![语音合成.jpg](https://upload-images.jianshu.io/upload_images/9130153-401f0f852291377b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 4.API使用风险评估
图片灰暗
![暗蒲公英花.jpg](https://upload-images.jianshu.io/upload_images/9130153-74d5a74558e2005f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
输出结果


```python
import base64
import requests
url_host = "http://plantgw.nongbangzhu.cn"
app_code = '38ef43ff3c704a7c8bc5f934185b3a3d' #这里替换为你购买的AppCode
# 植物花卉识别接口_v2的请求示例
def recognize2():
    url_path = '/plant/recognize2'

    with open("./pics/暗蒲公英花.jpg", "rb") as image_file:
        img_base64 = base64.b64encode(image_file.read()).decode('ascii')
        body = {'img_base64': img_base64}

        headers = {'content-type': "application/x-www-form-urlencoded", 'authorization': "APPCODE " + '38ef43ff3c704a7c8bc5f934185b3a3d'}
        response = requests.request("POST", url_host+url_path, data=body, headers=headers) # 默认utf-8
        print(response.text)

    return
recognize2()
```

```json

{"Status":0,"Message":"OK","Result":[{"Score":"21.48","AliasList":["红毛大字草"],"Genus":"虎耳草属","InfoCode":"54rnyde9GLF7wR4i","AliasName":"红毛大字草","Family":"虎耳草科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%BA%A2%E6%AF%9B%E8%99%8E%E8%80%B3%E8%8D%89/120d6ca9d339de3ab7245cf239ad26cd443bfdccf4e6de083f90f5f5c57955f9.jpeg","LatinName":"Saxifragarufescens",
"Name":"红毛虎耳草"},
{"Score":"4.06","AliasList":[],"Genus":"星果草属","InfoCode":"oXlVI0VNZdLaedPm","AliasName":"","Family":"毛茛科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%98%9F%E6%9E%9C%E8%8D%89/90500c265a59f7ab961096372778d28dc567f032a997bea7d91895ee68c1e691.jpeg","LatinName":"Asteropyrum peltatum",
"Name":"星果草"},
{"Score":"2.87","AliasList":[],"Genus":"水毛茛属","InfoCode":"Glr2LtWgQR1CcBv4","AliasName":"","Family":"毛茛科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%B0%B4%E6%AF%9B%E8%8C%9B/abb8e9fda07414340cab3916495d11fb2ba015225f867660a6627a578e71ed5a.jpeg","LatinName":"Batrachium bungei",
"Name":"水毛茛"},
{"Score":"1.64","AliasList":["异叶水车前","龙爪菜"],"Genus":"水车前属","InfoCode":"j6Q5iuIK3EWPOdho","AliasName":"异叶水车前、龙爪菜","Family":"水鳖科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E6%B5%B7%E8%8F%9C%E8%8A%B1/26f4ed8bbc7d71603d73afce4cac80bf9291b7b8f1a70562b9976ec5590c0850.jpeg","LatinName":"Ottelia acuminata",
"Name":"海菜花"},
{"Score":"1.50","AliasList":[],"Genus":"淫羊藿属","InfoCode":"k3v1uRBPjzoGmQpR","AliasName":"","Family":"小檗科","ImageUrl":"https://api.aiplants.cn/resource/1001/%E7%B2%97%E6%AF%9B%E6%B7%AB%E7%BE%8A%E8%97%BF/ba6b39491fb2641199574174486066e574a19552ad6398f774c260bd4a3c7d8e.jpeg","LatinName":"Epimedium acuminatum",
"Name":"粗毛淫羊藿"}]}
```



---
植物图片清晰识别的效果最好，甚至使用模糊的、图片上有字体遮盖的图片，曼莎珠花属石蒜科，但并不是石蒜，所以识别结果有偏差。
但是使用昏暗且模糊化的图片，识别结果是错误的。光照和清晰度都在影响着植物的识别结果。

# 5.产品原型
1.产品结构图
![image](https://upload-images.jianshu.io/upload_images/9130153-d38b22726728f866.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.产品流程图
![image](https://upload-images.jianshu.io/upload_images/9130153-547beb11a20bb447.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3.产品原型

![image](https://upload-images.jianshu.io/upload_images/9130153-1fa5cbb8e34ab8bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/9130153-63f9e88a7f7002a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image](https://upload-images.jianshu.io/upload_images/9130153-329945e5e88ec3d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
