---
title: "Title of the Post"
date: "2020-04-01T00:00:00"
slug: "post-slug"
excerpt: "Here I summarize this fantastic post"
status: "publish"
output: hugodown::md_document
rmd_hash: b702c045bfd24741

---

Nice subsection
---------------

[A link](https://masalmon.eu)

Some inline code, [`crul::ok()`](https://docs.ropensci.org/crul/reference/ok.html).

<div class="highlight">

<pre class='chroma'><code class='language-r' data-lang='r'><span class='k'>usethis</span>::<span class='nf'><a href='https://usethis.r-lib.org/reference/use_git.html'>use_git</a></span>()
<span class='nf'>ggplot</span>(<span class='k'>mtcars</span>)
<span class='nf'><a href='https://rdrr.io/r/graphics/plot.html'>plot</a></span>(<span class='m'>1</span><span class='o'>:</span><span class='m'>19</span>)
<span class='k'>a</span> <span class='o'>&lt;-</span> <span class='kc'>TRUE</span></code></pre>

</div>

Maths
-----

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

$$x = a_0 + \frac{1}{a_1 + \frac{1}{a_2 + \frac{1}{a_3 + a_4}}} $$
