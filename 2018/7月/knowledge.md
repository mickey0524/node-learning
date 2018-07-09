* Node中的path模块

	`path`模块提供了一些工具函数，用于处理文件与目录的路径。可以通过以下方式使用:
	
	```js
	const path = require('path');
	```
	
    * path.delimiter

        提供指定平台的路径分隔符, windows为;, posix为:
    
    * path.join([...paths])

        使用平台特定的分隔符把全部给定的`path`片段连接到一起，并规范化生成的路径

        长度为零的 path 片段会被忽略。 如果连接后的路径字符串是一个长度为零的字符串，则返回 '.'，表示当前工作目录

        ```js
        path.join('/first', 'second', 'three', '..', 'four'); // 返回: '/first/second/four'
        path.join('/first', '..'); // 返回: '.'
        ```

    * path.resolve([...paths])

        `path.resolve()`方法会把一个路径或路径片段的序列解析为一个绝对路径

        ```js
        path.resolve('first') // /Users/name/first
        path.resolve('..') // /Users
        ```

* Node中的EventEmitter模块

	EventEmitter模块是Node中一个相当重要的模块，是大多数 Node.js 核心 API 都采用惯用的异步事件驱动架构，基本用法如下所示:
	
	```js
	const EventEmitter = require('events');
	
	const myEmitter = new EventEmitter();
	
	myEmitter.on('event', (name) => {
		console.log(`${name} trigger an event!`);
	});
	
	myEmitter.emit('event', 'mickey');
	```
	
	* eventEmitter.on(event[, ...args])

		监听事件的触发
		
	* eventEmitter.emit(event[, ...args])

		触发事件
		
	* eventEmitter.once()

		参数和on方法一样，区别是once方法只监听一次事件的触发
	
	* 当在`EventEmitter`实例中发生错误的时候，如果没有为`error`事件设置监听器，会导致node进程崩溃，因此好的实践都会设置一个error的catch函数

		```js
		myEmitter.on('error', (err) => {
			console.log('something wrong happened!!!');
		});
		``` 
	
	* eventEmitter.removeListener(eventName, listener)

		移除实例中eventName事件下的listener监听器，node V10.0之后新增off的语法糖
	
	* eventEmitter.removeAllListeners([eventName])

		移除实例中的所有监听器

	* eventEmitter.setMaxListeners(n)

		设置当前`EventEmitter`实例的最大允许监听器数量
		
	* eventEmitter.getMaxListeners()
	
		获取当前`EventEmitter`实例的最大允许监听器数量
	
	* eventEmitter.prependListener(eventName, listener)
		添加 listener 函数到名为 eventName 的事件的监听器数组的开头。 不会检查 listener 是否已被添加。 多次调用并传入相同的 eventName 和 listener 会导致 listener 被添加与调用多次。
	
	* eventEmitter.prependOnceListener(eventName, listener)
	
		添加一个单次 listener 函数到名为 eventName 的事件的监听器数组的开头。 下次触发 eventName 事件时，监听器会被移除，然后调用	
		
	
	