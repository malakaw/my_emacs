<center>
FAQ
</center>

* 注释字符乱码怎么处理
<br/>
注释的中文会出现乱码的情况在emacs配置中添加
<br/>
<code>
(set-default-font "Source Code Pro-12")
(set-fontset-font "fontset-default" 'gb18030' ("STHeiti" . "unicode-bmp"))
</code>
