# 状态码

## 请求成功
- 200 **OK**: 请求执行成功并返回相应数据，如 `GET` 成功。
- 201 **Created**: 对象创建成功并返回相应资源数据，如 `POST` 成功；创建完成后响应头中应该携带头标 `Location` ，指向新建资源的地址。
- 202 **Accepted**: 接受请求，但无法立即完成创建行为，比如其中涉及到一个需要花费若干小时才能完成的任务。返回的实体中应该包含当前状态的信息，以及指向处理状态监视器或状态预测的指针，以便客户端能够获取最新状态。
- 204 **No Content**: 请求执行成功，不返回相应资源数据，如 `PATCH` ， `DELETE` 成功。

## 重定向
**重定向的新地址都需要在响应头 `Location` 中返回。**
- 301 **Moved Permanently**: 被请求的资源已永久移动到新位置。
- 302 **Found**: 请求的资源现在临时从不同的 URI 响应请求。
- 303 **See Other**: 对应当前请求的响应可以在另一个 URI 上被找到，客户端应该使用 `GET` 方法进行请求。比如在创建已经被创建的资源时，可以返回 `303` 。
- 307 **Temporary Redirect**: 对应当前请求的响应可以在另一个 URI 上被找到，客户端应该保持原有的请求方法进行请求。

## 条件请求
- 304 **Not Modified**: 资源自从上次请求后没有再次发生变化，主要使用场景在于实现数据缓存。
- 409 **Conflict**: 请求操作和资源的当前状态存在冲突。主要使用场景在于实现并发控制。
- 412 **Precondition Failed**: 服务器在验证在请求的头字段中给出先决条件时，没能满足其中的一个或多个。主要使用场景在于实现并发控制。

## 客户端错误
- 400 **Bad Request**: 请求体包含语法错误。
- 401 **Unauthorized**: 需要验证用户身份，如果服务器就算是身份验证后也不允许客户访问资源，应该响应 `403 Forbidden` 。如果请求里有 `Authorization`头，那么必须返回一个 `WWW-Authenticate` 头。
- 403 **Forbidden**: 服务器拒绝执行。
- 404 **Not Found**: 找不到目标资源。
- 405 **Method Not Allowed**: 不允许执行目标方法，响应中应该带有 `Allow` 头，内容为对该资源有效的 HTTP 方法。
- 406 **Not Acceptable**: 服务器不支持客户端请求的内容格式，但响应里会包含服务端能够给出的格式的数据，并在 `Content-Type` 中声明格式名称。
- 410 **Gone**: 被请求的资源已被删除，只有在确定了这种情况是永久性的时候才可以使用，否则建议使用 `404 Not Found`。
- 413 **Payload Too Large**: `POST` 或者 `PUT` 请求的消息实体过大。
- 415 **Unsupported Media Type**: 服务器不支持请求中提交的数据的格式。
- 422 **Unprocessable Entity**: 请求格式正确，但是由于含有语义错误，无法响应。
- 428 **Precondition Required**: 要求先决条件，如果想要请求能成功必须满足一些预设的条件。

## 服务端错误
- 500 **Internal Server Error**: 服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。
- 501 **Not Implemented**: 服务器不支持当前请求所需要的某个功能。
- 502 **Bad Gateway**: 作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
- 503 **Service Unavailable**: 由于临时的服务器维护或者过载，服务器当前无法处理请求。这个状况是临时的，并且将在一段时间以后恢复。如果能够预计延迟时间，那么响应中可以包含一个 `Retry-After` 头用以标明这个延迟时间（内容可以为数字，单位为秒；或者是一个 HTTP 协议指定的时间格式）。如果没有给出这个 `Retry-After` 信息，那么客户端应当以处理 500 响应的方式处理它。
> `501` 与 `405` 的区别是：`405` 是表示服务端不允许客户端这么做，`501` 是表示客户端或许可以这么做，但服务端还没有实现这个功能。


## 通用HTTP状态码对照表

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
| 413   | Request Entity Too Large | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息。 |
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