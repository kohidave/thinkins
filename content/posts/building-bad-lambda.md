---
title: "Building Bad Lambda"
date: 2020-01-20T20:57:39-08:00
draft: false
---

Here's a small confession, when I first joined the ECS team, I'd spun up a container exactly once in my entire life and had no idea how to use ECS, at all. There was around a month between when I accepted the ECS offer and when I'd actually start on the team, so this was my window to learn about containers, ECS, Fargate and everything else that I didn't know anything about. I picked up a copy of [Docker Deep Dive](https://www.amazon.com/Docker-Deep-Dive-Nigel-Poulton-ebook/dp/B01LXWQUFF) and plowed through it. I was really struck that containers were an excellent way of creating portable snapshots of your application, and having banged my head against the proverbial wall trying to deploy a rails app on EC2 years ago, I immediately groked their value.  I read through Docker Deep Dive, built images, dissected them, and just generally poked and prodded anything I could. It was honestly a lot of fun 🌈

When I pivoted my focus to ECS, I opened up the docs, but was having a hard time digesting all the new terminology. I skimmed over some of the terms, _cluster_, _services_, _fargate_, _target groups_, but none of the terms made a lot of progress penetrating my brain 🧠. Rather than try to absorb ECS through the docs (which is a lot like trying to learn a language by just thumbing through a dictionary), I decided to start with what I did know and go from there. So, what did I know about ECS? 

* I knew ECS was the way for me to "run" containers on AWS. 
* I knew Fargate was a magic term which meant I didn't have to deal with EC2. 

Ok, so I knew what ECS was for, so how could I use that to actually learn more about it? When I had that "a ha!" moment learning about Docker, it was because I figured out the problem it was trying to solve, and I could just start throwing problems at it, playing with it and refining my understanding. Now that I had a high level understanding of ECS, I needed to come up with a project I could build and play with, but what? 

Another thread that I had in the back of my mind was "If ECS is the place where I can run my code without needing to provision instances, how is that different from Lambda?" Lambda "just" takes some stored code, some user provided input, executes it and returns the results (this is a pretty simplified summary of what Lambda does). Well, what better way to see how ECS and Lambda are different than to try to build one with the other. 

## Bad Lambda

I had my project, build a "Bad Lambda" on Fargate and ECS.

I spent the next day at work writing a super simple, local service in Go which had the following APIs:

1. __CreateFunction__ which took a blob of ruby code, stored it in S3, and returned a function handle (which was just the name of the uploaded file in S3)
2. __ExecuteFunction__ which took in a json input and a function handle, downloaded the function code from S3, shelled out to ruby and ran eval on the code (omg don't tell security plz). It then took the output of that eval and stored it in S3 and returned a signed URL to the results file. 

I got this monstrosity working locally, with a Dockerfile, gnarly code and strong resolve to ignore the voice in my head asking me if I really wanted to be calling `eval` on arbitrary code passed in by users. That voice silenced, I started trying to figure out how to get it working in ECS. At this point, I just start googling and hoping for that one, super easy "How to Deploy a container to ECS in 5 simple steps" article, somewhere. I tumbled through some official documentation, a bunch of StackOverflow posts, a few useful Medium posts, and just for good measure, a couple of youtube videos.

Eventually, I managed to create the all the resources I needed:

1. A cluster, which is just a namespace for a bunch of related services.
2. An ECS Service, which is just my the thing that ensures that at least some specified number of containers is running at any given time.
3. An ECR Repo, where I could store BadLambda's images
4. A bespoke TaskDefinition, which was, more or less, a pointer to my BadLambda image and some configuration on the amount of CPU and Memory my container would have

Now that I had all these terms grounded in something I was trying to do, around me trying to deploy Bad Lambda, I was able to connect them together into my own mental model. I WAS INVINCIBLE (ok, I didn't understand what 99% of terms in the TaskDef meant, but I was making progress, ok?). I pushed BadLambda to ECR, registered my TaskDefinition and updated my BadLambda service to use that task definition.

After a few seconds, I was staring at Bad Lambda - two instances of my image, running on Fargate and managed by ECS. I didn't know exactly what I was doing, but I knew the shape of what I was looking at, and I had a toy that I could play around with.

## Playing is cool 😎 

I loved showing off this ridiculous tool, which was actually kind of cool, to my friends, and watch as they created and executed their own functions. Writing Bad Lambda gave me the motivation to plow through all the discomfort of having to learn a bunch of new concepts by giving me something to look forward to (BadLambda happily running untrusted code in the cloud 🌩). Building silly, wonderful experiments like this speaks to the power of experimenting. Even the best, most eloquent documentation is no substitute for actually playing, even if what I built drained the blood from our poor security engineer's face 🥰

So, are you stuck on a problem? Intimidated by the vocabulary or concepts of something in the computer world? Go play with it, you'll be delighted at how much you pick up and how much fun you'll have doing it.

* BadLambda was shut down after my experiments were done - no security engineer was harmed in the creation of this service.

** BadLambda also ran in the private subnet of a VPC, and could only be called from a bastion host in that VPC (so it wasn't actually exposed to the world). Be cool, don't run eval on strangers' code. 

