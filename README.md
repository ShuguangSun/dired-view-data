[![MELPA](https://melpa.org/packages/dired-view-data-badge.svg)](https://melpa.org/#/dired-view-data)
[![MELPA Stable](https://stable.melpa.org/packages/dired-view-data-badge.svg)](https://stable.melpa.org/#/dired-view-data)

# dired-view-data

View data from dired via ess(-r)

## Installation

Clone this repository or install from MELPA. Add the following to your `.emacs`:

``` elisp
(require 'dired-view-data)

;; global-minor-mode to `dired-mode'
(dired-view-data-global-mode)
;; or call minor-mode in dired buffer mannualy
;; (dired-view-data-mode 1)
```

In dired buffer, call `dired-view-data` (`V` or `C-c C-v`) on a data file (e.g., sas7bdat, xpt, rds, csv, rda or rdata), and buffer will pop up with data displayed.

Add below to make `dired-guess-shell-alist-user` recognize `dired-view-data` on some types of files.
``` elisp
(add-to-list 'dired-guess-shell-alist-user
             (list "\\.\\(sas7bdat\\|xpt\\|rds\\|csv\\|rda\\|rdata\\)$"
                   '(progn
                      (if (y-or-n-p-with-timeout "Read to R? " 4 nil)
                          (progn
                            (dired-view-data--do (dired-get-filename))
                            (keyboard-quit))
                        (if (eq system-type 'windows-nt)  ;; for w32
                            (w32-shell-execute "open" file-name nil 1))))))
```
Or `(setq dired-view-data-guess-shell-alist-p t)` with `dired-view-data-mode`,
which make `dired-do-shell-command` (`S-!`) for those files.

## Customization

You can modify or add new format via `dired-view-data-data-name-format`.
