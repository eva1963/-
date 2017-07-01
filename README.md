##前端问题总结


在平时的项目上我们总会遇到这样那样的问题，有时候为了赶项目我们不得不采取采取一些简单的但未必是最好的解决方案，所以我在空闲的时候就像把这些当时做出来的不是最优解决方案的一些问题重新梳理一下，然后找到最优解决方案，参照一些大网站的作法使得自己的网站更扎实，更稳定！

---

###1.多个大小相同的li自动循环

我们先来看一下图中：

![Mou icon](img/01.jpg)

旧解决方案：

ul + li  都按百分比，然后一行四个的话，每个li宽度都是25%，然后统一设置padding-right的值，再用css3的:nth-child(4n)将每个4n个li的padding值设置为0，之前一直这样做，但是一直都知道这样是不对的，你们也许发现了，如果最后一个padding值为0的话那么宽度自然就会比其他有padding值的li要宽，所以这个不是最优解决方案！

新方案：

最近浏览GitHub官网发现人家有一个页面也是这个排版，但是几个盒子大小都是出奇的一致，所以我就看了下，有兴趣了也可以自己浏览[点击这里](https://github.com/explore)，这个解决方案就是把父级元素的margin值设置为父，然后里面的盒子该怎么设置还怎么设置，这样自己元素就不会因为外间距的问题折行了，比如子元素的margin-right都为15px,那么就把ul的margin-right设置为-15px，这样就好了，原理暂时不清楚，待探究~

补充：这个其实有很多方案的，像是直接盒子布局不要布局padding而是换成margin可能也可以解决这个问题！


###2.左侧小三角的css实现

这个其实主要讲的是drop-shadow和普通box-shadow的差别，drop-shadow其实才算是真正意义上的投影，而box-shadow可能用阴影来描述更为合适；(但是目前drop-shadow兼容性并不是很好，慎用)
![Mou icon](img/shadow.jpg)


###3.字体上下间隙的解决方法
我们都知道当定义了字体大小之后，字体上下总会有些间隙不能去除，用line-height=100%可能可以解决你的这一大烦恼；

![Mou icon](img/font-1.jpg)
![Mou icon](img/font-2.jpg)

###4.CSS 截断字符串
单行截断字符串,这里必须指定字符串的宽度


	/* 指定字符串的宽度 */
    
    width:300px;   
    
    overflow: hidden;  
    
    /* 当字符串超过规定长度，显示省略符*/ 
    
    text-overflow:ellipsis;  
    
    white-space: nowrap;  

###5.去掉 a，input 在移动端浏览器中的默认样式

####5.1.禁止 a 标签背景
在移动端使用 a标签做按钮的时候，点按会出现一个“暗色”的背景，去掉该背景的方法如下

a,button,input,optgroup,select,textarea {
    -webkit-tap-highlight-color:rgba(0,0,0,0); /*去掉a、input和button点击时的蓝色外边框和灰色半透明背景*/
}

####5.2.禁止长按 a，img 标签长按出现菜单栏
使用 a标签的时候，移动端长按会出现一个 菜单栏，这个时候禁止呼出菜单栏的方法如下：

a, img {
    -webkit-touch-callout: none; /*禁止长按链接与图片弹出菜单*/
}

####5.3.流畅滚动

body{
    -webkit-overflow-scrolling:touch;
}


###<font color="#f3e3076">6.去掉selected默认的样式</font>

刚才看到张鑫旭大大的博客才知道，appearance还有很多属性，但是可能目前支持兼容性不是很好，有一个***menulist***我觉得在处理select的时候可能用的上，**另外这个属性并不是专属于select的，而是所有input输入框都拥有这个属性！**

	appearance:none;
	-moz-appearance:none;
	-webkit-appearance:none;
	
===
	
IE10浏览器下，**::-ms-expand**可以改变下拉框元素的下拉按钮样式。

	::-ms-expand {
    	padding: .5em;
    	color: #34538b;
    	border: 1px solid #a0b3d6;
    	background: #f0f3f9;
	}


	
	
###7.IE9下的兼容代码


	<!--[if lt IE 9]>
	<script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
	<script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
	<![endif]-->
	
###<font color="#f3e3076">8.display: table-cell;与大小不一定的元素的垂直居中</font>

	/*这里的大小是根据高宽上限128像素图片设置的*/
	div {
		display:table-cell;  /* 重点1 */
		width:1em; 
		height:1em; 
		border:1px solid #beceeb; 
		font-size:144px;
		text-align:center;  /* 重点2 */
		vertical-align:middle; /* 重点3 */
	} 
	div img{
		vertical-align:middle; /* 重点4 */
	}
	
	
	
###9.让英文同汉字一样自动换行
因为很多时候我们没有注意到同样的盒子内部有时候输入汉字他能够自己折行，按照盒子大小自动换行，但是英文却不行，这个很常见，但是为了是自己有个记性，特写在此！	

	word-break: break-all;


###10.让图片或者文字垂直居中的方法（vertical-align）

	html:
	<p style="height:200px"><img src=""><i></i></p>
	
	css:
	img { vertical-align: middle;}
	
	i {
	display: inline-block;  	/* inline-block化 */
	width: 0;					/* 0宽度100%高度的辅助元素 */
	height: 100%;
	vertical-align: middle;
	}
	
	
	
	
###<font color="#f3e3076">11.给input的placeholder文字设置色值</font>

IE浏览器下的写法：

	:-ms-input-placeholder {
    	color: mediumvioletred;
    	text-indent: 5px;
	}
	
Chrome浏览器：

	::-webkit-input-placeholder {
    	color: mediumvioletred;
    	text-indent: 5px;
	}
	
FireFox浏览器：FireFox浏览器下占位符文字的透明度默认是0.54，因此需要强制opacity: 1让placeholder值颜色与IE/Chrome一致。
	
	::-moz-placeholder {
    	color: mediumvioletred;
    	text-indent: 5px; /* 不起作用 */
    	opacity: 1!important;
	}


###12.伪元素::-ms-value
可以更改文本框(如type=text, type=password等)以及下拉框(select)的样式。例如下面的HTML代码：

	::-ms-value {
    	padding: 4px;
    	color: #34538b;
    	border: 1px solid #a0b3d6;
    	background-color: #f0f3f9;
	}
	
###13.<font color='#f3e3076'>display: inline-block 引起的间隙问题</font>
现在我们布局列表的时候很少用到float浮动了，因为浮动会让盒子的高度塌陷，随之会出现很多令人头痛的问题，现在我们大概都使用display： inline-block比较多，但是这个又会因为换行导致元素块与块之间会产生一定的间隙

1.处理这个间隙我们一般的方法是用<font color='#f3e3076'>**font-size：0；**</font>

2.但是有时会因为就兼容性失效，那就在介绍一个别的方法，就是<font color='#f3e3076'>**letter-spacing： -4px；**</font>这个兼容性较之稍微好一点；

###14.不同尺寸的icon小图标自动居中最佳方案

这些小的问题解决方案都是摘自张鑫旭大大<http://www.zhangxinxu.com>的博客，有兴趣的同学可以自己到他的网站中查看，说不定自己也没能收货很多意想不到的东西哦~

这里只是展示主要代码，详细案例在HTML网页中有实例：

	.icon {
		display: inline-block;
		width: 20px;	
		height: 20px;
		background: url("image/icon.png") no-repeat center;
		white-space: nowrap;
		letter-spacing: -1em;
		text-indent: -99em;
		color: transparent;
		}
	<!-- 这个很重要，是决定icon居中的核心 -->
	.icon:before {	content: '\3000';	}		
  
###14. 利用flex布局，使内容部分高度为100%
最近面试问到一个问题，想到就记下来吧！
实现一个页面，header =30px,footer = 30px,中间的container部分高度100%，用flex布局如何实现？

实现方法：
1.	首先要保证html,和body的高度是100%
2.	父元素.wrapper的高度设置为100%，如下：
	height: 100%;
 	display: flex;
  	flex-direction: column;

3. 子元素header，footer的高度，如：
	height: 30px;

4. 子元素container的属性设置为 flex: 2;
即可实现


###15.怎么让Chrome支持小于12px 的文字？
	1、用图片：如果是内容固定不变情况下，使用将小于12px文字内容切出做图片，这样不影响兼容也不影响美观。
	2、使用12px及12px以上字体大小：为了兼容各大主流浏览器，建议设计美工图时候设置大于或等于12px的字体大小，如果是接单的这个时候就需要给客户讲解小于12px浏览器不兼容等事宜。
	3、继续使用小于12px字体大小样式设置：如果不考虑chrome可以不用考虑兼容，同时在设置小于12px对象设置-webkit-text-size-adjust:none，做到最大兼容考虑。
	4、使用12px以上字体：为了兼容、为了代码更简单 从新考虑权重下兼容性。

###16.让页面里的字体变清晰，变细用CSS怎么做？
	-webkit-font-smoothing: antialiased;

###17.经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧 ？

* png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.
* 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。
* IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。
    浮动ie产生的双倍距离 #box{ float:left; width:10px; margin:0 0 0 100px;}

    这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

    渐进识别的方式，从总体中逐渐排除局部。

    首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。
    接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
    css
            .bb{
                background-color:red;/*所有识别*/
             background-color:#00deff\9; /*IE6、7、8识别*/
             +background-color:#a200ff;/*IE6、7识别*/
             _background-color:#1e0bd1;/*IE6识别*/
            }

  *  IE下,可以使用获取常规属性的方法来获取自定义属性,
	 也可以使用getAttribute()获取自定义属性;
	 Firefox下,只能使用getAttribute()获取自定义属性。
	 解决方法:统一通过getAttribute()获取自定义属性。

  *  IE下,even对象有x,y属性,但是没有pageX,pageY属性;
	 Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。

  *  解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

  *  Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
	 可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
  	L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}
	
###18、关于空格符\&ensp;和\&emsp;

其中的\&ensp;和\&emsp;由于具有某一超赞的特性，使其可以登上web届的舞台！什么特性呢？如上表加粗展示
       1. 透明； 
       2. 宽度正好跟中文正好是1:2和1:1的关系
于是，一些中文排版对齐什么的，直接就可以使用这两个空格调节，如：
![Mou icon](img/8.jpg)
 
结果轻松实现了2字/3字/4字中文的等宽两端对齐效果了
![Mou icon](img/22.png)	

###16、解决position的fixed属性在搜狗浏览器中的兼容问题
![Mou icon](img/clipboard.png)

###17.js的优化法则：
1.内存的手动释放，减少内存的占用；
2.减少DOM的回流机制，因为浏览器的重新渲染非常耗性能


