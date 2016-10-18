javascript notepad
================

#常用函数，整理，



1、用js改变embed标签的src值
------------------------
**参考链接**
http://www.cnblogs.com/jingangel/archive/2012/07/23/2604741.html
```
var tabv = document.getElementById("f_tabv");
var tabva = tabv.getElementsByTagName("a");
var tabcv = document.getElementById("f_tab_cv");
tabcv.innerHTML = '<EMBED src="abc.wmv" autostart="true" width="545" height="325" type="video/x-ms-asf"></EMBED>';
for(var i=0; i<tabva.length; i++){
  tabva[i].onclick=function(){
      var href1 = this.getAttribute("href");
        var href2 = '<EMBED src="'+href1+'" autostart="true" width="545" height="325" type="video/x-ms-asf"></EMBED>';
        tabcv.getElementsByTagName("embed")[0].style.display="none";
        tabcv.innerHTML="";
        tabcv.innerHTML=href2;
        for(i=0; i<tabva.length; i++){
          tabva[i].className='';
        }
        this.className = "act";
        return false;
    }
}
```

2、动态更改视频
---------------
>**JQuery**方法，
>- 在战舰猎手官网上用应用
>- 兼容ie

```
(function setSrc(obj){ 
  var play = $(".play");
  var playLen = $(".play").length;
  var videoPar = $(".video_pop")
  var videoParHTML = null;
  //$(videoParHTML).appendTo(videoPar);    
  
  for (var i=0;i<playLen;i++) {
    //var _index = i;
    //console.log(_index)
    
    play.eq(i).click(function(){
      var iTargetSrc = $(this).attr("dateSrc");   //获取点击播放视频的url
      var iTargetName = $(this).attr("videoname");   //获取点击播放视频的名称
      videoParHTML = '<div class="close" onclick="Tips.hideVideo();"><img src="images/video_x.png" /></div>'
              +'<h2 class="video_tit">'+iTargetName+'</h2>'
              +'<embed allowscriptaccess="never" allownetworking="internal" invokeurls="false" src='
              +iTargetSrc
              +' pluginspage="http://www.macromedia.com/go/getflashplayer" type="application/x-shockwave-flash" quality="high" autostart="0" wmode="transparent" align="middle"></embed>';
      
      //console.log(iTargetSrc)
      //console.log(iTargetName)
      //alert(iTargetSrc)
      //alert(iTargetName)
  
      
      $(".video_pop embed").hide();         //隐藏embed 标签
      $(".video_pop").html("");           //清空
    
      $(videoParHTML).appendTo(videoPar); 
      showHide('#fade_div','.video_pop');
      
      
      var parentWidth = $("embed").parent().width();
      var parentHeight = $("embed").parent().height();
      
    
      $("embed").css({
        "width":parentWidth,
        "height":parentHeight
      })

    });
  }
})();

```


3、图片预加载
----------

>**jQuery** 图片预加载， 插件 lazyload
>**参考链接** http://www.ijquery.cn/?p=253

```
(function lodinImg(){
 var images = new Array()
    function preload() {
            for (i = 0; i < preload.arguments.length; i++) 
            {
                images[i] = new Image()
          images[i].src = preload.arguments[i]                               
             }
    }
    preload(
           /*
            "images/gift1.png",
            "images/gift2.png",
            "images/gift3.png",
            "images/gift4.png"
            */
    )
})();
```


4、移动端响应式脚本，动态改变尺寸
---------------------------------

>- 转换比例 1rem = 100px
>- 使用移动端和pc设备
````
!(function(win, doc){
    function setFontSize() {
        // 获取window 宽度
        // zepto实现 $(window).width()就是这么干的
        var winWidth =  window.innerWidth;
        // doc.documentElement.style.fontSize = (winWidth / 640) * 100 + "px" ;
        // 2016-01-13 订正
        // 640宽度以上进行限制 需要css进行配合
        var size = (winWidth / 640) * 100;
        doc.documentElement.style.fontSize = (size < 100 ? size : 100) + "px" ;
    }
    var evt = "onorientationchange" in win ? "orientationchange" : "resize";
    var timer = null;
    win.addEventListener(evt, function () {
        clearTimeout(timer);
        timer = setTimeout(setFontSize, 300);
    }, false);
    win.addEventListener("pageshow", function(e) {
        if (e.persisted) {
            clearTimeout(timer);
            timer = setTimeout(setFontSize, 300);
        }
    }, false);
    // 初始化
    setFontSize();
}(window, document));
````

5、 判断是IOS设备or安卓设备
------------------------------

>- 方法一：
```
var u = navigator.userAgent;
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1;  //android终端
var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/);             //ios终端
if(isAndroid) {
  alert('这是Android');
}
if(isiOS) {
  alert('这是IOS');
}
```

>- 方法二：

````
if(/(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent)) {
  //alert(navigator.userAgent);
  alert('这是IOS');
} else if(/(Android)/i.test(navigator.userAgent)) {
  //alert(navigator.userAgent);
  alert('这是Android');
} else {
  alert('这是PC');
};
````
>- 微信浏览器or非微信浏览器。

```
function is_weixn() {
  var ua = navigator.userAgent.toLowerCase();
  if(ua.match(/MicroMessenger/i) == 'micromessenger') {
    alert('在微信里打开');
  } else {
    alert('不在微信里打开');
  }
}
is_weixn();
```