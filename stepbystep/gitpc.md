# 在PC上面配置GIT（以UBUNTU为例）

其他操作系统可进行参照。
## 1. GIT本地环境配置

### 1.1 下载并安装git
执行命令
```
sudo apt-get install git
```

### 1.2 配置用户信息
在命令模式下，输入如下命令，配置user name 和 user email  
```
git config --global user.name "John Doe"    (其中 John Doe 改成注册时候用的name)  
git config --global user.email johndoe@example.com  (其中，邮箱地址改成自己注册时的地址)  
```
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
## 2. 通过SSH连接Github
### 2.1 安装SSH
```
sudo apt-get install ssh
```
### 2.2 创建密钥文件
```
ssh-keygen -t rsa -C johndoe@example.com (你的github账号邮箱)
```
首先 ssh-keygen 会确认密钥的存储位置和文件名（默认是 .ssh/id_rsa）,然后他会要求你输入两次密钥口令，留空即可。所以一般选用默认，全部回车即可。
默认密钥文件路径在~/.ssh，id_rsa是私钥文件，id_rsa.pub是公钥文件

### 2.3 将公钥添加到Github
```
第一步，进入到~/.ssh目录，里面有两个文件 id_rsa和id_rsa.pub。
第二步，执行gedit id_rsa.pub,把里面内容全部复制之后关闭文件。
第三步，进入到github网站，单击个人图标右边的向下三角，选择里面的settings
第四步，单击页面左边一栏里面的SSH and GPG keys
第五步，单击新出画面右上角的 New SSH key
第六步，把刚才复制内容黏贴到下面一个方框里，并在上面标题栏为这个公钥命名，保存退出
```

### 2.4 测试刚才SSH公钥添加是否成功
```
ssh -T git@github.com
```
如果结果为 “ ...You've successfully authenticated, but GitHub does not provide shell access”，则说明成功。

## 3. GIT 基本使用方法
### 3.1 在github网站上新建一个自己的仓库
以我这个网站为例。
进入仓库后右边有个绿色按钮 clone or download（可以选择SSH，因为刚才已经成功），复制这段地址，以我的为例就是git@github.com:kingsone995/kingsone995.github.io.git。
### 3.2 将网站内容clone下来
```
1，在ubuntu电脑上新建一个目录github（名字自己取，建议用短英文）
2，进入github目录
3，输入命令：git clone git@github.com:kingsone995/kingsone995.github.io.git
```

### 3.3 查看状态 git status
进入kingsone995.github.io目录，运行命令 git status，看到内容为
```
192:kingsone995.github.io XXX$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```
### 3.4 修改文件，查看反应
对stepbustep/gitpc.md的文件进行修改后保存。
然后再执行git status命令。看到：
```
192:kingsone995.github.io XXX$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   stepbystep/gitpc.md

no changes added to commit (use "git add" and/or "git commit -a")
```
看到这个文件被修改，但是没有加入到仓库中。

### 3.5 加入修改信息git add *
执行命令： 
```
git add *
```

再执行git status，看到
 ```
 192:kingsone995.github.io XXX$ git add *
192:kingsone995.github.io XXX$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   stepbystep/gitpc.md
```
提示可以提交了。

### 3.6 进行提交git commit
执行命令 
```
git commit
```
看到结果为：
```
192:kingsone995.github.io XXX$ git commit
[master 231a1d3] test
 1 file changed, 62 insertions(+), 5 deletions(-)
192:kingsone995.github.io XXX$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

弹出来的提示是后面上传到github网站后每个文件的说明。
这一步完成后本地git仓库更新完毕。

### 3.7 提交到网站git push
执行命令
```
git push
```
看到结果
```
192:kingsone995.github.io XXX$ git push
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 4 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 2.02 KiB | 2.02 MiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:kingsone995/kingsone995.github.io.git
   9dd142e..231a1d3  master -> master
```
表明文件已经被上传到网站，这是可以到网站上去查看是否是最新文件。



