# Linux实用建议

[toc]

> 以下很多软件大多都有`.deb`包
>
> 对于桌面环境，我首推KDE Plasma，更接近Windows的习惯，同时自定义程度也高

##  Git配置

由于国内GFW的存在，在不用魔法的情况下，很难流畅访问Github

同时，在进行`git clone`操作时，很难完成，所以需要给`Git`做一点小配置，走`ssh`而不是默认的`http`

1. 编辑`~/.gitconfig`

    ```bash
    [url "git@github.com:"]
        insteadOf = https://github.com/
        insteadOf = https://www.github.com/
        insteadOf = http://github.com/
        insteadOf = git@github.com:
    [user]
        name = #你的用户名#
        email = #你的邮箱#
    ```

    添加以上配置

2. 配置`ssh key`

    i. 终端里输入`ssh-keygen -t ed25519 -C "#你的邮箱#"`一路默认回车即可[^1]

    ii. 打开`~/.ssh/id_ed25519.pub`，打开[Github SSH GPG keys配置](https://github.com/settings/keys)添加刚刚复制的key[^2]
    
    测试：在终端里输入`ssh -T git@github.com`，得到以下输出即为成功：
    
    ```
    Hi #你的用户名#! You've successfully authenticated, but GitHub does not provide shell access.
    ```

## 软件

### 音视频

- VLC - 不用多说
- mpv - 默认很简陋
- QQ/网易云音乐/Yes  Play Music/Spotify

### 文档

- pdf/epub等：`Okular`
  > 对于WPS中设置为粗体的字体糊成一团的问题，请下载旧版freetype，如2.13.0[^3]
- Office：请用`WPS`
- P图：`GIMP`或是用`wine`运行Photoshop
- 看图：`Gwenview`
- 截图：`flameshot`

## 其他
- 更好的终端[^4]

  1. 安装`zsh`，通过`chsh`更改默认shell为`/usr/bin/zsh`

  2. 安装`zim`

     `curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh`

     编辑`~/.zimrc`

     ```
     #添加下面的插件
     zmodule romkatv/powerlevel10k
     ```

  3. 输入`zimfw install`


### 系统字体小修小补

你会发现上面的`powerlevel10k`安装后，字体显示很怪，需要我们配置一下字体[^5][^6]

1. 在[Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases)下载一个自己喜欢的字体

   i. 如果你用的是Archlinux,你可以安装`ttf-nerd-fonts-symbols`

2. 安装`Noto Sans`字体，[`Inter`字体](https://github.com/rsms/inter/releases)，[`twemoji`字体](https://github.com/13rac1/twemoji-color-font/releases)

3. 编辑`~/.config/fontconfig`

   ```
   <?xml version="1.0"?>
   <!DOCTYPE fontconfig SYSTEM "urn:fontconfig:fonts.dtd">
   <fontconfig>
   
     <!-- Default system-ui fonts -->
     <match target="pattern">
       <test name="family">
         <string>system-ui</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>sans-serif</string>
       </edit>
     </match>
   
     <!-- Default sans-serif fonts-->
     <match target="pattern">
       <test name="family">
         <string>sans-serif</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Noto Sans CJK SC</string>
         <string>Noto Sans</string>
         <string>Twemoji</string>
       </edit>
     </match>
   
     <!-- Default serif fonts-->
     <match target="pattern">
       <test name="family">
         <string>serif</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Noto Serif CJK SC</string>
         <string>Noto Serif</string>
         <string>Twemoji</string>
       </edit>
     </match>
   
     <!-- Default monospace fonts-->
     <match target="pattern">
       <test name="family">
         <string>monospace</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Noto Sans Mono CJK SC</string>
         <string>Symbols Nerd Font</string>
         <string>Twemoji</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="prgname" compare="not_eq">
         <string>chrome</string>
       </test>
       <test name="family" compare="contains">
         <string>Noto Sans Mono CJK</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Inter</string>
       </edit>
     </match>
   
   
     <match target="pattern">
       <test name="lang">
         <string>zh-HK</string>
       </test>
       <test name="family">
         <string>Noto Sans CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans CJK HK</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>zh-HK</string>
       </test>
       <test name="family">
         <string>Noto Serif CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <!-- not have HK -->
         <string>Noto Serif CJK TC</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>zh-HK</string>
       </test>
       <test name="family">
         <string>Noto Sans Mono CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans Mono CJK HK</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>zh-TW</string>
       </test>
       <test name="family">
         <string>Noto Sans CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans CJK TC</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>zh-TW</string>
       </test>
       <test name="family">
         <string>Noto Serif CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Serif CJK TC</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>zh-TW</string>
       </test>
       <test name="family">
         <string>Noto Sans Mono CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans Mono CJK TC</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ja</string>
       </test>
       <test name="family">
         <string>Noto Sans CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans CJK JP</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ja</string>
       </test>
       <test name="family">
         <string>Noto Serif CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Serif CJK JP</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ja</string>
       </test>
       <test name="family">
         <string>Noto Sans Mono CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans Mono CJK JP</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ko</string>
       </test>
       <test name="family">
         <string>Noto Sans CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans CJK KR</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ko</string>
       </test>
       <test name="family">
         <string>Noto Serif CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Serif CJK KR</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang">
         <string>ko</string>
       </test>
       <test name="family">
         <string>Noto Sans Mono CJK SC</string>
       </test>
       <edit name="family" binding="strong">
         <string>Noto Sans Mono CJK KR</string>
       </edit>
     </match>
   
     <!-- Replace monospace fonts -->
     <match target="pattern">
       <test name="family" compare="contains">
         <string>Source Code</string>
       </test>
       <edit name="family" binding="strong">
         <string>Inter</string>
       </edit>
     </match>
       <match target="pattern">
       <test name="lang" compare="contains">
         <string>en</string>
       </test>
       <test name="family" compare="contains">
         <string>Noto Sans CJK</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Noto Sans</string>
       </edit>
     </match>
   
     <match target="pattern">
       <test name="lang" compare="contains">
         <string>en</string>
       </test>
       <test name="family" compare="contains">
         <string>Noto Serif CJK</string>
       </test>
       <edit name="family" mode="prepend" binding="strong">
         <string>Noto Serif</string>
       </edit>
     </match>
   
   </fontconfig>
   ```

---

NVdia驱动安装，版本不一，自行搜索**_最好无视CSDN_**

Debian Wiki，Arch Wiki都将会很有用

---
[^1]: [生成SSH密钥](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[^2]: [新增SSH密钥](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
[^3]: [WPS Office](https://wiki.archlinux.org/title/WPS_Office#Fonts_are_too_bold)
[^4]: [终端美化](https://arch.icekylin.online/guide/advanced/beauty-3.html)
[^5]: [Linux 下的字体调校指南](https://szclsya.me/zh-cn/posts/fonts/linux-config-guide/)
[^6]: [用 fontconfig 治理 Linux 中的字体](https://catcat.cc/post/2021-03-07/)
