---
layout: single
title:  "How I changed theme on GitHub Pages"
date:   2024-11-30 19:00:00 +0100
categories: jekyll update
---

I chose to change from the default theme `minima` to something nicer. One of the most used themes is [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes/tree/master?tab=readme-ov-file). I decided to change to it. What did it take?

I used this [Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/), but it was not very practical. It covers aspects of various ways to make the switch, but repeats some instructions and is not very clear overall, so I ended up adjusting files repeatedly before I set it up allright. 

Put together, the basic instructions to follow, for a switch from theme `minima` to `minimal-mistakes-jekyll` on GitHub Pages:

1. change `Gemfile` to contain
```
source "https://rubygems.org"

gem "jekyll", "~> 4.3.4"
gem "minimal-mistakes-jekyll"

group :jekyll_plugins do
  gem "jekyll-include-cache"
  gem "github-pages"
end

```

2. replace your `_config.yaml` by the one from [the theme repo here](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml), edit it to customize: fill your info, choose one of the nine themes by setting `minimal_mistakes_skin` and so on. Here is a [Full list of configurations](https://mmistakes.github.io/minimal-mistakes/docs/configuration/).

3.  make sure your `index.md` contains 
```
---
layout: home
author_profile: true
---
```

4. change layout in existing posts. If you have just the default post from setting up the default GitHub Pages profile, that means, in file `_posts/0000-00-00-welcome-to-jekyll.md` change layout to `layout: single`

5. we still have to make the About page to work. Create a directory `_pages` and move into it files `about.md`, `404.html`. Change their layout to `layout: single` as well. Then create a directory `_data` with file `navigation.yml`, which represents the top strip with navigation links (See more on [the navigation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/)). The content of the file would be:

``` 
# main links
main:
  - title: "About"
    url: /about/
```

That should do the trick!  

Since we have GitHub Pages hosting the site, it will deploy automatically. Just go to your site at `username.github.io` and see the result!  

Full customization instructions are [in the Minimal Mistakes docs](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).
 
 