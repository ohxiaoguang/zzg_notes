卸载  radeon-profile-git

文件解压缩
sudo pacman -S unarchiver
unar xxx.zip

常用软件 开发环境

git
ssh
zsh
google-chrome
https://teaper.dev/Arch-Linux-java-febe1fe5bc764929aaeb02ed933c04f8

idea
https://teaper.dev/IntelliJ-IDEA-846ad50b0d314522b2d27e3b4248e18b

阿里云盘
https://teaper.dev/Aria2-80bafc0844fb4e008d8df14c456732d6


美化
https://archlinuxstudio.github.io/ArchLinuxTutorial/#/advanced/beauty




清理pacman缓存
sudo pacman -Sc


查看aur仓库
https://aur.archlinux.org/packages/

wiki
https://wiki.archlinux.org/title/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Arch%E7%94%A8%E6%88%B7%E8%BD%AF%E4%BB%B6%E6%BA%90%EF%BC%88AUR%EF%BC%89




pacman -S package_name        # 安装软件
pacman -S extra/package_name  # 安装不同仓库中的版本
pacman -Syyu                   # 升级整个系统，y 是更新数据库，yy 是强制更新，u 是升级软件
pacman -Ss string             # 在包数据库中查询软件
pacman -Si package_name       # 显示软件的详细信息
pacman -Sc                    # 清除软件缓存，即 /var/cache/pacman/pkg 目录下的文件
pacman -R package_name        # 删除单个软件
pacman -Rs package_name       # 删除指定软件及其没有被其他已安装软件使用的依赖关系
pacman -Qs string             # 查询已安装的软件包
pacman -Qi package_name       # 查询本地安装包的详细信息
pacman -Ql package_name       # 获取已安装软件所包含的文件的列表
pacman -U package.tar.zx      # 从本地文件安装
pactree package_name          # 显示软件的依赖树
 
 
yay -S 包名     # 安装软件
yay -Ss 关键字  # 根据关键字搜索软件包
yay -Rns 包名   # 卸载软件
yay -G 包名     # 可以只下载aur包而不构建