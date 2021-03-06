# blog-pwa
An experiment in mixing Hugo and Polymer PRPL into a progressive web app blog.

## Features

* It's a progressive web app with all the fixin's (service worker, PRPL pattern, H2, et cetera)
* Renders if there is no JavaScript via `<noscript>` injected fallback to static generation
* Renders metadata to linkbots when sharing without the need for client JavaScript via server side detection and alternative render path

## The basics

* [Hugo](https://gohugo.io/) to manage posts and metadata
* [Polymer and web components](https://www.polymer-project.org) app shell based on PRPL and the [SHOP](https://shop.polymer-project.org/) demo
* h2-push via [http2push-gae](https://github.com/GoogleChrome/http2push-gae) for Google App Engine for serving
* [letsencrypt-nosudo](https://github.com/arkarkark/letsencrypt-nosudo) for Let's Encrypt generation on Google App Engine

## The not-so-basics

I wrote a couple `zsh` utility scripts to power most of the shuffle and build of the site. Why not an `npm` script or a `gulp` or `grunt` task you ask? Frankly, because I just felt like writing some shell scripts. Don't you want to sometimes just write some shell scripts? Is that just me?

The gist of the tools employed and their uses include.

* `sed` is amazing and helps rangle some of the JSON output from Hugo (years of old posts + multiple times moved = fun!)
* `zmv` is the thing you don't know about but probably should. Renames files fast to proper type (Hugo won't output pure JSON at moment)
* `jq` is blazing fast over lots of files; validates my json output so I know things will load in the PWA and Python
* `polymer-cli` works without a lot of fuss and handles the frontend generation
* `http2-push-manifest` is super useful and works out of the box with http2push-gae

## Setup

```
➜ git clone git@github.com:justinribeiro/blog-pwa.git
➜ cd blog-pwa
➜ chmod +x utilities/builder.zsh

# check for tooling
➜ ./utilities/builder.zsh -t check

# get deps
➜ ./utilities/builder.zsh -t setup

# run dev env
➜ ./utilities/builder.zsh -t dev
```

## By the web perf numbers

A progressive web app is only as good as the web performance it offers. I mean, who wants to sit around waiting 10 seconds for a blog post to initially load? No one. So I pulled out my trusty [LG Optimus Exceed 2](http://www.lg.com/us/cell-phones/lg-VS450PP-optimus-exceed-2) to test on. Never heard of it? It's because it was a new middle of the road powered device from about 2.5 years ago. The device could be had pre-paid at your local market for between $15-$35 USD (I bought it for $21 on Amazon a while back), and away you go.

How does that device fair on regular 3G for a first and second load? [View the chrome timeline comparison](https://chromedevtools.github.io/timeline-viewer/?loadTimelineFromURL=https://storage.googleapis.com/jdr-public-traces/TimelineRawData-20170112-LG-VS450PP-regular3G-justinribeiro-com-firstrun.json?dl=0,https://storage.googleapis.com/jdr-public-traces/TimelineRawData-20170112-LG-VS450PP-regular3G-justinribeiro-com-secondrun.json?dl=0).

Just want the timelines json files? Download via links below:

* [Download - First load](https://storage.googleapis.com/jdr-public-traces/TimelineRawData-20170112-LG-VS450PP-regular3G-justinribeiro-com-firstrun.json)
* [Download - Second load](https://storage.googleapis.com/jdr-public-traces/TimelineRawData-20170112-LG-VS450PP-regular3G-justinribeiro-com-secondrun.json)

## Additional thoughts and words

You can read a blog post and see the site in action: [some post](https://example.com).