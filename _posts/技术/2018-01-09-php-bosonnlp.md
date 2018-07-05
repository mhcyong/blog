---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/1505981853.jpg
date: 2018-01-09 15:54
title: PHP利用BosonNLP接口提取关键词
category: 技术
cslug: technology
tags:
- 工具
- 代码
- PHP
---

我们写文章的时候，一般都会有填写标签这个要求，这种用户不仅反感，还可能填写错误，从而带来不好的体验，如果能让程序分析自动提取标签，就避免了以上问题，只要这个程序够好就行。  
在这里，我们调用bosonNLP的接口来实现：  
```php
//开始文章标签的处理
$API_TOKEN = "您的API";
$SENTIMENT_URL = 'http://api.bosonnlp.com/keywords/analysis?top_k=3';
$data = $request->get('title').$request->get('content');
$ch = curl_init();
curl_setopt_array($ch, array(
    CURLOPT_URL => $SENTIMENT_URL,
    CURLOPT_HTTPHEADER => array(
        "Accept:application/json",
        "Content-Type: application/json",
        "X-Token: $API_TOKEN",
    ),
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => json_encode($data, JSON_UNESCAPED_UNICODE),
    CURLOPT_RETURNTRANSFER => true,
));
$output = curl_exec($ch);
curl_close($ch);

$output_arr = array();
if (!empty($output)) {
$output_arr = json_decode($output, true);
}

//结束文章标签的处理
```

这个$output_arr数组就是接口提取的关键词。