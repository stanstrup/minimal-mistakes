---
layout: post
title: "CLI Goodies"
modified:
categories: technical
excerpt: "My commandline productivity toolkit"
tags: [CLI, zsh, bash, prezto, antigen, prompt, technical, productivity, tools, plugins, completions, linux, unix]
image:
  feature: zsh.png
  credit: Srijan R. Shetty
comments: true
date: 2015-09-27T17:43:02+05:30
---

> Today, I finally have most of the goodness of my shell packed as a single repository. I say most because, I still have some things stuck in antigen with no clear migration path. Until then give these goodies a whirl, and do give a shout out to me if you need any help setting them up; I've added instructions of getting them up and ready with the common - a metric defined by the number of GitHub stars the framework has - frameworks out there. (My favourite is undoubtedly `Prezto` for it's super fast startup).

##Installation

**Installing under [Prezto](https://github.com/sorin-ionescu/prezto)**

{% highlight bash %}
  cd .zprezto
  git submodule add https://github.com/srijanshetty/cli-goodies.git modules/cli-goodies
{% endhighlight %}

Add `cli-goodies` to your `.zpreztorc` file:

{% highlight text %}
  # Set the Prezto modules to load (browse modules).
  # The order matters.
  zstyle ':prezto:load' pmodule \
    'environment' \
    'terminal' \
    'editor' \
    'history' \
    'directory' \
    'spectrum' \
    'utility' \
    'completion' \
    'prompt' \
    'cli-goodies'
{% endhighlight %}

**Installing under oh-my-zsh**<br>
I haven't tried using `cli-goodies` with `oh-my-zsh` and I think the following should work in theory.

{% highlight bash %}
    wget https://raw.github.com/srijanshetty/cli-goodies/master/init.zsh -O $HOME/.oh-my-zsh/custom/cli-goodies.zsh
{% endhighlight %}

**Installing using [Antigen](https://github.com/zsh-users/antigen)**<br>
If you use [Antigen](https://github.com/zsh-users/antigen), adding the following line to `.zshrc` should load `cli-goodies`.

{% highlight bash %}
    antigen-bundle srijanshetty/zsh-dwim
{% endhighlight %}

**Using `cli-goodies` anywhere else**<br>
Anyone running `zsh` should only need to add the following line to their `.zshrc`:

{% highlight bash %}
    source init.zsh
{% endhighlight %}

##Dependencies

You'll need to install `peru` to get the completions working. Peru is a simple file downloader with a declarative syntax. While `curl` could be used to accomplish the same, `peru` is simpler to read.

{% highlight bash %}
pip install peru
peru sync
{% endhighlight %}

##Features
**Completions**

- [_beet](https://github.com/sampsyo/beets/blob/master/extra/_beet)
- [_geeknote](https://github.com/s7anley/zsh-geeknote/master/_geeknote)
- [_git-annex](https://github.com/Schnouki/git-annex-zsh-completion/master/_git-annex)
- [_grunt](https://github.com/gruntjs/grunt-cli/master/completion/zsh)
- [_gulp](https://github.com/srijanshetty/gulp-autocompletion-zsh/master/_gulp)
- [_pip](https://github.com/srijanshetty/zsh-pip-completion/master/_pip)
- [_pandoc](https://github.com/srijanshetty/zsh-pandoc-completion/master/_pandoc)
- [_rvm](https://github.com/rvm/rvm/master/scripts/extras/completion.zsh/_rvm)
- [_sheet](https://github.com/oscardelben/sheet/master/contrib/completion/sheet.zsh)
- [_hub](https://github.com/github/hub/blob/master/etc/hub.zsh_completion)
- [_offline](https://github.com/srijanshetty/offline/blob/master/_offline)
- [_sdp](https://raw.githubusercontent.com/srijanshetty/sdp/master/_sdp)
- [_repos](functions/_repos)

**Scripts/Functions**

- [cron-wallpaper](https://github.com/srijanshetty/cron-wallpaper): Change wallpapers using cron.
- [dnd](https://github.com/srijanshetty/dnd): DND mode for Elementary OS.
- [folder2md](https://github.com/srijanshetty/folder2md): Convert a directory tree to markdown.
- [offline](https://github.com/srijanshetty/offline): Stores commands when offline and execute later in batch.
- [pastebin](functions/pastebin): Create a pastie using [sprunge.us](http://sprunge.us)
- [proxy](functions/proxy): Enable/disable proxy settings.
- [repos](functions/repos): Helper for [myrepos](myrepos.branchable.com).
- [sdp](https://github.com/srijanshetty/sdp): scp for directories.
- [showtoiletfonts](functions/showtoiletfonts): Show available toilet fonts.
- [stats-cli](https://github.com/srijanshetty/stats-cli): Compute avg, sd, min, max from a list.
- [transfer](http://transfer.sh): Use [transfer.sh](https://transfer.sh) to transfer files from the CLI.

I hope that you have fun using these tools as much as I do. PRs are encouraged.<br><br>
Fin.
