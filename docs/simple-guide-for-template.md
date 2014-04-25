# HTML模板常用标签设置整理

工作中免不了要接触到HTML，通常都会用编辑器的代码片段，或者诸如Emmet这类自动完成的工具生成HTML模板。对于PC端的Web页面，总会涉及到很多标签的设置问题，今天作个整理归类，方便参考。

- __DOCTYPE设置，推荐使用HTML5 doctype__

```html
<!DOCTYPE html>
<!-- 貌似DOCTYPE关键字不区分大小写 -->
<!-- 也可以这样写 -->
<!doctype html>
```

实际上`DOCTYPE`设置还支持一些可选项，但是一般情况下我们都用不到。详细信息可参考：

> - [W3C规范中推荐的有效DTD配置列表](http://www.w3.org/QA/2002/04/valid-dtd-list.html)
> - [HTML5 DOCTYPE声明规范](http://dev.w3.org/html5/html-author/#doctype-declaration)
> - [HTML规范中的DOCTYPE编写语法](http://www.w3.org/html/wg/drafts/html/master/syntax.html#the-doctype)

- __为`html`元素设置标准的`lang`属性__

```html
<html lang="zh-cmn-Hans" /> <!-- 针对简体中文的设置 -->
<html lang="zh-cmn-Hant" /> <!-- 针对繁体中文的设置 -->
```

在访问外文站点的时候，Chrome通常都会提示是否翻译语言神马的就是基于`html`元素的`lang`属性决定的。以前一直都写`zh-cn`的，查阅资料发现并不规范。

`lang`属性还可以用于其他元素设置地区代码已区别[不同地区汉语使用差异](https://zh.wikipedia.org/wiki/%E4%B8%8D%E5%90%8C%E5%9C%B0%E5%8C%BA%E6%B1%89%E8%AF%AD%E4%BD%BF%E7%94%A8%E5%B7%AE%E5%BC%82)。更多的资料可以参考知乎上的一个讨论：

> - [网页头部的声明应该是用 lang="zh" 还是 lang="zh-cn"？](http://www.zhihu.com/question/20797118)
> - [W3C规范之lang属性](http://www.w3.org/TR/html5/dom.html#attr-lang)

- __字符编码设置__

```html
<meta charset="utf-8" />
```

优先选用精简的写法，并且推荐使用`UTF-8`编码，可选的还有`GBK`、`gb2312`、针对繁体中文的`Big5`以及其他外文编码选项。

老版本写法：

```html
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
```

但是在HTML5中，这两者基本上是等价的。使用简写的方式更方便记忆，本身简写就被设计为向后兼容。

> - [Meta Charset Attribute](https://code.google.com/p/doctype-mirror/wiki/MetaCharsetAttribute)

- __IE兼容性meta写法__

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
```

在IE8中引入了文档兼容性这个东西，刚开始主要是对IE6的兼容性模式扩展。`content`属性有很多可选值，但是推荐优先使用最新版IE兼容性模式。参考资料：

> - [MSDN - 定义文档兼容性](http://msdn.microsoft.com/zh-cn/library/cc288325\(v=vs.85\).aspx)
> - [Stackoverflow - IE兼容性模式之间的差异讨论](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e)

上面是IE浏览器可以设置的兼容性模式，国内的360安全浏览器对这一设置作了扩展：

```html
<meta name="renderer" content="webkit|ie-comp|ie-stand" />
```

这里的`content`属性可选值有`webkit`，`ie-comp`，`ie-stand`。这三个选项区分大小写，分别代表启用极速模式，兼容模式，IE模式。

目前国内双核浏览器的默认内核模式情况：

- 搜狗告诉浏览器：默认使用IE内核（兼容模式）
- 360极速浏览器：默认使用Chromium内核（极速模式）
- 傲游浏览器：默认使用Webkit内核（极速模式）
- QQ浏览器：默认使用IE内核（兼容模式）

> 关于国内双核浏览器的兼容模式资料来源于QQ群中网友的讨论，具体情况没有详细测试。

— __favicon设置__

```html
<link type="image/x-icon" rel="shortcut icon" href="/favicon.ico" /> <!-- retina screen ? -->
<link type="image/ico" rel="shortcut icon" href="/favicon.ico" /> <!-- normal -->
```

这个都懂的，:smile:。

- __SEO优化配置__

```html
<meta name="description" content="" /> <!-- 页面描述 -->
<meta name="keywords" content=""/> <!-- 页面关键词 -->
<meta name="author" content="basecss, i@basecss.net" /> <!-- 声明网页作者 -->
<meta name="robots" content="index,follow" /> <!-- 定义搜索引擎索引页面的方式 -->
<title>页面标题</title>
```

这个大家都懂的。参考资料：

> - [meta description](http://www.w3.org/TR/html5/document-metadata.html#meta-description)
> - [Metadata](http://www.w3.org/wiki/HTML/Training/Metadata)
> - [&lt;meta name="robots"&gt;标记设置](http://msdn.microsoft.com/zh-cn/library/ff724037\(v=expression.40\).aspx)

— __针对移动设备的`viewport`设置__

```html
<meta name="viewport" content="initial-scale=1, maximum-scale=3, minimum-scale=1, user-scalable=no, minimal-ui" />
```

`viewport`配置中的`content`属性中的参数选项：

- `width` 设置viewport宽度（数值/device-width)，`width`取值一直都用的`device-width`，据说这样设置会导致iPhone5添加快速启动入口到主屏幕之后再以WebApp的形式全屏模式打开会出现黑边现象 - [WebAPP ViewPort iPhone5 黑边解决方案](http://bigc.at/ios-webapp-viewport-meta.orz)
- `height` 设置viewport高度（数值/device-height）
- `initial-scale` 初始缩放比例
- `minimum-scale` 最小缩放比例
- `maximum-scale` 最大缩放比例
- `user-scalable` 是否允许用户缩放，可选值：`yes`，`no`
- `minimal-ui` __iOS 7.1 beta2__中新增的属性，可以再页面加载时最小化浏览器上下状态栏，值为布尔值，可直接写上`minimal-ui`。

参考资料：

> - [一份网友整理的响应式设计指南](http://www.adamkaplan.me/grid/)
> - [PPK整理的viewport浏览器兼容性列表](http://www.quirksmode.org/mobile/tableViewport.html)
> - [PPK编写的两边关于viewport的文章](http://www.quirksmode.org/blog/archives/2010/06/a_tale_of_two_v_1.html) - PS：网上可以找到好几个版本的译文。
> - [Apple开发者中心关于viewport的文档](https://developer.apple.com/library/ios/documentation/appleapplications/reference/safariwebcontent/usingtheviewport/usingtheviewport.html)
> - [iOS 7.1 发布日志](https://developer.apple.com/library/iOS/releasenotes/General/RN-iOSSDK-7.1/index.html)

PS：`viewport`貌似就是Apple在自家的Safari浏览器中引入的概念。

- __移动端的各种其他meta标签配置__

```html
<meta name="apple-touch-fullscreen" content="yes"/> <!-- 添加主屏幕之后再次启动是否全屏 -->
<meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 是否允许页面以应用风格显示。-->
<!-- 设置这个属性为yes时，在iPhone5上从主屏幕启动时页面不能撑满设备高度，可放弃设置viewport的width=device-width配置，然后在iPhone 5默认以640的宽度显示时，结合scale=0.5的方式适配设备，注意在CSS中尽量以640为基准排版页面 -->
<meta content="black" name="apple-mobile-web-app-status-bar-style" /> <!-- 状态栏在standalone状态下的表现方式，设置为default表示以白色的方式显示，black表示显示黑色，black-translucent表示显示黑色半透明。这个选项在设置apple-mobile-web-app-capable配置的content为yes时才有效 -->
<!--! 如果设置为default或black网页内容从状态栏底部开始; 如果设置为black-translucent网页内容充满整个屏幕，顶部会被状态栏遮挡。-->
<meta name="format-detection" content="telephone=no" /> <!-- 自动检测符合电话号码规则的文本，iOS默认将数字解析为电话号码，配置telephone=no可以禁用这一特性 -->
<meta name="apple-itunes-app" content="app-id=xxxx, affiliate-data=myAffiliateData, app-argument=myURL" /> <!-- iOS设备自带的smartbanner配置，这里的app-id用于配置自动显示下载app的banner，指定app id即可 -->
<meta name="apple-mobile-web-app-title" content="标题" /> <!-- 设置添加到主屏幕后显示的标题，iOS6中新增的 -->
```

参考资料：

> - [Apple开发者中心关于meta标签的文档](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)
> - [Promoting Apps with Smart App Banners](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)

- __启动图标设置__

```html
<!-- iOS设备启动图标设置 -->
<link rel="apple-touch-icon" href="icon57.png" sizes="57x57"> <!-- 非视网膜 iPhone 低于 iOS 7 -->
<link rel="apple-touch-icon" href="icon72.png" sizes="72x72"> <!-- 非视网膜 iPad 低于 iOS 7 -->
<link rel="apple-touch-icon" href="icon76.png" sizes="76x76"> <!-- 非视网膜 iPad iOS 7 -->
<link rel="apple-touch-icon" href="icon114.png" sizes="114x114"> <!-- 视网膜 iPhone 低于 iOS 7 -->
<link rel="apple-touch-icon" href="icon120.png" sizes="120x120"> <!-- 视网膜 iPhone iOS 7 -->
<link rel="apple-touch-icon" href="icon144.png" sizes="144x144"> <!-- 视网膜 iPad 低于 iOS 7 -->
<link rel="apple-touch-icon" href="icon152.png" sizes="152x152"> <!-- 视网膜 iPad iOS 7 -->
```

rel属性可选配置：

- `apple-touch-icon` 图片自动处理成圆角和高光等效果。
- `apple-touch-icon-precomposed` 禁止系统自动添加效果，直接显示设计原图。

PS：貌似`apple-touch-icon-precomposed`这个配置在苹果的新产品中不推荐使用（不支持？）了，但是旧版iOS设备仍然支持。

这一设置叫[Web Clip]，参考资料：

> - [Apple开发者中心Web应用程序配置文档](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)
> - [Apple官方文档之icon和图像设置规范](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/MobileHIG/IconMatrix.html#//apple_ref/doc/uid/TP40006556-CH27-SW1)
> - [IOS Webapp的桌面图标及更新](http://himeters.com/update-ios-webapp-touch-icon)

- __iOS启动画面设置__

```html
<link rel="apple-touch-startup-image" href="/splash-screen-320x480.png" /> <!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
<link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png" /> <!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
<link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png" /> <!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
<link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png" /> <!-- iPad 竖屏 768 x 1004（标准分辨率） -->
<link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png" /> <!-- iPad 竖屏 1536x2008（Retina） -->
<link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png" /> <!-- iPad 横屏 1024x748（标准分辨率） -->
<link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png" /> <!-- iPad 横屏 2048x1496（Retina） -->
```

注意事项：

- iPhone 和 iPod touch 的启动画面包含状态栏区域。
- iPad 的启动画面不包括状态栏区域。

参考资料：

> - [Apple开发者中心关于iPhone和iPad Web App icon设置的文档](https://developer.apple.com/library/ios/qa/qa1686/_index.html)

除了用上面这种方式设置启动画面之外，还可以结合媒体查询进行判断，有条件的设置：

```html
<!-- iPhone -->
<link href="/images/apple-touch-startup-image-320x460.png" media="(device-width: 320px) and (device-height: 480px) and (-webkit-device-pixel-ratio: 1)"
 rel="apple-touch-startup-image" />
<!-- iPhone Retina -->
<link href="/images/apple-touch-startup-image-640x920.png" media="(device-width: 320px) and (device-height: 480px) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />
<!-- iPhone 5 -->
<link href="/images/apple-touch-startup-image-640x1096.png" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />
<!-- 以上没有判断横竖屏... -->

<!-- iPad -->
<link href="/images/apple-touch-startup-image-768x1004.png" media="(device-width: 768px) and (device-height: 1024px) and (orientation: portrait) and (-webkit-device-pixel-ratio: 1)" rel="apple-touch-startup-image" />
<link href="/images/apple-touch-startup-image-748x1024.png" media="(device-width: 768px) and (device-height: 1024px) and (orientation: landscape) and (-webkit-device-pixel-ratio: 1)" rel="apple-touch-startup-image">
<link href="/images/apple-touch-startup-image-768x1004.png" media="(device-width: 768px) and (device-height: 1024px) and (orientation: portrait) and (-webkit-device-pixel-ratio: 1)" rel="apple-touch-startup-image" />
<link href="/images/apple-touch-startup-image-748x1024.png" media="(device-width: 768px) and (device-height: 1024px) and (orientation: landscape) and (-webkit-device-pixel-ratio: 1)" rel="apple-touch-startup-image" />
```

- __其他设置__ 

```html
<meta name="msapplication-TileColor" content="#000"/> <!-- Windows 8 磁贴颜色 -->
<meta name="msapplication-TileImage" content="icon.png"/> <!-- Windows 8 磁贴图标 -->
<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml" /> <!-- 添加 RSS 订阅 -->
```

> 题外点，Android设备中也可以添加屏幕启动图标：
> 
> 1. 首先添加书签中
> 2. 长按已添加的书签选择添加到桌面
> 3. 通过桌面图标启动应用程序并选择使用哪种浏览器打开
> 参考 - [Chrome开发者中文关于Andorid设备添加屏幕启动的说明文档](https://developer.chrome.com/multidevice/android/installtohomescreen)

### 参考链接

- [常用HTML头部标签](https://github.com/yisibl/blog/issues/1)
- [iOS 7 的 Safari 和 HTML5：问题，变化和新 API](http://jinlong.github.io/blog/2013/09/23/safari-ios7-html5-problems-apis-review/)
- [W3C HTML5规范之文档元数据](http://www.w3.org/TR/html5/document-metadata.html)
- [你需要知道的HTML meta](http://blog.liming.it/?p=27) - 眼花缭乱，不要慌，并不是都得用上。收集在这里以备参考。
- [HTML meta标签列表 - @2010](http://code.lancepollard.com/complete-list-of-html-meta-tags/)
- [mobile-boilerplate](https://github.com/h5bp/mobile-boilerplate) - 前人载入，后人乘凉。但不要忘了浇水。
- [favicon-cheat-sheet](https://github.com/audreyr/favicon-cheat-sheet)
- [每个页面都应该有的18个meta标签](http://www.iacquire.com/blog/18-meta-tags-every-webpage-should-have-in-2013)
- [Everything you always wanted to know about touch icons](http://mathiasbynens.be/notes/touch-icons)
- [Home screen web apps for Android thanks to Chrome 31+](http://www.mobilexweb.com/blog/home-screen-web-apps-android-chrome-31) - PS：这个博客总结了大量的移动Web App开发的知识点，值得学习。

嗯，暂时就写这么多，后续发现了再更新吧。感谢大牛们的贡献，感谢网友们的总结整理。

> @TODO
>
> 1. Android, Windows Phone等移动设备上一些独有的Web app特性考究。
> 2. 各个知识点的补充说明。
