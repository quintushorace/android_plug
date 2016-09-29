
<body>
<section class="content">
<ul class="items">
	<li style="background: #FFFFFF"><article class="wrap">
	<h1><a href="#" title="title">Android博客周刊专题之＃插件化开发＃</a></h1>
	<div class="content">本期专栏目讨论插件化开发。插件化涉及的东西很多，所以我们需要多个维度去学习。大概分为5个部分：预备知识、入门、进阶、系列、类库。一步一步深入了解插件的原理。本专栏会不定时更新相关内容，请留意更新的消息。请加入QQ群：149581646.会统一通知最新的文章。</div>
	<footer> Posted <time datetime="time">2016-03-16</time> by
	Jomeslu. </footer> </article></li>
</ul>

<article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>基础</b>
</div>
<h2 style="margin-left: 15px"><a href="https://www.ibm.com/developerworks/cn/java/j-lo-classloader/" target="_blank">1.Java 类加载器</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
类加载器（class loader）是 Java™中的一个很重要的概念。类加载器负责加载 Java 类的字节代码到 Java 虚拟机中。本文首先详细介绍了 Java 类加载器的基本概念，包括代理模式、加载类的具体过程和线程上下文类加载器等，接着介绍如何开发自己的类加载器，最后介绍了类加载器在 Web 容器和 OSGi™中的应用。</div><h2 style="margin-left: 15px"><a href="https://github.com/JustinSDK/JavaSE6Tutorial/blob/master/docs/CH16.md" target="_blank">2.反射原理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Java 提供的反射機制允許您於執行時期動態載入類別、檢視類別資訊、生成物件或操作生成的物件，要舉反射機制的一個應用實例，就是在整合式開發環境中所提供的方法提示或是類別檢視工具，另外像 JSP 中的 JavaBean 自動收集請求資訊也使用到反射，而一些軟體開發框架（Framework）也常見到反射機制的使用，以達到動態載入使用者自訂類別的目的。</div><h2 style="margin-left: 15px"><a href="http://www.jianshu.com/p/6f6bb2f0ece9" target="_blank">3.代理模式及Java实现动态代理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
定义：给某个对象提供一个代理对象，并由代理对象控制对于原对象的访问，即客户不直接操控原对象，而是通过代理对象间接地操控原对象。</div> </article><article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>入门</b>
</div>
<h2 style="margin-left: 15px"><a href="http://blog.csdn.net/u013478336/article/details/50734108" target="_blank">1.Android动态加载dex技术初探</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
  Android使用Dalvik虚拟机加载可执行程序，所以不能直接加载基于class的jar，而是需要将class转化为dex字节码，从而执行代码。优化后的字节码文件可以存在一个*.jar中，只要其内部存放的是*.dex即可使用。</div><h2 style="margin-left: 15px"><a href="http://104.236.134.90/2016/02/02/Android%E6%8F%92%E4%BB%B6%E5%8C%96%E5%9F%BA%E7%A1%80/" target="_blank">2.Android插件化入门</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
