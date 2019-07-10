---
layout: post
title: LaTeXiT and ghostscript 9.27
tags: homebrew, macOS, latex
---

A couple weeks ago, I started my day with a usual `brew upgrade`, then got to work on an upcoming paper deadline... only to find that LaTeXiT broke, and everything would be half-rendered. It didn't take long to find the culprit: ghostscript was a likely candidate, so I checked what brew had upgraded, and as expected Ghostscript had been upgraded to 9.27. However, it took about an hour to figure out how to actually roll back to 9.26, as a lot of previous methods to do this in homebrew have been deprecated.  

I finally managed to fix this by directly adjusting the ghostscript formula. I finally fixed it by actually going to the homebrew-core folder (`cd /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core`), finding the commit for ghostscript 9.26 (`git log master -- Formula/ghostscript.rb`), checking it out and (`git checkout 6ec0c1a03ad789b62`) and then re-installing ghostscript, uninstalling ghostscript (`brew uninstall ghostscript`), then reinstalling it making sure not to touch anything else (`HOMEBREW_NO_AUTO_UPDATE=1 brew install ghostscript`).  

At this point you can checkout the master branch again, and pin ghostscript so that it won't be upgraded anymore (`brew pin ghostscript`). You can now continue your life!  

In the meantime I've pinged Pierre Chatelier, the maintainer of LaTeXiT, and he suggested also an alternative: [install a patched version of ghostscript](https://www.tug.org/mactex/morepackages.html). I'm lazy, so I like letting hombrew do everything (also meaning, I didn't test this), but if you need ghostscript 9.27 for whatever reason, there's this.