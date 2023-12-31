---
author:
  name: "Ryan Carr"
date: 2023-10-26
linktitle: Why I'm Blogging
type:
- post
- posts
title: Why I'm Blogging
weight: 10
series:
- Hugo 101
---

As easy as it is writing in Notion, I want a blogging platform so that I can show off the stuff that I build. Lots of people on Reddit have talked about how having a blog to document what you do with your homelab can actually be better than having a certificate for IT. It could help get a job. 

I also realized the power of having a blog for writing a post of certain topics that were hard to solve or took a lot of research to do. If I had done this for programming, I probably would have saved a lot of time. I could have just gone back to the blog posts I made and see exactly how I solved a particular issue.

### Blogging Platforms

I want to self-host the blog on my own domain. No Twitter, no medium, no wordpress.com. Some options I can find are:

- [Blot](https://blot.im/) → Super minimal, all posts written in markup and stored in a folder in Dropbox. $4 per month
- [Wordpress.org](http://Wordpress.org) → A little bit overkill. I also hate the theming
- [Hugo](https://gohugo.io/) → This looks like the way to go for me
- [Notion](https://www.notion.so) → I would really like to use this but Its not as pretty to have a notion link as my blog domain. there are some services available to make a website from a notion page but they cost around $15 per month. But I may want to come back to this in the future because the drag-and-drop interface is wonderful.

### Hugo

I followed [this guide](https://www.freecodecamp.org/news/your-first-hugo-blog-a-practical-guide/) for the installation instructions.

[This](https://github.com/rhazdon/hugo-theme-hello-friend-ng) is the theme I chose. There are more to go through [here](https://themes.gohugo.io/).

All posts are written in markup. I push all the updates to Github. Perferably a script auto deploys the files to a static Nginx web server.
