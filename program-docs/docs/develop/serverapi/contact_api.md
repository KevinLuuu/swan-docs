---
title: 消息推送介绍
header: develop
nav: serverapi
sidebar: contact_api
---

 

1. 使用超级管理员或管理员账号登录开发者平台后，按提示填写相关信息，具体如下：

- URL: 开发者用来接收消息的接口 URL。开发者所填写的URL 必须以 http:// 或 https:// 开头，分别支持 80 端口和 443 端口。
- Token: 可由开发者可以任意填写，用作生成签名（该 Token 会和接口 URL 中包含的 Token 进行比对，从而验证安全性）。
- EncodingAESKey: 由开发者手动填写或随机生成，将用作消息体加解密密钥。
- 消息加解密方式：明文模式（默认）.兼容模式和安全模式。可以选择消息数据格式：XML 格式（默认）或 JSON 格式。

2. 验证消息的确来自百度服务器

开发者提交信息后，百度服务器将发送POST请求到填写的服务器地址URL上，POST请求携带参数如下表所示：

| 参数      | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| signature | 百度加密签名，signature结合了开发者填写的token参数和请求中的timestamp参数.nonce参数。 |
| timestamp | 时间戳                                                       |
| nonce     | 随机数                                                       |
| echoStr   | 随机字符串                                                   |

开发者通过检验 signature 对请求进行校验（下面有校验方式）。若确认此次 POST 请求来自百度服务器，请原样返回 echoStr 参数内容，则接入生效，成为开发者成功，否则接入失败。加密/校验流程如下：

1. 将token.timestamp.nonce三个参数进行字典序排序
2. 将三个参数字符串拼接成一个字符串进行sha1加密




