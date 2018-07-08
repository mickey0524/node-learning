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
                 
