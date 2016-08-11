---
layout: post
title:  "Jekyll Deploy"
date:   2016-08-11
tags: [jekyll, yaml, liquid, markdown]
---
Journey to Creating a Jekyll Journal while learning yaml, liquid, and markdown too!
<!--more-->

To Retrieve a pre-made GemFile (Move over after creating)
{% highlight shell %}
rails new temporary-app
{% endhighlight %}

Jekyll Compose for Easy Post Creation & Syntax
{% highlight shell %}
gem install jekyll-compose
bundle exec jekyll post "NewPost"

**Commands (draft, post, publish, unpublish, page)**
bundle exec jekyll publish _drafts/my-new-draft.md --date 2014-01-24

**In Gemfile**
gem 'jekyll-compose', group: [:jekyll_plugins]
{% endhighlight %}

Ruby Gems: Installation and Update
{% highlight shell %}
gem install bundler
gem install rails

gem update --system
gem install rubygems-update
update_rubygems
{% endhighlight %}

Don't get how this works...(Look into the future)
{% highlight shell %}
https://github.com/timble/jekyll-pagination#installation
{% endhighlight %}

