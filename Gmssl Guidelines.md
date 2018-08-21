### Gmssl Guidelines

---

*Edited  by ~April at 2018/08/21*

[TOC]

#### 背景知识

> 国密算法是国家商用密码算法的简称。自2012年以来，国家密码管理局以《中华人民共和国密码行业标准》的方式，陆续公布了SM2/SM3/SM4等密码算法标准及其应用规范。其中“SM”代表“商密”，即用于商用的、不涉及国家秘密的密码技术。其中 **SM2为基于椭圆曲线密码的公钥密码算法标准，包含数字签名、密钥交换和公钥加密，用于替换RSA/Diffie-Hellman/ECDSA/ECDH等国际算法；SM3为密码哈希算法，用于替代MD5/SHA-1/SHA-256等国际算法；SM4为分组密码，用于替代DES/AES等国际算法；SM9为基于身份的密码算法，可以替代基于数字证书的PKI/CA体系。** 通过部署国密算法，可以降低由弱密码和错误实现带来的安全风险和部署PKI/CA带来的开销。												-- 参见 gmssl.org



#### gmssl命令行

```code
#sm4 加密, 回车后输入密码
$ gmssl sms4 -e -in <yourfile> -out <yourfile>.sms4

#sm4 解密
$ gmssl sms4 -d -in <yourfile>.sms4

#生成 sm3摘要
$ gmssl sm3 <yourfile>

#生成 sm2私钥 并 签名
$ gmssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:sm2p256v1 \
                -out signkey.pem
$ gmssl pkeyutl -sign -pkeyopt ec_scheme:sm2 -inkey signkey.pem \
                -in <yourfile> -out <yourfile>.sig

#从私钥 导出 公钥 用于 验签
$ gmssl pkey -pubout -in signkey.pem -out vrfykey.pem
$ gmssl pkeyutl -verify -pkeyopt ec_scheme:sm2 -pubin -inkey vrfykey.pem \
                -in <yourfile> -sigfile <yourfile>.sig

#生成 sm2私钥 及 证书请求(需要配置openssl)
$ gmssl ecparam -genkey -name sm2p256v1 -text -out user.key
$ gmssl req -new -key user.key -out user.req

查看证书请求
gmssl req -in user.req -noout -text -subject
```



#### 什么是证书请求

1. 生成客户端的密钥，即客户端的公私钥对，且要保证私钥只有客户端自己拥有。
2. 以客户端的密钥和客户端自身的信息(国家、机构、域名、邮箱等)为输入，生成证书请求文件。其中 **客户端的公钥和客户端信息是明文保存在证书请求文件中的**，而客户端私钥的作用是对客户端公钥及客户端信息做签名，自身是不包含在证书请求中的。然后 **把证书请求文件发送给CA机构**。
3. CA机构接收到客户端的证书请求文件后，首先校验其签名，然后审核客户端的信息，最后 **CA机构使用自己的私钥为证书请求文件签名，生成证书文件，下发给客户端**。此证书就是客户端的身份证，来表明用户的身份。



--未完待续



#### 参考资料

1. [Gmssl官网](http://gmssl.org/docs/quickstart.html )
2. [[openssl 证书请求和自签名命令req详解](https://www.cnblogs.com/gordon0918/p/5409286.html)]





