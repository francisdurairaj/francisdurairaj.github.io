---
layout: post
title: "gh-pages in sync with master"
description: "gh-pages in sync with master"
headline: mail sender
categories: 
  - Blogging 
  - "web development"
tags: blog git 
imagefeature: 
imagecredit: 
imagecreditlink: 
comments: true
mathjax: false
featured: true
published: true
---

Easily keep gh-pages in sync with master

normal github workflow

{% highlight js %} 

git add .
git status // to see what changes are going to be commited
git commit -m 'Some descriptive commit message'
git push origin master

{% endhighlight %} 

Commands given below is used to update the gh-pages in sync with the master

{% highlight js %} 

git checkout gh-pages // go to the gh-pages branch
git rebase master // bring gh-pages up to date with master
git push origin gh-pages // commit the changes
git checkout master // return to the master branch

{% endhighlight %} 	