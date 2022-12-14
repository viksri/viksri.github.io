---
layout: post
title:  "Customizing Jekyll website"
date:   2022-12-18 15:03:05 +0530
categories: jekyll
---


This post is to document list of steps that I performed to customize this website.

### Changing to dark theme
I love dark themes so obviously first step for me was to figure out how to change white pages into something dark.
For this I cloned [minima theme](https://github.com/jekyll/minima) on my local system.
Latest code had some dark theme related chanegs which were not present in gem. After a bit of tweaking, I was able to
change it into dark theme.

### Adding categories in posts
It is always good to have some sort of categrization in posts, so that I can refer back to posts related to a particaulr category.
Jekyll supports this via `categories` field in front matter. In case someone reading does not know, content between `---` in the start
of page is called front matter.
Followed steps mentioned in [blog](https://blog.webjeda.com/jekyll-categories/) to show categries on individual posts and header.

### Adding buttons
I really liked the way buttons are shown in header of [hacker theme](https://github.com/pages-themes/hacker). So I cloned that theme
and copied the style of button. I tweaked it a bit to make it smaller and then used buttons to show categories within individual posts.
I also copied color scheme and font of this theme as it looked really cool.

### Adding sidebar
I liked the sidebar on right side of main content in [architect theme](https://github.com/pages-themes/architect). So again a bit of
copy + paste + tweak from that theme and I was able to add a left sidebar to show recent posts.
