# 1、HTML

## 1.1 简介

Hyper Text Markup Language，超文本标记语言；主要通过标记对网页中的文本、图片、按钮等内容进行描述。标记由标签和属性组成。

- 标签

~~~html
标签是对页面空间布局的一种标记；分为自闭合标签和成对标签

<br/> 自闭合标签
<h1></h1> 成对标签
~~~

- 属性

~~~
是对标签功能的一个定义和补充；属性是不占页面空间的
~~~

## 1.2 基本标签

~~~html
<!DOCTYPE html> 协议头，这是5的协议头，标记了html的版本
<!--注释-->
<html></html>网页的根标签，所有其他的标签都被包含在根标签中
<head></head> 头部标签，包含了网页的一些信息
<meta charset='utf-8'>设置字符集  
<meta name='keywords' content='关键词等'>
<meta name='description' content='描述信息'> 搜索引擎优化，让爬虫能搜索到的关键词和描述信息
<title> 展示页面的名称
<body>主体标签，所有在网页中显示的其他的内容和标签都被其包含
<hn>标题标签
<p>段落标签
<br>换行标签
~~~

~~~html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
	</body>
</html>
~~~

## 1.1 标签的类型和关系

- 类型

双标签：有开始，有闭合

单标签：又叫自闭合标签

- 关系

嵌套关系：包含关系，是祖先和后代之间的关系

并列关系：同级关系，是兄弟之间的关系

## 1.3 常用标签

~~~html
1、图片标签 用于展示图片
<img src='position'>图片标签，其中的属性定位了资源的位置 

属性：
- src：文件的位置
- width：图片的宽度，单独设置会同比例缩小；同时设置长度图片会发生畸变
- border：设置边框
- title：提示文本
- alt：替换文本；当图片不存在时，进行提示

2、a标签 用于跳转超链接
<a href="" target=""></a> 超链接标签

属性：
- href：跳转到的网页路径
- target：对跳转
		 _self 默认值，从对那个钱选项卡直接跳转到目标页
		 _blank 重新打开一个选项卡跳转到目标页
~~~

## 1.4 路径关系

即当前文件和其他文件的位置关系，路径是忽略大小写的

- 相对路径

~~~
同级相对路径：当前页面与目标文件在同一目录下；填写 文件名，或者填写 ./文件名
下一级相对路径：当前页面在目标文件的上一级，即目标文件的父文件夹与当前页面同级；填写 /文件夹/文件名
上一级相对路径：当前页面在目标文件的下一级，即目标文件与当前页面的父文件夹同级；填写 ../文件名
>> ../ 的作用就是跳出当前级别的文件夹一级，类似于鼠标单击返回的动作
~~~

- 绝对路径

~~~
绝对路径就是文件在磁盘中的物理位置；但是出于安全的考虑，浏览器不能直接通过盘符的绝对路径访问磁盘中的文件，但是可以通过网络路径对绝对路径中的文件进行访问
~~~

## 1.5 页面背景

~~~html
背景图的尺寸与标签的尺寸无关
<body bgcolor=''></body>等标签都可根据属性设置
1、背景色
	bgcolor属性对页面设置背景色
2、背景图
	backgroud属性对页面设置背景图
~~~

# 2、页面锚点

## 2.1 跳转到顶部

~~~html
<a href='#'></a>

空连接：当没有想好跳转到哪个网页时，可以设置成空连接，空连接会返回顶部
~~~

## 2.2 锚点连接

~~~html
<a href='#one'></a>

锚点连接：在网页内部进行跳转，需要给目标连接设置id属性，通过锚点连接跳转到id标签的位置
~~~

# 3、列表

## 3.1 无序列表

~~~html
无序列表：是被一组ul标签管理的li列表项；无序列表没有先后顺序
ul标签只能包含li；li可以包含其他标签

<ul>
    <li>无序列表1</li>
    <li>无序列表2</li>
    <li>无序列表3</li>
    <li>无需列表4</li>
</ul>
~~~

## 3.2 有序列表

