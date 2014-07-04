<center>
FAQ
</center>
# 不需要安装第三方模块 #
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
(defun copy-thing (begin-of-thing end-of-thing &optional arg)
  "copy thing between beg & end into kill ring"
  (save-excursion
    (let ((beg (get-point begin-of-thing 1))
          (end (get-point end-of-thing arg)))
      (copy-region-as-kill beg end)))
  )
(defun paste-to-mark(&optional arg)
  "Paste things to mark, or to the prompt in shell-mode"
  (let ((pasteMe
     	 (lambda()
     	   (if (string= "shell-mode" major-mode)
               (progn (comint-next-prompt 25535) (yank))
             (progn (goto-char (mark)) (yank) )))))
    (if arg
        (if (= arg 1)
            nil
          (funcall pasteMe))
      (funcall pasteMe))
    ))
(defun copy-word (&optional arg)
  "Copy words at point into kill-ring"
  (interactive "P")
  (copy-thing 'backward-word 'forward-word arg)
  ;;(paste-to-mark arg)
  )
(global-set-key (kbd "C-c w")         (quote copy-word))
</code></pre>
**快捷键  C-c w**

* 如何替换“换行符”或是自动添加一行
<br/>
**C-q C-j**
<br/>
C-q is for quoted-insert, and C-j is a newline (0xa).
<br/>
替换就是 M-x replace-string
* 如何移动／复制／剪切行
<br/>
<pre><code>
(defun move-line-up ()
  "Move up the current line."
  (interactive)
  (transpose-lines 1)
  (forward-line -2)
  (indent-according-to-mode))
(defun move-line-down ()
  "Move down the current line."
  (interactive)
  (forward-line 1)
  (transpose-lines 1)
  (forward-line -1)
  (indent-according-to-mode))
(global-set-key [(meta shift up)]  'move-line-up)
(global-set-key [(meta shift down)]  'move-line-down)
(global-set-key "\M-w"
                (lambda ()
                  (interactive)
                  (if mark-active
                      (kill-ring-save (region-beginning)
                                      (region-end))
                    (progn
                      (kill-ring-save (line-beginning-position)
                                      (line-end-position))
                      (message "copied line")))))
(global-set-key "\C-w"
                (lambda ()
                  (interactive)
                  (if mark-active
                      (kill-region (region-beginning)
                                   (region-end))
                    (progn
                      (kill-region (line-beginning-position)
                                   (line-end-position))
                      (message "killed line")))))
</code></pre>
**C-w  剪切行**
<br/>
**M-w  复制行**
<br/>
**meta shift up/down 上下移动行**
<br/>
