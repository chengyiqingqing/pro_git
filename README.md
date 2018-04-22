# pro_git
* 需要重新配git，但是有些细节记不清了，所以重新梳理一下

## git命令行的类别

### 1. git基本操作

* 1.配置用户名和密码

    git config --global user.name "chengyiqingqing"
    
    git config --global user.email 17839221829@163.com
    
* 2.仓库操作相关；
    
    git init  初始化仓库；
    > 1. 将作用域移动到该文件夹下：cd 文件路径/文件夹名字；
    > 2. 初始化仓库：git init；
    
    git add ./git add 文件名.后缀 /git add *.后缀
    > 1. 添加所有文件到暂存区： git add .       
    > 2. 添加某个文件到暂存区： git add 文件名.后缀   
    > 3. 添加某类文件到暂存区： git add *.后缀   
    
    git commit -m "描述提交信息：提交了add的操作"；
    > 1. 将暂存区的数据提交至本地代码仓库： git commit -m "提交信息"    
    
    git log 查看commit提交记录；
    > 1. 查看提交信息：git log （使用了sha-1加密了提交信息）     
    > 2. 查看用户名和邮箱信息：git log
    > 3. 查看提交的文件：git log
    > 4. 解释说明：commit提交之后，git status 看不到提交前暂存区的状态。但是使用git log就可以了。
    
### 2. 介绍四个概念

* 1.暂存区：staging area（或index）  

    1. 进行add操作的文件都在暂存区。
    
    2. 种大米的地方叫做工作区；收割大米，通过add操作放在作出变更的地方晒太阳，而不是放在仓库，这个地方叫做暂存区；晒完之后放到仓库里，叫做本地仓库。

* 2.工作区：work area

    1. 工作区，就是我们进行工作的地方。即为项目文件夹内。

* 3.本地仓库：local repository

    1. 本地仓库，就是我们自己工作的电脑上，保存“版本数据"的地方。

* 4.远程仓库：local repository

    1. 为防止我们本地电脑上的数据丢失，或错误删除等操作，我们将自己的数据备份到
远程服务器上，这个服务器可以理解成代码仓库。

	
### 3. git分支的基本操作

* 1.git分支，如何保存版本数据

    > 1. 创建分支: git branch 分支名
    > 2. 查看所有本地分支(可以查看当前分支)： git branch 
    > 3. 查看当前分支状态(可以查看当前分支)： git status 
    > 4. 切换到新的分支: git checkout 分支名；
    > 5. 再次查看状态（看在哪个分支上）：git status
    
* 2.git分支合并

    git checkout -b  要创建的新分支名；（它相当于下面两行命令）
    > 1. git branch newBranch
    > 2. git checkout newBranch；
    > 3. 假如你在master分支上做了修改操作，但是并未提交。直接创建分支并切换了分支
    那么就会出现问题
    > 4. 在你转化分支之前，尽量保持一个清洁的暂存区环境。（但是出现这样的误操作，
    可以使用stashing和amending进行修复，后面会提到）
    
    git 分支本地合并
    > 1. git checkout master
    > 2. git merge newBranch；
    > 3. 将newBranch上的分支合并到master分支上。
    > 4. 肯定是master分支变了，而newBranch分支并未改变。
    ，fastForward代表没有冲突。直接master就是newBranch一样了，指针前移。
    > 5. 如果想要的功能已经实现了，并且就在master分支上那么可以删除newBranch分支了
    > 6. git checkout -d newBranch 这样就删除了该分支；记住不可以在当前分支删除当前分支；
    
 * 3.解决合并分支中产生的冲突及git stash命令。
     
     工作到一半（在工作区），只是进行了一些修改并未添加暂存区的操作。但是不想提交。此时
     有新的紧急工作进来，需要先切换新的分支上工作，git会阻止切换。解决方案：git stash命令
     > 1. 创建新分支: git branch branch_01
     > 2. 创建新分支并切换：git branch branch_02
     > 3. 修改新分支02中的内容后:git branch branch_01
     > 4. 报错信息如下：error:commit or stash your changes before switching branches
     > 5. 再次查看状态（看在哪个分支上）：git status   
     > 6. 那么通过执行这条命令就可以保存工作区的状态：git stash 然后在切换分支完成紧急任务
     > 7. 在完成了紧急任务之后，回复刚才的工作区状态：git checkout b_02;
     git stash list；git stash apply 填入list下的状态；
      
## git的远程交互配置信息：从SSH公钥私钥配置开始

