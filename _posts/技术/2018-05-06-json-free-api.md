---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/Snipaste_2018-05-06_10-15-28.png
date: 2018-01-07 19:10
title: 整理的一些JSON格式免费接口API 
category: 技术
ascription: technology
tags:
- 接口
- 开发
---

**快递单号跟踪接口**  
`http://www.kuaidi100.com/query?type=快递公司代号&postid=快递单号`  
快递公司编码:  
申通="shentong" EMS="ems" 顺丰="shunfeng" 圆通="yuantong" 中通="zhongtong" 韵达="yunda"
天天="tiantian" 汇通="huitongkuaidi" 全峰="quanfengkuaidi" 德邦="debangwuliu" 宅急送="zhaijisong"  


**淘宝商品搜索建议接口**  
`http://suggest.taobao.com/sug?code=utf-8&q=商品关键字&callback=cb`  
其中callback是回调函数设定  

 
**百度百科接口**  
`http://baike.baidu.com/api/openapi/BaikeLemmaCardApi?scope=103&format=json&appid=379020&bk_key=关键字&bk_length=600`  


**淘宝IP接口**  
`http://ip.taobao.com/service/getIpInfo.php?ip=171.88.100.127`  


**手机信息查询接口**  
`http://tcc.taobao.com/cc/json/mobile_tel_segment.htm?tel=手机号`  


**地图接口**
阿里云根据地区名获取经纬度接口   
`http://gc.ditu.aliyun.com/geocoding?a=苏州市`  
获取用户经纬度，以及获取附近建筑物名  
`http://ditu.amap.com/service/regeo?longitude=121.04925573429551&latitude=31.315590522490712`  


**文字转语音接口**  
`https://tts.baidu.com/text2audio?lan=zh&ie=UTF-8&spd=2&text=需要转换成语音的文字`