开发者将插件代码封装成Jar或者APK。宿主下载或者从本地加载Jar或者APK到宿主中。将宿主调用插件中的算法或者Android特定的Class（如Activity）</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/u010687392/article/details/47121729?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io" target="_blank">3.插件化开发—动态加载技术加载已安装和未安装的apk</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
动态加载技术就是使用类加载器加载相应的apk、dex、jar（必须含有dex文件），再通过反射获得该apk、dex、jar内部的资源（class、图片、color等等）进而供宿主app使用。</div><h2 style="margin-left: 15px"><a href="https://blog.tingyun.com/web/article/detail/166" target="_blank">4.Android动态加载技术三个关键问题详解</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
动态加载技术（也叫插件化技术）在技术驱动型的公司中扮演着相当重要的角色，当项目越来越庞大的时候，需要通过插件化来减轻应用的内存和CPU占用，还可以实现热插拔，即在不发布新版本的情况下更新某些模块。</div> </article><article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>进阶</b>
</div>
<h2 style="margin-left: 15px"><a href="http://mp.weixin.qq.com/s?__biz=MzAwMTcwNTE0NA==&mid=400217391&idx=1&sn=86181541ce0164156dfab135ed99bb5c&scene=0&key=b410d3164f5f798e61a5d4afb759fa38371c8b119384c6163a30c28163b4d4d5f59399f2400800ec842f1d0e0ffb84af&ascene=0&uin=MjExMjQ&pass_ticket=Nt5Jaa28jjFxcQO9o%2BvQiXX%2B0iXG5DlZlHNW97Fk1Ew%3D" target="_blank">1.携程Android App插件化和动态加载实践</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
携程Android App的插件化和动态加载框架已上线半年，经历了初期的探索和持续的打磨优化，新框架和工程配置经受住了生产实践的考验。本文将详细介绍Android平台插件式开发和动态加载技术的原理和实现细节，回顾携程Android App的架构演化过程，期望我们的经验能帮助到更多的Android工程师。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/hkxxx/article/details/42194387" target="_blank">2.动态加载APK原理分享</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
 被加载的apk称之为插件，因为机制类似于生物学的"寄生"，加载了插件的应用也被称为宿主。
