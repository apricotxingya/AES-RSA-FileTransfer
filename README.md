# AES-RSA-FileTransfer  

## 0x00 简介  
**windows下用AES，RSA来实现文件的加密安全传输**  
具体使用python的`pycrypto`、`m2crypto`两个模块来实现  

## 0x01 大概思路  
Alice拥有： AES秘钥，Bob公钥，Alice的私钥  
Bob拥有：Alice的公钥，Bob的私钥   

大概思路就是Alice先用AES加密文件，然后拿Bob的RSA公钥加密AES秘钥；  
Bob接收到加密文件之后，用自己的RSA私钥解密出AES秘钥，再解密文件。  
另外还有MD5签名，可以验证文件的完整性  

## 0x02 流程图  
Alice加密流程图：  
![加密](data:image/jpeg;base64,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)    
Bob解密流程图：  
![解密](data:image/jpeg;base64,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)

## 0x03 实际加解密流程  

**加密**
```
这是一个加解密文件程序，请按照提示输入！

请选择：
1.加密文件  2.解密文件 3.退出
> 1
请把以下文件放在与此程序同一路径下：
1.要加密的文件
2.AES秘钥文件
3.你的RSA私钥文件
4.接收者的RSA公钥文件
放好之后，回车继续
> 
请输入要加密的文件名:
> new.txt
请输入AES秘钥文件名：
> AES_key
开始对原文件进行AES加密......
要加密文件的长度是：  242
需要填充的数据长度 :  14
原文件AES加密完成！
开始对原文件进行MD5摘要
MD5摘要完成！
请输入你的RSA私钥文件名：
> Alice_private_key
开始对MD5摘要签名
MD5摘要签名完成！
对签名进行AES加密
要加密文件的长度是：  256
需要填充的数据长度 :  0
签名AES加密完成！
请输入接收者RSA公钥文件名：
> Bob_public_key
开始对AES秘钥进行RSA加密
AES秘钥RSA加密完成！
开始对iv进行RSA加密
对iv的RSA加密完成！
加密过程结束！
你需要发送给接收者的文件有：
1.已加密文件：file_encrypted
2.加密后的AES秘钥文件：AES_key_encrypted
3.AES加密后的初始化向量文件：file_iv_encrypted
4.加密后的签名文件：file_signature_encrypted
5.填充位数文件：fill_number

最后请删除程序所在路径下加入和生成的文件，谢谢！
回车结束程序
```




**解密**  

```
这是一个加解密文件程序，请按照提示输入！

请选择：
1.加密文件  2.解密文件 3.退出
> 2
请把以下文件放在与此程序同一路径下：
1.加密的文件
2.加密的AES秘钥文件
3.加密的签名文件
4.加密的iv文件
5.你的RSA私钥文件
6.发送者的RSA公钥文件
7.填充位数文件
放好之后，回车继续
> 
请输入加密的AES秘钥文件名：
> AES_key_encrypted
请输入加密的AES初始化向量文件名：
> file_iv_encrypted
请输入你的RSA私钥文件名：
> Bob_private_key
开始解密AES秘钥
AES秘钥解密完成！
开始解密AES初始化向量
AES初始化向量解密完成！
请输入加密的文件名：
> file_encrypted
请输入填充位数文件名：
> fill_number
开始对加密文件进行AES解密
加密文件AES解密完成！
请输入加密的签名文件名：
> file_signature_encrypted
加密签名文件AES解密
加密签名文件AES解密完成！
请输入发送者的公钥文件名：
> Alice_public_key
开始签名文件RSA解密
签名文件RSA解密完成，得到原文件MD5值！
MD5值校验成功！
解密程序运行完毕，请提取解密文件，并删除此程序所在路径下导入及生成的文件，谢谢！
回车结束程序
```

## 0x04 环境配置  
用virtualenv配个虚拟环境最好了，我配了下发现有20M，就不上传了  
virtualenv生成虚拟环境之后，执行下面2条命令安装：  
`pip install pycrypto`  
`pip install M2CryptoWin32`  
M2CryptoWin64可以自行测试  

## 0x05 其他  
还有一个不用输这么多名字的版本，就是那些文件的名字都已经固定了，需要一开始把对应的文件改成相应的名字  
