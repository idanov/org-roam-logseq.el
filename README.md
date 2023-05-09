# org-roam-logseq.el

This package is a converter of Logseq-style links to org-roam links.

There's a few prerequisites to making sure it will work.

# Logseq configuration

Ensure these settings are in your `config.edn`:
```clojure
:preferred-format :org
:org-mode/insert-file-link? false
:journal/page-title-format "yyyy-MM-dd"
:journal/file-name-format "yyyy_MM_dd"
```

# org-roam configuration


```elisp
(setq
  ;; your shared directory between Logseq and org-roam
  org-roam-directory "~/org/roam"
  ;; dailies directory is set to the Logseq default
  org-roam-dailies-directory "journals/"
  ;; exclude all syncthing folders and anything under logseq/ from being indexed by org-roam
  org-roam-file-exclude-regexp "\\.st[^/]*\\|logseq/.*$"
  )
```


```elisp
;; ensure org-roam is creating nodes similarly to Logseq
;; bear in mind that it won't be exact mapping due to Logseq's built-in
;;    :file/name-format :triple-lowbar
(setq org-roam-capture-templates '(("d" "default"
                                    plain
                                    "%?"
                                    :target (file+head "pages/${slug}.org" "#+title: ${title}\n")
                                    :unnarrowed t)))

;; ensure your org-roam daily template follows the journal settings in Logseq
;;    :journal/page-title-format "yyyy-MM-dd"
;;    :journal/file-name-format "yyyy_MM_dd"
(setq org-roam-dailies-capture-templates '(("d" "default"
                                            entry
                                            "* %?"
                                            :target (file+head "%<%Y_%m_%d>.org" "#+title: %<%Y-%m-%d>\n"))))
```

# Credits

This repository is based on and inspired by [this gist](https://gist.github.com/zot/ddf1a89a567fea73bc3c8a209d48f527).

There's a few modifications made by me and all of the code in this repo is re-licensed under [MIT](./LICENSE), as permitted by [William R. Burdick Jr.](https://github.com/zot/) in the original work.
