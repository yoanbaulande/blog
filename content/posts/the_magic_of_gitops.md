+++
title = "The Magic of GitOps"
date = 2025-04-07
draft = false

[taxonomies]
categories = ["Posts"]
tags = ["homelab", "gitops", "infra"]

[extra]
lang = "en"
toc = true
comment = false
copy = true
math = false
mermaid = false
outdate_alert = false
outdate_alert_days = 120
display_tags = true
truncate_summary = false
featured = false
reaction = false
+++

## Introduction

Over the past few days, I decided to dive into building my own homelab, you can actually check out the repo [here](https://github.com/yoanbaulande/homelab) if you're curious ^^.

While researching which technologies to use, I stumbled upon the concept of *GitOps*, a very interesting way to manage and deploy applications.

## Mindset

When we think about a classic homelab setup, the first idea that comes to mind is spinning up a server and manually configuring everything with tons of clicks and web interfaces.

But when you start deploying multiple servers, those manual steps quickly become repetitive. That’s where automation steps in! This beautiful concept is here to make our lives easier. And we can bring automation to our homelab using *Kubernetes* along with a GitOps system.

GitOps is all about having a **single source of truth**, which, in our case, is our Git repository. The system checks the configurations defined in the Git repo and applies them to our **cluster** accordingly.

GitOps falls under the broader umbrella of *infrastructure as code*, which means managing your infrastructure using config files. This approach helps keep everything **maintainable** and **standardized**.

## In Practice

To explain this without getting too technical: let’s say my Git repo is a file which specifies that I want one instance of a web server. The GitOps system will deploy exactly one web server in my cluster.

Now, if I currently have two web servers running, the system will automatically remove one to match what’s defined in the Git repo.

So it’s not just blindly deploying apps, it’s intelligently managing the cluster to align with the needs defined in our source of truth.

![GitOps in a nutshell](https://blogs.vmware.com/cloud/wp-content/uploads/sites/136/2021/02/GitOps-in-a-nutshell.png)

One of the major benefits of using Git as the source of truth is *version control*. Everything is **tracked** and **saved**, giving us the flexibility to roll back changes if needed.

## My Use Case

Infrastructure automation is becoming one of the biggest challenges for IT departments. Personally, I’m testing out [FluxCD](https://fluxcd.io/). Even though I’m only using it in a small-scale homelab, I can already see all the benefits.

Honestly, after trying out this philosophy, I’m pretty confident I won’t be going back to the old-school homelab setup with *Proxmox* and a bunch of VMs.

GitOps has all the advantages and prerequisites to be adopted in large-scale enterprise infrastructures. In fact, it’s already [happening](github.com/argoproj/argo-cd/blob/master/USERS.md), more and more companies are moving toward this GitOps approach, which bundles together many of the best *DevOps* practices.

## Great Resources

If you’re interested in diving deeper into this fascinating topic, here are some great resources I recommend:

- [I talk about Kubernetes, ArgoCD & GitOps (a little) by Kuberdenis](https://youtu.be/0oh2E0phV3w?si=bhzgqBjT9LjREfFp)
- [What is GitOps? by GitLab](https://about.gitlab.com/topics/gitops/)
- [What is GitOps? by Matthew Casperson](https://octopus.com/blog/what-is-gitops)