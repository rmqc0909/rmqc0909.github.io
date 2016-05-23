---
layout: post
title: 基于流的自动化构建工具--Gulp
keywords: Gulp
categories : [JavaScript]
tags : [JavaScript, Gulp]
---
Gulp是基于“流”的自动化构建工具（关于这个“流”，待会还有详细的说明）。相信使用过Unix的朋友都知道“管道”的概念，前一级的的**输出**变成后一级的**输入**。每个插件专注于完成单一的职责，像一条自动化的流水线一样，只要把合适的插件组合起来，这样就可以解决复杂的问题。

Gulp上手比较简单，除去一些简单的任务之外，还是有一些高级应用需要注意的。

###基础操作
Gulp配置一个任务只需像写代码那样轻松：

{% highlight javascript %}
  gulp.task('scripts', function() {  
    return gulp.src('./src/filepath/.js')
      .pipe(uglify())
      .pipe(concat('all.min.js'))
      .pipe(gulp.dest('build/'));
  });
{% endhighlight %}


###Gulp的流
Gulp虽然基于Node，但是它没有使用Node中fs模块的流，而是包装了一层vinyl。vinyl是一种描述文件的数据格式，通过vinyl-fs把Node的原生文件封装成vinyl。这种“流”是启用 object mode 的流，而不是Buffers等Node流。因此在使用Gulp的过程中，偶尔会遇到 **Streaming not supported** 这样的错误。

{% highlight javascript %}
  var uglify = require('gulp-uglify');  
  var rename = require('gulp-rename');

  gulp.task('bundle', function() {  
    return fs.createReadStream('app.js')
      .pipe(uglify())
      .pipe(rename('bundle.min.js'))
      .pipe(gulp.dest('dist/'));
  });
{% endhighlight %}

**vinyl-source-stream** 便是一个转换工具,于是可以：

{% highlight javascript %}
  var source = require('vinyl-source-stream');  
  var marked = require('gulp-marked');

  fs.createReadStream('file')  
  .pipe(source())
  .pipe(marked())
  .pipe(gulp.dest('dist/'));
{% endhighlight %}
