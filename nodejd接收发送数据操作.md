# -// 引入express
const express = require("express");

// 创建应用对象
const app = express();


// btn01接收数据
app.post("/server",(request,response)=>{
    // 设置响应头，设置允许跨越。
    response.setHeader("Access-Control-Allow-Origin","*");
    // 设置响应体
    response.send("HELLO AJAX POST");
});

// btn02发送数据
app.post("/serverr",(request,response)=>{
    // 设置响应头，设置允许跨越。
    response.setHeader("Access-Control-Allow-Origin","*");
    request.on('data',function(data){
        let str = data.toString('utf8')  // buffer转换成str
        console.log(str);
        let json = JSON.parse(str)
        console.log(json); // 终于接收到了数据。。。
        console.log(json.a);
    })
    // 设置响应体
    response.send("HELLO AJAX POST");
});

// 监听端口启动服务
app.listen(8000,()=>{
    console.log("服务已经启动，8000端口监听中。。。");
})

// 客户端代码：
const xhr = new XMLHttpRequest();
                // 设类型与url
                xhr.open("POST","http://127.0.0.1:8000/serverr");

                // 设置请求头   content-type设置请求体内容的类型
                // xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
                xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded;charset=UTF-8");
                
                // 发送，括号里面可以写参数，多个参数用&隔开。可以传递给服务器
                xhr.send('{"a":100,"b":200}');
                // 事件绑定
                xhr.onreadystatechange = function(){
                    if(xhr.readyState == 4){
                        if(xhr.status >=200 & xhr.status<300){
                            console.log(xhr.response);
                        }
                    }
                }
