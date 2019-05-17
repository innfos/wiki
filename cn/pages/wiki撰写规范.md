# wiki撰写规范

- mdwiki是用于链接INNFOS官网，面向客户的一个平台。为完善INNFOS官网的Wiki信息，请相关同事各自负责各自的部分，在严格审查及时更正产品资料信息的同时，做到格式的统一。

## 格式要求
### 标题
- 每个大标题间加一条线，例如：# wiki撰写规范  ----；
- 英文版本中所有标题开头字母要大写，例如：## Introduction；
- 文本的内外标题要统一；
- 文本的一级标题要加序号（注：只适用于篇幅较大的文本）；

### 表格
- 所有表格的第一行表格颜色为蓝色；
- 在同一标题内容下，整体表格宽度要统一。（表格中的小表格宽度视文字多少来定。注：一般以文字不换行后的宽度为合适宽度）；

### 说明和注释
编辑wiki时要充分利用markdown的样式。例如：
Note: 在同一标题内容下，表格宽度统一。

### 图片要求
- 图片上传时，请查看图片的大小，若图片过大请将图片压缩后上传；
- 在编写图片代码时要统一格式。代码格式如下：

<img src="../img/026.png" style="width:600px">

Note: 所有页面中的图片格式以本代码为准，特殊情况下除外。如产品系列中的图片格式；带图号的图号要将图号居中对齐，代码格式如下：

<p><div class="md-text" style="text-align: center;"><strong>图3-1</strong></div></p >

### 图片要求
- 在文字中如果有关键词出现，请将关键词标红。例如：` 0x00`；
- 16进制数标为红色字样；在单独写16进制数时，务必以0x开头，且x为小写字母，x后所加的内容统一为两位字符；0x后如果为字母符号，请将字母统一大写。例如：` 0xFF`；
- 专有名词要大写；当专有名词为公司制定且第一次出现时，要将其添加备注及解释。例如：ECB（Ethernet CAN Bridge）

### 版本变更记录
在制作版本变更记录表格时，要有版本号、更新时间、更改类型、位置及更新内容，并以此为规范运用于每个文档中。其中版本号命名格式为VX.X.X, 例如：V1.0.0。 更新时间格式为20XX.XX.XX, 例如：2019.05.17。（型号数据因为涉及的修改很多，可以在稳定之后，小的修改采用以上格式）


This is an H2
-------------


### 锚点与链接 Links

[普通链接](http://localhost/)

[普通链接带标题](http://localhost/ "普通链接带标题")

直接链接：<https://github.com>

[锚点链接][anchor-id] 





#### 行内代码 Inline code

执行命令：`npm install marked`





#### JS代码　

```javascript
function test(){
	console.log("Hello world!");
}
 
(function(){
    var box = function(){
        return box.fn.init();
    };

    box.prototype = box.fn = {
        init : function(){
            console.log('box.init()');

			return this;
        },

		add : function(str){
			alert("add", str);

			return this;
		},

		remove : function(str){
			alert("remove", str);

			return this;
		}
    };
    
    box.fn.init.prototype = box.fn;
    
    window.box =box;
})();

var testBox = box();
testBox.add("jQuery").remove("jQuery");
```
