# emacs.d
my emacs plugins config

File Edit Options Buffers Tools Emacs-Lisp Help                                                          
 1(require 'package)
 2(add-to-list 'package-archives '("elpy" . "https://jorgenschaefer.github.io/packages/"))
 3
 4(package-initialize)
 5;;(elpy-enable)                                                                                        
 6;;                                                                                                     
 7(global-linum-mode t)
 8(column-number-mode t)
 9
10
11;;autocomplete                                                                                         
12(add-to-list 'load-path "~/.emacs.d/auto-complete/")
13(require 'auto-complete-config)
14(ac-config-default)
15
16;;yasnippet                                                                                            
17(add-to-list 'load-path "~/.emacs.d/auto-yasnippet")
18(require 'auto-yasnippet)
19;;(yas/global-mode 1)                                                                                  
20
21;;clang                                                                                                
22(add-to-list 'load-path "~/.emacs.d/auto-complete-clang/")
23(require 'auto-complete-clang)
24(setq ac-auto-start t)
25(setq ac-quick-help-delay 0.5)
26;; (ac-set-trigger-key "TAB")                                                                          
27;; (define-key ac-mode-map [(control tab)] 'auto-complete)                                             
28;;(define-key ac-mode-map [(control tab)] 'auto-complete)                                              
29(defun my-ac-config () (setq ac-clang-flags (mapcar(lambda (item)(concat "-I" item))
30                       (split-string "                                                                 
31                                      /usr/include/c++/6                                               
32                                      /usr/include/x86_64-linux-gnu/c++/6                              
33                                      /usr/include/c++/6/backward                                      
34                                      /usr/lib/gcc/x86_64-linux-gnu/6/include                          
35                                      /usr/local/include                                               
36                                      /usr/lib/gcc/x86_64-linux-gnu/6/include-fixed                    
37                                      /usr/include/x86_64-linux-gnu                                    
38                                      /usr/include                                                    
                                                                                                         
39                                      ")))
40(setq-default ac-sources '(ac-source-abbrev ac-source-dictionary ac-source-words-in-same-mode-buffers)
  )
41(add-hook 'emacs-lisp-mode-hook 'ac-emacs-lisp-mode-setup)
42;; (add-hook 'c-mode-common-hook 'ac-cc-mode-setup)                                                    
43(add-hook 'ruby-mode-hook 'ac-ruby-mode-setup)
44(add-hook 'css-mode-hook 'ac-css-mode-setup)
45(add-hook 'auto-complete-mode-hook 'ac-common-setup)
46(global-auto-complete-mode t))
47(defun my-ac-cc-mode-setup ()
48  (setq ac-sources (append '(ac-source-clang ac-source-yasnippet) ac-sources)))
49(add-hook 'c-mode-common-hook 'my-ac-cc-mode-setup)
50;; ac-source-gtags                                                                                     
51(my-ac-config)
