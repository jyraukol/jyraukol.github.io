---
layout: post
title:  "Running Jekyll on Windows 10"
date:   2017-02-15 07:00:48 +0300
categories: jekyll
---
# How to get Jekyll running on Windows 10

I've been meaning to try out Jekyll for some time. Installing Jekyll was simple on my Linux laptop, but Jekyll isn't officially supported on Windows. On Windows 10, getting Jekyll to run,
required some additional steps. Writing them down also makes for great practice writing Jekyll posts.

If you want to learn more about Jekyll, head on over to [https://jekyllrb.com/](https://jekyllrb.com/).

## Bash on Ubuntu on Windows

The Linux Subsystem and Bash on Ubuntu on Windows was used during the installation. It's a nice tool anyways, so install it first. You can find the installation instructions and more
information from [Microsoft Developer Network](https://msdn.microsoft.com/en-us/commandline/wsl/about).

## Installing Ruby

Jekyll uses Ruby. Good instructions for installing Ruby can be found at [Go Rails](https://gorails.com/setup/windows/10) that I used. I'll just summarize the process here, but check out the link.
There's also info on getting Rails installed on Windows.

**Install required dependencies for Ruby**
```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
```
**Install Ruby, I used the rbenv route:**
```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 2.4.0
rbenv global 2.4.0
ruby -v
```
Now we are ready to install Jekyll itself. It's simple, just install the Ruby gem.
Install the bundler gem at the same time.
```
gem install jekyll bundler
```
Create a new Jekyll site and get it running:
```
jekyll new jekyll-test
cd jekyll-test
jekyll serve
```
Jekyll should start up and you can access the site at localhost:4000.
## Issues
You might notice a warning about automatic generation not working with
Bash on Ubuntu on Windows. Jekyll will automatically generate and serve files
that have been changed while Jekyll is running. This is nice when developing
your site.
But this feature might not work on Windows 10 or Jekyll won't even start.
If you have trouble starting Jekyll, you can disable automatic generation:
```
jekyll serve --no-watch
```
With the no-watch argument you have to restart Jekyll to see changes to your site.

The issue is detailed [here](https://github.com/Microsoft/BashOnWindows/issues/216).
It has been resolved and should be included in the next big Windows 10 update,
the Creators Update. So you can just live without automatic generation for now
and wait for the update. If you are subscribed to the Windows Insider builds,
you should have the update already.

## Resources
* [https://jekyllrb.com/](https://jekyllrb.com/)
* [https://labs.sverrirs.com/jekyll/](https://labs.sverrirs.com/jekyll/)
Another way of installing Jekyll.
