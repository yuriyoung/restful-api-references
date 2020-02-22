## Success Responses 成功响应

1. **GET** - 获取单个资源，HTTP响应状态码: ***200***
```javascript
    HTTP/1.1 200
    Content-Type: application/json

    {
        "id": 10,
        "name": "shirt",
        "color": "red",
        "price": "￥23.99"
    }
```
2. **GET** - 获取资源列表，HTTP响应状态码: ***200***
```javascript
    HTTP/1.1 200
    Pagination-Count: 100
    Pagination-Page: 5
    Pagination-Limit: 20
    Content-Type: application/json
    
    [
      {
        "id": 10,
        "name": "shirt",
        "color": "red",
        "price": "￥123.88"
      },
      {
        "id": 11,
        "name": "coat",
        "color": "black",
        "price": "￥2300.99",
      }
    ]
```
3. **POST** - 建立一个新的资源，HTTP响应状态码: ***201***
```javascript
    HTTP/1.1  201
    Location: /v1/items/12
    Content-Type: application/json
 
    {
      "message": "The item was created successfully"
    }
```
4. **PATCH/PUT** - 更新一个指定的资源，HTTP响应状态码: ***200/204***
> 如果需要返回更新后的资源

```javascript
    HTTP/1.1  200
    Content-Type: application/json
 
    {
        "id": 10,
        "name": "shirt",
        "color": "red",
        "price": "￥23.99"
    }
```
> 如果不需要返回更新后的资源

```javascript
    HTTP/1.1  204
```
5. **DELETE** - 删除一个指定的资源，HTTP响应状态码: ***204***
```javascript
    HTTP/1.1  204
```

## Error Responses 错误响应


1. **GET** - 指定的资源不存在，HTTP响应状态码: ***404***

```javascript
    HTTP/1.1  404
    Content-Type: application/json
 
    {
      "message": "The item does not exist"
    }
```
2. **DELETE** - 指定的资源不存在，HTTP响应状态码: ***404***
```javascript
    HTTP/1.1  404
    Content-Type: application/json
 
    {
      "message": "The item does not exist"
    }
```
3. **POST** - 建立新的资源时字段验证失败，HTTP响应状态码: ***400***
```javascript
    HTTP/1.1  400
    Content-Type: application/json
    
    {
        "message": "Validation errors in your request", /* 可选的错误消息 */
        "errors": [
            {
                "message": "Oops! The value is invalid",
                "code": 34,
                "field": "email"
            },
            {
                "message": "Oops! The format is not correct",
                "code": 35,
                "field": "phoneNumber"
            }
        ]
    }
```
4. **PATCH** - 更新指定的资源时字段验证失败，HTTP响应状态码: ***400/404***

> 要更新的资源存在时
```javascript
    HTTP/1.1  400
    Content-Type: application/json
    
    {
        "message": "Validation errors in your request", /* 可选的错误消息 */
        "errors": [
            {
                "message": "Oops! The format is not correct",
                "code": 35,
                "field": "phoneNumber"
            }
        ]
    }
```

> 要更新的资源不存在时
```javascript
    HTTP/1.1  404
    Content-Type: application/json
 
    {
      "message": "The item does not exist"
    }
```
5. **VERB** - Unauthorized 未授权的请求，HTTP响应状态码: **401**
```javascript
    HTTP/1.1  401
    Content-Type: application/json
 
    {
      "message": "Authentication credentials were missing or incorrect"
    }
```
6. **VERB** - Forbidden 请求被拒绝，HTTP响应状态码: **403**
```javascript
    HTTP/1.1  403
    Content-Type: application/json
 
    {
      "message": "The request is understood, but it has been refused or access is not allowed"
    }
```
7. **VERB** - Conflict 在创建时资源已存在或资源类型不支持时的请求，HTTP响应状态码: **409**
```javascript
    HTTP/1.1  409
    Content-Type: application/json
 
    {
      "message": "Any message which should help the user to resolve the conflict"
    }
```
8. **VERB** - Too Many Requests 请求过于频繁，HTTP响应状态码: **429**
```javascript
    HTTP/1.1  429
    Content-Type: application/json
 
    {
      "message": "The request cannot be served due to the rate limit having been exhausted for the resource"
    }
```
9. **VERB** - Internal Server Error 服务器错误，HTTP响应状态码: **500**
```javascript
    HTTP/1.1  500
    Content-Type: application/json
 
    {
      "message": "Something is broken"
    }
```
10. **VERB** - Service Unavailable 服务不可用，HTTP响应状态码: **503**
```javascript
    HTTP/1.1  503
    Content-Type: application/json
 
    {
      "message": "The server is up, but overloaded with requests. Try again later!"
    }
```

## Validation Error Responses 验证字段错误响应

根据不同的需求，验证错误格式可能不同。下面是一些常用的格式，但与上回应格式不同：

- 格式1：
```javascript
    HTTP/1.1  400
    Content-Type: application/json
    
    {
        "message": "Validation errors in your request", /* skip or optional error message */
        "errors": {
            "email": [
                  "Oops! The email is invalid"
                ],
            "phoneNumber": [
                  "Oops! The phone number format is not correct"
                ]
        }
    }
```
- 格式2：
```javascript
    HTTP/1.1  400
    Content-Type: application/json
    
    {
        "message": "Validation errors in your request", /* skip or optional error message */
        "errors": {
            "email": [
              {
                "message": "Oops! The email is invalid",
                "code": 35
              }
            ],
            "phoneNumber": [
              {
                "message": "Oops! The phone number format is not correct",
                "code": 36
              }
            ]
        }
    }
```

...
