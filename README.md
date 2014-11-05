dynamic_background
==================

####动态背景  
利用多层背景的交替淡入淡出，实现一种背景在不停变换的效果，先看图。
效果图：  
![效果图](https://raw.githubusercontent.com/uedtianji/dynamic_background/master/img/1.gif)  
[DEMO地址](http://cssdeck.com/labs/collab/9fz8mhu9)  

#####步骤
============
1.利用css的```radial-gradient```创建一个镜像渐变的背景。其中的```80% 20%```为渐变中心的x,y位置。  
>具体的radial-gradient用法可以参见[这里](http://www.w3cplus.com/content/css3-gradient)  


```css
.dynbg__bg{
	position: absolute;
	top: 0px;
	left: 0px;
	width:100%;
	height:100%;
	background:-moz-radial-gradient(80% 20%,farthest-side, #edbf47, #D58123);
	background:-webkit-radial-gradient(80% 20%,farthest-side, #edbf47, #D58123);
}
```
![效果图](https://raw.githubusercontent.com/uedtianji/dynamic_background/master/img/1-1.jpg)  
[在线代码](http://cssdeck.com/labs/uxdoorq0)  

2.重复第一步创建4个拥有不同的渐变背景的DIV。渐变中心点的位置分别为```80% 20%``` ```80% 80%``` ```20% 80%``` ```20% 20%```   
```css
.dynbg__bg{
	position: absolute;
	top: 0px;
	left: 0px;
	width: 100%;
	height: 100%;
	background-size: 100% 100%;
}
.dynbg__bg1{
	background:-moz-radial-gradient(80% 20%,farthest-side, #edbf47, #D58123);
	background:-webkit-radial-gradient(80% 20%,farthest-side, #edbf47, #D58123);
	z-index: 4;
}
.dynbg__bg2{
	background:-moz-radial-gradient(80% 80%,farthest-side, #edbf47, #D58123);
	background:-webkit-radial-gradient(80% 80%,farthest-side, #edbf47, #D58123);
	z-index: 3;
}
.dynbg__bg3{
	background:-moz-radial-gradient(20% 80%,farthest-side, #edbf47, #D58123);
	background:-webkit-radial-gradient(20% 80%,farthest-side, #edbf47, #D58123);
	z-index: 2;
}
.dynbg__bg4{
	background:-moz-radial-gradient(20% 20%,farthest-side, #edbf47, #D58123);
	background:-webkit-radial-gradient(20% 20%,farthest-side, #edbf47, #D58123);
	z-index: 1;
}
```  
四个div的效果  
![效果图](https://raw.githubusercontent.com/uedtianji/dynamic_background/master/img/2.jpg)  

3.将四个div按顺序叠加摆放，并依照顺序将div的透明度由1变为0再变为1。最后一个div的透明度不需要变，所以一个需要变化3个div，每个div的变化有两个状态，所以一共有6个状态。我们将100%除以6，分成0%,16.6667%,33.3333%,50%,66.6667%,83.3333%,100%。每个div在不同阶段的状态如下。  
```css
@-webkit-keyframes dynbg__ani1{
  0%{
    opacity: 1;
  }
  16.6667%{
    opacity: 0;
  }
  33.3333%{
    opacity: 0;
  }
  50%{
    opacity: 0;
  }
  66.6667%{
    opacity: 0;
  }
  83.3333%{
    opacity: 0;
  }
  100%{
    opacity: 1;
  }
}
@-webkit-keyframes dynbg__ani2{
  0%{
    opacity: 1;
  }
  16.6667%{
    opacity: 1;
  }
  33.3333%{
    opacity: 0;
  }
  50%{
    opacity: 0;
  }
  66.6667%{
    opacity: 0;
  }
  83.3333%{
    opacity: 1;
  }
  100%{
    opacity: 1;
  }
}
@-webkit-keyframes dynbg__ani3{
  0%{
    opacity: 1;
  }
  16.6667%{
    opacity: 1;
  }
  33.3333%{
    opacity: 1;
  }
  50%{
    opacity: 0;
  }
  66.6667%{
    opacity: 1;
  }
  83.3333%{
    opacity: 1;
  }
  100%{
    opacity: 1;
  }
}
```  
再给div的class加上动画属性  
```css
.dynbg__bg{
  ...
  -webkit-transition:all 1s linear;
  -moz-transition:all 1s linear;
  ...
}
.dynbg__bg1{
  ...
  -webkit-animation:dynbg__ani1 infinite 8s;
  -moz-animation:dynbg__ani1 infinite 8s;
}
.dynbg__bg2{
  ...
  -webkit-animation:dynbg__ani2 infinite 8s;
  -moz-animation:dynbg__ani2 infinite 8s;
}
.dynbg__bg3{
  ...
  -webkit-animation:dynbg__ani3 infinite 8s;
  -moz-animation:dynbg__ani3 infinite 8s;
}
.dynbg__bg4{
  ...
}
```
这样就将3张图片按顺序由显示渐变为透明再变回显示了。  
>transition的使用方法可以参考[这里](http://www.w3cplus.com/content/css3-transition/)  
>animation的使用方法可以参考[这里](http://www.w3cplus.com/content/css3-animation)  


![效果图](https://raw.githubusercontent.com/uedtianji/dynamic_background/master/img/3.gif)  

4.最后在最上面加上一层平铺的半透明的点来增加质感。  
```css
.dynbg__bg0{
	background-repeat: repeat;
	background: -webkit-radial-gradient(rgba(255,255,255,0.4) 5%, transparent 10%);
	background: -moz-radial-gradient(rgba(255,255,255,0.4) 5%, transparent 10%);
	background-size: 16px 16px;
	z-index: 5;
}
```  
![效果图](https://raw.githubusercontent.com/uedtianji/dynamic_background/master/img/1.gif)  
[在线代码](http://cssdeck.com/labs/collab/9fz8mhu9)  

###如有问题或者建议请微博<a href="http://weibo.com/uedtianji" target="_blank">@UED天机</a>。我会及时回复

==========  


####相关阅读  
1.[波浪状动态背景](https://github.com/cyclegtx/wave_background)