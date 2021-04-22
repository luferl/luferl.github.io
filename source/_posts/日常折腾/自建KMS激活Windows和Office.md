---
title: 自建KMS激活Windows和Office
date: 2021-04-22 09:43:56
tags: [日常折腾]
categories: 日常折腾
---
&emsp;&emsp;KMS在服务器可用的情况下会自动续期，只要不关闭KMS的服务或计划任务，所以并不需要180天手动激活一次。
# Windows激活
&emsp;&emsp;下文提供了各个windows版本的GVLK秘钥，可以在安装系统时即输入该初始秘钥，也可安装后手动设置。

&emsp;&emsp;激活方式:  
&emsp;&emsp;以管理员身份运行 Windows PowerShell或CMD，输入如下命令。
```cmd
#如果安装时即输入了初始秘钥，可以跳过前两步。
slmgr /upk
# 卸载当前产品密钥
slmgr /ipk 秘钥序列号
# 安装产品密钥 (参考下文 GVLK 密钥)
slmgr /skms kms.xxxxx.com
# 设置 KMS 服务器
slmgr /ato
# 立即激活
slmgr /xpr
# 查看激活剩余时间
slmgr /dlv
# 查看激活详细信息
```
## Windows 10
|操作系统版本|KMS 客户端安装程序密钥|
|-|-|
|Windows 10 专业版|W269N-WFGWX-YVC9B-4J6C9-T83GX|
|Windows 10 专业版 N|	MH37W-N47XK-V7XM9-C7227-GCQG9|
|Windows 10 专业工作站版|	NRG8B-VKK3Q-CXVCJ-9G2XF-6Q84J|
|Windows 10 专业工作站版 N|	9FNHH-K3HBT-3W4TD-6383H-6XYWF|
|Windows 10 专业教育版|	6TP4R-GNPTD-KYYHQ-7B7DP-J447Y|
|Windows 10 专业教育版 N|	YVWGF-BXNMC-HTQYQ-CPQ99-66QFC|
|Windows 10 教育版|	NW6C2-QMPVW-D7KKK-3GKT6-VCFB2|
|Windows 10 教育版 N|	2WH4N-8QGBV-H22JP-CT43Q-MDWWJ|
|Windows 10 企业版|	NPPR9-FWDCX-D2C8J-H872K-2YT43|
|Windows 10 企业版 N|	DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4|
|Windows 10 企业版 G|	YYVX9-NTFWV-6MDM3-9PT4T-4M68B|
|Windows 10 企业版 G N|	44RPN-FTY23-9VTTB-MP9BX-T84FV|
|Windows 10 企业版 LTSC 2019|	M7XTQ-FN8P6-TTKYV-9D4CC-J462D|
|Windows 10 企业版 N LTSC 2019|	92NFX-8DJQP-P6BBQ-THF9C-7CG2H|
## Windows 7
|操作系统版本|KMS 客户端安装程序密钥|
|-|-|
|Windows 7 专业版|	FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4|
|Windows 7 专业版 N|	MRPKT-YTG23-K7D7T-X2JMM-QY7MG|
|Windows 7 专业版 E|	W82YF-2Q76Y-63HXB-FGJG9-GF7QX|
|Windows 7 企业版|	33PXH-7Y6KF-2VJC9-XBBR8-HVTHH|
|Windows 7 企业版 N|	YDRBP-3D83W-TY26F-D46B2-XCKRJ|
|Windows 7 企业版 E|	C29WB-22CC8-VJ326-GHFJW-H9DH4|
## Windows 8
|操作系统版本|	KMS 客户端安装程序密钥|
|-|-|
|Windows 8.1 专业版|	GCRJD-8NW9H-F2CDX-CCM8D-9D6T9|
|Windows 8.1 专业版 N|	HMCNV-VVBFX-7HMBH-CTY9B-B4FXY|
|Windows 8.1 企业版|	MHF9N-XY6XB-WVXMC-BTDCT-MKKG7|
|Windows 8.1 企业版 N|	TT4HM-HN7YT-62K67-RGRQJ-JFFXW|
|Windows 8 专业版|	NG4HW-VH26C-733KW-K6F98-J8CK4|
|Windows 8 专业版 N|	XCVCF-2NXM9-723PB-MHCB7-2RYQQ|
|Windows 8 企业版|	32JNW-9KQ84-P47T8-D8GGY-CWCK7|
|Windows 8 企业版 N|	JMNMF-RHW7P-DMY6X-RF3DR-X2BQT|
## Windows Server
|操作系统版本|	KMS 客户端安装程序密钥|
|-|-|
|Windows Server Datacenter|	6NMRW-2C8FM-D24W7-TQWMY-CWH2D|
|Windows Server Standard|	N2KJX-J94YW-TQVFB-DG9YT-724CC|
|Windows Server 2019 Datacenter|	WMDGN-G9PQG-XVVXX-R3X43-63DFG|
|Windows Server 2019 Standard|	N69G4-B89J2-4G8F4-WWYCC-J464C|
|Windows Server 2019 Essentials|	WVDHN-86M7X-466P6-VHXV7-YY726|
|Windows Server 2016 Datacenter|	CB7KF-BWN84-R7R2Y-793K2-8XDDG|
|Windows Server 2016 Standard|	WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY|
|Windows Server 2016 Essentials|	JCKRF-N37P4-C2D82-9YXRT-4M63B|
|Windows Server 2012 R2 Server Standard|	D2N9P-3P6X9-2R39C-7RTCD-MDVJX|
|Windows Server 2012 R2 Datacenter|	W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9|
|Windows Server 2012 R2 Essentials|	KNC87-3J2TX-XB4WP-VCPJV-M4FWM|
|Windows Server 2012|	BN3D2-R7TKB-3YPBD-8DRP2-27GG4|
|Windows Server 2012 N|	8N2M2-HWPGY-7PGT9-HGDD8-GVGGY|
|Windows Server 2012 单语言版|	2WN2H-YGCQR-KFX6K-CD6TF-84YXQ|
|Windows Server 2012 特定国家/地区版|	4K36P-JN4VD-GDC6V-KDT89-DYFKP|
|Windows Server 2012 Server 标准版|	XC9B7-NBPP2-83J2H-RHMBY-92BT4|
|Windows Server 2012 MultiPoint 标准版|	HM7DN-YVMH3-46JC3-XYTG7-CYQJJ|
|Windows Server 2012 MultiPoint 高级版|	XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G|
|Windows Server 2012 Datacenter|	48HP8-DN98B-MYWDG-T2DCC-8W83P|
|Windows Server 2008 R2 Web 版|	6TPJF-RBVHG-WBW2R-86QPH-6RTM4|
|Windows Server 2008 R2 HPC 版|	TT8MH-CG224-D3D7Q-498W2-9QCTX|
|Windows Server 2008 R2 标准版|	YC6KT-GKW9T-YTKYR-T4X34-R7VHC|
|Windows Server 2008 R2 企业版|	489J6-VHDMP-X63PK-3K798-CPX3Y|
|Windows Server 2008 R2 Datacenter|	74YFP-3QFB3-KQT8W-PMXWJ-7M648|
|面向基于 Itanium 系统的 Windows Server 2008 R2	|GT63C-RJFQ3-4GMB6-BRFB9-CB83V|
|Windows Web Server 2008|	WYR28-R7TFJ-3X2YQ-YCY4H-M249D|
|Windows Server 2008 标准版|	TM24T-X9RMF-VWXK6-X8JC9-BFGM2|
|不带 Hyper-V 的 Windows Server 2008 标准版|	W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ|
|Windows Server 2008 企业版|	YQGMW-MPWTJ-34KDK-48M3W-X4Q6V|
|不带 Hyper-V 的 Windows Server 2008 企业版|	39BXF-X8Q23-P2WWT-38T2F-G3FPG|
|Windows Server 2008 HPC|	RCTX3-KWVHP-BR6TB-RB6DM-6X7HP|
|Windows Server 2008 Datacenter|	7M67G-PC374-GR742-YH8V4-TCBY3|
|不带 Hyper-V 的 Windows Server 2008 数据中心版|	22XQ2-VRXRG-P8D42-K34TD-G3QQC|
|面向基于 Itanium 系统的 Windows Server 2008|	4DWFP-JF3DJ-B7DTH-78FJB-PDRHK|
# Office激活
&emsp;&emsp;使用KMS激活Office，需要安装`VOL（批量版）`版本。  
&emsp;&emsp;可以自行下载所需版本的VOL安装包，VOL会自带初始秘钥，无需手动填写。

