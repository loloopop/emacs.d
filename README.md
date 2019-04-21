;; emacs.d
;; my emacs plugins config

File Edit Options Buffers Tools Emacs-Lisp Help                                                          
 (require 'package)
 (add-to-list 'package-archives '("elpy" . "https://jorgenschaefer.github.io/packages/"))
 
 (package-initialize)
 ;;(elpy-enable)                                                                                        
 ;;                                                                                                     
 (global-linum-mode t)
 (column-number-mode t)
 

;;autocomplete                                                                                         
(add-to-list 'load-path "~/.emacs.d/auto-complete/")
(require 'auto-complete-config)
(ac-config-default)

;;yasnippet                                                                                            
(add-to-list 'load-path "~/.emacs.d/auto-yasnippet")
(require 'auto-yasnippet)
;;(yas/global-mode 1)                                                                                  

;;clang                                                                                                
(add-to-list 'load-path "~/.emacs.d/auto-complete-clang/")
(require 'auto-complete-clang)
(setq ac-auto-start t)
(setq ac-quick-help-delay 0.5)
;; (ac-set-trigger-key "TAB")                                                                          
;; (define-key ac-mode-map [(control tab)] 'auto-complete)                                             
;;(define-key ac-mode-map [(control tab)] 'auto-complete)                                              
(defun my-ac-config () (setq ac-clang-flags (mapcar(lambda (item)(concat "-I" item))
                       (split-string "                                                                 
                                      /usr/include/c++/6                                               
                                      /usr/include/x86_64-linux-gnu/c++/6                              
                                      /usr/include/c++/6/backward                                      
                                      /usr/lib/gcc/x86_64-linux-gnu/6/include                          
                                      /usr/local/include                                               
                                      /usr/lib/gcc/x86_64-linux-gnu/6/include-fixed                    
                                      /usr/include/x86_64-linux-gnu                                    
                                      /usr/include                                                                                       
                                      ")))
(setq-default ac-sources '(ac-source-abbrev ac-source-dictionary ac-source-words-in-same-mode-buffers)
  )
(add-hook 'emacs-lisp-mode-hook 'ac-emacs-lisp-mode-setup)
;; (add-hook 'c-mode-common-hook 'ac-cc-mode-setup)                                                    
(add-hook 'ruby-mode-hook 'ac-ruby-mode-setup)
(add-hook 'css-mode-hook 'ac-css-mode-setup)
(add-hook 'auto-complete-mode-hook 'ac-common-setup)
(global-auto-complete-mode t))
(defun my-ac-cc-mode-setup ()
  (setq ac-sources (append '(ac-source-clang ac-source-yasnippet) ac-sources)))
(add-hook 'c-mode-common-hook 'my-ac-cc-mode-setup)
;; ac-source-gtags                                                                                     
(my-ac-config)
