## 什么的防抖和节流？

防抖和节流是两种应对web页面中频繁触发事件的优化方案。

## 防抖 `debounce`

顾名思义，防抖就是防止抖动，避免事件的重复触发。  
应用场景：

1.  点击按钮事件，用户在一定时间段内的点击事件，为了防止和服务端的多次交互，我们可以采用防抖。
2.  输入框的自动保存事件
3.  浏览器的`resize`事件

总之，防抖可以概括为触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间。 根据以上概念，我们可以尝试一下实现一个防抖函数：

```javascript
function debounce(fun,wait){
    let timer;
    return (...args)=>{
    	if (timer){
        	clearTimeout(timer);
        }
        timer = setTimeout(()=>{
        	fun(...args);
        },wait)
    }
}
window.onresize = debounce(()=>{
	console.log(1);
},1000);
//页面在频繁resize的时候，控制台也只会打印一次1
```

## 节流 `throttle`

还是顾名思义，节流就是减少流量，将频繁触发的事件减少，并每隔一段时间执行。即，控制事件触发的频率。  
应用场景：

1.  `scroll`事件，滚动的过程中每隔一段时间触发事件。（可见 [如何实现图片的懒加载](https://juejin.cn/post/6896292983813963783 "https://juejin.cn/post/6896292983813963783")中的应用） 节流可以概括为高频事件触发，但在n秒内只会执行一次，节流会稀释函数的执行频率。 根据以上概念，我们可以尝试一下实现一个节流函数：

```javascript
//利用时间间隔实现
function throttle1(fun,wait){
	let time1 = 0;
	return (...args)=>{
   		const time2 = Date.now()
        const timeInterval = time2 - time1;
 		if ( timeInterval < wait){
 			return 
 		}else {
			time1 = time2;
            fun(...args);
		}
    }
}
window.onresize = throttle1(()=>{
	console.log(1);
},1000);
//页面在频繁resize的时候，控制台会每隔1秒打印一次

//利用定时器实现
function throttle2(fun,wait){
	let timer;
	return (...args)=>{
		if (timer){
			return
		}else {
			timer = setTimeout(()=>{
				timer = null;
				fun(...args);
			},wait);
		}
	}
}
window.onresize = throttle2(()=>{
	console.log(1);
},1000);
//页面在频繁resize的时候，控制台会每隔1秒打印一次
```

## 总结：

**防抖：触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间，<font color="red">多次触发只执行最后一次</font>**  
**节流：高频事件触发，但在n秒内只会执行一次，节流会稀释函数的执行频率，<font color="red">会多次执行</font>**
