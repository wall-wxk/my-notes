# XMLHttpRequest

```javascript
// 实例化 XMLHttpRequest
let xhr = new XMLHttpRequest()
// 定义加载完成回调函数，打印结果
xhr.onload = function () {
  console.log('请求成功')
}
// 定义加载出错时的回调函数，打印错误
xhr.onerror = function (err) {
  console.error('请求失败')
}

// 超时时间单位为毫秒
xhr.timeout = 1000

// 当请求超时时，会触发 ontimeout 方法
xhr.ontimeout = () => console.log('请求超时')

// 请求完成
xhr.onreadystatechange = () => {
    if (xhr.readyState == 4) {
        if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
            // xhr.responseText
            // 判断接受数据的内容类型
            var type = xhr.getResponseHeader('Content-type'); 
            if(type.indexOf('xml') !== -1 && xhr.responseXML) { 
                response = xhr.responseXML; //Document对象响应 
            } else if(type === 'application/json') { 
                response = JSON.parse(xhr.responseText); //JSON响应 
            } else { 
                response = xhr.responseText; //字符串响应 
            }; 
        } else {
            // 请求失败
        }
    }
}
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded;charset=UTF-8')
// 设置请求目标
const asyncFlag = true; // 是否异步
xhr.open('GET', '/path/to/text', asyncFlag)
// 开始发起请求
xhr.send();
```

```javascript
fetch('/path/to/text', {
        method: 'POST',
        headers: new Headers({
            'Content-Type':'application/json'
        }),
        body: JSON.stringify(data)
    })
    .then(res => {
        if(res.ok){
            return res.json();
        }

        throw new Error('Network response not ok!');
    })
    .then(response => {
        console.log('请求成功')
    })
    .catch(err => {
        console.error('请求失败')
    })
```