# 在PC上面配置GIT

## 下载并安装git
每位同学结合自己的操作系统，下载并安装合适git。具体请从git官网下载，并根据说明安装。此处从略。

## 配置git
在命令模式下，输入如下命令，配置user name 和 user email  
git config --global user.name "John Doe"    (其中 John Doe 改成注册时候用的name)  
git config --global user.email johndoe@example.com  (其中，邮箱地址改成自己注册时的地址)  

另外，上述命令中的空格要注意。如果执行过程中提示错误，说明有命令敲错。  

成功后，执行下述命令，能够看到新的配置已经有效。
git config --list

下面是我电脑上的显示结果，有最后两行说明成功。具体拼写请各位仔细检查。
```
credential.helper=osxkeychain
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
filter.lfs.clean=git-lfs clean -- %f
user.name=John Doe
user.email=johndoe@example.com
```

