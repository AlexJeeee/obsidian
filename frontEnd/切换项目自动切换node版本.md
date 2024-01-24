1. 安装 nvm：[https://github.com/nvm-sh/nvm](https://github.com/nvm-sh/nvm)
    
2. 用编辑器打开下面文件 ~/.zshrc
    
3. 找到 plugins=() 方法，在里面加一个 nvm ，如 plugins=(nvm)
    
4. 在 plugin=() 方法的上面一行添加下面代码：zstyle ':omz:plugins:nvm' autoload yes
    
5. 恭喜你完成了 nvm 的安装
    

如何验证是否安装成功

1. 在项目根下执行 ehco 18 > .nvmrc 添加文件 .nvmrc 文件
    
2. 重新进入项目根目录，命令行上出现 Found '/Users/zhuning/Projects/sqb/xxx/.nvmrc' with version <18>
    

Now using node v18.16.0 (npm v6.14.16) 

1. 恭喜你完成了自动切换 node 版本的配置