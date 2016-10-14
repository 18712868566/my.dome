#用js改变embed标签的src值

参考链接
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