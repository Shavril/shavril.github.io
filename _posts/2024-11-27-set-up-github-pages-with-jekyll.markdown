---
layout: post
title:  "How I set up a website on GitHub Pages"
date:   2024-11-27 19:00:00 +0100
categories: jekyll update
---

I decided to set up this site on `GitHub Pages`. It uses `Jekyll` to compile `Markdown` language into a html site. To be able to use it, I had to set up and install a couple of tools first. 

1. Set up repository on GitHub in [this way](https://pages.github.com/)
2. Get [GitHub Desktop](https://github.com/apps/desktop)
3. Install Ruby. Since I use Windows, I used [RubyInstaller](https://rubyinstaller.org/).  
   RubyInstaller is a self-contained Windows-based installer that includes the Ruby language, an execution environment, important documentation, and more. 
	- Download and install a Ruby+Devkit version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/). Use default options for installation.
    - in `PowerShell`, run `ridk install`. This is needed for installing gems with native extensions. You can find additional information regarding this in the RubyInstaller Documentation. From the options choose `MSYS2 and MINGW development toolchain`.
4. [Install Jekyll](https://jekyllrb.com/docs/installation/windows/). Open a new `PowerShell` window, so that changes to the `PATH` environment variable becomes effective. Install Jekyll and Bundler using `gem install jekyll bundler`
5. Check if Jekyll has been installed properly by `jekyll -v`, if the command does not work, restart the system and try again. 
6. Still in the `PowerShell`, go into the local repository folder you created earlier with GitHub Desktop and create a new Jekyll project with `jekyll new project_name`. I wanted it to be in the root of repository, but it doesn't allow only `jekyll new`, so I created a project and the moved the files into parent directory, it worked as well. 
7. Use `Github Desktop` to `commit` and `push` the changes to the repository. GitHub should automatically run checks and deploy the site.
8. Go to `https://your_username.github.io/` to see the default main page!
