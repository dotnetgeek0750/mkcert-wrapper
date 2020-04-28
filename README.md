- 什么是mkcert-wrapper


mkcert-wrapper是一款基于mkcert制作的工具，可以：
- [x] 同时生成IIS、Nginx证书
- [x] 部门以前负责证书维护的同事离职了，使用mkcert-wrapper无缝迁移
- [x] 维护域名列表清晰明了
- [x] 使用方便，下载到任意本地磁盘合法目录都可运行



- 怎么使用mkcert-wrapper

1. 从github下载本目录到电脑磁盘上，注意存放的路径不能有 “-”、“中文” 等特殊符号
2. 带上你学习mkcert的知识，将你日后要制作证书的签发机构rootCA.pem、rootCA-key.pem 放进CAROOT文件夹中
3. 用记事本打开Gen.bat文件
4. 在域名列表上，增加或者删除域名，有三个注意事项：
- [x] 域名支持*通配符格式,但只支持一个层级，比如 *.abc.com，能匹配 x.abc.com，但不匹配x.y.abc.com；
- [x] 每一行的域名行头要有一个空格符；
- [x] 非最后一行域名的结尾，要有一个换行符 ^
5. 保存Gen.bat文件，然后双击运行，证书就生成在OUTPUT目录里。
6. 使用OUTPUT里的证书去安装




-  Gen.bat示例

```
cd "%~dp0"
set CAROOT=%~dp0\CAROOT

@echo +++++++Generate IIS Cert +++++++

mkcert -pkcs12 -p12-file %~dp0\OUTPUT\server.pfx^
 "*.domain.com"^
 "*.dev.domain.com"^
 "aaaa.domain.com"


@echo +++++++ Generate Nginx Cert +++++++

mkcert -cert-file  %~dp0\OUTPUT\server.crt -key-file %~dp0\OUTPUT\server.key^
 "*.domain.com"^
 "*.dev.domain.com"^
 "aaaa.domain.com"

pause
```
