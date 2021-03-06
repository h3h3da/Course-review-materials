# 密码学部分

## 应用密码学提纲

### 密码杂凑函数
1. 密码杂凑函数的定义和安全性：抗原性攻击、抗第二原像攻击、抗碰撞
2. 密码杂凑函数的比特安全性及原理
3. 常用密码杂凑函数极其构造方式、杂凑值长度和安全性
4. 密码杂凑函数的应用

### 分组密码
1. 对加密通信的攻击：选择明文攻击、选择密文攻击
2. 分组密码的定义
3. 分组密码的两种典型构造：Feistel网络和S-P网络
4. 常用分组密码极其构造方式、密钥长度和安全性
5. 分组密码的模式（加密模式）

### 序列密码
1. One-Time Pad
2. 序列密码的概念及其与分组密码的区别

### MAC和AEAD
1. 完整性（Integrity）及其对安全性的影响
2. MAC（消息认证码）算法的定义
3.AEAD的定义
4. 常用的MAC算法和AEAD模式

### 密码分析
1. 差分密码分析
2. 线性密码分析

### 公钥密码
1. 单向函数和单向陷门函数的定义和实例
2. 群、环、域的定义和实例
3. 公钥加密（Public Key Encryption）的定义
4. 欧几里得算法和扩展欧几里得算法
5. Diffie-Hellman、ElGamal加密算法
6. 椭圆曲线的定义和椭圆曲线算术：点加、倍点、点的标量乘法（PPoint Scalar Multiplication）
7. 椭圆曲线困难问题ECDLP
8. 椭圆曲线密钥长度和比特安全性的关系

### 素数和素性测试
1. 素数、本原根（Primitive Roots）的定义
2. 费马小定理、欧拉公式
3. 素数生成算法
4. Miller-Rabin素性测试算法

### RSA算法
1. RSA加密、RSA签名
2. 为什么教科书中的RSA算法不安全
3. RSA的填充方案

### 数字证书与PKI
1. 数字签名的概念与典型数字签名suanfa
2. 数字证书、根证书、证书链、CA、PKI的概念，通过浏览器观察网站的证书链，了解现实中证书的各个域、DV/EV/OV证书的区别
3. 基于身份的密码（Identity-Based Cryptography）的定义、典型构造、应用以及和传统公钥密码/PKI的区别


### 数学困难问题
1. 离散对数问题、椭圆曲线离散对数问题、证书分解问题、DH问题、ECDH问题、RSA问题
2. 平滑数的概念及其作用
3. 大步小步法和Pohlig-Hellman算法

### 硬件安全
1. 密码硬件安全等级1~4级的主要特征
2. 侧信道攻击的种类

### 密文计算算法
1. 同态加密、基于属性的加密（Attribute-Base Encryption）、可搜索加密、秘密共享/秘密分割、零知识证明、承诺、隐私信息获取（PIR）、不经意传输（OT）的基本概念和应用场景
2. 典型同态加密算法支持的密文计算能力（明文类型和支持的计算类型、数量）