~~~html
有序列表：是被一组ol标签管理的li列表项；有序列表会自动添加先后顺序
ol标签只能包含li；li可以包含其他标签

<ol>
	<li>无序列表1</li>
    <li>无序列表2</li>
    <li>无序列表3</li>
    <li>无需列表4</li>
</ol>
~~~

## 3.3 自定义列表

~~~html
自定义列表：是被一组dl标签管理的列表项；dt是列表标题，dd是列表子项
dl标签只能包含dt和dd标签，dt和dd标签可以包含其他标签

<dl>
	<dt>亚洲</dt>
    <dd>中国</dd>
    <dd>日本</dd>
</dl>
~~~

# 4、表格标签和属性

## 4.1 表格标签

~~~html
表格标签：由table标签包含的 caption表格标题 th表头标签 tr行标签 td单元格标签；td是以当前列中最宽的为基准

<table>
    <caption>表格标题</caption>
    <tr>
    	<th>姓名</th>
        <th>年龄</th>
        <th>性别</th>
        <th>爱好</th>
    </tr>
    <tr>
    	<td>小明</td>
        <td>18</td>
        <td>男</td>
        <td>英语</td>
    </tr>
</table>
~~~

 ## 4.2 属性

~~~html
以下属性都是在table标签中设置的，会影响表格全局；给单独单元格表填设置只会影响单独单元格>>

border:设置边框
width:宽度
height:高度
cellspacing:单元格之间的间距
align:文本对齐方式，left 左对齐（默认）、center 居中、right 右对齐
~~~

## 4.3 跨行、列操作

~~~html
 通过属性对行和列进行跨列操作

colspan="": 跨列，引号中输入跨列的列数
rowspan='': 跨行，引号中输入跨行的行数
~~~

# 5、表单

## 5.1 标签和属性

~~~html
表单标签
<form></form>:表单，将所有被提交的标签包含其中，提交出去
属性：
action 提交地址
method 表单的提交方式：get（通过url提交） post（通过请求报文提交）

<label></label>:标题
属性：
for='id' > 关联输入框表单中的id值

<input></input>:表单框
属性：
id='' 给标签起唯一标识名，用于被关联
type='' > text:输入框 password:密码（会被隐藏） radio:单选框 checkbox:复选框 button:按钮（普通按钮） submit:提交（提交按钮） reset:重置（清空表单）
name='' 给单选框或多选框进行分组
checked='checked' checked='' checked 默认选中，三种属性方式效果一样


<select>：下拉菜单，可以替代input单选框的功能
    <optgroup>：下拉组
        属性：
        label 下拉组标题
        <option></option>：下拉选项
        属性：
		selected 默认选项，三种写法和checked一致
    </optgroup>
</select>

<textarea></textarea>：文本域，多行文本

<button></button> 按钮
属性：
type button:普通按钮 submit:提交按钮（默认） reset:重置按钮
~~~

# 6、常用标签2

~~~html
左侧和右侧的标签都具备显示效果，左侧常用于图标；右侧的标签除了具备显示效果外，更强调语义，爬虫会根据语义标签来获取文本信息
<b></b><strong></strong> 加粗
<i></i><em></em> 倾斜
<u></u><ins></ins> 下划线
<s></s><del></del> 删除线
~~~

# 7、特殊字符

