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