往往不是所有的apk都可作为插件被加载，往往需要遵循一定的"开发规范"，还需要插件项目引入某种api类库，业界通常都是这么做的。</div><h2 style="margin-left: 15px"><a href="http://www.cnblogs.com/coding-way/p/4669591.html" target="_blank">3.Android插件化的一种实现</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Android的插件化已经是老生常谈的话题了，插件化的好处有很多：解除代码耦合，插件支持热插拔，静默升级，从根本上解决65K属性和方法的bug等等。下面给大家介绍一下我们正在用的差价化框架。本片主要以类图的方式向大家介绍插件话框架的实现。</div><h2 style="margin-left: 15px"><a href="http://mogu.io/117-117" target="_blank">4.蘑菇街 App 的组件化之路</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
随着我街业务的蓬勃发展，产品和运营随时上新功能新活动的需求越来越强烈，经常可以听到“有个功能我想周x上，行不行”。行么？当然是不行啦，上新功能得发新版本啊，到时候费时费力打乱开发节奏不说，覆盖率也是个问题。</div><h2 style="margin-left: 15px"><a href="http://www.codekk.com/open-source-project-analysis/detail/Android/FFish/DynamicLoadApk%20%E6%BA%90%E7%A0%81%E8%A7%A3%E6%9E%90?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io" target="_blank">5.DynamicLoadApk 源码解析</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
DynamicLoadApk 是一个开源的 Android 插件化框架。插件化的优点包括：(1) 模块解耦，(2) 动态升级，(3) 高效并行开发(编译速度更快) (4) 按需加载，内存占用更低等等DynamicLoadApk 提供了 3 种开发方式，让开发者在无需理解其工作原理的情况下快速的集成插件化功能。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/singwhatiwanna/article/details/22597587" target="_blank">6.Android apk动态加载机制的研究</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
问题是这样的：我们知道，apk必须安装才能运行，如果不安装要是也能运行该多好啊，事实上，这不是完全不可能的，尽管它比较难实现。在理论层面上，我们可以通过一个宿主程序来运行一些未安装的apk，当然，实践层面上也能实现，不过这对未安装的apk有要求。我们的想法是这样的，首先要明白apk未安装是不能被直接调起来.</div><h2 style="margin-left: 15px"><a href="http://tech.meituan.com/mt-android-auto-split-dex.html" target="_blank">7.美团Android DEX自动拆包及动态加载简介</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
作为一个android开发者，在开发应用时，随着业务规模发展到一定程度，不断地加入新功能、添加新的类库，代码在急剧的膨胀，相应的apk包的大小也急剧增加， 那么终有一天，你会不幸遇到这个错误.
</div><h2 style="margin-left: 15px"><a href="http://mp.weixin.qq.com/s?__biz=MzAwOTE0ODEwMQ==&mid=401731625&idx=1&sn=9bf2bacfbba43ba9dc7b2e854b64e66c&scene=23&srcid=1231ni0s2Y0OMfYSoNhkkJ47#rd&ADUIN=289832127&ADSESSION=1451551778&ADTAG=CLIENT.QQ.5425_.0&ADPUBNO=26509" target="_blank">8.途牛原创|途牛Android App的插件实现</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
途牛的插件化是基于dynamic-load-apk（github）实现的。定义了宿主和插件的通信方式，使得两者能够互起对方的页面，调用彼此的功能。同时对activity的启动方式singletask等进行了模式实现，并增加了对Service的支持等。总之使得插件开发最大限度的保持着原有的Android开发习惯。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/singwhatiwanna/article/details/23387079" target="_blank">9. Android apk资源加载和activity生命周期管理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
博主分析了Android中apk的动态加载机制，并在文章的最后指出需要解决的两个复杂问题：资源的访问和activity生命周期的管理，而本文将会分析这两个复杂问题的解决方法。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/singwhatiwanna/article/details/39937639" target="_blank">10.APK动态加载框架（DL）解析</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
首先要说的是动态加载技术（或者说插件化）在技术驱动型的公司中扮演这相当重要的角色，当项目越来越庞大的时候，需要通过插件化来减轻应用的内存和cpu占用，还可以实现热插拔，即在不发布新版本的情况下更新某些模块。
</div> </article><article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>系列</b>
</div>
<h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004062866" target="_blank">1.Kaedea---Android动态加载技术 简单易懂的介绍</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
我们很早开始就在Android项目中采用了动态加载技术，主要目的是为了达到让用户不用重新安装APK就能升级应用的功能（特别是 SDK项目），这样一来不但可以大大提高应用新版本的覆盖率，也减少了服务器对旧版本接口兼容的压力，同时如果也可以快速修复一些线上的BUG。</div><h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004062880" target="_blank">2.Kaedea---Android动态加载基础 ClassLoader的工作机制</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
早期使用过Eclipse等Java编写的软件的同学可能比较熟悉，Eclipse可以加载许多第三方的插件（或者叫扩展），这就是动态加载。这些插件大多是一些Jar包，而使用插件其实就是动态加载Jar包里的Class进行工作。</div><h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004062899" target="_blank">3.Kaedea---Android动态加载补充 加载SD卡的SO库</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Android中JNI的使用其实就包含了动态加载，APP运行时动态加载.so库并通过JNI调用其封装好的方法。后者一般是使用NDK工具从C/C++代码编译而成，运行在Native层，效率会比执行在虚拟机的Java代码高很多，所以Android中经常通过动态加载.so库来完成一些对性能比较有需求的工作（比如T9搜索、或者Bitmap的解码、图片高斯模糊处理等）。</div><h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004062952" target="_blank">4.Kaedea---Android动态加载入门 简单加载模式</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Java程序中，JVM虚拟机是通过类加载器ClassLoader加载.jar文件里面的类的。Android也类似，不过Android用的是Dalvik/ART虚拟机，不是JVM，也不能直接加载.jar文件，而是加载dex文件。</div><h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004062972" target="_blank">5.Kaedea---Android动态加载进阶 代理Activity模式</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
简单模式中，使用ClassLoader加载外部的Dex或Apk文件，可以加载一些本地APP不存在的类，从而执行一些新的代码逻辑。但是使用这种方法却不能直接启动插件里的Activity。</div><h2 style="margin-left: 15px"><a href="https://segmentfault.com/a/1190000004077469" target="_blank">6.Kaedea---Android动态加载黑科技 动态创建Activity模式</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
还记得我们在代理Activity模式里谈到启动插件APK里的Activity的两个难题吗，由于插件里的Activity没在主项目的Manifest里面注册，所以无法经历系统Framework层级的一系列初始化过程，最终导致获得的Activity实例并没有生命周期和无法使用res资源。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/jiangwei0910410003/article/details/17679823" target="_blank">7.尼古拉斯---插件开发基础篇：动态加载技术解读</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
在目前的软硬件环境下，Native App与Web App在用户体验上有着明显的优势，但在实际项目中有些会因为业务的频繁变更而频繁的升级客户端，造成较差的用户体验，而这也恰恰是Web App的优势。本文对网上Android动态加载jar的资料进行梳理和实践在这里与大家一起分享，试图改善频繁升级这一弊病。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/jiangwei0910410003/article/details/41384667" target="_blank">8.尼古拉斯---插件开发开篇：类加载器分析</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
这篇文章主要介绍了Android中主要的两个类加载器：PathClassLoader和DexClassLoader,他们的区别，联系，用法等问题，以及我们在制作插件的过程中会遇到哪些常见的问题。这篇文章也是后续两篇文章的基础，因为如果不了解这两个类的话，我们将无法进行后续的操作。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/jiangwei0910410003/article/details/47679843" target="_blank">9.尼古拉斯---插件开发中篇：资源加载问题(换肤原理解析)</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
这篇文章主要通过现在一些应用自带的换肤技术的解读来看看，在开发插件的过程中如何解决一些资源加载上的问题，这个问题为何要单独拿出来解释，就是因为他涉及的知识很多，也是后面一篇文章的基础，我们在需要加载插件中的资源文件的时候。</div><h2 style="margin-left: 15px"><a href="http://blog.csdn.net/jiangwei0910410003/article/details/48104455" target="_blank">10.尼古拉斯---插件开发终极篇：动态加载Activity(免安装运行程序)</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
这篇文章主要是讲解了如何加载插件中的Activity。从而实现免安装运行程序，同时这篇文章也是对前三篇文章知识的综合使用。下载很多应用都会使用到插件技术，因为包的大小和一些功能的优先级来决定哪些模块可以制作成插件。</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/01/28/understand-plugin-framework-overview/" target="_blank">11.Weishu---Android插件化原理解析——概要</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
类的加载可以使用Java的ClassLoader机制，但是对于Android来说，并不是说类加载进来就可以用了，很多组件都是有“生命”的；因此对于这些有血有肉的类，必须给它们注入活力，也就是所谓的组件生命周期管理.</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/01/28/understand-plugin-framework-proxy-hook/" target="_blank">12.Weishu---Android插件化原理解析——Hook机制之动态代理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
使用代理机制进行API Hook进而达到方法增强是框架的常用手段，比如J2EE框架Spring通过动态代理优雅地实现了AOP编程，极大地提升了Web开发效率；同样，插件框架也广泛使用了代理机制来增强系统API从而达到插件化的目的.</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/02/16/understand-plugin-framework-binder-hook/" target="_blank">13.Weishu---Android插件化原理解析——Hook机制之Binder Hook</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Android系统通过Binder机制给应用程序提供了一系列的系统服务，诸如ActivityManagerService，ClipboardManager， AudioManager等；这些广泛存在系统服务给应用程序提供了诸如任务管理，音频，视频等异常强大的功能。</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/03/07/understand-plugin-framework-ams-pms-hook/" target="_blank">14.Weishu---Android 插件化原理解析——Hook机制之AMS&PMS</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
在前面的文章中我们介绍了DroidPlugin的Hook机制，也就是代理方式和Binder Hook；插件框架通过AOP实现了插件使用和开发的透明性。在讲述DroidPlugin如何实现四大组件的插件化之前，有必要说明一下它对AMS以及PMS的Hook方式。</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/03/21/understand-plugin-framework-activity-management/" target="_blank">15.Weishu---Android 插件化原理解析——Activity生命周期管理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
之前的 Android插件化原理解析 系列文章揭开了Hook机制的神秘面纱，现在我们手握倚天屠龙，那么如何通过这种技术完成插件化方案呢？具体来说，插件中的Activity，Service等组件如何在Android系统上运行起来？
</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/04/05/understand-plugin-framework-classloader/" target="_blank">16.Weishu---Android 插件化原理解析——插件加载机制</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
上文 Activity生命周期管理 中我们地完成了『启动没有在AndroidManifest.xml中显式声明的Activity』的任务；通过Hook AMS和拦截ActivityThread中H类对于组件调度我们成功地绕过了AndroidMAnifest.xml的限制。
</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/04/12/understand-plugin-framework-receiver/" target="_blank">17.Weishu---Android插件化原理解析——广播的管理</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
在Activity生命周期管理 以及 插件加载机制 中我们详细讲述了插件化过程中对于Activity组件的处理方式，为了实现Activity的插件化我们付出了相当多的努力；那么Android系统的其他组件，比如BroadcastReceiver，Service还有ContentProvider，它们又该如何处理呢？</div><h2 style="margin-left: 15px"><a href="http://weishu.me/2016/05/11/understand-plugin-framework-service/" target="_blank">18.Weishu---Android 插件化原理解析——Service的插件化</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
在 Activity生命周期管理 以及 广播的管理 中我们详细探讨了Android系统中的Activity、BroadcastReceiver组件的工作原理以及它们的插件化方案，相信读者已经对Android Framework和插件化技术有了一定的了解；</div> </article><article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>类库</b>
</div>
<h2 style="margin-left: 15px"><a href="https://github.com/Qihoo360/DroidPlugin" target="_blank">1.DroidPlugin</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
是360手机助手在Android系统上实现了一种新的插件机制</div><h2 style="margin-left: 15px"><a href="https://github.com/limpoxe/Android-Plugin-Framework" target="_blank">2.Android-Plugin-Framework</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
此项目是Android插件开发框架完整源码及示例。用来通过动态加载的方式在宿主程序中运行插件APK。</div><h2 style="margin-left: 15px"><a href="https://github.com/wequick/Small" target="_blank">3.Small</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
世界那么大，组件那么小。Small，做最轻巧的跨平台插件化框架。里面有很详细的文档</div><h2 style="margin-left: 15px"><a href="https://github.com/singwhatiwanna/dynamic-load-apk" target="_blank">4.dynamic-load-apk</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Android 使用动态加载框架DL进行插件化开发</div><h2 style="margin-left: 15px"><a href=" https://github.com/mmin18/AndroidDynamicLoader" target="_blank">5.AndroidDynamicLoader</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Android 动态加载框架，他不是用代理 Activity 的方式实现而是用 Fragment 以及 Schema 的方式实现</div><h2 style="margin-left: 15px"><a href="https://github.com/CtripMobile/DynamicAPK" target="_blank">6.DynamicAPK</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
实现Android App多apk插件化和动态加载，支持资源分包和热修复.携程App的插件化和动态加载框架.</div><h2 style="margin-left: 15px"><a href="https://github.com/bunnyblue/ACDD/blob/master/README-Zh.md" target="_blank">7.ACDD</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
非代理Android动态部署框架</div><h2 style="margin-left: 15px"><a href="https://github.com/houkx/android-pluginmgr" target="_blank">8.android-pluginmgr</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
不需要插件规范的apk动态加载框架。</div> </article><article class="wrap"
	style=" margin-top:40px ">

<div style="font-size: 30px; font: '宋体'; margin-bottom: 20px"><b>参考视频</b>
</div>
<h2 style="margin-left: 15px"><a href="http://www.infoq.com/cn/presentations/the-realization-principle-and-application-of-droidplugin" target="_blank">1.DroidPlugin的实现原理及其应用</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
Droid Plugin是360手机助手在2015年初研发的一个全新的基于Android平台的插件机制.</div><h2 style="margin-left: 15px"><a href="http://v.youku.com/v_show/id_XNTMzMjYzMzM2.html" target="_blank">2.android插件化及动态部署</a>
</h2>

<div style="margin-top: 15px; margin-left: 25px; margin-bottom: 20px">
 阿里技术沙龙第十六期《android插件化及动态部署》视频</div> </article> </section>


