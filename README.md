# Container Tools

Welcome to the site for [Buildah](https://github.com/projectatomic/buildah/blob/master/README.md). This [site](https://containers.github.io/buildah.io) features announcements and news around Buildah, and occasionally other [container tooling](https://github.com/containers/) news.

![Buildah logo](https://github.com/containers/buildah.io/blob/main/images/buildah.png)

## Website Contributors

The website runs on GitHub Pages via [Jekyll](https://jekyllrb.com/) to make it as convenient as possible for you to contribute.

Before you start, please verify that you've an entry for yourself in the top level _config.yml file in the 
`authors` section.  Your entry should look like the following example.  Please note if you do not have a gravatar, a twitter account or simply don't want to share a particular field, just leave the field blank or completely remove the particular line.

```
  jsmith:
    name: Jessica Smith
    display_name: Jessica Smith
    gravatar: c69c8419c8e4d1bbedc7874281453781 
    email: jsmith@mycompany.com
    web: https://mywebsite.com
    twitter: JSmithOnTwitter
    github: JSmithOnGitHub
```

You can add blog posts by adding a file to the `_posts` folder. The file must use the following naming convention: `yyyy-mm-dd-relevant-title-here.md`.  In the file itself, you will need to start with the following metadata:


```
---
title: <your title here>
layout: default
author: <author id, from the example above 'jsmith'>
categories: [blogs]
tags: <your tags here>
---
![buildah logo](https://buildah.io/images/buildah.png)

{% assign author = site.authors[page.author] %}
# My Blog Title
## By {{ author.display_name }} [GitHub](https://github.com/{{ author.github }}) [Twitter](https://twitter.com/{{ author.twitter }})

<yourtext in markdown format goes here, check out other blog posts if you're unsure how to proceed>
```

Please pay attention to the `categories: [blogs]` section. Currently, there are 3 categories available: `[blogs]`, `[releases]`, and `[new]`.

**NOTE:** If you want to add a ':' (colon) to your title, you will need to instead use `&#58;`, otherwise the post will not be displayed on the index page.  For example:

```
Instead of:

title: My first blog post: Can you believe it?

use:

title: My first blog post&#58; Can you believe it?
```

# New 'main' branch

To be more inclusive, the `master` branch for this repository has been renamed to `main`.  If you have a local clone, you can update it by running:

```
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```
