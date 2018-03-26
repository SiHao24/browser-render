# browser-render
浏览器性能优化
### 为何把js放在body最下面：
    script阻塞浏览器的渲染。先渲染HTML页面，然后在执行script代码，性能优化问题。
    img并不会阻塞dom树的渲染。
onload VS DOMContentLOaded  
onload：页面的全部资源加载完成才会执行，包括图片、视频等。
DOMContentLoaded：渲染完成即可执行，此时图片、视频可能没有加载完。
1.从输入url到得到HTML的详细过程：
    1）浏览器根据DNS服务器得到域名的IP地址；
    2）向这个IP的及其发送http请求
    3）服务器收到、处理并返回http请求
    4）浏览器得到返回内容
2.window.onload和DOMContentLoaded的区别
    onload：页面的全部资源加载完成才会执行，包括图片、视频等。
    DOMContentLoaded：渲染完成即可执行，此时图片、视频可能没有加载完。
3.性能优化：
    原则：
        多实用内存、缓存或者其他方发；
        减少CPU操作，减少网络；
    入手：
        加载页面和静态资源
        页面渲染
    1）静态资源的压缩和合并
    2）静态资源缓存
    3）使用CDN让资源加载更快一些(CDN不同区域的网络优化)
    4）使用SSR后端渲染，数据直接输出到HTML中(server side render服务端渲染)
    渲染优化
        1）CSS放前面，JS放后面
        2）懒加载(图片懒加载，下拉加载更多)
        3）减少DOM查询，对DOM查询做缓存
        4）减少DOM操作，多个操作尽量合并在一起执行
        5）事件节流
        6）尽量执行操作(DOMContentLoaded)
