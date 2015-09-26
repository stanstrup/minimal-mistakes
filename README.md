# My Personal Website

This is the raw version of my website which is hosted [here](http://srijanshetty.in). The website is powered by [Minimal Mistakes Jekyll Theme](https://github.com/mmistakes/minimal-mistakes), with two major changes:

- **Automated Deploys**: Directly deploy to GitHub pages by running `npm run deploy`
- **Category wise display of articles**: In addition to the timeline that *minimal-mistakes* provides, I've configured a page to display all the posts by categories.
- **Projects Page**: A display of all the creative talent in you.

## Instructions

**Creating New Posts**
    $ octopress new post "Title"

**Creating New Pages**
    $ octopress new page "Title"

**Deploying to Server **
    $ npm run deploy

## Dependencies

- ruby
    - octopress
    - jekyll
    - bundler
- NPM
    - grunt
    - grunt-contrib-clean
    - grunt-contrib-jshint
    - grunt-contrib-uglify
    - grunt-contrib-watch
    - grunt-contrib-imagemin
    - grunt-svgmin
    - grunt-gh-pages