[HTML特殊字符符号大全 – WEB骇客 (webhek.com)](https://www.webhek.com/post/html-enerty-code.html)

~~~html
&acute;	©	&copy;	>	&gt;	µ	&micro;	®	&reg;
&	&amp;	°	&deg;	¡	&iexcl;		&nbsp;	»	&raquo;
¦	&brvbar;	÷	&divide;	¿	&iquest;	¬	&not;	§	&sect;
•	&bull;	½	&frac12;	«	&laquo;	¶	&para;	¨	&uml;
¸	&cedil;	¼	&frac14;	<	&lt;	±	&plusmn;	×	&times;
¢	&cent;	¾	&frac34;	¯	&macr;	“	&quot;	™	&trade;
€	&euro;	£	&pound;	¥	&yen;				
„	&bdquo;	…	&hellip;	·	&middot;	›	&rsaquo;	ª	&ordf;
ˆ	&circ;	“	&ldquo;	—	&mdash;	’	&rsquo;	º	&ordm;
†	&dagger;	‹	&lsaquo;	–	&ndash;	‚	&sbquo;	”	&rdquo;
‡	&Dagger;	‘	&lsquo;	‰	&permil;		&shy;	˜	&tilde;
≈	&asymp;	⁄	&frasl;	←	&larr;	∂	&part;	♠	&spades;
∩	&cap;	≥	&ge;	≤	&le;	″	&Prime;	∑	&sum;
♣	&clubs;	↔	&harr;	◊	&loz;	′	&prime;	↑	&uarr;
↓	&darr;	♥	&hearts;	−	&minus;	∏	&prod;	‍	&zwj;
♦	&diams;	∞	&infin;	≠	&ne;	√	&radic;	‌	&zwnj;
≡	&equiv;	∫	&int;	‾	&oline;	→	&rarr;		
α	&alpha;	η	&eta;	μ	&mu;	π	&pi;	θ	&theta;
β	&beta;	γ	&gamma;	ν	&nu;	ψ	&psi;	υ	&upsilon;
χ	&chi;	ι	&iota;	ω	&omega;	ρ	&rho;	ξ	&xi;
δ	&delta;	κ	&kappa;	ο	&omicron;	σ	&sigma;	ζ	&zeta;
ε	&epsilon;	λ	&lambda;	φ	&phi;	τ	&tau;		
Α	&Alpha;	Η	&Eta;	Μ	&Mu;	Π	&Pi;	Θ	&Theta;
Β	&Beta;	Γ	&Gamma;	Ν	&Nu;	Ψ	&Psi;	Υ	&Upsilon;
Χ	&Chi;	Ι	&Iota;	Ω	&Omega;	Ρ	&Rho;	Ξ	&Xi;
Δ	&Delta;	Κ	&Kappa;	Ο	&Omicron;	Σ	&Sigma;	Ζ	&Zeta;
Ε	&Epsilon;	Λ	&Lambda;	Φ	&Phi;	Τ	&Tau;	ς	&sigmaf;
~~~

# 8、H5

## 8.1简介

html5是建立在html4的基础之上，新增了一些有定义的标签，一些标签属性，新增了一些api、应用程序接口，本地存储，地理位置，绘制图形，视频和音频等；H5新增的这些功能，只能用在高级浏览器上。

## 8.2 新增语义标签

~~~html
<header>头部标签</header>
<nav>导航标签</nav>
<section>主体
	<aside>侧边栏</aside>
  <artical>文章标签</artical>
</section>
<footer>底部标签</footer>
~~~

## 8.3 新增属性

~~~
1、禁用属性
	disabled="disabled"；三种写法和checked一样
2、非空验证
	required="required"
3、自动获取焦点
	autofocus="autofocus"
4、提示文本
	placeholder="提示文本"
5、自动补全
	autocomplete="on"；开启 autocomplete="off"；默认值（关闭）配合name属性使用，根据name属性值，将成功提交的文本存储到下拉列表
~~~

## 8.4 新增表单属性

~~~html
1、邮箱类型
	<input type="email"></input>
2、网址类型
	<input type="url"></input>
3、本地时间类型
	<input type="datetime-local"></input>
4、月类型
	<input type="month"></input>
5、日类型
	<input type="date"></input>
6、周类型
	<input type="week"></input>
7、颜色类型
	<input type="color"></input>
8、滑块类型
	<input type="range"></input>
~~~

8.5 音视频标签

- 音频标签

~~~html
<audio src="music/xxx.mp3" controls="controls"></audio> controls:控制面板
	loop="loop":循环播放
	autoplay="autoplay":自动播放
<audio>
	<source>用于引入多文件
</audio>
~~~

- 视频标签

~~~html
<video></video> 使用和属性和音频标签类似

~~~

