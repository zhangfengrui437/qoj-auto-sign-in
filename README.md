##你好，我是一个c2026届的蒟蒻，我叫张锋睿，我也在弄这个签到，无意间发现您也在弄，~~我就是个蒟蒻~~，我发现最近qoj的证书出问题了，所以最近几天都无法登陆，要把那个py文件里的代码改一改才行，我给您看一下我的代码。————2024.10.12
```python
import hmac as hash
from re import search,M
from requests import get,post
from requests.utils import dict_from_cookiejar
from os import getenv
headers={"User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.122 Safari/537.36 SE 2.X MetaSr 1.0"}
username="XXXXXXXXXXXX"
password=hash.new("FEqAm2pnA6Ed622VqmqLuSKdJ2WJplCT".encode(),"##############".encode(),"MD5").hexdigest()
r1=get("https://qoj.fzoi.top",headers=headers,verify=False)
cookie1=dict_from_cookiejar(r1.cookies)
r2=get("https://qoj.fzoi.top/login",headers=headers,cookies=cookie1,verify=False)
text=r2.text
jntm=search(r"_token : \"([A-Za-z0-9]+)\"",text,M)
if jntm==None:
    print("Error!")
    exit()
token=jntm.group(1)
r3=post("https://qoj.fzoi.top/login",cookies=cookie1,headers=headers,data={"username":username,"password":password,"ip":"","_token":token,"response":"","login":""},verify=False)
cookie2=dict_from_cookiejar(r3.cookies)
if cookie2=={}:
    print("Something Wrong!")
    exit()
cookie1.update(cookie2)
get("https://qoj.fzoi.top/punch",headers=headers,cookies=cookie1,verify=False)
print("OK!{}".format(username))
get("https://qoj.fzoi.top/logout",headers=headers,cookies=cookie1,params={"_token":token},verify=False)
```
# qoj自动签到
1. Fork/Import code这个仓库（最好Import code成私有仓库）
2. 打开`qoj_login.py`，将`XXXXXXXX`改为qoj用户名，将`########`改为qoj密码
3. （你可以去点一下`Actions`，然后点击`qojqiandao`，点一下`run workflows`并选择`run`，如果成功签到，接下来开始设置定时服务，若没有`Actions`，请选择`Settings`>`Actions`>`General`>`Allow all actions and reusable workflows`，并点击`save`）
4. 打开`.github/workflows/main.yml`，将以下代码
   ``` ymal
   on: workflow_dispatch
   ```
   改为
   ``` ymal
   on: 
      workflow_dispatch: 
      schedule:
         - cron: 0 22 * * *
   ```
