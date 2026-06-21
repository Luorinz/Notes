1、**配置 Git 全局用户名和邮箱：** 安装完成后，打开电脑的终端（Windows 用户打开 Git Bash 或 CMD），运行以下两行命令（把名字和邮箱换成你自己的，**建议和你的 GitHub/Gitee 账号一致**）：

```bash
git config --global user.name "luorinz"
git config --global user.email "luorinz@hotmail.com"
```

2、创建本地目录，初始化git，链接github仓库
```bash
git init

git remote add origin https://github.com/luorinz/Notes.git

git pull origin master
```
3、登录github