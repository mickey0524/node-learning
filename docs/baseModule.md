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
		
* Node中的os模块

    * os.cpus()

        返回一个对象数组，包含每个逻辑CPU内核的信息，一个非常典型的应用就是开多进程的时候	
* Node中的fs模块

    node.js当中的fs模块主要对应着系统的文件操作

    * fs.stat(path, callback)

        该方法用于检查文件的状态，可以借此来判断某个文件是否存在。`path`参数传入该文件的绝对物理路径，该`callback`回调参数有两个参数`err`和`stats`。其中`err`为错误信息参数, `stats`为一个文件状态对象，如果文件不存在，`stats`数值为undefined

        ```js
        const path = require('path');
        const fs = require('fs');
        const fsPath = path.resolve('./1.txt');

        fs.stat(fsPath, (err, stats) => {
            if (err) throw err;
            console.log(stats);
        });
        ```

    * fs.writeFile(path, data[, options], callback)

        该方法可用于往指定文件当中写入内容，该内容会覆盖文件当中原有的内容。若传入的文件路径当中的文件不存在，则先完成该文件的穿件，再往里面写入指定内容。`path`参数为该文件的绝对物理路径，`data`为需要写入该文件当中的数据内容，其中`options`参数可选，可以传入编码格式，若不传则默认为`utf-8`。`callback`回调参数当中只有一个错误信息参数`err`，一般在写入失败时触发调用
        
        ```js
        const fsPath = path.resolve('./1.txt');
        
        fs.writeFile(fsPath, 'mickey0524', (err) => {
            if (err) throw err;
            console.log('写入成功');
        });
        ```
        
    * fs.appendFile(path, data[, options], callback)

   	     writeFile会覆盖文件，appendFile是追加文件
   	 
    * fs.unlink(path, callback)

   	     该方法可用于完成指定文件的删除。`path`参数为该文件的绝对物理路径，`callback`回调参数当中只有一个错误信息参数`err`，一般在该文件不存在或者删除文件失败时触发调用
   	     
   	     ```js
   	     fs.unlink(fsPath, (err) => {
   	         if (err) throw err;
   	         console.log('删除成功');
   	     });
   	     ```
   	    
	* fs.readFile(path[, options], callback)

	    该方法用于读取指定文件当中的内容，`path`参数为该文件的绝对物理路径，其中`options`参数可选，可以传入编码格式，如读取文本文件时，可传入'utf8',若不指定编码格式，则默认输出读取的文件内容为Buffer形式，故一般都会传入该参数。`callback`回调参数当中有两个参数`err`和`data`，其中`err`为错误信息参数，一般在在文件不存在或者读取文件失败时触发调用，`data`为文件内容
	    
	    ```js
	    fs.readFile(fsPath, (err, data) => {
	    	if (err) throw err;
	    	console.log(data);
	    });
	    ```
   * fs.rename(oldPath, newPath, callback)

   		该方法可用于移动或重命名指定文件。`oldPath`参数为该文件原来的路径，`newPath`参数为该文件移动或重命名之后的路径，这两个参数都必须能传入文件完整的绝对物理路径。`callback`回调参数当中只有一个错误信息参数，一般在`oldPath`当中指定的文件不存在或者该操作失败时触发调用
   		
   		```js
   		fs.rename(oldPath, newPath, (err) => {
   			if (err) throw err;
   			console.log('rename操作成功');
   		});
   		```
   		
   	* fs.readdir(path, callback)

   		该方法可以用于读取一个指定目录当中的信息。其中`path`为该目录的绝对物理路径，`callback`回调函数当中有两个参数`err`和`files`，`err`为错误信息参数，一般在该目录不存在或读取失败时触发调用，`files`为一个数组对象，包含该目录下的所有文件夹与文件的名字。（仅为文件夹的名字和文件名，不是路径形式）
   		
   		```js
   		fs.readdir(dirPath, (err, files) => {
   			if (err) throw err;
   			console.log(files);
   		});
   		```
  
  * fs的操作默认是异步的，可以在api后加上`Sync`来使得操作变成同步，同步操作需要使用`try catch`来捕获可能发生的错误