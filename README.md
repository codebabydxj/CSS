# CSS
话说css 适配兼容

>一、浮动问题
简述：
我们在平时切页面时,经常会出现用完浮动(float),忘记删除.下面的布局出现莫名其妙的空白高度,导致布局调整失败

```
1.父级div定义height
    原理:父级div手动定义height,就解决了父级div无法自动获取到高度问题
    优点:简单,代码少,容易掌握
    缺点:只适合高度固定的不惧,要给出精确的高度,如果高度和父级div不一样
2.结尾处加空div标签clear:both
    原理：添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度
    
    优点：简单，代码少，浏览器支持好，不容易出现怪问题
    缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不爽
    
3.父级div定义伪类:after和zoom
    原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题
    优点：浏览器支持好，不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等）
    缺点：代码多，不少初学者不理解原理，要两句代码结合使用，才能让主流浏览器都支持
4.父级div定义overflow:hidden
    原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度
    
    优点：简单，代码少，浏览器支持好
    缺点：不能和position配合使用，因为超出的尺寸的会被隐藏(只推荐没有使用position或对overflow:hidden理解比较深的朋友使用)

5、5.父级div定义overflow:auto
    原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度
    
    优点：简单，代码少，浏览器支持好
    
    缺点：内部宽高超过父级div时，会出现滚动条。
    
6.父级div也一起浮动

    原理：所有代码一起浮动，就变成了一个整体
    
    优点：没有优点
    
    缺点：会产生新的浮动问题。
    
7.父级div定义display:table

    原理：将div属性变成表格
    
    优点：没有优点
    
    缺点：会产生新的未知问题
    
8.结尾处加br标签clear:both
    原理：父级div定义zoom:1来解决IE浮动问题，结尾处加br标签clear:both
```

>避免使用浮动

```
1.表格布局

2.使用display:inline-block
    IE6/7不支持display:inline-block属性，只是可以让标签有类似于inline-block的属性.使用text-align:justify;做测试的时候的一些样式表现证实了：确实IE6/7是不支持display:inline-block属性，只是让其表现的跟inline-block一样，对于inline水平的元素，其表现度可以用perfect一词来形容了

所以拿li举例 ul{display:inline-block;} li{display:inline;}

3.一点小阻挠：inline-block元素间的换行符空格间隙问题
    可在父级元素样式下写font-size:0; 子级元素各自给特定的font-size
    letter-spacing可以尝试给负值来解决.但是，Opera浏览器下极限是间隙1像素，0像素会反弹，换行符间隙还原
4.更进一步：更加灵活的inline-block列表布局

    使用text-align:justify可以实现自动等宽水平排列的列表布局，而且是两端对齐的，不需要计算宽度，一切都是浏览器自动的，很方便很强大。
                    
5、详细教程(http://www.zhangxinxu.com/wordpress/2010/11/拜拜了浮动布局-基于displayinline-block的列表布局/)
```

>二、居中

```
链接:http://blog.csdn.net/chenmoquan/article/details/41547609
1、水平居中—使用 text-align
2、margin: auto 居中
3、table-cell 居中
4、Absolute 居中
5、使用 translate 居中
6、使用 Flexbox 居中
7、使用 calc 居中
```

>三、常见的兼容性问题

```
  1、常见的问题:height设置100%没有高度,但是有宽度
  2、造成这个现象的原因是:浏览器解析规则引发的高度自适应问题

  兼容问题主要存在:
    IE和FireFox浏览器的常见问题margin,padding,box-sizing
    *{margin:0;padding:0;box-sizing:border-box;}
    IE的不兼容问题(比如一些标签video,audio等标签)
    <!--[if !IE]><!--> 除IE外都可识别 <!--<![endif]-->
    <!--[if IE]> 所有的IE可识别 <![endif]-->
    <!--[if IE 6]> 仅IE6可识别 <![endif]-->
    <!--[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-->
    <!--[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-->
    <!--[if IE 7]> 仅IE7可识别 <![endif]-->
    <!--[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-->
    <!--[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-->
    <!--[if IE 8]> 仅IE8可识别 <![endif]-->
    <!--[if IE 9]> 仅IE9可识别 <![endif]-->
```

>四、css hack

```
1、hack的利弊
    一般情况下，我们尽量避免使用CSShack，但是有些情况为了顾及用户体验实现向下兼容，不得已才使用hack。比如由于IE8及以下版本不支持CSS3,而我们的项目页面使用了大量CSS3新属性在IE9/Firefox/Chrome下正常渲染，这种情况下如果不使用css3pie或htc或条件注释等方法时,可能就得让IE8-的专属hack出马了。使用hack虽然对页面表现的一致性有好处，但过多的滥用会造成html文档混乱不堪，增加管理和维护的负担。相信只要大家一起努力，少用、慎用hack，未来一定会促使浏览器厂商的标准越来越趋于统一，顺利过渡到标准浏览器的主流时代。抛弃那些陈旧的IE hack，必将减轻我们编码的复杂度，少做无用功。
    
2、hack的方式     Hack主要针对IE浏览器
    CSS hack方式一：条件注释法
    CSS hack方式二：类内属性前缀法
    CSS hack方式三：选择器前缀法
```

