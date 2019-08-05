---
layout: wiki
title: 常见 HTTP 状态码及含义
categories: [http, response]
description: 常见 HTTP 状态码及含义
keywords: http, response, status code
---

> HTTP 状态码由 3 位十进制数字组成，最高位表示状态码的分类，后面两位表示该分类下的不同状态。

## 一、概述

类型 | 含义
---  | ---
1XX | 信息，表示临时响应需要继续处理。
2XX | 成功，表示服务器已成功处理相应请求。
3XX | 重定向，表示需要进一步操作来完成请求。
4XX | 客户端错误，表示客户端请求不符合服务器要求（包括不支持、已被禁止或需要授权等情形）。
5XX | 服务端错误，表示服务器在处理相应请求时发生内部错误。

## 二、常用状态码详细说明


状态码 | 原语                  | 含义
---    | ---                   | ---
200    | OK                    | 请求被服务器正常处理
204    | No Content            | 请求已成功处理，但是没有内容返回
206    | Partial Content       | 范围请求被成功处理，并返回指定范围的内容
301    | Moved Permanently     | 请求的资源已被永久重定向到其他位置
302    | Found                 | 请求的资源被临时重定向到其他位置
303    | See Other             | 应使用 GET 请求新 URI 定向获取请求资源
304    | Not Modified          | 附带条件的请求（if-modified-since）得到了条件不满足的应答
307    | Temporary Redirect    | 与 302 含义相同，但严格遵守禁止 POST 变 GET 的标准
400    | Bad Request           | 请求报文中存在语法错误或参数错误，服务器不理解
401    | Unauthorized          | 发送的请求需要有 HTTP 认证信息或者认证失败了
403    | Forbidden             | 对请求资源的访问被服务器拒绝了
404    | Not Found             | 服务器找不到请求的资源
500    | Internal Server Error | 服务器质性请求的时候出错了
503    | Service Unavailable   | 服务器超负载或正停机维护，无法处理请求



























































