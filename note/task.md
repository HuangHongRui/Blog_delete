#任务12笔记
<pre>
- 什么是 CSS hack
- 谈一谈浏览器兼容的思路
- 列举5种以上浏览器兼容的写法
- 以下工具/名词是做什么的
条件注释
IE Hack
js 能力检测
html5shiv.js
respond.js
css reset
normalize.css
Modernizr
postCSS
一般在哪个网站查询属性兼容性？
</pre>

浏览器兼容问题。
属性、框架、不同的浏览器不兼容（bug）。
条件注释、单独的hark


版本越老问题越多，特别是IE。。

同产品 版本越老 bug越多
版本月高，功能越多。
不同产品不同标准，不同实现方式-。-


如果想处理，就是解决兼容的问题


区分；
标准
老的浏览器——范围抽象（像IE，包括IE8）

如果要设置兼容某些浏览之前，需要先查浏览器市场份额——
配合 use i can，
【browserhacks】

- 思路：

如果现在要做一份产品，想考虑的问题是我们这个网站否要要做浏览器兼容，
说白了，要兼容IE几？6~9？

1. 要不要做？
2. 老板的要求。。
3. 主动权和说服？（产品的角度。用户是谁。用啥浏览器，我们的碗网站是...）
如果是政府...那么就需要考虑都考虑到兼容都ie6，稳定性、功能使用实现比效果特效炫酷更重要，不用去考虑什么先进框架
	如果受众是集中在很年轻的范围内。电商、直播平台、网站等，那么网站效果，体验很重要，这时需要考虑兼容到IE几？如果IE6，那么效果就很难实现，或成本大。

产品角度、
成本角度


做到什么程度？

如何做？


假如一定要兼容IE6/7 那么就需要使用jquery（1点多的版本）

第二，根据兼容需求，选择兼容工具。。/库（实现目标，简化工作）



- 渐进增强|优雅降级。。

- 渐进增强的本质：
确保最基本功能（先及格，再做其他效果），再去适当或更好的加效果。。

优雅降级：先用适用性最好的功能等技术做好一个产品网站后，再去覆盖低端兼容

先确保标准范围内达到目的，对于低端的浏览器再去覆盖，覆盖越多越好，覆盖不了就算，不可能因为地段浏览器导致最好的技术和框架给丢掉。

- 行动

合适的框架。。。

Bootstrap（>=ie8）

jQuery 1.~（>= ie6）, jq 2.~(>=ie9)

vue(>=ie9)

开发之前必要考虑这些兼容性问题。。不然到时会从头来的




条件注释：
可被用来向IE提供及隐藏代码


条件注释在IE9还可以工作。在IE10中开始无法正常工作

- [! !IE] 非IE执行





css hack？

3种表示形式
- CSS属性前缀法
- 选择器前缀法
- IE条件注释法


css属性：
	记住bug使用（ie6 的_ ， IE6/7的 *  ,ie6——8 的\9）
	'_color:red'
	'*color:red'
	'color:yellow\9'

<!--[if IE 7]>
<link rel="stylesheet" href="ie7.css" type="text/css"/>
<![endif]-->
这段是在IE10下生效的，会进行一个判断。。IE10以上识别不了


常见属性的兼容情况：

inline-block >= ie8
min-width/min-height : >=ie8
:before,：after : >=ie8
div:hover: >=ie8
background-size: >=ie9
圆角 >= ie9
阴影 >=ie9
动画/渐变 >=ie10


- 常见兼容处理例子

<pre>`clearfix:after {
	content: '';
	display: block;
	clear: both;
}
.clearfix {
	*zoom: 1; /*只对ie6、7有效*/
｝
`</pre>


<pre>
`.target {
	display: inline-block;
	*display:inline;
	*zoom:1;
}`
</pre>


用这种方法会使代码乱七八糟。。


所以，更多会使用像<!--[if IE 7] -->这种..条件注释法.

常见的条件注释法
<pre>`
<!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
    <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
  <![endif]-->
`</pre>
<pre>`
<!DOCTYPE html>
<!--[if IEMobile 7 ]> <html dir="ltr" lang="en-US"class="no-js iem7"> <![endif]-->
<!--[if lt IE 7 ]> <html dir="ltr" lang="en-US" class="no-js ie6 oldie"> <![endif]-->
<!--[if IE 7 ]>    <html dir="ltr" lang="en-US" class="no-js ie7 oldie"> <![endif]-->
<!--[if IE 8 ]>    <html dir="ltr" lang="en-US" class="no-js ie8 oldie"> <![endif]-->
<!--[if (gte IE 9)|(gt IEMobile 7)|!(IEMobile)|!(IE)]><!--><html dir="ltr" lang="en-US" class="no-js"><!--<![endif]-->
`</pre>



