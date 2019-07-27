### git学习笔记

#### 1.git add: 将工作区代码提交到暂存区

#### 2.git commit: 将暂存区代码提交到本地仓库

#### 3.git status: 查看工作区和本地仓库代码之间的区别

常见的几种区别：

    1.Changes not staged for commit: 代表更改还没有暂存，提示要先将代码提交到暂存区

    2.Changes to be committed： 要提交的更改，代表代码已经提交到暂存区，下一把可以提交到本地仓库了

    3.nothing to commit, working tree clean: 提交完成，工作区干净，也就是说工作区和本地仓库代码一致了

#### 4.git reset: 将暂存区文件退回到工作区
    
    比如：我往暂存区里提交了一个文件，但是发现这个文件是错的，想把这个文件退出暂存区，就会用到git reset: git reset HEAD 文件

#### 5.git checkout -- 文件： 将文件在工作区的修改全部撤销

    比如： 我写了一些代码，但是发现别人已经写好了。于是我需要将工作目录做的修改都撤销。

    撤销分为两种，
    一种是: 这个代码已经提交到暂存区了，然后自己又开始修改，此时checkout只会撤回到和暂存区一样的代码。

    一种是：代码还未提交到暂存区，那么checkout会撤回到和本地版本库一样的代码。

    那么，如果是第一种情况怎么办? 因为我们自己写的代码是无用代码，而且已经提交到暂存区，那我们应该先将暂存区的文件退出，这样的话，checkout就可以返回和版本一样的代码了。

    先 git reset HEAD xxx.js
       git checkout -- xxx.js


#### 6.git rm: 删除文件

    这个命令行的用法： 如果工作区的一个文件删除了，要保证本地版本库的这个文件也要删除，可以使用git rm

    先 git rm xxx.js
       git commit -m "删除xxx.js"

    但是笔者不太习惯这个用法：因为删除也算是一次修改。
    
    笔者习惯直接本地删除代码
    rm xxx.js

    然后: git add xxx.js

    git commit -m"xxx.js"

#### 7.git clone  git pull的区别：

    一般而言，都是先在git服务器创建远程仓库，比如github创建一个项目。然后让很多开发者去开发。很少有那种开发者先在本地初始化git本地仓库，再去和远程仓库连接。

    比如： 公司的github项目地址在 https://github/xxx/xxx_project.git

    如果是第一次拉取项目，需使用git clone。

    git clone: 是在本地没有版本库的时候，从远程服务器克隆整个版本库到本地，是一个本地从无到有的过程。

    git pull：在本地有版本库的情况下，从远程库获取最新commit 数据（如果有的话），并merge（合并）到本地。

    通常情况下，远程操作的第一步，是使用git clone从远程主机克隆一个版本库到本地。

    本地修改代码后，每次从本地仓库push到远程仓库之前都要先进行git pull操作，保证push到远程仓库时没有版本冲突。

#### 8. git branch xxx: 创建分支

    git branch: 查看分支
    git checkout 分支名： 切换分支
    git branch 分支名: 创建分支
    git checkout -b 分支名： 创建分支并切换到该分支
    git checkout -d 分支名： 删除分支
    git marge 分支名：合并某分支到当前分支


#### 9.常见问题：
    
    1.Your branch is ahead of 'origin/master' by 1 commit.

    代表当前本地仓库要比远程仓库提前一个版本。

    什么操作会导致这样呢？

    比如 本地文件我修改以后，还未进行commit，则不会有这个错。
    如果进行了commit，则说明了我们向本地仓库提交了commit，当然也就会提示上面的提示。
    
#### 10.如果相同的文件，别人先提交到远程仓库，怎么办？

    当别人先提交修改后，自己git push时会失败，所以应该使用git pull先进行拉取，再进行提交

    在push远程仓库之前，记住：

    先拉取(pull), 后提交(push)
#### 11. git push: 提交本地仓库代码到远程仓库

#### 12.如果我做了工作区某个文件的修改，但是还未add和commit，但是另外一个同事也对这个文件进行了修改并提交到了远程仓库，此时我们直接进行pull操作会发生是什么？

    git pull origin/master

    会提示：  Your local changes to the following files would be overwritten by merge: (合并会导致你的本地修改被覆盖)
    Please commit your changes or stash them before you merge.

    所以我们可以将这个文件先stash住，
    git stash
    git pull origin master
    git stash pop
    git add .
    git comit -m"xxx"
    git push


#### 13. 不要轻易的将本地创建的分支push到远程仓库，因为这样可能会导致bug的出现。一般远程仓库分支由项目组长创建。
