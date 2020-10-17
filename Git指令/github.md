 ### 添加密钥
 1. 切换至ssh文件夹并查看是否有密钥

 - 切换至ssh文件夹：`cd ~/.ssh`

 2. 指定生成目录文件名字

 - 指定生成目录文件名字：`ssh-keygen -t rsa -C "xxxx@qq.com" -f ~/.ssh/idlock_rsa`

执行这条命令会如上图提示文件保存路径，可以直接按 Enter，然后提示输入 passphrase（密码），输入两次（可以不输直接两次 Enter），
 此时会生成`idlock_rsa`和`idlock_rsa.pub`两个文件，其中`idlock_rsa`是公钥，`idlock_rsa.pub`是密钥

3. 查看密钥

- 查看密钥指令：`cat idlock_rsa.pub`,可查看并复制密钥至SSH
