---
layout: post
title: Building Developer Environments in Azure, Finding VM Images
date: 2016-03-31 15:00:00 -0500
published: true
tags: Azure, Awesome, Crazy Cool
---

Recently I published a quick video over at RawTech. on Channel 9. I was in need of a development environment running in Azure. This is a fairly common ordeal for me and I have some scripts laying around that build different one’s out. The problem is they are all based on the old hotness… the Service Management API. I wanted to start with a simple, single VM running VS2015, but I wanted to use ARM templates. 

I found a problem right away… ARM templates don’t use VM Image names like the service management API. Here’s my story of discovering this and how I overcame such a problem.

<iframe src="http://ianp.co/1UX6AoZ" width="960" height="540" allowFullScreen frameBorder="0"></iframe>