###git服务器与远程操作
* 1.首先生成公钥和私钥

    用SSH生成公钥和私钥 
    > 1. git config -- username "shaowenwen"
    > 2. git config -- email "shaowenwen@email.com"
    > 3. ssh-keygen -t rsa -C "shaowenwen@email.com"
    
    用SSH生成公钥和私钥 
    > 1. git config -- username "shaowenwen"
    > 2. git config -- email "shaowenwen@email.com"
    > 3. ssh-keygen -t rsa -C "shaowenwen@email.com"
    
        1.然后它会询问我们公钥保存在哪里？我们直接就默认就可以了。直接回车。
        Generating public/private rsa key pair.
        Enter file in which to save the key (C:\Users\Administrator\.ssh):(不用添，直接回车)
        2.回车之后，它还会询问你打开私钥的话，要不要密码。
        Created directory '/home/d7/.ssh'.
        Enter passphrase(empty for no passphrase):(也是直接回车)
        3.又问了一遍，还是直接回车：
        它就帮我们生成公钥和私钥了。公钥和私钥的路径我默认路径:C:\Users\Administrator\.ssh\下的
        id_rsa,id_rsa.pub
        4.找到d_rsa.pub，在gitlab上配置；
        然后打开id_rsa.pub,将里面的内容，写入gitlab上的key_blank就行了，label_blank随便取。
        
* 2.操作远程仓库

    1.git clone 仓库URL
    > 1. 自动创建了本地的master 分支用于跟踪远程仓库中的master 分支
    > 2. 适用场景1：直接克隆别人的远程分支，但是修改后push不上去。如果想push
    那么先fetch一下到自己远程仓库上，然后clone自己的这个仓库，修改后push上去才可以。
    > 3. 适用场景2：直接克隆别人的远程分支或者克隆自己的远程分支修改后再push上去。
    
    2.git fetch 远程仓库名 或者 url地址。
    > 1. git fetch origin 
    > 2. 适用场景1：git fetch (默认是origin):从远程仓库抓取数据到本地.(gitlab协作，大家共同适用同一个远程分支)
    > 3. 适用场景2：git fetch url ：从别人远程仓库，拉取数据到自己的远程仓库。
    
    3.git merge 远程仓库名/分支名
    > 1. git merge origin/master
    > 2. 适用场景1：（有冲突） 产生冲突的原因，就是别人修改了a文件，push上去了，你也修改了a文件。
        此时git合并的时候不知道远程对a的修改生效还是你本地的对a的修改生效。
    > 3. 适用场景2：（没有冲突）别人修改了b文件push了，你修改了commit了a文件。那么不会冲突，你merge
        之后，你的本地就有了修改后的b文件，和你commit的a文件。
    > 4.我在本地merge的时候，感觉和pull好像没有区别。回头再看看这个点。
        
    4.git pull 远程仓库名 分支名
    > 1. git pull origin/master
    > 2. 适用场景1：（有冲突） 产生冲突的原因，就是别人修改了a文件，push上去了，你也修改了a文件。
        此时git合并的时候不知道远程对a的修改生效还是你本地的对a的修改生效。
    > 3. 适用场景2：（没有冲突）别人修改了b文件push了，你修改了commit了a文件。那么不会冲突，你merge
        之后，你的本地就有了修改后的b文件，和你commit的a文件。
    > 4.相当于git fetch + git merge 远程仓库名/分支名
    
    5.git push 远程仓库名 分支名
    > 1. git push origin master
    > 2. 适用场景1：（push前远程有修改)你需要先同步pull一下。然后再push才能成功。
    > 3. 适用场景2： (push前远程有修改)你没有修改，push没成功。因为远程别人修改了b文件，你本地没有修改；
        但是你修改了a文件，远程没修改。你说远程的b文件依照你本地的还是用远程自身的。所以不让你push
        
    6.git branch查看分支
    > 1. git branch 查看本地分支；结果：*master branch1,branch2;
    > 2. git branch -r 查看远程分支remote的。结果：origin/master这样事儿的。
    > 3. git branch -vv 查看本地分支和远程分支的关系。
    
    7.git branch --set-upstream master origin/origin
    > 1. git branch --set-upstream branch1 origin/master 将本地分支branch1与远程master建立关系。
    > 2. master是从远程master克隆下来的，自动有关系；而branch1是在本地主分支master上建立的,与远程分支没有关系
    
    8.远程仓库的重命名和删除
    > 1. git remote rename 原名 新名字
    > 2. git branch -rm 远程仓库名
    
    