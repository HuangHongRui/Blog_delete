# Work-13

> 记录..

---

## 垂直居中

margin-left: -? | margin-top: -? 可等于： transform: translate(-?%, ?%); 来代替.

vertical-align: arg? | 使函数文本垂直+参数

display: table-cell 实现居中 。作用于表格和行内元素。



:before | :after 目的为了省标签.

:after 用途之一(抽象化)..
```
.clearfix:after {
	content: "";
	display: block;
	clear: both;
	*zoom: 1; <!-- 兼容IE -->
}
```

应用-替代标签...

```
.tooltip:before{
  content: "";
  display: inline-block;
  /* border:1px solid #fff; */
  background: #fff;
  position: absolute;
  width:10px;
  height:10px;
  margin-top: -15px;
  transform:rotateZ(45deg);
}
<!-- 抽象化之前↓ -->
/* .caret {
  border:1px solid white;
  background: #fff;
  display: inline-block;
  position: absolute;
  width:10px;
  height:10px;
  margin-top: -16px;
  transform:rotateZ(45deg);
} */
```


普通居中
```
.ct{
  padding: 40px 0;
  text-align: center;
  background: #eee;
}
```


绝对定位实现的居中
```
html,body {
  height: 100%;
}


.dialog {
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -200px;
  margin-top: -150px;
  
  width: 400px;
  height: 300px;
  box-shadow: 0px 0px 3px #000;
}

.dialog .header{
  padding: 10px;
  background: #000;
  color: #fff;
}
.dialog .content{
  padding: 10px;
}
```


vertical-align 实现的居中
```
.box{
  width: 300px;
  height: 200px;
  border: 1px solid ;
  text-align: center;
}

.box:before{
  content: '';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
.box img{
  vertical-align: middle;
  background: blue;
}
```



table-cell 实现居中
```
.box{
  width: 300px;
  height: 200px;
  border: 1px solid ;
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}

```



