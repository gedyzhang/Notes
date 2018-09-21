## vim编辑器的使用
### 进入vim编辑器
$ vim 文件名
### 进入insert模式
进入vi编辑器后，默认为normal模式，按i进入insert模式，左下角会显示-INSERT-，此模式下可以对文件进行编辑和修改；编辑完成后按esc回到normal模式
### 回到命令模式
 按shift+；回到命令模式
### 退出vi编辑器
按wq! [enter] 保存并退出vim编辑模式；q!是不保存就退出；w!存盘
### *normal模式*下的一些命令
- i 进入insert模式，按Esc退出insert模式
- x 删除光标所在位置的字符
- :wq 存盘退出（:w 存盘，:q 退出，:q后面可以跟文件名）
- dd 删除当前行，并将删除的内容保存到剪贴板里
- p 粘贴剪贴板的内容

#### [vim入门攻略]（http://coolshell.cn/articles/5426.html）
