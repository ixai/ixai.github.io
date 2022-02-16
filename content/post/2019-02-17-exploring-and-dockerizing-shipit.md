---
title: Exploring and Dockerizing Shipit
date: 2019-02-17
slug: exploring-and-dockerizing-shipit
---

I recently looked into [Shipit](https://github.com/Shopify/shipit-engine) to see if it was a fit for my team's development workflow. The idea behind the [merge queues](https://engineering.shopify.com/blogs/engineering/introducing-the-merge-queue) seemed very attractive to me. Enter the setup guide:

> Deploying and hosting a Rails application is not trivial, and this document assumes you know how to do it.
>
> In the future we'd like to provide it fully packaged inside a Docker container, but it hasn't been done yet.

And so I took a stab at dockerizing my first Rails application. I packaged the resulting code as a repository ([ixai/shipit-docker](https://github.com/ixai/shipit-docker)) that contains instructions on how to build the Docker image and run it using `docker-compose`.

The setup itself is very straightforward, and is mostly the result of following their [setup guide](https://github.com/Shopify/shipit-engine/blob/master/docs/setup.md) and modifying the docker files provided by [arthurnn/shipit_docker](https://github.com/arthurnn/shipit_docker).

As someone not familiar with Rails (or Ruby), most of the issues I ran into were with the configuration of the application. As a result, I tried to simplify the Rails template and configure the application by mounting and copying files instead. I understand this might not be consistent with the Rails ecosystem or the 12factor methodology, but I believe it to be simpler. Particularly, setting the GitHub app's private key in the `config/secrets.yml` file wasn't evident: I wasn't able to set it as an environment variable since it's a multiline string.

Once the application was up and running, the main problem was that webhooks sent by GitHub weren't reaching my Shipit instance ([#871](https://github.com/Shopify/shipit-engine/issues/871)). Luckily it was a known issue and had an easy fix.

The repo is not production-ready, so take it as an easy way to try out Shipit and sell it to your team. One thing I was dissapointed to find out is that the browser plugin that allows you to queue merges from the GitHub interface isn't publicly available yet. This means that introducing Shipit would require a workflow disruption: don't merge from GitHub, do it from Shipit. For me, this is a minor inconvenience, but I see how others could opose it. Shipit also provides much more than merge queues, so while that was my main objective this time I'll need to keep exploring its fit into my team's workflow.
