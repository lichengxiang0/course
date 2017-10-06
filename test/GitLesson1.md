#github说明  

git是一个版本控制系统，也称SCM  

##操作步骤
最开始时的操作，  git config --list   查看当前的变量情况  
git config --global user.name "李呈祥"  
git config --global user.email "624786053@qq.com"  


这样设置完成之后就可以推送了。深度理解：通过上面的操作，本质上是把本地的仓库和远程仓库关联起来，这样才可以推送到网上。进去根目录：cd ~
在隐藏文件  .gitconfig  里面就是我们上面设置的，以后添加的变量可以直接到这个文件中去找  