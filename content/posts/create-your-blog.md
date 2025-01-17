+++
title = "Create your Blog with Zola and Cloudflare Pages"
date = 2025-01-17
draft = false

[taxonomies]
categories = ["Posts"]
tags = ["blog", "markdown", "tutorial"]

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

In this post, I'll document my journey of creating a static website using [Zola](https://www.getzola.org/) and hosting it on [Cloudflare Pages](https://pages.cloudflare.com/).

If you're reading this post, it means the blog setup was successful! :)

## Technology Choices

I chose Zola primarily because it perfectly matched my needs with its straightforward approach. Zola makes it simple to create a static site and integrate a blog. One of my must-have requirements was theme support, as I'm neither an artist nor a designer by nature. What really won me over was Zola's advanced Markdown note management capabilities.

While [Bear Blog](https://bearblog.dev/) was an option, I found it too minimalistic for my needs. [Hugo](https://gohugo.io/) is another excellent framework, but it comes with many features I didn't need and adds unnecessary complexity.

As for hosting, I opted for Cloudflare Pages because its **free plan** is more than sufficient for my small static site. A major advantage was its built-in support for various frameworks, including Zola.

Beyond its clean and comprehensive interface, which I particularly appreciate, Cloudflare has built a true ecosystem. This makes it incredibly easy to register a domain name on their platform, link it to your site with just a few clicks, and configure all security settings seamlessly.

## Installation

After installing Zola (installation guide available [here](https://www.getzola.org/documentation/getting-started/installation/)), create your project by running the `zola init` command. You'll be asked several questions to initialize the project. For now, you can leave everything at default settings (these parameters can be modified later).

```bash
zola init myblog

> What is the URL of your site? (https://example.com):
> Do you want to enable Sass compilation? [Y/n]:
> Do you want to enable syntax highlighting? [y/N]:
> Do you want to build a search index of the content? [y/N]:
```

Next, navigate to the created directory, initialize a Git repository, and install a theme. I personally chose the [Serene theme](https://www.getzola.org/themes/serene/), but you can create your own theme or choose one from the community [here](https://www.getzola.org/themes/).

```bash
git init

git submodule add -b latest https://github.com/isunjn/serene.git themes/serene
```

Follow the theme-specific instructions to configure and integrate it with your blog.

Create a Git repository on [GitHub](https://github.com/) or [GitLab](gitlab.com), then push your initialized blog and theme to this repository.

```bash
git remote add origin https://github.com/<your-gh-username>/<repository-name>
git branch -M main
git push -u origin main
```

## Deployment

Head to the [Cloudflare dashboard](https://dash.cloudflare.com/), and from the Home menu, navigate to: **Workers & Pages** > **Create application** > **Pages** > **Connect to Git**

Select your repository, then choose Zola as your framework in the deployment configuration.

You'll need to add an **Environment Variable** in the *advanced* section to specify the Zola version. For example: `ZOLA_VERSION: 0.19.2`

After these steps, deploy your site. The dependencies will install, and the site will build before deployment.

During my first deployment, I encountered a build issue:

```
Executing user command: zola build
/bin/sh: 1: zola: not found
Failed: Error while executing user command. Exited with error code: 127
Failed: build command exited with code: 1
Failed: error occurred while running build command
```

Create the project anyway, even if the deployment fails. Then go to the project settings, find the build section, and change the *Build system version* from the default **2** to version **1**.

Note that using version 1 means you'll have slightly older application versions. If you want to use newer versions, you can add specific **Environment Variables** in the *Variables and Secrets* settings. For example: `NODE_VERSION: 23`

On the second deployment, I encountered another issue:

```
Error: Failed to build the site
Error: Failed to load theme serene
Error: Reason: Failed to open file /opt/buildhome/repo/themes/serene/theme.toml
Error: Reason: No such file or directory (os error 2)
Failed: build command exited with code: 1
Failed: error occurred while running build command
```

To fix this user structure issue, go to the settings in *Build configuration* and modify the *Build command* to (if you use the same theme as me):
`rm -rf themes/serene && git clone --depth 1 -b latest https://github.com/isunjn/serene.git themes/serene && zola build`

The deployment should now work, and you'll be able to see your static site at the provided address.

To set up a custom domain, go to the *Custom domains* section and follow the guided steps to add your domain name.

Finally, return to your code and modify the *config.toml* file at the repository root to replace "*example.com*" with your domain name:

```toml
# The URL the site will be built for
base_url = "https://my-zola-project.pages.dev"
```

Don't forget to commit and push your changes so Cloudflare can deploy the updates with the new version!