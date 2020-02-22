## 通用HTTP响应状态码

| 状态码 | 编码  | 状态说明     |
| ----- | ----- | ----------- |
| 100   | Continue | 继续请求。这个临时响应用来通知客户端，它的部分请求已经被服务器接收，且仍未被拒绝。 |
| 101   | Switching Protocols | 切换协议。只能切换到更高级的协议。例如，切换到HTTP的新版本协议。 |
| 200   | OK | 请求成功。 |
| 201   | Created | 创建类的请求完全成功。 |
| 202   | Accepted | 已经接受请求，但未处理完成(任务提交成功，当前系统繁忙，下发的任务会延迟处理)。 |
| 203   | Non-Authoritative Information | 非授权信息，请求成功。 |
| 204   | No Content	 | 请求完全成功，同时HTTP响应不包含响应体。在响应OPTIONS方法的HTTP请求时返回此状态码(任务提交成功)。 |
| 205   | Rest Content | 重置内容，服务器处理成功。 |
| 206   | Partial Content | 服务器成功处理了部分GET请求。 |
| 300   | Multiple Choices | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择。 |
| 301   | Moved Permanently	 | 永久移动，请求的资源已被永久的移动到新的URI，返回信息会包括新的URI。 |
| 302   | Found | 资源被临时移动。 |
| 303   | See Other | 查看其它地址。使用GET和POST请求查看。 |
| 304   | Not Modified | 所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。 |
| 305   | Use Proxy | 所请求的资源必须通过代理访问。 |
| 306   | Unused | 已经被废弃的HTTP状态码。 |
| 400   | BadRequest | 非法请求。建议直接修改该请求，不要重试该请求。 |
| 401   | Unauthorized | 在客户端提供认证信息后，返回该状态码，表明服务端指出客户端所提供的认证信息不正确或非法。 |
| 402   | Payment Required | 保留请求。 |
| 403   | Forbidden | 请求被拒绝访问。返回该状态码，表明请求能够到达服务端，且服务端能够理解用户请求，但是拒绝做更多的事情，因为该请求被设置为拒绝访问，建议直接修改该请求，不要重试该请求。 |
| 404   | NotFound | 所请求的资源不存在。建议直接修改该请求，不要重试该请求。 |
| 405   | MethodNotAllowed | 请求中带有该资源不支持的方法。建议直接修改该请求，不要重试该请求。 |
| 406   | Not Acceptable | 服务器无法根据客户端请求的内容特性完成请求。 |
| 407   | Proxy Authentication Required | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权。 |
| 408   | Request Time-out | 服务器等候请求时发生超时。客户端可以随时再次提交该请求而无需进行任何更改。 |
| 409   | Conflict | 服务器在完成请求时发生冲突。返回该状态码，表明客户端尝试创建的资源已经存在，或者由于冲突请求的更新操作不能被完成。 |
| 410   | Gone | 客户端请求的资源已经不存在。返回该状态码，表明请求的资源已被永久删除。 |
| 411   | Length Required	 |服务器无法处理客户端发送的不带Content-Length的请求信息。 |
| 412   | Precondition Failed | 未满足前提条件，服务器未满足请求者在请求中设置的其中一个前提条件。 |
| 413   | Request Entity Too Large | e	由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息。 |
| 414   | Request-URI Too Large | 请求的URI过长（URI通常为网址），服务器无法处理。 |
| 415   | Unsupported Media Type | 服务器无法处理请求附带的媒体格式。 |
| 416   | Requested range not satisfiable | 客户端请求的范围无效。 |
| 417   | Expectation Failed	 | 服务器无法满足Expect的请求头信息。 |
| 422   | UnprocessableEntity	 | 请求格式正确，但是由于含有语义错误，无法响应。 |
| 429   | TooManyRequests | 	表明请求超出了客户端访问频率的限制或者服务端接收到多于它能处理的请求。建议客户端读取相应的Retry-After首部，然后等待该首部指出的时间后再重试。 |
| 500   | InternalServerError | 表明服务端能被请求访问到，但是不能理解用户的请求。 |
| 501   | Not Implemented	 | 服务器不支持请求的功能，无法完成请求。 |
| 502   | Bad Gateway	 | 充当网关或代理的服务器，从远端服务器接收到了一个无效的请求。 |
| 503   | ServiceUnavailable | 被请求的服务无效。建议直接修改该请求，不要重试该请求。 |
| 504   | ServerTimeout | 请求在给定的时间内无法完成。客户端仅在为请求指定超时（Timeout）参数时会得到该响应。 |
| 505   | HTTP Version not supported | 服务器不支持请求的HTTP协议的版本，无法完成处理。 |