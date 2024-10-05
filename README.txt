喜欢的请在Github上给个Star喵~

具体EFI、OC、BIOS怎么配置请自行百度，网上教程很多。如果是y7000p2020H，则可以直接使用本EFI，无需做任何修改。BIOS的设置自行更改

注意：
  1）本EFI仅对10300H/10750H/10875H处理器的config进行了修改，其余cpu序号的需要自行使用OCAT工具，对照config.plist修改对应CPU型号的config
  2）原生WIFI和蓝牙驱动需要在正常启动Mac系统后使用OpenCore_Patcher进行Patch才可生效
  3）使用OTA升级系统前请升级OpenCore和Kext驱动版本至最新，避免OTA后无法进入系统

OCAT下载地址：https://github.com/ic005k/OCAuxiliaryTools/releases
OpenCore_Patcher下载地址：https://github.com/dortania/OpenCore-Legacy-Patcher/releases

以下部分来自https://github.com/xiaoMGitHub/LEGION_Y7000Series_Hackintosh，本EFI是在此基础上进行的升级，感谢xiaoMGithub

1、使用前准备
   1）从github的仓库中下载一键修改BIOS工具（https://github.com/xiaoMGitHub/LEGION_Y7000Series_Insyde_Advanced_Settings_Tools）
   2) 解压后，双击批处理脚本
   3）依次执行 2、4、5
   4）如果是八代处理器则需要额外多执行 1
   5）重启

2、替换EFI，成功进入MacOS后，打开终端执行下面的命令

   sudo sh -c "$(curl -fsSL https://gitee.com/xiaoMGit/Y7000Series_Hackintosh_Fix/raw/master/Script/Optimize.sh)"

3、小键盘相关设置（8代处理器的机器不需要执行）

  1）已经执行了上面的步骤，8代处理器的机器不需要执行
  2）打开终端执行 open /usr/local/bin/
  3）打开 系统偏好设置 > 安全性与隐私 > 隐私 > 辅助功能
  4）将 setleds 添加到辅助功能

4、屏蔽PM981、PM981a、自带镁光、自带海力士固态

   1) 打开 EFI/OC/config.plist
   2) 搜索 SSDT-DNVMe.aml
   3）将上方的 <key>Enabled</key> 修改为 <key>Enabled</key>
	     <false/>                 <true/>

5、处理器型号为10300H/10750H/10875H的机器需要特别设置
   1）进 BIOS 
   2）设置 Configuration 中的 DPTF 为 Disabled
   3）这样设置的好处是可以通过 ACPI 补丁来禁用独显降低黑果功耗
   4）该选项使用本 EFI 为必须设置

6、开启休眠（hibernatemode 25）
   1）适用8代、10代处理器，9代处理器不提供支持，留点空间给某些人折腾，请支持原创
   2）使用最新的EFI
   3）上述步骤2中的命令执行7即可

7、触控板带实体按钮的机型设置
   1）系统偏好设置 > 触控板 > 取消勾选"用力点按和触感反馈"
   2）该设置主要是针对2018款的y7000以及部分2019款y7000