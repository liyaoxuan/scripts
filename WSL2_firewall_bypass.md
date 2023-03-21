1. 创建任务计划程序，命名为**WSL2-firewall-bypass**，设置操作为启动程序，程序和参数如下
   
   ```powershell
   cmd /c start "" /min powershell -WindowStyle hidden -c Get-NetFirewallRule -DisplayName 'WSL' | Get-NetFirewallInterfaceFilter -AssociatedNetFirewallRule ^|Set-NetFirewallInterfaceFilter -InterfaceAlias 'vEthernet (WSL)'
   ```
   
   2.在WSL的`.zshrc`中添加如下内容
   
   ```bash
   ret=$(schtasks.exe /run /tn "WSL2-firewall-bypass")
   if [ ${ret:0:7} != "SUCCESS" ]; then
       echo $ret
   fi
   ```
   
   