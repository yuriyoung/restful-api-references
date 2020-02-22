# RESTful API URL Structure

## 协议(Protocol)
API与用户的通信协议，总是使用HTTPs协议。

## 域名(Domain)
```http
- https://api.example.com
```

## 版本(Versioning)
```http
- https://api.example.com/v1
- https://api.example.com/v1.0
```

## 请求方法(Request Verb)
- 如果请求头中存在 `X-HTTP-Method-Override` 或参数中存在 `_method`（拥有更高权重），且值为 `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `OPTIONS`, `HEAD` 之一，则视作相应的请求方式进行处理。
- **GET, DELETE, HEAD**
  - 参数风格为标准的 GET 风格的参数，如 `url?a=1&b=2`。
- **POST, PUT, PATCH, OPTIONS**
  - 默认情况下请求实体会被视作标准 `json` 字符串进行处理，但依旧推荐设置头信息的 `Content-Type` 为 `application/json` 。
  - 在一些特殊接口中（会在文档中说明），可能允许 `Content-Type` 为 `application/x-www-form-urlencoded` 或者 `multipart/form-data` ，此时请求实体会被视作标准 `POST` 风格的参数进行处理。

关于方法语义的说明：
- **OPTIONS** 用于获取资源支持的所有 HTTP 方法

- **HEAD** 用于只获取请求某个资源返回的头信息

- **GET** 用于从服务器获取某个资源的信息
  - 完成请求后返回状态码 `200 OK`
  - 完成请求后需要返回被请求的资源详细信息
  ```http
  GET https://api.example.com/v1.0/products/123
  ````

- **POST** 用于创建新资源
  - 创建完成后返回状态码 `201 Created`
  - 完成请求后需要返回被创建的资源详细信息
  ```http
  POST https://api.example.com/v1.0/products
  ````

- **PUT** 用于完整的替换资源或者创建指定身份的资源，比如创建 id 为 123 的某个资源
  - 如果是创建了资源，则返回 `201 Created`
  - 如果是替换了资源，则返回 `200 OK`
  - 完成请求后需要返回被修改的资源详细信息
  ```http
  PUT https://api.example.com/v1.0/products/123
  ````

- **PATCH** 用于局部更新资源
  - 完成请求后返回状态码 `200 OK`
  - 完成请求后需要返回被修改的资源详细信息
  ```http
  PATCH https://api.example.com/v1.0/products/123
  ````

- **DELETE** 用于删除某个资源
  - 完成请求后返回状态码 `204 No Content`
  ```http
  DELETE https://api.example.com/v1.0/products/123
  ````

## 头部(Headers)
- **Accept**: 服务器需要返回什么样的 `Content`。如果客户端要求返回 `application/xml`，服务器端只能返回 `application/json`，那么最好返回status code 406 not acceptable（RFC2616），当然，返回 `application/json` 也并不违背 `RFC` 的定义。一个合格的REST API需要根据 `Accept` 头来灵活返回合适的数据。为了避免API的变动导致用户使用中产生意外结果或调用失败，最好强制要求所有访问都需要指定版本号。请避免提供默认版本号，一旦提供，日后想要修改它会相当困难。最适合放置版本号的位置是头信息(HTTP Headers)，在 Accept 段中使用自定义类型(content type)与其他元数据(metadata)一起提交。例如:
  ```http
  Accept: application/vnd.heroku+json; version=2
  ```

- **If-Modified-Since/If-None-Match**: 如果客户端提供某个条件，那么当这条件满足时，才返回数据，否则返回 `304 Not Modified` 。比如客户端已经缓存了某个数据，它只是想看看有没有新的数据时，会用这两个header之一，服务器如果不理不睬，依旧做足全套功课返回 `200 OK` ，那就既不专业，也不高效。

- **If-Match**: 在对某个资源做 `PUT/PATCH/DELETE` 操作时，服务器应该要求客户端提供 `If-Match` 头，只有客户端提供的 `Etag` 与服务器对应资源的 `Etag` 一致，才进行操作，否则返回 `412 Precondition Failed` 。在所有返回的响应中包含ETag头信息，用来标识资源的版本。这让用户对资源进行缓存处理成为可能，在后续的访问请求中把 `If-None-Match` 头信息设置为之前得到的ETag值，就可以侦测到已缓存的资源是否需要更新。


## 路径(Endpoint)
[ ] TODO

## 命名(Naming)
- 避免的命名
  某些名称在API域名中被重载，以至于它们失去了所有意义，或者与其他域名中的常见用法冲突，而这些域在使用REST API时是无法避免的，服务中不应使用以下名称:
  - Context
  - Scope
  - Resource

## 资源Resource)
[ ] TODO

## 集合(Collections)
```http
POST https://api.example.com/v1.0/users
```
[ ] TODO

## 分页(Pagination)
[ ] TODO

## 过虑参数(Filtering)
[ ] TODO

## 排序(Sorting)
[ ] TODO

