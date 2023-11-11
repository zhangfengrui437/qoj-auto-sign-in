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
