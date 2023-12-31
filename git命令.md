## 安装
    官方网址：https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git
## 初次安装配置
* 在window的用户文件下有一个文件名字是 .gitconfig 的配置文件，里面记录了当前用户使用的配置

* 配置用户名
    git config --global user.name '用户名'
* 配置邮箱
    git config --global user.email '2495900371@qq.com'

* 查看git全部命令文档（在网页中打开，无需网络）
    git help config

* 在终端中打开帮助文档
    git cofig -h

## 初始化项目和git仓库
    git init

    如果自己有一个尚未进行版本控制的项目目录,想要用Git来控制它，需要执行如下两个步骤:
        ①在项目目录中，通过鼠标右键打开“Git Bash" 
        ②执行gitinit命令将当前的目录转化为Git仓库
    git init命令会创建一个名为 .git 的隐藏目录,

    这个.git目录就是当前项目的Git仓库,里面包含了初始的必要文件，这些文件是Git仓库的必要组成部分。

## 基本状态
    未跟踪(Untracked)   不被git所管理的文件
    未修改(Unmodified)  工作区的文件和git仓库的文件内容一致
    已修改(Modified)    工作区的文件和git仓库的文件内容不一致
    已暂存(Staged)      工作区的被修改的文件放到暂存区，准备将修改后的文件保存到git仓库

## 检查文件所处于什么状态
    git status
    git status -s 使用精简的方式展示 
    
    在未跟踪的文件前面显示两个红色问号 "??"
    在已修改且已放入暂存区的文件显示    "绿色的 M "
    在已修改未被放入暂存区的文件显示    "红色的 M "
    在使用git add后的文件进入暂存区    "绿色的 A "
    被删除后的文件会在文件开头显示      "绿色的 D "

## 跟踪文件，将文件添加到暂存区
    git add 文件名或文件夹
    此时如果再用git status -s查看文件状态，则在文件名字前面显示一个绿色的A 说明文件或文件夹已被跟踪，处于暂存状态

## 提交文件更新
    git commit -m '提交成功的文本'

## 撤销对文件的修改
    git checkout -- 文件名

    把工作区中对应的文件还原成git仓库中保存的文件
    会将所有的修改都丢失，且无法恢复,危险性比较高，谨慎操作
## 向暂存区一次性提交多个文件
    git add .
## 取消暂存的文件
    git reset HEAD 文件名
    git reset HEAD .                取消多个文件

## git的工作流程

    git commit -a -m 描述信息
    Git标准的工作流程是工作区→暂存区→Git仓库,但有时候这么做略显繁琐，
    此时可以跳过暂存区,直接将工作区中的修改提交到Git仓库,这时候Git工作的流程简化为了工作区→Git仓库。
    Git提供了一-个跳过使用暂存区域的方式，只要在提交的时候，
    给 git commit加上-a选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交, 从而跳过git add步骤:

## 移除文件
    从Git仓库中移除文件的方式有两种:
        ①从Git仓库和工作区中同时删除对应的文件
            git rm -f 文件名
        
        ②只从Git仓库中移除指定的文件，但保留工作区中对应的文件
            git rm --cached 文件名
## 忽略文件
    -般我们总会有些文件无需纳入Git的管理,也不希望它们总出现在未跟踪文件列表。在这种情况下，
    我们可以创建一个名为.gitignore的配置文件,列出要忽略的文件的匹配模式。
    文件.gitignore的格式规范如下:
        ①以#开头的是注释
        ②以/结尾的是目录
        ③以/开头防止递归
        ④以!开头表示取反
        ⑤可以使用glob模式进行文件和文件夹的匹配( glob指简化了的正则表达式)

## glob模式
    所谓的glob模式是指简化了的正则表达式:
        ①星号*匹配零个或多个任意字符
        ②[abc] 匹配任何一一个列在方括号中的字符( 此案例匹配- -个a或匹配一一个b或匹配- -个c)
        ③问号?只匹配-一个任意字符
        ④在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配(比如[0-9]表示匹配所有0到9的数字)
        ⑤两个星号 **表示匹配任意中间目录(比如a/**/z可以匹配a/z、a/b/z 或a/b/c/z等)

## 查看提交历史

    * 按时间先后顺序列出提交历史，最近提交的在上面
     git log

    * 只显示最新的两条提交历史，数字可以按需填写
     git log -2

    * 在一行上展示最近两条提交的历史信息
     git log -2 --pretty=oneline

    * 在一行上展示最近两条提交的历史信息，并自定义输出的格式

     git log -2 --pretty=oneline:"%h | %an | %ar | %s"

    参数：
    %h     提交的简写哈希值
    %an    作者名字
    %ar    作者修订日期，按多久以前的方式显示
    %s     提交说明

## 回退到指定的版本

 * 在一行显示所有的提交历史
    git log --pretty=oneline

 * 返回指定id的版本
    git reset --hard 哈希值id

 * 返回旧版本后，查看最新版本
    git reflog --pretty=oneline

## 添加到github远程仓库

连接远程仓库
    git remote add origin 仓库地址

第一次推送到远程仓库
    git push -u origin master

第二次后就可以不用使用上面代码
    git push

## SSH的创建

    ①打开Git Bash

    ②粘贴如下的命令,并将your_ _email@example.com替换为注册Github账号时填写的邮箱:
●
    ssh-keygen -t rsa -b 4096 -C "邮箱'

    ③连续敲击3次回车，即可在C:\Users\用户名文件夹\.ssh目录中生成id_ rsa 和id_ rsa.pub 两个文件

## 配置SSH

    ①使用记事本打开id_ _rsa.pub 文件，复制里面的文本内容
    ②在浏览器中登录Github,点击头像-> Settings -> SSH and GPG Keys -> New SSH key
    ③将id_ _rsa.pub文件中的内容,粘贴到Key对应的文本框中
    ④在Title文本框中任意填写一一个名称，来标识这个Key从何而来

检测是否配置成功

    ssh -T git@github.com
    执行完后输入yes
    成功则提示：Hi tsdxxx! You've successfully authenticated, but GitHub does not provide shell access.


## 使用SSH提交到GitHub仓库中

 新建一个仓库
 在项目根目录文件中 打开git base

链接远程仓库
 git remote add origin git@github.com:tsdxxx/bishe.git 

 git branch -M main

 推送到仓库
 git push -u origin main

 ## 将远程仓库的文件克隆到本地
  git clone 远程仓库的地址



## 查看连接的远程仓库
 git remote -v

## 移除连接的仓库
git remote remove origin