&emsp;&emsp;强烈推荐使用Office Tool Plus进行安装，同时更推荐用这个工具来卸载老版本的Office。  
&emsp;&emsp;https://otp.landian.vip/zh-cn/。
## Office Tool Plus激活
&emsp;&emsp;打开Office Tool Plus，进入部署功能，选择所需版本的批量授权版，进行安装，由于Office套装不带Visio，我这里还额外添加了Visio，选好之后点右上角“开始部署”即可。

![部署](https://pic.lufer.cc/images/2021/04/22/image.png)

&emsp;&emsp;随后会进入自动安装过程。

![开始安装](https://pic.lufer.cc/images/2021/04/22/image5b3b15c6e68d1379.png)

返回首页，进入激活功能。

![激活界面](https://pic.lufer.cc/images/2021/04/22/imagec0f74af727608cab.png)

&emsp;&emsp;展开许可证管理，选择刚才安装的产品，然后安装许可证。  
&emsp;&emsp;如果安装了其他产品，需要都安装许可证，例如我装了Visio，就还要在安装一次Visio的许可证。  
&emsp;&emsp;展开KMS管理，输入KMS主机地址，点击保存设置。  
&emsp;&emsp;最后点击右上角激活。

&emsp;&emsp;成功激活。

![激活成功](https://pic.lufer.cc/images/2021/04/22/imaged294b529ce92b2cf.png)

## 手动激活
&emsp;&emsp;以Office2016为例，查找 Office 安装目录，默认情况下 Office 2016 64 位版安装目录为`C:\Program Files\Microsoft Office\Office16`，其他版本请自行查找。  
&emsp;&emsp;以管理员身份运行 Windows PowerShell或CMD，输入如下命令。
```cmd
cd "C:\Program Files\Microsoft Office\Office16"
# 进入 Office 安装目录,请自行根据安装的 Office 版本修改目录.
cscript ospp.vbs /dstatus
# 查看当前激活状态,期限,版本,密钥等信息.安装 VOL 版 Office 默认情况下已安装产品密钥.继续执行以下步骤激活.
cscript ospp.vbs /sethst:kms.xxxxx.com
# 设置 KMS 服务器
cscript ospp.vbs /act
# 立即激活
```
