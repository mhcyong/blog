---
layout: blog
technology: true
background: green
background-image: https://obdr74yw6.qnssl.com/php.jpg
date: 2018-01-09 16:18
title: 真正验证一个邮件地址的有效性
category: 技术
ascription: technology
tags:
- PHP
- 代码
---

一个邮件地址是否有效关系一定程度上决定了这个用户是否是优质用户，或者说成为优质用户的潜质更大。所以在用户注册的时候，我们通常会绞尽脑汁来验证一个邮箱地址的有限性。  
本文并不是简单地讨论使用正则表达式来验证一个邮箱地址是否正确，而是希望通过更多的手段来真正验证一个邮箱地址的邮箱性。  
本文验证一个邮件地址有效性的内容包含以下几个内容：  
1、最常规的正则表达式的匹配  
2、邮件的 DNS 有效性  
3、检验 MX 记录的有效性  
4、屏蔽一次性邮件服务商  
5、更多细节，比如发起发信请求  
## **validator.pizza**
在这里推荐大家可以使用 https://www.validator.pizza 邮件验证服务，免费，准确率还很高。具体的实现方式是通过向 validator.pizza 发起 HTTP 请求，用来验证用户邮箱地址是否有效，比如，普通的 PHP 代码可以是这个样子：  
```php
$email = "12345@qq.com"; // 这是一个垃圾邮件
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://www.validator.pizza/email/' . $email);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
$response = curl_exec($ch);
curl_close($ch);
var_dump($response);
```
或者在 Laravel 的项目当中，我们还可以直接扩展 Validator 来实现邮件地址有效性的验证,在 AppServiceProvider 的 boot() 方法添加下面的代码：  
```php
public function boot()
    {
        Validator::extend('isValid', function ($attribute, $value, $parameters, $validator) {
                $request = (new Client())->get('https://www.validator.pizza/email/' . $value);
                $body = json_decode($request->getBody()->getContents());
                switch ( $body ) {
                    case $body->status == 400:
                        return false;
                    case !$body->mx:
                        return false;
                    case $body->disposable:
                        return false;
                    default:
                        return true;
                }
            }, '邮箱地址不可用');
}        
```
然后在验证的时候可以这样使用：  
`$this->validate(request(),['email'=>'required|isValid'])`  
这样一来，基本上就可以应付 90% 以上的邮件地址验证，包含一次性邮件地址验证和有效性验证。