>五、更换渲染模式

```
1、IE 兼容模式
    Bootstrap中不支持 IE 古老的兼容模式。为了让 IE 浏览器运行最新的渲染模式下，建议将此 <meta> 标签加入到你的页面中：
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
2、国产浏览器高速模式
    国内浏览器厂商一般都支持兼容模式（即 IE 内核）和高速模式（即 webkit 内核），不幸的是，所有国产浏览器都是默认使用兼容模式，这就造成由于低版本 IE （IE8 及以下）内核让基于 Bootstrap 构建的网站展现效果很糟糕的情况。幸运的是，国内浏览器厂商逐渐意识到了这一点，某些厂商已经开始有所作为了！

3、将下面的 <meta> 标签加入到页面中，可以让部分国产浏览器默认采用高速模式渲染页面：
        <meta name="renderer" content="webkit">
```

>六、浏览器内核

```
1、IE: trident内核
   Firefox：gecko内核
   Safari:webkit内核
   Opera:以前是presto内核，Opera现已改用Google Chrome的Blink内核
   Chrome:Blink(基于webkit，Google与Opera Software共同开发)

2、浏览器内核对于浏览器而言，是基础，是依托。如果没有了浏览器内核，那么浏览器是无法独立存在且产生作用的。其实浏览器内核学名叫做渲染引擎，起到的作用就是显示网页。它的存在，决定了网页的呈现的内容、格式以及效果。所以说，一个好的浏览器，一定是基于有一个稳定、高端、作用明显的浏览器内核的。
3、WebKit内核，它是目前应用范围最大的开源内核，新出的X5内核也同样是依托于WebKit的基础上，对其进行深度的开发和拓展才形成的。目前应用于各大主流浏览器，包括AppleSafari（苹果浏览器）Android自带浏览器、Symbian手机浏览器等。Firefox内核，同样也是开源内核，但是它的应用范围相对来说就要小不少了。同时还有IE内核，它的存在已经有了一定的历史，但是由于存在较严重的安全问题，渐渐被取代。
```

>七、让H5页面适应所有的iphone手机以及安卓机型的六大技巧

```
1、兼容iphone各版本机型最佳的方式就是自适应

2、viewport 简单粗暴的方式：
        <meta name="viewport" content="width=320,maximum-scale=1.3,user-scalable=no">
3、为什么是1.3？
    目前大部分页面都是以320px为基准的布局，而iphone6的宽度比是375/320 = 1.171875，iphone6+则是 414/320 = 1.29375那么以1.29倍也就约等于1.3了。
    为了让手机也能获得良好的网页浏览体验，Apple找到了一个办法：在移动版(iOS)的Safari中定义了viewport meta标签①，它的作用就是创建一个虚拟的窗口(viewport)，而且这个虚拟窗口的分辨率接近于桌面显示器，Apple将其定位为980px②。以一代iphone下的Safari来说就是：
        viewport全部属性&值如下：
        
        width: viewport宽度
        
        height: viewport高度
        
        initial-scale: 初始缩放比例
        
        maximum-scale: 最大缩放比例
        
        minimum-scale: 最小缩放比例
        
        user-scalable: 是否允许用户缩放例：width=960 或 device-width
        
        height=1000 或 device-height
        
        initial-scale=0.5
        
        maximum-scale=2
        
        minimum-scale=1
        
        user-scalable=1 或 0 (yes 或 no)layout viewport的默认值在Apple实现viewport后，其他浏览器也加入了对viewport meta的支持，但彼此间还是有些差异，差异最大的是layout viewport的表现：Safari iPhone: 980px
        Opera: 850px
        Android WebKit: 800px
        IE: 974px最后关注下width=device-width其实这个属性&值很有意思，字面意应该是viewport宽度等于设备宽度，但在实际中不同的浏览器都给出了个定值：320px；这个值还是源于 Apple，因为早期iphone的分辨率为320px × 480px，大量为iphone量身定制的网站都设置了viewport:width=device-width，并且按照宽度320px来设计制作，所 以其他浏览器加入viewport支持时为了兼容性也将device-width定义为了320px。注解① 除此之外不同移动浏览器厂商也有不同的解决方案，例如UCweb就是使用中间件技术
```

>八、REM 布局

