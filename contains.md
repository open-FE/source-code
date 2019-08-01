# 节点关系不仅仅指元素节点的关系，document文档节点也包含在内。在最新的浏览器中，所有的节点都已经装备了contains()方法

```
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <title>contains</title>  
</head>  
<body>  
    <div id="p-node">  
        <div id="c-node">子节点内容</div>  
    </div>  
    <script>  
        //兼容的contains方法  
        function fixContains(a, b) {  
            try {  
                while ((b = b.parentNode)){  
                    if (b === a){  
                        return true;  
                    }  
                }  
                return false;  
            } catch (e) {  
                return false;  
            }  
        }  
        var pNode = document.getElementById("p-node");  
        var cNode = document.getElementById("c-node").childNodes[0];  
        alert(fixContains(pNode, cNode));        //true  
        alert(fixContains(document, cNode));     //true  
    </script>  
</body>  
</html>

```
