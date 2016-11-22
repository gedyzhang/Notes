# install-workstation12-and-centso7
记录一下我在安装VMware workstation12和centos7过程中遇到的一些问题
###输入许可秘钥点击继续时提示“您无权输入许可秘钥，请使用系统管理员权限重试”
运行exe时，右击-以管理员身份运行，等安装完出现vmware图标后，依旧右击以管理员身份运行，输入密钥就可以了
###VMware Workstation 12序列号：
5A02H-AU243-TZJ49-GTC7K-3C61N，此序列号仅供个人学习交流使用，不可用作商业用途
###安装VM时出现failed to install the hcmon driver
进入C:\Windows\System32\drivers，删掉hcmon.sys文件，重新安装即可
