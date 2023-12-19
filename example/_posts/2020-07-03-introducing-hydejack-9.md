---
layout: post
title: About me
# image: 
#   path: /assets/img/blog/jeremy-bishop@0,5x.jpg
# description: >
#   Version 9 is the most complete version of Hydejack yet.
#   Modernized design, big headlines, and big new features.
sitemap: false
---

I’m a master student in Bioinformatics at Northeastern University. I earned my bachelor degree in NEU as well, majoring in computer science with a biology minor. I’m broadly interested in computational biology, especially perturbation modeling in epigenomics. 

I used to work at the gnomAD team and Seqr team of Broad Institute and at the Devsci department of Genentech. I’m currently advised by Professor [Predrag Radivojac](https://www.khoury.northeastern.edu/home/radivojac/) at Northeastern University.

I was borned and stayed in Fuzhou until 10th grade. I finished my high school in Beverly Hills and am spending my college years in Boston.


## Personal Interests:
### Books:

  [*Philosophy, Volume 1*](https://www.goodreads.com/book/show/17303798-philosophy-volume-1) by Karl Jasper

  [*The Life of the Mind*](https://en.wikipedia.org/wiki/The_Life_of_the_Mind) by Hannah Arendt

### Music:

  [*Tchaikovsky’s Piano Concerto No. 1*](https://www.youtube.com/watch?v=2DmfJu3oNDM) by Martha Argerich or Yuja Wang

### Movie:

  [*Kung Fu Hustle*](https://en.wikipedia.org/wiki/Kung_Fu_Hustle) by Stephen Chow and other movies he directed




Version 9 is the most complete version of Hydejack yet.
{:.lead}

[Modernized](#linking-in-style) [design](#whats-in-the-cards), [big headlines](#ready-for-the-big-screen), big new features: [Built-In Search](#built-in-search), [Sticky Table of Contents](#sticky-table-of-contents), and [Auto-Hiding Navbar](#auto-hiding-navbar). That [and more](#and-much-more) is Hydejack 9.

- Table of Contents
{:toc .large-only}

## Linking in Style

Ever since the introduction of Dark Mode, link styles have been a bit of an issue. Specifically, finding an accent color that worked on both light and dark backgrounds was the problem. With Hydejack 9, the [link style](#linking-in-style) has been revamped so that legibility is no longer tied to the choice of accent_color, giving you much more freedom in creating a unique design flavor for your site.
 
## Ready for the Big Screen

The theme on which Hydejack is based was designed for a different era of the web. Hydejack has inherited many of its limitations, but over time I've made adjustments, such as centering the content column for better reading ergonomics. 

With version 9, Hydejack takes full advantage of large displays. Whether it's design indulgences such as oversized headlines, or quality of life improvements such as a floating table of contents, Hydejack now finds use for all that extra screen real estate[^1]. 
 
## What's in the Cards?

Hydejack 9 now lets you use content cards for both projects and posts. 
The cards have been redesigned with a new hover style and drop shadows and they retain their unique transition-to-next-page animations, which now also work on the `blog` layout. The new `grid` layout lets you do that.

Good images are key to making the most out of content cards. For that reason, a [chapter on images](../../docs/basics.md#adding-images) has been added to the documentation.
 
## Built-In Search

Hydejack now has Built-In Search. It even works offline. I've been prototyping many approaches and eventually settled on a fully client-side, off-the-main thread solution that perfectly fits the use case of personal sites and shows surprisingly good results[^2]. 

The new search UI is custom made for Hydejack and shows beautiful previews of your posts and pages, right on top of your regular content.

Together with the Auto-Hiding Navbar, your entire content library is now only a couple of keystrokes away.
 
## Auto-Hiding Navbar

A navbar that's there when you need it, and disappears when you don't. Simple as that.
 
## Sticky Table of Contents

Already a staple on so many sites on the web, this pattern is now also available in Hydejack. 
What's unique about it is that it simply picks up the table of contents already created by kramdown's `{:toc}` tag and transparently upgrades it to a fully dynamic version.
 
## …and much more

Other noteworthy changes include:
- Support for Jekyll 4
- Choice between MathJax and KaTeX for math rendering
- Use of `jekyll-include-cache` for drastically improved page building speeds
- New variables configuration file — adjust content width, sidebar width, font size, etc...
- ...and the option to disable grouping projects by year.

Read the the [CHANGELOG](../../CHANGELOG.md){:.heading.flip-title} for the full scope of features and improvements made in Hydejack 9.
Maybe just glance at it to confirm that it is indeed a pretty long list.
 
## Even More to Come

New features for 9.1 are already lined up. Code block headers and code line highlights for even better technical blogging, as well as download buttons on the resume page for PDF, vCard, and Resume JSON are just around the corner.
 
## Get It Now
The Free Version of Hydejack is now availabe on [RubyGems](https://rubygems.org/gems/jekyll-theme-hydejack)
and for the first time also on [GitHub Packages](https://github.com/hydecorp/hydejack/packages). 
The source code is available on [GitHub](https://github.com/hydecorp/hydejack) as always.

The PRO Version is scheduled to release on July 7th on Gumroad. Pre-Orders are open now:

<div class="gumroad-product-embed" data-gumroad-product-id="nuOluY"><a href="https://gumroad.com/l/nuOluY">Loading…</a></div>



[^1]: If you are a fan of the old two-column layout, or don't like modern design tropes such as mega headlines, Hydejack lets you revert these changes on a case-by-case basis via configuration options.

[^2]:
      Search was mainly tested for English and German. Please let me know about issues in other languages. 
      While I've tried to find a multi-language solution, most showed drastically worse  results for the English base case.
      If you're technically inclined, you can adopt the code located in `_includes/js/search-worker.js` to your needs.


