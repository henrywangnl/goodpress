
<!-- README.md is generated from README.Rmd. Please edit that file -->

# goodpress (or badpress?)

> Write to WordPress, from R Markdown, with a modern stack.

<!-- badges: start -->

[![Project Status: Concept – Minimal or no implementation has been done
yet, or the repository is only intended to be a limited example, demo,
or
proof-of-concept.](https://www.repostatus.org/badges/latest/concept.svg)](https://www.repostatus.org/#concept)
<!-- badges: end -->

The goal of goodpress is to post to [WordPress](https://wordpress.org/)
from [R Markdown](https://rmarkdown.rstudio.com/). This is mostly a
prototype since I don’t use WordPress myself. I need the prototype for a
course. :smile\_cat:

**Important disclaimer**: I don’t use WordPress, so I am not sure you
should trust me. You are welcome to volunteer to take over this
package/concept, but please tell me about it so I can add a link to your
package.

## Installation

You can install the released version of goodpress from this repository:

``` r
# install.packages("remotes")
remotes::install_github("maelle/goodpress", ref = "main")
```

### Authentication

From WordPress point-of-view this package is a “remote application”
therefore it needs your website to use an [authentication
*plugin*](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/#authentication-plugins).
At the moment, for the sake of simplicity, this package only relies on
[Application
Passwords](https://wordpress.org/plugins/application-passwords/).

You cannot install plugins if you use wordpress.com (unless you have a
costly business plan there), therefore with wordpress.com you cannot use
the REST API. There are paid services out there providing a domain name,
hosting and a one-click WordPress install, for a few dollars a month,
that you could use if you don’t roll your own server.

Here’s what I did to be able to use this package on my [test
website](https://rmd-wordpress.eu/):

  - Installed and activated the [Application Passwords
    plugin](https://wordpress.org/plugins/application-passwords/).
  - Created a new user with editor rights, not admin, and from the admin
    panel I created an application password for “rmarkdown” for that
    user.
  - In `.Renviron`, save username as `WP_USER` and password as `WP_PWD`.
  - Edited the [.htaccess file of my
    website](https://github.com/georgestephanis/application-passwords/wiki/Basic-Authorization-Header----Missing)

### Syntax highlighting

#### For R

To get syntax highlighting for R blocks, at the moment you need to add
custom CSS.

  - Find `system.file(file.path("css", "code.css"), package =
    "goodpress")` and copy it to your clipboard.
  - From your WordPress admin dasbhoard, go to Appearance \> Customize
    \> Additional CSS. Paste the CSS there and click on publish.

You could edit colors that are in the CSS file.

Later I hope to make this process easier, maybe by adding inline styles.

#### Other languages

I haven’t explored that yet.

## Workflow

Partly aspirational for now (what works at the moment is in `?wp_post`).

  - Create your posts in folders, one folder per post, with index.Rmd
    knitted to index.md and figures under a “figs” folder (so they can
    be different from non R related media).
  - The post index.Rmd should use
    [`hugodown::md_document`](https://hugodown.r-lib.org/reference/md_document.html)
    as an output format.
  - Run the function `wp_post()` that takes the path as argument, create
    a draft post in your website, uploads all image media stored in the
    “figs” folder, edits the references to image media and then
    publishes the post.
  - The first time you run `wp_post()` in a folder, it creates a file
    called `.wordpress.yml` that contains, in particular, the URL and ID
    of the post on your WordPress next time. This way, next time the
    function is run, the post is *updated*.

The “one post per folder” thing is inspired by Hugo leaf bundles.

On disk your post is stored as index.Rmd and index.md, but before upload
to the WordPress API it is transformed to HTML using
[`commonmark`](https://github.com/jeroen/commonmark) and a few regular
expressions.

## Motivation

The current best tool for writing from R Markdown to WordPress,
[`knitr::knit2wp()`](http://tobiasdienlin.com/2019/03/08/how-to-publish-a-blog-post-on-wordpress-using-rmarkdown/),
relies on a package that hasn’t been updated in years and that depends
on the no longer recommended
[`RCurl`](https://frie.codes/curl-vs-rcurl/) and `XML`. In the meantime,
WordPress gained a [REST API](https://developer.wordpress.org/rest-api/)
that to my knowledge isn’t wrapped in any [working R
package](https://github.com/jaredlander/wordpressr).

There is also the solution to [use a plug-in to sync a GitHub repo with
a WordPress blog](https://github.com/mAAdhaTTah/wordpress-github-sync/)
(see [this website](https://abcdr.thinkr.fr/soumettre-un-article/) and
[its source](https://github.com/ThinkR-open/abcdR)) but it doesn’t
handle media. If you use a GitHub repo:

  - You could set up something like a GitHub Action that’d interact with
    WordPress REST API each time you push to the default branch.
  - Are you still sure you don’t want to use a [static website generator
    instead](https://gohugo.io/tools/migrations/)? :wink: More
    seriously, I am interested in blogging workflows so feel free to
    tell me why you use WordPress (in an issue for instance).
