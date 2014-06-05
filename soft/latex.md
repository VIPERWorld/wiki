# LaTex使用

页眉页脚: http://blog.sina.com.cn/s/blog_9908653401010lx6.html

中文 xelatex

使用字体
```latex
\documentclass{article} 
\usepackage{fontspec}
\setmainfont{STHeiti J} % 文字见下面
\begin{document} 
你好
\end{document} 
```

其中字体描述信息为
```bash
fc-list :lang=zh
或者
fc-list
```
命令输出的
```bash
/home/zodiac1111/.fonts/STHeiti-Light.ttc: 黑体\-韩语,黑體\-韓語,Heiti K,黒体\-韓国語,Heiti\-한국어:style=细体,細體,Mager,Fein,Light,Ohut,Fin,Leggero,ライト,가는체,Licht,Tynn,Leve,Светлый,Fina
/usr/share/fonts/truetype/arphic/uming.ttc: AR PL UMing CN:style=Light
/usr/share/fonts/truetype/arphic/uming.ttc: AR PL UMing HK:style=Light
/usr/share/fonts/truetype/wqy/wqy-microhei.ttc: 文泉驿等宽微米黑,文泉驛等寬微米黑,WenQuanYi Micro Hei Mono:style=Regular
/home/zodiac1111/.fonts/STHeiti-Medium1.ttc: 黑体\-日本语,Heiti J:style=中等,Medium
/home/zodiac1111/.fonts/STHeiti-Light.ttc: 黑体\-简,黑體\-簡,Heiti SC,黒体\-簡,Heiti\-간체:style=细体,細體,Mager,Fein,Light,Ohut,Fin,Leggero,ライト,가는체,Licht,Tynn,Leve,Светлый,Fina
/home/zodiac1111/.fonts/STHeiti-Medium2.ttc: STHeiti T0C:style=Medium
/usr/share/fonts/zh_CN/simsum.ttf: 方正魏碑_GBK,FZWeiBei\-S03:style=Regular
/usr/share/fonts/wps-office/FZYTK.TTF: 方正姚体_GBK,FZYaoTi\-M06:style=Regular
/usr/share/fonts/wps-office/FZSSK.TTF: 方正书宋_GBK,FZShuSong\-Z01:style=Regular
```

格式:
```bash
<路径>: 中文名,英文名:style=<样式>
```

其中的英文名部分 ,如
```text
FZShuSong\-Z01
```
但是dash(-) 不需要反斜杠转义.