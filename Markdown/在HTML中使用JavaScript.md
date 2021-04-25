# 在HTML中使用JavaScript
## <script>元素
使用script元素，可以在html中添加JavaScript代码。它有下面几个属性:
- async : 可选。表示应该立即下载脚本，但不妨碍页面中的其他操作，比如下载其他资源或者等待加载其他脚本。只对外部文件有效
- charset ：可选。表示通过src属性指定的代码的字符集。
- defer ：可选。表示脚本延迟到文档完全被解析或显示之后在执行。只对外部脚本文件有效。
- language ：已经废弃
- src ：可选。表示包含要执行代码文外部文件
- type ：可选。可以看成是language的替代属性；表示编写代码使用的脚本语言的内容类型。最常用的text/javascript。再不指定这个值的情况下，默认也是text/javascript

**使用script元素的两种方式**：
- 直接在页面中嵌入JavaScript代码，例子代码如下:
```
<script type="text/javascript">
    function sayHello(){
        alert("Hello!");
    }
</script>
```
- 外部包含JavaScript文件（这种比较常用）, 例子代码如下:
```
<script type="text/script" src="example.js" />
```

script的src属性可以指向当前HTML页面所载域之外的某个域中的URL，例如:
```
<script type="text/javascript" scr="http://www.srivezs.com/afile.js"></script>
```

## 标签位置
按照惯例来说，所有script标签都应该放在页面的head元素中，比如:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>在HTMl中使用JavaScript</title>
    <script>
        function sayHello(){
            alert("hello");
        }
    </script>
</head>
<body>
test
</body>
</html>
```
这种做法的目的就是把所有的外部文件(包括CSS文件和JavaScript文件)的引用都放在相同的地方。这种做法会导致，必须等到全部JavaScript代码下载、解析和完成之后，才会开始呈现页面内容。对于需要很多JS代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间浏览器的窗口将是一片空白。为了避免这种问题，现代Web应用程序一般都把JS引用放在body元素中页面的内容后面。如下所示:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>在HTMl中使用JavaScript</title>
</head>
<body>
test
<!--JS引用--->
<script type="text/javascript" src="http://www.strivezs.com/alter.js"></script>
</body>
</html>
```

## 延迟脚本
defer属性用于表明脚本在执行时不会影响页面的构造。即：脚本会延迟到整个页面都解析完毕后在运行。设置了这个属性相当于告诉浏览器立即下载脚本，但是延迟执行。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>在HTMl中使用JavaScript</title>
    <script type="text/javascript" defer="defer" src="http://www.strivezs.com/alter.js"></script>
</head>
<body>
test
</body>
</html>
```
一般页面最好包含一个延迟脚本，因为延迟脚本的执行不一定按照顺序的。

## 异步脚本
async这个属性只适用于外部脚本，并告诉浏览器立即下载文件。但和defer不同的是，标记为async的脚本并不保证按照指定它们的先后顺序执行。
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>在HTMl中使用JavaScript</title>
    <script type="text/javascript" async src="http://www.strivezs.com/alter.js"></script>
    <script type="text/javascript" async src="http://www.strivezs.com/blter.js"></script>
</head>
<body>
test
</body>
</html>
```

第二个脚本可能在第一个脚本之前执行，因此要保证两个脚本互不依赖。异步脚本一定会在页面的load事件前执行。

## 在XHTML中的用法
之前的代码在XHTML中不能够很好的运行。如下面代码在XHTML中是无效的。
```
<script type="text/javascript">
    function sayHello(){
        if (a < b){
            alert("A");
        }
    }
</script>
```
因为'<'会被识别成新的一个标签。解决办法可以使用&lt来替代'<'。

另外最好的办法是:CDATA来解决
```
<script type="text/javascript">
// ![CDATA[
    function sayHello(){
        if (a < b){
            alert("A");
        }
    }
//]]
</script>
```

只需要添加[CDATA[]]就可以解决这个问题了。

## <noscript>元素
noscript标签用于下面两种情况:
- 浏览器不支持脚本
- 浏览器支持脚本但是被禁用了
只要符合上述任何一个条件，浏览器都会显示<noscript>中的内容。除此之外不会显示noscript的内容。  
简单例子：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>noscript</title>
</head>
<body>
<!--主要内容-->
test
<noscript>
    <p>本页面需要支持Script才能够显示。</p>
</noscript>
<!--js代码-->
<script type="text/javascript" async src="http://www.strivezs.com/blter.js"></script>
</body>
</html>
```
