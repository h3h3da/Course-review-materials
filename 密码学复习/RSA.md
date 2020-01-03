# RSA

## RSA加密算法

生成素数p,q，令n=pq，![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibuzcm84j304m00i0kz.jpg)

1. 选择e，使![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibw14pguj303g00i0iy.jpg)
2. 计算![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibxeh824j304d00k0l6.jpg)
3. 公钥：n、e
4. 私钥：d、n
5. 加密时，发送方计算![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibxtv5ecj303t00i0iw.jpg)
6. 解密时，接收方计算![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibyaij0vj308n00k0ob.jpg)

7. 例题

```
1. 在RSA算法中,已知p=3,q=11,公钥(加密密钥)e=7,明文M=5,求欧拉凼数fΦ(n) ; 私钥d 和密文C；

解：
n = pq = 33
phi(n)=(p-1)(q-1) = 2 * 10 = 20
ed = 1 mod (\phi(n))
用扩展欧几里德可求出 d = 3 （直接看出来也可以.）
加密 密文C = (M^e)mod n = (5^7)mod 20 = 5
解密 明文M = (C^d)mod n = (5^3)mod 20 = 5

2. RSA算法中,素数p=7,q=11,加密密钥e=7,计算解密密钥d

解：
N=pq=7*11=77
(p-1)(q-1)=6*10=60
根据公式d× e ≡ 1 (mod (p-1)(q-1))
又e=7,所以 7*d≡ 1 (mod 60).即 7d mod 60 = 1.
7x43=301.301除以6刚好余1.
所以d=43

3. 已知RSA算法中,素数p=5,q=7,模数n=35,公开密钥e=5,密文c=10,求明文m

解：
Φ(n)=4*6=24,设私钥为d,由de ≡ 1 mod 24,即5d ≡ 1 mod 24,得d=5；
m = (c^d) mod 24 = 16
```


## RSA签名

1. 签名时计算![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibyse2qaj301n00g0aq.jpg)，D表示待签名的文档
2. 验证时，计算![](https://tva1.sinaimg.cn/large/006tNbRwly1gaibz9iwwhj300i00d07b.jpg)是否等于D
3. RSA-PSS签名方案

## RSA的安全性

RSA可能受到如下5种方式的攻击：

· 穷举攻击：试图穷举所有可能的密钥

· 数学攻击：试图分解两个素数的乘积

· 基于硬件故障的攻击：这种方法应用产生签名过程中处理器发生的故障

· 计时攻击：依赖于解密算法的运行时间

· 选择密文攻击：利用了RSA算法的性质

RSA抗穷举攻击的方式是使用大的密钥空间，所以e和d的位数越大越好，但是密钥产生的过程和加/解密过程都包含了复杂的计算，密钥越大，系统的运行速度越慢

### 对RSA的攻击方式
· 攻击思路：分解n为两个素因子p,q。这样可以计算出φ(n)=(p-1)(q-1)，从而可以确定d=e^(-1) mod φ(n) 

· 现在已知的，从e和n确定d的算法时间复杂度至少和因子分解问题一样。因此可以将因子分解的性能作为基准来评价RSA的安全性

· 20世纪90年代一直采用的是二次筛法来进行因子分解。

· 而新的算法：一般数域筛法，可以对RSA-130进行攻击，能够分解比RSA-129更大的数而且计算代价仅为二次筛法的20%

## RSA的填充方案
· 为了防止RSA受到选择密文攻击，RSA公司推荐使用 最优非对称加密填充（OAEP）的方案

· OAEP算法：
```
1. 明文M被填充padding
2. 可选参数集P作为hash函数的输入，输出产生H(P),并用0填充以达到期望长度
3. 将M+padding+H(P)放入数据块DB内
4. 选择一个随机种子作为hash函数的输入，该hash函数称为掩码生成函数（MGF）
5. 将输出的哈希值与DB做异或运算，产生掩码DB（maskedDB）
6. 掩码DB作为MGF的输入，产生一个hash值，该hash值与随机种子进行异或，产生掩码种子
7. 掩码种子和掩码DB连接起来构成消息EM，完成消息的填充
8. 最后直接用RSA对EM进行加密即可
```