```
1、REM布局
    REM是CSS3新增的一种单位，并且移动端的支持度很高，android2.x+，ios5+ 都支持。REM是相对于dom结构的根元素来设置大小，也就是html这个元素。相较于em单位，rem使用上更容易理解及运用。
    REM与PX的换算可以查看网址： https://offroadcode.com/prototypes/rem-calculator/
    假设，html我们设置font-size:12px; 也就是说12px相对于1rem，那么18px也就是 18/12 = 1.5rem。
    那么我们以320px的设计布局为基准，将html设置为font-size:100px，即100px = 1rem。(设置100px是为了方便计算)那么可以将大部分px单位除以100就可以直接改成rem单位了。
    
    REM如何做响应式布局？
    
2、如果仅仅是适配ip6+设备，那么使用media query就行
    伪代码如下：
        /*320px布局*/
        
        html{font-size: 100px;}
        body{font-size: 0.14rem /*实际相当于14px*/}

        /* iphone 6 */
        
        @media (min-device-width : 375px) and (max-device-width : 667px) and (-webkit-min-device-pixel-ratio : 2){
            html{font-size: 117.1875px;}
        }
        
        /* iphone6 plus */
        
        @media (min-device-width : 414px) and (max-device-width : 736px) and (-webkit-min-device-pixel-ratio : 3){
            html{font-size: 129.375px;}
        }
3、如果是完全自适应，那么可以通过JS来控制

    (function (doc, win) {
    
        var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',

        /*recalc重新计算*/
        recalc = function () {
        
             var clientWidth = docEl.clientWidth;
             if (!clientWidth) return;
            docEl.style.fontSize = 100 * (clientWidth / 320) + 'px';
         };

        // Abort if browser does not support addEventListener
        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false); //false由里向外
        doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);

4、图片自适应
    REM布局，那么用百分比布局也能实现一样的效果，但是用百分比布局，必须要面临一个问题：图片宽度100%，页面加载时会存在高度塌陷的问题
    那么可以用padding-top设置百分比值来实现自适应。
    公式如下：
        padding-top = (Image Height / Image Width) * 100%
    原理：padding-top值为百分比时，取值是是相对于宽度的。
    .cover{position: relative; padding-top: 100%; height: 0; overflow: hidden;}
    .cover img{position: absolute; top: 0; width: 100%;}
5、图片高清化
    设备像素比问题
    <img src="small.jpg" srcset="small.jpg 640w 1x, small-hd.jpg 640w 2x, large.jpg 1x, large-hd.jpg 2x"> 
    不过目前前端这边图片的实现基本都用lazyload的方式实现。srcset的图片加载方式在实际项目中运用还比较少。
6、背景图高清化
    media query 实现高清化
    img标签的高清化，可以通过JS判断devicePixelRatio的值来加载不同尺寸的图片，但是对于背景图，写在CSS中的，用JS来判断就略麻烦了，还好CSS通过media query也能判断dpr。
    目前兼容性最好的背景图高清化实现方式，使用media query的 -webkit-min-device-pixel-ratio 做判断：(代码见下页)

7、/* 普通显示屏(设备像素比例小于等于1)使用1倍的图 */
  .css{
      background-image: url(img_1x.png);
  }

  /* 高清显示屏(设备像素比例大于等于2)使用2倍图  */
  @media only screen and (-webkit-min-device-pixel-ratio:2){
      .css{
    background-image: url(img_2x.png);
      }
  }

 /* 高清显示屏(设备像素比例大于等于3)使用3倍图  */
  @media only screen and (-webkit-min-device-pixel-ratio:3){
      .css{
    background-image: url(img_3x.png);
      }
  }
详细的各种机型和对应的-webkit-min-device-pixel-ratio 值

8、image-set 实现高清化
image-set，它是Webkit的私有属性，也是Css4的一个属性，它是为了解决Retina屏幕下的图像显示而生。
使用方式也很简单。伪代码如下：
    .css {
      background-image: url(1x.png);    /*不支持image-set的情况下显示*/
      background: -webkit-image-set(
            url(1x.png) 1x,/* 支持image-set的浏览器的[普通屏幕]下 */
            url(2x.png) 2x,/* 支持image-set的浏览器的[2倍Retina屏幕] */
            url(3x.png) 3x/* 支持image-set的浏览器的[3倍Retina屏幕] */
            );
     }
目前移动端的支持程度来看，ios7+，android 4.4+ 下已经支持了。如果仅仅是做ip6+的高清适配方案。 image-set 也是一种实现方案。

使用image-set 与 media query 实现有什么区别及好处？
image-set不需要告诉浏览器使用什么图像，而是直接提供了图像让浏览器选择。这就意味着，如果在低网速下，浏览器可以选择加载低分辨率的图片。（PS：好智能的样子）
但是相比如media query的实现，image-set仅支持单个图片的高清化，不适合在css sprite下使用。 并且兼容性也是一大硬伤。
一般来说，用在LOGO区域，单个图片图标的区域下，也是个不错的选择。


9、关于图片列表适配
    也就是要让布局更灵活，在电商网站里面，商品列表是一个非常常见的结构。一种比较智能的列表方式是：两端对齐，间距自适应。(圣杯布局)
    那么可以使用FLEXBOX布局来实现两端对齐的效果，也可以使用 text-align:justify 的方式实现。
    具体实现办法：http://www.ghugo.com/inline-block-justify/
    
css4新增选择器:  http://css4-selectors.com/selectors/
```
