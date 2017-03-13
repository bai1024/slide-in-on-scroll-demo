#slide-in-on-scroll

##效果图
<center>![img](http://ok7n02kz6.bkt.clouddn.com/Fhd7KA5KueOnSYCXQ-SRzieyeUIl.gif)</center>>

## 知识点
1.`debounce`

在找关于`debounce`资料的时候看到一个很有意思的例子，一下子就懂了`debounce`。
> 想象一下你准备回家，进了电梯，准备关门的时候突然你的邻居出现了，正冲向电梯，然后你把正在关上的电梯门打开了，（这个时候的你就是在推迟电梯的出发时间）。假如这种情况一直发生，一直会有人准备冲进电梯，你就一次又一次的打开电梯门。这样就会推迟电梯的出发。

这样一解释，是不是就容易理解多了呢~

在这里列举几个`debounce`的应用场景：
- input 中输入文字自动发送 ajax 请求进行自动补全，只需要在输入完最后一个词的时候处理就可以了。
- resize window 重新计算样式或布局
- mouseleave时隐藏二级菜单：debounce，并合理使用 cancel 方法

2.`scrollY`文档垂直滚动的像素值。

3·`innerHeight`浏览器视口的高度

图解（1）：

![](http://ok7n02kz6.bkt.clouddn.com/FqnbWfM710Sdh443CUm0KnxZ35uG.png)

4.`offsetTop` 当前元素顶部到其父元素顶部之间的距离。（见图解（3））

## 实现过程

首先考虑什么时候开始让图片进入呢？决定了是在图片的一半(留给图片空间的一半)进入视野后，图片进入。然后要思考，如何判断图片的一半已经进入视野了呢？

代码里是这样实现的：

//开始滚动

```javascript
const slideInAt = (window.scrollY + window.innerHeight) - sliderImage.height / 2;
```

图解（2）：
![example](http://ok7n02kz6.bkt.clouddn.com/Fi7xTAXm6-RiAsMXJQ8LkyHtRLLT.png)

//当图片的一半进入视野时

```javascript
const imageBottom = sliderImage.offsetTop + sliderImage.height;
```

图解（3）：
![example](http://ok7n02kz6.bkt.clouddn.com/FjCuqSYYCy6-qnk1JI1w_dZ742t3.png)通过上面两张图可以看到，当 `slideInAt` 的长度大于`imageBottom`时图片的一半已经超过视野了。也就是说只要判断`slideInAt`大于`imageBottom`就可以执行让图片进入的代码了~