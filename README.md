# browser-render
浏览器性能优化
### 为何把js放在body最下面：
    script阻塞浏览器的渲染。先渲染HTML页面，然后在执行script代码，性能优化问题。
    img并不会阻塞dom树的渲染。
### onload VS DOMContentLOaded  
onload：页面的全部资源加载完成才会执行，包括图片、视频等。  
DOMContentLoaded：渲染完成即可执行，此时图片、视频可能没有加载完。  
#### 1. 从输入url到得到HTML的详细过程：
    1. 浏览器根据DNS服务器得到域名的IP地址；  
    2. 向这个IP的及其发送http请求   
    3. 服务器收到、处理并返回http请求  
    4. 浏览器得到返回内容
#### 2.window.onload和DOMContentLoaded的区别
    onload：页面的全部资源加载完成才会执行，包括图片、视频等。
    DOMContentLoaded：渲染完成即可执行，此时图片、视频可能没有加载完。
#### 3.性能优化：
    原则:  
        多实用内存、缓存或者其他方发；   
        减少CPU操作，减少网络；
    入手：
        加载页面和静态资源   
        页面渲染  
    1)静态资源的压缩和合并  
    2）静态资源缓存(通过连接名称控制缓存，只有内容改变的时候，链接名称才会改变)   
    3）使用CDN让资源加载更快一些(CDN不同区域的网络优化 bootcdn)   
    4）使用SSR后端渲染，数据直接输出到HTML中(server side render服务端渲染 Vue React提出的概念) jsp、php、asp都属于后端渲染   
    渲染优化    
        1）CSS放前面，JS放后面    
        2）懒加载(图片懒加载，下拉加载更多)
```html
    <img id="img1" src="preview.png" data-realsrc="abc.png"/>>
```   
```javascript
    var img1 = document.getElementById('img1');
    img1.src = img1.getAttribute('data-realsrc');
```    
        3）减少DOM查询，对DOM查询做缓存   
```javascript
    //未缓存 DOM 查询
    var i; 
    for(i = 0; i < document.getElementsByTagName('p').length; i++) {  //做十次dom查询
        //todo
    }


    //缓存了 DOM 查询  
    var pList = document.getElementsByTagName('p');
    var i;
    for(i = 0; i < pList.length; i++) {  、、只做一次dom查询
        //todo
    }
```   
        4）减少DOM操作，多个操作尽量合并在一起执行   
```javascript
    var listNode = document.getElementById('list');

    //要插入10个li标签
    var frag = document.createDocumentFragment();
    var x, li;
    for(x = 0; x < 10; x++) {
        li = document.createElement('li');
        li.innerHTML = 'List item ' + x;
        frag.appendChild(li); 
    }

    listNode.appendChild(frag);
```   
        5）事件节流
```javascript
    var textarea = document.getElementById('text');
    var timeoutId;
    textarea.addEventListener('keyup', function() {
        if(timeoutId) {
            clearTimeout(timeoutId);
        }

        timeoutId = setTimeout(function() {
            //触发change事件
        }, 100)
    })
```    
        6）尽量执行操作(DOMContentLoaded)    
