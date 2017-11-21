# Cloudgo-IO

---

## 要求
1. 支持静态文件服务
2. 支持简单 js 访问
3. 提交表单，并输出一个表格
4. 对 `/unknown` 给出开发中的提示，返回码 `5xx`

## 实现
1、见代码。实验中使用了Negroni的logging中间件，第一次访问得到的反应如下：

``` 
[negroni] listening on :8080
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 2.357753ms | localhost:8080 | GET / 
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 56.266µs | localhost:8080 | GET /main.css 
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 25.696µs | localhost:8080 | GET /test.js 
[negroni] 2017-11-16T05:34:13-08:00 | 404 | 	 36.723µs | localhost:8080 | GET /favicon.ico 
[negroni] 2017-11-16T05:34:13-08:00 | 404 | 	 37.846µs | localhost:8080 | GET /favicon.ico 
``` 

2、可以看见程序相应了客户端的请求，返回了主页，以及静态目录的css文件和js文件  
访问`localhost:8080/api`会返回一串JSON数据，在test.js 中使用Jquery的Ajax方法请求这个地址，打开firefox的开发者工具，可以看到console记录下了返回的数据  

```HTML
123
Hi Kingchiu
```

3、对应在服务端程序也可以看到，请求了/api路径
```
[negroni] 2017-11-16T06:49:38-08:00 | 200 | 	 113.166µs | localhost:8080 | GET /api
```

4、访问`localhost:8080/unknown`浏览器会看见501 not implement的字样    
而服务端也会显示出现了501错误：
```
[negroni] 2017-11-20T07:11:57-08:00 | 501 | 	 61.707µs | localhost:8080 | GET /unknown 
```
