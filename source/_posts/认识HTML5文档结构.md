在没有接触 HTML5 文档之前，相信很多人对 XHETML 文档结构比较熟悉，由于 XHTML 文档是 HTML 向 XML 规范过渡版本，其文档格式也基本按 XML 规范进行要求

1.  必须为文档定义命名空间，其值为http://www.w3.org/1999/xhtml
2.  MIME type 不能是 text/html,而是 text/xml、application/xml 或者 application/xml+html
3.  必须有根元素，根元素为<html>,即<html>的开始和结束标签不能省略
4.  所有元素只要有了开始标签，就不能有结束标签，或者自闭合
5.  所有元素都得严格遵守大小写，元素名称必须为小写

因此 XHTML 文档格式变得严格了许多，也因为 XML,其可读性和规范性提高了不少。但最终，我们要在 HTML 的宽容性和 xml 的规范性之间找到最佳的平衡点，一味追求极端始终是一个错误
但是当问到一个 HTML5 文档必须有哪些内容时，恐怕很少有人能正确的做出回答，为了帮助读者更好地对 HTML5 页面有一个简单的理解和认识，也为了读者能够顺利读懂 HTML5 网页代码的准确意思，下面给出了一个详细的、符合标准的 HTML5 文档结构代码，并进行详细注释

```html
<!DOCTYPE html>
<!--声明文档结构类型-->
<html lang=zh-cn>
<!--声明文档文字区域-->
<head>
 <!--文档头部区域-->
 <meta charset=utf-8>
 <!-- 文档的头部区域中元数据区的字符集定义，utf-8表示国际通用的字符集编码格式-->
 <!--[if IE]><![endif]-->
 <!--文档的头部区域兼容性写法-->
 <title>文档标题</title>
 <!--文档的头部区域的标题。title内容对于SEO来说及其重要-->
 <!--[if IE 9]><meta name=ie content=9><![endif]-->
 <!--文档的头部区域兼容性写法-->
 <!--[if IE 8]><meta name=ie content=8><![endif]-->
 <!--文档的头部区域兼容性写法-->
 <meta name=description content=文档描述信息>
 <!--文档的头部区域元素据区关于文档描述的定义-->
 <meta name=author content=文档作者>
 <!--文档头部区域元素据区关于开发人员姓名的定义-->
 <meta name=copyright content=版本信息>
 <!--文档头部区域元素据区关于版权的定义-->
 <link rel=shortcut icon herf=favicon.ico>
 <!--文档头部区域的兼容性写法-->
 <link rel=apple-touch-icon herf=custom_icon.png>
 <!--文档头部区域app设备的图标的引用-->
 <meta name=viewport content=width=device-width,user-scalable=no>
 <!--文档的头部区域对于不同接口设备的特殊声明。宽=设备款，用户不能自行缩放-->
 <link rel=stylesheet herf=main.css>
 <!--文档头部区域样式文件的引用-->
 <!--[if IE]><link rel=stylesheet herf=win-ie-all.css><![endif]-->
 <!--文档头部区域的兼容性样式文件引用写法-->
 <!--[if IE 7]><link rel=stylesheet type=text/css herf=win-ie7.css><![endif]-->
 <!--文档头部区域的IE7浏览器的兼容性写法-->
 <!--[if lt IE 8]><script src=http://ie7-js.googlecode.com/svn/version/2.0(beta3)/IE8.js></script><![endif]-->
 <!--文档头部区域的关于让IE8也兼容HTML5的JavaScript脚本-->
 <script src=script.js></script>
 <!--文档的头部区域JavaScript脚本文件调用-->
</head>
<body>
    <header>HTML5文档的头部区域</header>
    <nav>HTML5文档的导航区域</nav>
    <section>HTML5文档的主要内容区域
        <aside>HTML5文档的主要内容区域的侧边导航或菜单区</aside>
        <article>HTML5文档的主要内容区域的内容区
             <section>以下是一个section和article的嵌套
                <aside></aside>
                <article>
                    <header>
                    HTML5文档的嵌套区域，可以对某个article区域进行头部和脚部的定义，这样做，可以有非常清晰和严谨的文档目录结构关系
                    <footer>
                </article>
             </section>
        </article>
    </section>
    <footer>HTML5文档的脚部区域</footer>
</body>
</html>
```

当然，并不是每个 HTML5 文档都需要上面部分，一个最简单的 HTML5 文档需要的内容如下

```html
<!DOCTYPE html>
```

该句声明了文档类型，除了大小写可以任意变化外，其他内容都是不能变动的，那么究竟时怎样的规则，导致一个最简单的源码文件必须有 doctype 声明呢？根据标准，一个 HTML 文档由如下内容组成（严格按照顺序）：

1.  一个 BOM 标记，且这个 BOM 标记必须为 U+FEFF
2.  n 个空格或注释
3.  DOCTYPE 声明
4.  n 个空格或注释
5.  一个 HTML 元素
6.  n 个空格或注释

再回过来看一下文档组成，除了 0-n 个空格或注释这些没有多大意义的元素之外，组成的列表中还说明有一个 HTML 元素，但是最简单的源码却没有。这是因为在 HTML 的规范中，一直存在“隐式标签”这样的概念，关于隐式标签，大致可以这样解释：
一部分元素，当满足特定的前提条件时，其开始标签或结束标签可以在源码中省略，被省略的标签称为”隐式标签“
