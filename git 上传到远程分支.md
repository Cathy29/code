1.数据导入在分支origin/dataImport 下面
打包系统在分支origin/package 下面

git init
git remote add origin http://10.5.0.222/Cathy/DataImportSystem.git 远程仓库名字为origin
git add .
git commit -m""
git push origin master:origin/dataImport  (本地：远程)
（删除origin：git remote rm origin）

2.注：git ssh无法使用 在复制url时，改gitlab.example.com为10.5.0.222
git add 时出现modified: xxx(modified content, untracked content) 则xxx文件夹内可能有.git文件 删掉即可。

3.显示.git等隐藏文件的方法：
defaults write com.apple.finder AppleShowAllFiles TRUE
killall Finder 重启finder

若想隐藏文件：
defaults write com.apple.finder AppleShowAllFiles -bool false
killall Finder 

4.Git error： hint: Updates were rejected because the remote contains work that you do hint: not have locally. This is usually caused b
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
方法： 
git pull origin master
 git push origin master


hadoop 赋权问题：
Permission denied: user=dr.who, access=WRITE, inode="/user/spark/DATA/LOAD":root:spark:drwxr-xr-x
给文件夹赋权限：sudo -u hdfs hadoop fs -chmod 777 /user/spark/DATA/LOAD
给用户赋权：sudo -u hdfs hadoop fs -chown root /user/spark/DATA/LOAD
删除文件（夹）：hadoop fs -rm（r） /user/spark/DATA/LOAD/h

