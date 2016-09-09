# 移动端的click事件和tap事件以及解决方案

	+、在移动设备上没有了鼠标输入，hover等，取而代之的是touch
	+、移动web页面上的click的响应会慢上300ms

	+、使用Tap事件代替click事件，解决300ms延迟问题

	+、Tap为自定义事件，原理如下：
		在touchstart, touchend时记录时间，手指位置，在touchend时进行比较，如果手指位置为同一位置（或允许移动一个非常小的位移）且
	间隔时间较短（一般认为是200ms）,且过程中未曾出发过touchmove，即可认为触发了移动端的tap事件
	
	zepto的tap事件绑定在document上的，会有点透bug，原因就是click的300ms延迟，tap事件触发之后，会在300ms的时候触发click

	solution： Tap点透的解决方案
	1、使用缓动动画，将300ms的时间“浪费”掉
	2、中间dom层的加入，让中间层接受这个“穿透事件”，稍后隐藏
	3、“上下”都使用tap事件，原理上解决tap点透（但不可避免原生标签（比如下面是a,或者input,button，还是会有原生的click效果）的click事件）
	4、改用Fastclick库