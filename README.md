# dired-view-data

View data from dired via ess(-r)

## Installation

Clone this repository (TODO:, or install from MELPA). Add the following to your `.emacs`:

``` elisp
(require 'dired-view-data)
```

In dired buffer, call `dired-view-data` on a data file (e.g., sas7bdat, xpt, rds, cs, rda or rdata), and buffer will pop up with data displayed.

Call `dired-view-data-initialization` can do some set up. It define key `C-c C-r` for dired-view-data in dired-mode, and

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

which make `dired-do-shell-command` (`S-!`) for those files.

## Customization

You can modify or add new format via `dired-view-data-data-name-format`.
