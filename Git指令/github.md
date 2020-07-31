### 创建生成 SSH 密钥

1. 查看是否已经存在密钥

`cd ~/.ssh`

- 如果没有密钥，则创建密钥

```
ssh-keygen -t rsa -C 'xxxx@qq.com' # 生成密钥
ssh-keygen -t rsa -C "xxxx@qq.com" -f ~/.ssh/ww_rsa # 指定生成目录文件名字
ssh -T git@github.com   # 测试是否成功
```

执行这条命令会如上图提示文件保存路径，可以直接按 Enter，

然后提示输入 passphrase（密码），输入两次（可以不输直接两次 Enter），

然后会在 .ssh 目录生产两个文件：id_rsa 和 id_rsa.pub

用记事本打开.ssh 目录下的 id_rsa.pub 文件，复制里面的内容，或者直接执行命令查看 2.

这个密钥用来跟 github 通信，在本地终端里生成然后上传到 github
