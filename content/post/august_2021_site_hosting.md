---
title: "Hosting this site"
date: 2021-09-14
---
### How it Began
I have had a personal site since 2016, but the hosting has changed over the time.  It started out with one of those free Google sites which can be viewed below.
{{< image src=/images/google_site.png  set=fit >}}
That looked dated from when it was first published, and some of the components in the site no longer exist. And it was hard to update the site since I had to log into ui and it wasn't that easy to make updates.

The second iteration is I found a free Wordpress hosting provider which worked, but I let my account lapse since I didn't log in enough and the site was deleted.  After that I bought a domain (flowalex.tech)[^1] and got a cheap hosting provider where I had a Drupal site.  I had a few issues with that, the first is that they only supported Drupal 7 (I wanted to use Drupal 8) and they charged quite a bit for a ssl cert and I couldn't use lets encrypt, so I used CloudFlare for the free ssl and a proxy to route traffic to the site.  Since it was too much work keeping that updated and they required a ssl cert to keep hosting the site I decided to let that one lapse.

## Where it is Today
 A few years ago I learned about Hugo and using it for hosting a blog/personal site with GitHub/GitLab and decided to host it on GitLab using their static site generator CI/CD template[^2]. at first I was just using the free url from GitLab, [flowalex.gitlab.io](https://flowalex.gitlab.io), the site is still available at this url, and had been using that and had routed my other personal domain (alexanderwolf.io) through cloudflare to the gitlab site for the analytics data, since the gitlab.io address already had ssl.
{{< image src=/images/hugo_site_v1.png  set=fit >}}
I was happy with GitLab and having the site there, I even had a second one created to share recipes and use as a digital cookbook.  After a while I was getting tired of the theme that I had been using and wanted something different so I started using Netlify to host some of the sites, and I tried routing my flowalex.tech domain through Cloudflare to it, but that wasn't something that can be done so I gave up on that and use the self generated urls for testing the different jamstack generators and different Hugo themes.
{{< image src=/images/netlify_tests.png  set=fit >}}

In April of 2021 Cloudflare announced Cloudflare Pages[^3], a tool to host static sites that are built from GitHub.  When they first came out I took a look to see how they worked and created a test blog, [blog.flowalex.tech/](https://blog.flowalex.tech/) to see how it worked and then also created a personal notes site.  While it didn't intergrate with GitLab one of the features I liked better than the GitLab CI/CD pipeline is that Cloudflare would generate a preview when you made a PR to see if everything looked good and built on their platform.  Since most content on the GitLab version had already been migrated for testing Cloudflare Pages, all I had to do was remove the a records and cnames that were pointing to gitlab and configure them to point to the Cloudflare pages site (Took about 5 mintues). I'm currently using the free plan and I haven't come anywhere near the limit of 500 builds a month or had any issues with only having one build run at a time.

{{< image src=/images/cloudflare_pages.png  set=fit >}}

[^1]: This url doesn't host anything currently
[^2]:https://docs.gitlab.com/ee/user/project/pages/
[^3]: https://pages.cloudflare.com
