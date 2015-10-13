---
layout: post
title: "Announcing Uptime End of Life"
published: true
excerpt: "Uptime, the remote monitoring application using Node.js, MongoDB, and Twitter Bootstrap that I started almost 4 years ago as an exercise, won't be maintained anymore. Read on to see why."
image: /images/uptime2.png
tags:
- Node.js
- Uptime
---

<a href="https://github.com/fzaninotto/uptime"><img src="/images/uptime2.png" class="medium"/></a>

[Uptime](https://github.com/fzaninotto/uptime), the remote monitoring application using Node.js, MongoDB, and Twitter Bootstrap, has done its time. I started this project almost 4 years ago as an exercise to learn Node.js. It became much more popular than I expected (more than 2,800 starts on GitHub!), and I quickly found myself spending more time maintaining it than I could give. During the past 2 years, my support on this project has been reduced to almost zero, and the number of open issues has been rising. So it's time to officially announce Uptime's end of life for good.

There are many reasons why maintaining this app isn't very rewarding. The architecture is not very good, all third-party components are outdated, MongoDB causes many problems in production. If I had to rebuild Uptime today, I'd probably create an API-first app written in [Go](https://golang.org/), and a fully static frontend written in [React.js](https://facebook.github.io/react/), with charts in [d3.js](http://d3js.org/). One of our interns at marmelab even [gave it a try](https://github.com/marmelab/uptime). 

But most of all, I don't use Uptime myself anymore. Maintaining an open-source project that you don't use is like carrying someone else's grocery bag. It's fun at first, but it's hard to keep doing it every day when you need to do your own shopping.

There are many, many alternatives to uptime, open-source or commercial, doing a much better job. See for instance [this list of more than 100 Website Monitoring Services](http://www.supermonitoring.com/blog/the-updated-list-of-website-monitoring-services/). Some of these are really great, and deserve the few euros or dollars per month that they ask for the service. That's another motivation for me: what's the point of building a free tool to replace commercial alternatives? Open-source is about creating value. Uptime is destroying value.

Anyway, it's been fun building this product and watching it rise in popularity. I have no doubt that current Uptime users will find a cheap alternative for their needs. 
