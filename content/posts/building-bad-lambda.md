---
title: "Building Bad Lambda"
date: 2020-01-20T20:57:39-08:00
draft: false
---

Here's a small confession, when I first joined the ECS team, I'd spun up a container exactly once in my entire life and had no idea how to use ECS, at all. There was around a month between when I accepted the ECS offer and when I'd actually start on the team, so this was my window to learn about containers, ECS, Fargate and everything else that I didn't know anything about. I picked up a copy of [Docker Deep Dive](https://www.amazon.com/Docker-Deep-Dive-Nigel-Poulton-ebook/dp/B01LXWQUFF) and plowed through it, learning about Dockerfiles, Docker Images, Overlay FS, local networking and so much more. I followed along, built images, inspected them, dissected them, and just generally poked and prodded anything I could. It was a lot of fun 🌈.

When I pivoted my focus to ECS, I opened up the docs, but was having a hard time digesting all the terminology. I skimmed over some of the terms, Cluster, Services, Fargate, Target Groups - but none of the terms made a lot of progress penetrating my brain 🧠. Rather than try to absorb ECS through the docs (which is a lot like trying to learn a language by just reading a dictionary), I decided to start with what I did know and go from there. So, what did I know about ECS? 

* I knew ECS was the way for me to run containers on AWS. 
* I knew Fargate was a magic term which meant I didn't have to deal with EC2. 

Ok, so I knew what ECS was for, so how could I use that actually learn more about it? Well, I figured if I could actually build something on top of these tools, I'd plow through the terminology and learn by doing. But what could I build? 

Bad Lambda.

I knew that Fargate was the 'serverless' of containers, and I was a little confused by how that would be different from Lambda, so I decided to try and build a bad version of Lambda using ECS and Fargate! 

I spent a day writing a super simple service in Go which had the following APIs:

1. __CreateFunction__ which took a blob of ruby code, stored it in S3, and returned the function name (which was just the name of the file in S3)
2. __ExecuteFunction__ which took in a json input and a function name, downloaded the function code from S3, shelled out to ruby and ran eval on the code (omg don't tell security plz). It then took the output of that eval and stored it in S3. It returned a signed URL to the results. 

I got this monstrosity working locally, with a Dockerfile, gnarly code and strong resolve to ignore the voice in my head asking me if I really wanted to be calling `eval` on arbitrary code passed in by users. That voice silenced, I started trying to figure out how to get it working in ECS. "Deploy container to ECS" I googled, to limited success. "Run container in ECS", I tried instead - slowly making progress in learning the parlance. Eventually, with an ECR repo created, my image pushed and a bespoke taskdef deployed to my service, I was staring at Bad Lambda - running 2 Fargate tasks, managed by ECS. I didn't know exactly what I was doing, but I knew the shape of what I was looking at, and I had a toy that I could play around with.

I loved showing off this ridiculous tool, which was actually kind of cool, to my friends, and watch as they created and executed their own functions. Writing Bad Lambda gave me the motivation to plow through all the discomfort of having to learn a bunch of new concepts by giving me something to look forward to (BadLambda happily running untrusted code in the cloud 🌩). Building silly, wonderful experiments like this speaks to the power of experimenting. Even the best, most eloquent documentation is no substitute for actually playing, even if what I built drained the blood from our poor security engineer's face 🥰

* BadLambda was shut down after my experiments were done - no security engineer was harmed in the creation of this service.

** BadLambda also ran in the private subnet of a VPC, and could only be called from a bastion host in that VPC (so it wasn't actually exposed to the world). Be cool, don't run eval on strangers' code. 

