# 判断元素是否是元素节点

```
<!DOCTYPE html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>isElement</title>  
</head>  
<body>  
    <div id="test">aaa</div>  
    <!--这是一个注释节点-->  
    <script>  
        var testDiv = document.createElement('div');  
        var isElement = function (obj) {  
            if (obj && obj.nodeType === 1) {//先过滤最简单的  
                if( window.Node && (obj instanceof Node )){ 
                //如果是IE9,则判定其是否Node的实例  
                    return true; //由于obj可能是来自另一个文档对象，因此不能轻易返回false  
                }  
                try {//最后以这种效率非常差但肯定可行的方案进行判定  
                    testDiv.appendChild(obj);  
                    testDiv.removeChild(obj);  
                } catch (e) {  
                    return false;  
                }  
                return true;  
            }  
            return false;  
        }  
        var a = {  
           nodeType: 1  
        }  
        console.log(isElement(document.getElementById("test")));  
        //结果：  true  
        console.log(isElement(document.getElementById("test").nextSibling));  
        //结果：  false  
        console.log(isElement(a));  
        //结果：  false  
    </script>  
</body>  
</html>
```
