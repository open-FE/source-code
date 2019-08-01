# 判断会否是XML节点

```
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>isXML</title>  
</head>  
<body>  
    <script>  
        //Sizzle, jQuery自带的选择器引擎  
        var isXML = function(elem) {  
            var documentElement = elem && (elem.ownerDocument || elem).documentElement;  
            return documentElement ? documentElement.nodeName !== "HTML" : false;  
        };  
        console.log(isXML(document.getElementById("test")));  

        //但这样不严谨，因为XML的根节点，也可能是HTML标签，比如这样创建一个XML文档  
        try {  
            var doc = document.implementation.createDocument(null, 'HTML', null);  
            console.log(doc.documentElement);  
            console.log(isXML(doc));  
        } catch (e) {  
            console.log("不支持creatDocument方法");  
        }  
    </script>  
</body>  
</html>
```
```
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>isXML</title>  
</head>  
<body>  
    <script>  
        //我们看看mootools的slick选择器引擎的源码：  
        var isXML = function(document) {  
            return (!!document.xmlVersion) || (!!document.xml) || (toString.call(document) == '[object XMLDocument]')  
                    || (document.nodeType == 9 && document.documentElement.nodeName != 'HTML');  
        };  

        //精简版  
        var isXML = window.HTMLDocument ? function(doc) {  
            return !(doc instanceof HTMLDocument);  
        } : function(doc) {  
            return "selectNodes" in doc;  
        }  
    </script>  
</body>  
</html>
```
