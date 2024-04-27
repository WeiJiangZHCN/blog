# Fetch()

Fetch API 提供了一个 JavaScript 接口，用于访问和操纵 HTTP 管道的一些具体部分，例如请求和响应。它还提供了一个全局 fetch() 方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。

```JS
syntax:fetch(url, options)
async function fetchData() {
    const response = await fetch('https://api.github.com/users/octocat');
    return await response.json();//也可以是blob(),formData(),text(),arrayBuffer()。
}

```

## 流式获取

```JS
async function* streamAsyncIterable(stream){
     const reader = stream.getReader();
        while(true){
            const {done,value} = await reader.read();
            if(done){
                return;
            }
            yield value;
        }
    }
async function fetchData() {
    const response = await fetch('http://47.121.25.246/');
    for await (let i of streamAsyncIterable(response.body)){
        console.log(i);//chunk
        console.log(new TextDecoder("utf-8").decode(i));
    }
}
fetchData();
```
