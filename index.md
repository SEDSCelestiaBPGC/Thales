---
layout: default
title: Home
nav_order: 1
description: "Thales is the SEDS Celestia Documentation system. Containing docs for Korolev, Edu, Thales & Blog"
permalink: /
---

# Focus on making Quality Content
{: .fs-9 }
This website is a guide to using Celestia's Web Platforms for development. It includes documentation for Korolev, Wordpress, Edu & Thales
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/SEDSCelestiaBPGC/Thales){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## Getting started

### Basic Principles

**Speed** is the first of all priorities while writing code. Try to not ship code which does not help the user. For example, the user should not have to download React/Vue just to get some basics working after which the website finally builds or don't add Javascript for tasks which can be done with just HTML or CSS. With that said, if they add significant irreplaceable value, go all in.

> *The most optimum code is that which never runs*

**Quality** closely follows speed, have people test out and give brutal feedback for features and components. If more that 95% people don't like it. Do better. Make it again.

**Representation** If it is not fitting in place. Get rid of it. Find a better place for it, or a better feature for the place.

We use the stacks for each website
- Korolev: `Svelte (HTML, SCSS, JS)`
- Edu: `SvelteKit (HTML, SCSS, JS), Docker`
- Thales: `Jekyll (HTML + Markdown, SCSS, JS, Ruby)`