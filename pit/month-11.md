11 月我们踩过的坑
===

> Author: larry.koo  Date: 2017-11-29

### Spring MVC 中 HTTPConverter 对象序列化的问题

**踩坑**

关于 `Spring Boot 1.5.6+` 版本，发现通过 `Restful` 发起的 HTTP 请求到另一个 Service 的时候，请求的 Request 参数竟然被 Spring 强制序列化了，导致 Service 端接收到参数之后无法进行对象的解析，报出`can not read json string`的异常；


**填坑**


### Spring Controller 中，持久化对象无法返回到 Response 中的问题

**踩坑**

日常编码中，有的同事，不经意间将持久化层的 `Domain` 对象或者一些 `Spring IOC` 的封装对象直接作为 `Response` 在 `Controller` 当中进行返回，殊不知这些对象在 `HTTPConverter` 进行 `JSON` 对象转换的时候，可能会遇到类型不明确的问题，或者无法序列化的问题；

**填坑**

解决办法很简单，就是不要这么做，`Controller` 中作为 `Response Object` 返回的对象必须是我们自己定义的 `DTO` 对象，而且必须实现序列化接口；这应该是编码规范，遵循这样的规范，就不会再出现返回 `Response Object` 无法解析的问题；

