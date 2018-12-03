Document owner: 陈文娟

target release:2018.11.25

## 产品名称
绿植计划

## 产品定位：
认识绿植
## 用户需求：
- 亲近大自然
- 认识更多植物（显得很博学，可以装X）
- 学习过程中有趣快乐
- 能和好友分享美丽的植物照片
- 栽培植物知识

## 解决问题：
- 怎么直接看到植物就能知道名称以及详细资料
- 在好友or女/男神面前显得博学
- 快乐的学习

## 目标用户：
- 16-45岁
- 适合植物爱好者、花艺爱好者、孩子家长、教育者、旅行者、摄影爱好者、文艺小青年以及任何热爱生活、喜欢植物的人。


## 产品优势：
 
 线上的类似软件都没有游戏功能，不能更好的吸引非植物爱好者。
 游戏的设置可以增加用户的黏性。
 
## 产品架构
![image](https://upload-images.jianshu.io/upload_images/9130153-4157cf549371949e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)
## 界面
![image](https://upload-images.jianshu.io/upload_images/9130153-34979540d9a1c4ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/313/format/webp)![image](https://upload-images.jianshu.io/upload_images/9130153-1fb6fd463b437b38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/311/format/webp)
![image](https://upload-images.jianshu.io/upload_images/9130153-685c16325df63b87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/826/format/webp)

## 产品基本功能：
1.  拍照识别植物之后，会显示植物的基本介绍，详情看原型。
2. 用户看完绿植介绍时，就会掉落一些植物碎片或金币，植物碎片可以合成特殊植物，（上传此地图上没有的植物的图片，可获得特殊奖励）。
3. 识别的植物会变成卡通版植物呈现在我的花园里，可选择种植或不种植。
4. 在我的花园中，每天浇水除草，会加速植物的种植速度。
5. 可以添加好友，去好友的花园里采花，可帮好友除虫，浇水。
6. 赠送花朵给好友。

## 项目规划
1. 社交模块、植物美图分享
2. 植物种植课程上线
3. 与淘宝花店合作
## 功能实现
- 细粒度图像识别-植物识别api
- 调用阿里开发的花伴侣api
- 可以出现植物百科，植物名称，类别。
- 花伴侣智能植物识别-品类最全，含花卉，植物和农田杂草共一万一千种，使用植物所权威图库。也提供百科接口，含形态特征，花语，养护等
- 正常返回示例
```
{
  "Status":0,
  "Message":"OK",
  "Result":[
    {
      "Name":"日本晚樱",                                   //植物名称
      "LatinName":"Cerasus serrulata var. lannesiana",   //植物拉丁名 
      "AliasName":"",                                    //植物别名，顿号分割的字符串格式
      "AliasList":[]                                     //别名列表，数组格式
      "Family":"蔷薇科",                                  //所属科名
      "Genus":"樱属",                                     //所属属名
      "Score":"77.97"，                                   //可能性百分率（77.97%）
      "ImageUrl":"http://xxx/.../xxx.jpg",               //植物例图
      "InfoCode":"VRSIihzEBztyp3Hl"                      //植物百科信息获取接口需要的代号
    },
    {
      "Name":"大叶早樱",
      "LatinName":"Cerasus subhirtella",
      "AliasName":"小彼岸",
      "AliasList":[小彼岸]
      "Family":"蔷薇科",
      "Genus":"樱属",
      "Score":"20.45"，
      "ImageUrl":"http://xxx/.../xxx.jpg",
      "InfoCode":"VRSIihzEBztyp3Hl"
    },
    ...]
}
```
