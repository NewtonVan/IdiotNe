---
title: Let Hexo Next Support Latex
mathjax: true
date: 2019-09-13 22:45:04
tags:
	- Blog
	- Front-end
categories: Programming
---

# Overview
***

This blog is to record one important function newly opened by my blog. It trouble me for a long time to insert math equation. 

# Open MathJax In Next Theme
***

Next theme has already prepared the mathjax for supporting latex. Go to this file: `D:\MyBlog\Blog\themes\next\_config.yml` and rewrite this code.

```css
# ---------------------------------------------------------------
# Third Party Services Settings
# ---------------------------------------------------------------

# Math Equations Render Support
math:
  enable: true

  # Default (true) will load mathjax / katex script on demand.
  # That is it only render those page which has `mathjax: true` in Front Matter.
  # If you set it to false, it will load mathjax / katex srcipt EVERY PAGE.
  per_page: true

  engine: mathjax
  #engine: katex

  # hexo-rendering-pandoc (or hexo-renderer-kramed) needed to full MathJax support.
  mathjax:
    # Use 2.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/mathjax@2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    # For direct link to MathJax.js with CloudFlare CDN (cdnjs.cloudflare.com)
    #cdn: //cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML

    # See: https://mhchem.github.io/MathJax-mhchem/
    #mhchem: //cdn.jsdelivr.net/npm/mathjax-mhchem@3
    #mhchem: //cdnjs.cloudflare.com/ajax/libs/mathjax-mhchem/3.3.0

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin) needed to full Katex support.
  katex:
    # Use 0.7.1 as default, jsdelivr as default CDN, works everywhere even in China
    cdn: //cdn.jsdelivr.net/npm/katex@0.7.1/dist/katex.min.css
    # CDNJS, provided by cloudflare, maybe the best CDN, but not works in China
    #cdn: //cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.css

    copy_tex:
      # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
      enable: false
      copy_tex_js: //cdn.jsdelivr.net/npm/katex@0/dist/contrib/copy-tex.min.js
      copy_tex_css: //cdn.jsdelivr.net/npm/katex@0/dist/contrib/copy-tex.min.css
```

Make math **enable** and **per_page**to be true. 

# Important Shell Operation
***

I had tryed to support latex for millions of time. But it doesn't work just because this stupid command that most blogs don't mention.

`hexo clean`

Then `hexo d -g` can see the beautiful equation.

To solve some conflicts about the syntax between Latex and MarkDown. We use the pandoc plugin.

` npm un hexo-renderer-marked --save` 
Uninstall the marked renderer.

`npm i hexo-renderer-pandoc --save`
Install the pandoc renderer.

[Official Guidance](https://hexo-guide.readthedocs.io/zh_CN/latest/theme/[NexT]%E9%85%8D%E7%BD%AEMathJax.html)

