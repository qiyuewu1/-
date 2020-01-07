# node.js

## 1.特点

- 单线程
- 非阻塞I/O
- 事件驱动

## 2.安装与运行

- 官网下载msi，无脑安装
- 运行

 创建服务端运行的js文件（不允许有中文）如 demo.js

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

进入控制台：

```
node demo.js
```

根据ip：端口号访问

修改js文件，需重新启动eg：ctrl+c（停止）+  ↑ 

## 3.强调

- 无web容器，路由自定义

- js文件中写的相对路径是 相对于运行 node demo.js 时的路径，如

  ```
  C:\Users\sunyh> node demo.js
  ```

  则 相对路径就是相对于 C:\Users\sunyh

