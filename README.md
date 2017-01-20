# Windows Testing Deployment
Some trickys & settings for function testing smoothly about Windows.


## 1. Windows disable Hibernate

	powercfg -h off


## 2. Close Windows System UAC

	Control Panel->User Accounts and Family Safety->User Accounts->Change User Accounts Control Setting -> Never Notify.


## 3. Touchpad setting, enable scrollbar function


## 4. 将外置 Audio Jack 选项勾掉， Which device did you plug in? ->Mic in ->将勾去掉 -> OK


## 5. 将电源管理设成 "Do nothing" 和 "Never"


## 6. 系统保护关闭，system protection->local disk on -> configure-> Turn off system protection-> OK


## 7. NPI 阶段蓝屏之后将系统设为不重启


## 8. 在 DOS 分区中 C:\ 写一个标志文件 "%model%.flg"


## 9. 上传 Image 之前需要删除 Testlog 目录所有文件


## 10. win8 UAC调至最低
 * 一种方法是修改注册表:HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System 
 	EnableLua=0 (dword) 

 * 第二中方法是修改策略管理器,修改之后你的身份就是超级管理员.以管理员身份运行cmd,输入"gpedit.msc"打开组策略管理器,点击"Windows       Settings"-->"Security Settings"--->"Local Policies"--->"Security Options"--->从右边的选项中选择(在比较靠下的位置)"User  Account Control:Run all administrators in Admin Approval mode"中把"Enabled"设置成"Disabled".重新启动即可.


## 11. 有些程序的运行需要 Framwork 的运行环境,比如键盘设置的tool

装载.framework环境.先提取出"[Windows 8 企业版 RTM 64Bit 官方原版镜像]来自 Connect .ISO",然后打开cmd窗口运行"Dism /online /enable-feature /featurename:NetFx3 /All /Source:D:\sources\SxS /LimitAccess"其中"D:"可以自行修改,对应的是你已经提取出来的ISO中文件存放在的硬盘盘符.等运行完成之后会提示"Successfully"提示.在控制面板已安装程序中可以找到.Framework环境安装好了.


## 12. Win8下设置及其不自动进入S4(默认是在屏幕IDLE状况下超过180分钟，自动进入S4冬眠模式).

右键win8桌面右下角的电源---选择"Power Options"---选择"Change plan settings"---选择"change advanced power settings"---选择"Sleep"选项并打开---将"Hibernate after battery/ plugged in 180 minutes"手动均设置成"Never"


## 13. RTL网卡在M2需要将EC里的MAC ID重新写入LAN Chip

用PG Tool检查MACID写入正确

## 14 .避免 DELL WBDD 跑 Memory 報錯

	control panel>all control panel items>administrative tools>local Secrity policy>user rights assignment>lock pages in memory>every one

## 15. NPI 阶段某些 driver 未经 Microsoft 认证，需 enable Test mode 才可正常安装使用

	bcdedit -set TESTSIGNING ON

## 16.  Run Media Player Application in clean OS image


## 17. Windows Defender是微软自带的一个可以监听间谍软件和系统保护的服务，如果你已经安装了第三方的杀毒软件或者管家后，可以选择关闭该项功能以节省系统资源。

 * 1. 使用WIN+R组合键，调出运行窗口，然后输入“gpedit.msc”命令，回车
 * 2. 在打开的本地组策略窗口左侧，依次点击“计算机配置”--“管理模板”--“Windows 组件”--“Windows Defender”，然后在右侧找到“关闭Windows Defender”,双击打开
 * 3.在打开的设置窗口里，我们会看到默认设置“未设置”选项，我们更改为“已启用”，然后点击下方的“应用”按钮。
 * 4. 再次使用WIN+R组合键打开运行窗口，输入“gpupdate /force”命令，回车
 * 5. 此时系统会刷新你刚才的组策略设置，如果提示成功，则表示已经成功关闭了Windows Defender功能了。
 * 

## 18. 测试 Image build 好后把产线测试治具都插到机器上识别一次（Camera, USB）,最好每个 Config 都做一次识别


## 19. 验证 Wlan driver 是否可以下 command 自动安装