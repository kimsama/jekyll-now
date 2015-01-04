---
layout: post
title: Hello github.io!
---

Struggling hours with [Jekyll](http://jekyllrb.com/), finally set up the blog with [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. It maybe the easyest way as it say.

By the way, the default setting for syntax highlight with *pygments* does seem to work on Windows.
Just switching it to *'rouge'* runs fine.

Installed *rouge* with gem.

`$gem install rouge`

Then, changed highlighter in the *_config.yml* file.

`hightlighter: rouge`

***IMPORTANT:*** Commiting a *_config.yml* that uses *rouge* now causes "Page build failure" on GitHub. Before you commit & push, you must set highlighter: pygments in _config.yml, even if you don't care to install pygments locally. See more details at [Blogging on GitHub](http://loyc.net/2014/blogging-on-github.html).

