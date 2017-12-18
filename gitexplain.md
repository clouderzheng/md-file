##explain how to use github
####register in https://github.com 
####create a project in your repository
####install a github server in your computer
    windows用户请下载 http://msysgit.github.com/

    mac用户请下载 http://code.google.com/p/tortoisegit/

    一路next，安装成功后， 回到C盘，或任何文件夹下，点鼠标右键会多出一些菜单
    如 Git Init Hear、Git Bash、Git Gui ， 说明安装成功。

###配置Git
    我们先在电脑硬盘里找一块地方存放本地仓库，比如我们把本地仓库建立在C:\MyRepository\1ke_test文件夹下

    进入1ke_test文件夹 鼠标右键操作如下步骤：

    1）在本地仓库里右键选择Git Init Here，会多出来一个.git文件夹，这就表示本地git创建成功。
    2)右键Git Bash进入git命令行
###为了保险起见，我们先执行git init命令
    $ git init
###为了把本地的仓库传到github，还需要配置ssh key。
    $ ssh-keygen -t rsa -C "your_email@youremail.com"
    后面的your_email@youremail.com改为你的邮箱。我的邮箱是343070065@qq.com，也是在github上注册的那个邮箱：
    直接点回车，说明会在默认文件id_rsa上生成ssh key。 
    然后系统要求输入密码，直接按回车表示不设密码
    重复密码时也是直接回车，之后提示你shh key已经生成成功
    然后我们进入提示的地址下查看ssh key文件。 我的电脑的地址是C:\Users\Administrator\.ssh ，其中Administrator是我的电脑的名称
    打开id_rsa.pub，复制里面的key。里面的key是一对看不懂的字符数字组合，不用管它，直接复制。
    回到github网站，进入Account Settings，左边选择SSH Keys，Add SSH Key,
    title随便填，粘贴key。
###3）验证是否成功，在git bash下输入
    $ ssh -T git@github.com
    回车就会看到：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。
###4）接下来我们要做的就是把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们
    $ git config --global user.name "your name"
    $ git config --global user.email "your_email@youremail.com"
###提交上传
    1）接下来在本地仓库里添加一些文件，比如README

    在本地新建一个README文件  
    $ git add README

    $ git commit -m "first commit"
    2）上传到github 
    $ git push origin master

###