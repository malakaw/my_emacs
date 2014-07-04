<center>
FAQ
</center>

* 注释字符乱码怎么处理
<br/>
注释的中文会出现乱码的情况在emacs配置中添加
<br/>
<pre>
(set-default-font "Source Code Pro-12")
(set-fontset-font "fontset-default" 'gb18030' ("STHeiti" . "unicode-bmp"))
</pre>
* 如何复制光标所在的单词
<br/>
<pre><code>
(defun get-point (symbol &optional arg)
  "get the point"
  (funcall symbol arg)
  (point)
  )


(defun copy-word (&optional arg)
  "Copy words at point into kill-ring"
  (interactive "P")
  (copy-thing 'backward-word 'forward-word arg)
  ;;(paste-to-mark arg)
  )
(global-set-key (kbd "C-c w")         (quote copy-word))
</code>
</pre>
<br/>
**快捷键  C-c w**
