# 简介

Weex-request 是封装weex中的stream.fetch模块，实现了便捷方法和拦截请求，可以像axios一样使用。

# 安装

```bash
$ npm install weex-request --save
```

```javascript
import weexRequest from "weex-request";
```

# Example

Performing a `GET` request

```javascript
import weexRequest from "weex-request";

// Make a request for a user with a given ID
weexRequest.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .then(function () {
    // always executed
  });
```



weexRequest(config)

```javascript
// Send a POST request
weexRequest.all({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});

// GET request for remote image
weexRequest.all({
  method:'get',
  url:'http://bit.ly/2mTM3nY',
  type:'stream'
})
  .then(function(response) {
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
  });
```

### Request method aliases

For convenience aliases have been provided for all supported request methods.

##### weexRequest.all(config)

##### weexRequest.get(url[, config])

##### weexRequest.delete(url[, config])

##### weexRequest.head(url[, config])

##### weexRequest.options(url[, config])

##### weexRequest.post(url[, data[, config]])

##### weexRequest.put(url[, data[, config]])

##### weexRequest.patch(url[, data[, config]])



## Global weexRequest defaults

```javascript
// 设置默认选项
weexRequest.default.baseUrl = "https://api.github.com/";
weexRequest.default.headers = {
    "Content-Type": "application/json"
};
```



## Interceptors

You can intercept requests or responses before they are handled by `then` or `catch`.


```javascript
import weexRequest from "weex-request";

// 设置默认选项
weexRequest.default.baseUrl = "https://api.github.com/";
weexRequest.default.headers = {
    "Content-Type": "application/json"
};
// 拦截请求
weexRequest.interceptors.request = function(config) {
    console.log("config", config);
    return Promise.resolve(config);
};

// 拦截响应
weexRequest.interceptors.response = function(response) {
    console.log("response", response);
    return Promise.resolve(response);
};

export default weexRequest;
```