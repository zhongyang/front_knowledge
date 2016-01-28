# 手机屏幕适配那些事 


**所有的信息均参考自网络，已添加了相关的链接。如有侵权，请联系我删除**

**基础概念**

 - `DPI与PPI`

    DPI（Dots Per Inch）是印刷行业中用来度量空间点密度用的，这个值是打印机每英寸可以喷的墨汁点数。计算机显示设备从打印机中借鉴了DPI的概念，由于计算机显示设备中的原子单位不是墨汁点而是像素，所以就创造了PPI（Pixels Per Inch），这个值是屏幕每英寸的像素数量，即像素密度（Screen density）。由于各种原因，目前PPI(主要是iOS)和DPI(比如在Android中)都会用在计算机显示设备的参数描述中，不过二者的意思是一样的，都是代表像素密度
比如72dpi时，即表明每英寸内有72个像素。在屏幕显示时像素和屏幕上的点可以是点对点或非点对点

	> PPI = √（长度像素数² + 宽度像素数²） / 屏幕对角线英寸数

  举个简单的栗子，iphone5的ppi是多少？ppi=√（1136px² + 640px²）/4 in=326ppi（视网膜Retina屏）.这样大家就能够明白ppi和px的关系。
    
   高PPI屏幕显示的元素会比较精细（看起来会比较小），低PPI屏幕显示的元素相对来说就比粗糙（看起来会比较大），我们通过一幅图来看看在不同PPI下元素显示的区别：
![enter image description here](http://s0-weizhifeng-net.b0.upaiyun.com/images/dpi/blue-square-01.png)
 - `Retina`
 
 Retina display即视网膜屏幕，是苹果发布iPhone 4时候提出的，之所以叫做视网膜屏幕，是因为屏幕的PPI太高，人的视网膜无法分辨出屏幕上的像素点。iPhone 4/S的PPI为326，是iPhone 3G/S的两倍，如下图
 ![enter image description here](http://s0-weizhifeng-net.b0.upaiyun.com/images/dpi/retina-01.png)
 由于屏幕在宽和高的像素数量提高了整整一倍，所以之前非Retina屏幕上的一个像素渲染的内容在Retina屏幕上会用4个像素去渲染：1x1px(non Retina) = 2x2px(Retina)，这样元素的内容就会变得精细，比如：
 ![enter image description here](http://s0-weizhifeng-net.b0.upaiyun.com/images/dpi/retina-02.png)
 - `DP/PT/SP`
 
 随着移动设备屏幕PPI的不断提高，对于开发者来说以前用物理像素(Physical Pixel)来度量显示元素的方法已经不奏效了。为了解决这个问题，两大平台都提出了抽象像素的概念：iOS叫做PT（Point，显示点），Android中叫做DP/DiP（Device independent Pixel，设备无关像素）

 - `iPhone设备分辨率`

	![enter image description here](https://lh3.googleusercontent.com/-cYRQwy0Ba2A/VqnJm0o4QKI/AAAAAAAAADY/rbHWw9n3gGA/s0/%25E5%25B1%258F%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2016-01-28+%25E4%25B8%258B%25E5%258D%25883.54.47.png "屏幕快照 2016-01-28 下午3.54.47.png")

	![enter image description here](http://ww3.sinaimg.cn/mw690/51530583gw1ek7mqv36zxj20go099jrm.jpg)
![enter image description here](http://img.blog.csdn.net/20141226185359140)

 - `Android - 更为繁多的界面尺寸`

	Android开源自由的代价就是设备规范的不可控，市面上充斥着各种品牌的android手机，有着各种各样的尺寸和分辨率，为了适配各种不同分辨率的设备，同一个图标需要切成N份，每一份对应一个尺寸。
   
   Android里面开发用的尺寸单位是dp或sp（dp为元素表现尺寸，sp为字体尺寸）而不是iphone中的px。。。
	
	对于分辨率繁多的android设备，为了方便原生应用的界面适配，Google按照dpi大小将它们分成了4中模式（MDPI、HDPI、XHDPI和XXHDPI，也许有一天会增加第五种XXXHDPI，谁知道呢）：
	
	![enter image description here](http://ossweb-img.qq.com/upload/webplat/info/tgideas/201411/1415967636_1436653066_11532_imageAddr.jpg)
	
	一般情况下，手机分辨率与所运行的dpi模式是匹配的，例如hvga(320x480像素)的手机屏幕一般在3.5英寸左右，运行在mdpi模式下。当运行在mdpi下时，1dp=1px：也就是说设计师以320x480作为设计稿的尺寸时，在PS里定义一个item高48px，开发就会定义该item高48dp；Photoshop中14px大的字体，开发会定义为14sp。
	
**具体问题**

 - `原生App切图(使用工具，千万不要人工切图，不然会血喷屏幕)`
	 
	 http://www.cutandslice.me/
	 
	 http://www.cutterman.cn/v2/icview
	 
	 http://devrocket.uiparade.com/
	 
   http://macrabbit.com/slicy/
   

 - `Web App如何适配--rem` 

	rem（font size of the root element）是指相对于根元素的字体大小的单位。简单的说它就是一个相对单位。看到rem大家一定会想起em单位，em（font size of the element）是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过一个计算的规则是依赖根元素一个是依赖父元素计算。
	

	基于rem的原理，我们要做的就是: 针对不同手机屏幕尺寸和dpr动态的改变根节点html的font-size大小(基准值)。
	> rem = document.documentElement.clientWidth * dpr / 10

	具体如何写代码，请查阅参考链接和Google.
	
   rem兼容性
   
   ![enter image description here](http://img03.taobaocdn.com/tps/i3/T1VhurXvNXXXb9uvne-700-270.png) 
   

**参考**

http://jinjuan.me/appdesign-sizesetting/
	
http://www.woshipm.com/pd/43600.html
	
http://div.io/topic/1092
	
http://isux.tencent.com/web-app-rem.html
	
https://www.zhihu.com/question/21504656
	
http://ued.taobao.org/blog/2013/05/rem-font-size/
	
