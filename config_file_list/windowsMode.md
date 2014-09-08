<center>
emacs窗口布局自动保存跟复原
</center>

<pre><code>
;;
;; win:resume-windows --> windows 状态保存跟复原
;;______________________________________________________________________

;;; 安装
;; http://www.emacswiki.org/emacs/WindowsMode
;; http://www.gentei.org/~yuuji/software/
;; (install-elisp "http://www.gentei.org/~yuuji/software/windows.el")
;; (install-elisp "http://www.gentei.org/~yuuji/software/revive.el")

;;; windows.el 快捷键设定
(setq win:switch-prefix "\C-z")
;; 布局信息文件保存位置
(setq win:configuration-file "~/.windows")
(require 'windows)

(setq win:use-frame nil)
(win:startup-with-window)
(define-key ctl-x-map "C" 'see-you-again)

;; 启动时自动复原
(add-hook 'after-init-hook (lambda() (run-with-idle-timer 0 nil 'my-resume-windows)))
(defun my-resume-windows ()
  "restore windows status ."
  (interactive)
   (resume-windows t)
   (clear-active-region-all-buffers)
  )

;;;; 关闭时自动保存
(add-hook 'kill-emacs-hook 'win-save-all-configurations)

</code></pre>
