---
layout: blog
technology: true
background: blue
background-image: /thumbs/Laravel.png
date: 2018-01-09 16:23
title: Laravel配置多国语言包，中文提示
category: 技术
ascription: technology
tags:
- PHP
- Laravel
---

Laravel默认显示的是英文的错误信息，实际上laravel考虑到了国际化的问题，首先修改 config/app.php，将 locale 语言设置为中文，或者其它你想使用的语言。  
 ` 'locale' => 'zh-CN',`  
然后再 resources/lang 下面新建文件夹 zh-CN，
到https://github.com/caouecs/Laravel-lang/tree/master/src/zh-CN ，拷贝里面的文件到zh-CN文件夹里面。  
当然，laravel 也在控制器中集成了 validate 方法，换句话说，我们不一定要生成 request 类，这些工作我们可以直接在控制器中完成。  
```
  //注意 Request 的命名空间，不要弄错了
    public function store(\Illuminate\Http\Request $request) {

        $this->validate($request, [
            'title' => 'required|min:3',
            'body' => 'required',
            'published_at' => 'required|date'
        ]);

        Article::create($request->all());

        return redirect('articles');
    }
```
min:3 的判断也为最少3个中文，这两种方式都可以完成验证中文提示，其他语言类似。