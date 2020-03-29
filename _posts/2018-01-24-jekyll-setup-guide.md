---
layout: post
title:  "Jekyll Setup Guide"
date:   2018-01-24 00:00:00  +0800
categories: jekyll
---
As of now, this guide will only cover commands that are specific to linux environment since i used Ubuntu in creating this guide.

<!-- more -->

# Initial Project Setup

### 1. Install curl

{% highlight sh %}
sudo apt install curl
{% endhighlight %}


### 2. With curl, you can now install node.js
{% highlight sh %}
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs
{% endhighlight %}


### 3. You will need ruby to run jekyll
{% highlight sh %}
sudo apt-get install ruby-full
{% endhighlight %}


### 4. With these, you may install jekyll finally
{% highlight sh %}
gem install jekyll bundler
{% endhighlight %}


### 5. Now create your jekyll project
{% highlight sh %}
jekyll new my-awesome-site
{% endhighlight %}


### 6. Finally, we start our server
{% highlight sh %}
bundle exec jekyll serve
{% endhighlight %}


<h1>Some Extras</h1> 
<p>Here I cover some other stuff about installing brackets editor or if you encountered some of the issues I had or just want to install a plugin.</p>


### a. If you like to use Brackets code editor
{% highlight sh %}
sudo apt-get install brackets
{% endhighlight %}


### b. Wanna install github-pages?
{% highlight sh %}
#Copy and paste in gem file

source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins

#Then run bundle install in the command line
{% endhighlight %}


### c. Getting some damn errors?
{% highlight sh %}
sudo apt-get update
sudo apt-get install zlib1g-dev
sudo gem install nokogiri
bundle update
{% endhighlight %}


### d. Some jekyll commands for building
{% highlight sh %}
$ jekyll build
# => The current folder will be generated into ./_site

$ jekyll build --destination <destination>
# => The current folder will be generated into <destination>

$ jekyll build --source <source> --destination <destination>
# => The <source> folder will be generated into <destination>

$ jekyll build --watch
# => The current folder will be generated into ./_site,
# watched for changes, and regenerated automatically.

$ jekyll serve
# => A development server will run at http://localhost:4000/
# Auto-regeneration: enabled. Use `--no-watch` to disable.

$ jekyll serve --detach
# => Same as `jekyll serve` but will detach from the current terminal.
# If you need to kill the server, you can `kill -9 1234` where "1234" is the PID.
# If you cannot find the PID, then do, `ps aux | grep jekyll` and kill the instance.

$ jekyll serve --no-watch
# => Same as `jekyll serve` but will not watch for changes.
{% endhighlight %}


### e. If you forgot your commands, you may want to install jekyll docs
{% highlight sh %}
# Install the gem
sudo gem install jekyll-docs

# To launch the docs
bundle serve jekyll docs

# need to add in Gemfile
gem 'jekyll-docs'
{% endhighlight %}

### f. If you do not have the latest ruby (e.g. 2.4.X)

{% highlight sh %}
\curl -sSL https://get.rvm.io | bash -s stable

rvm list known

rvm install ruby-2.4.2
{% endhighlight%}