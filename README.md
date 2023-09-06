# Scaling Institutions with DevOps - The Book

<p align="center">
    <a href="https://github.com/flavienbwk/book-devops/actions/workflows/render.yml">
        <img src="https://github.com/flavienbwk/book-devops/actions/workflows/render.yml/badge.svg?branch=main" alt="Build" />
    </a>
    <a href="https://github.com/flavienbwk/book-devops/actions/workflows/markdownlint.yml">
        <img src="https://github.com/flavienbwk/book-devops/actions/workflows/markdownlint.yml/badge.svg?branch=main" alt="Markdownlint" />
    </a>
</p>

<p align="center">
    <img src="./fra/images/cover_a5_source.png" width="128px"/>
    <img src="./fra/images/fourthcover_a5_source.png" width="128px"/>
</p>

<h4 align="center">:fr:</h4>
<h3 align="center"><a href="./fra/README.md" alt="Accéder au livre en version française">Le DevOps pour transformer les institutions</a></h3>
<p align="center"><i>Le guide des décideurs pragmatiques pour comprendre et agir.</i></p>

<h4 align="center">:uk:</h4>
<h3 align="center">Scaling Institutions with DevOps<sup><a href="#footnote-1">[1]</a></sup></h3>
<p align="center"><i>The pragmatic decision-makers' guide to understanding and acting.</i></p>

<br/>

## What is it ?

This repo hosts a book about how to implement DevOps in large (and mainly public) organizations, written by an SRE/DevOps engineer : [me](https://berwick.fr). So I had to make it GitOps-compliant. I hope it will be community-driven over time to fill it with good resources or enhance some parts.

While you will be able to order the physical version soon, this is the digital and interactive copy.

## Summary

Numerous organizations have embarked on their journey towards digital transformation, yet find themselves grappling to carve out a coherent and potent strategy. In this quest for advancement, they often turn to a plethora of experts, harboring hopes of achieving success.

Confronted with the imperative necessity to evolve and sustain their operational momentum, a pervasive sense of fatalism begins to take hold. In this milieu, the DevOps movement emerges as a beacon of hope. Rooted in the principles that govern the world's most successful and expansive organizations, DevOps seeks to provide viable solutions to these pressing challenges.

This book is designed to be your gateway to understanding this transformative movement, which has found its stronghold in the largest and most prosperous organizations of the world.

Designed to be both accessible and insightful, this hands-on guide, enriched with illustrations, unfolds the opportunities that state-of-the-art DevOps technologies and methodologies have to offer. It demystifies the prerequisites for organizational adaptation and guides you on embarking on your own DevOps transformation, at any scale.

## Purpose

This book is filled with recommendations about DevOps practices, including versioning everything you do : from documentation, presentations, to infrastructure recipes (IaC). So this repo is a perfect illustration of how it can be done !

I believe the practice of writing a book the gitops-style is not a bad move : it's portable, iterative, open and automatable. Of course, it's far fetched for the use case, but this is a funny way to illustrate the methodology.

_That said, this way of writing is very convenient for not being annoyed by compatibility issues when I switch from my Windows to my Linux PC._

It automatically :

<!-- - [Checks spells](https://github.com/check-spelling/check-spelling/blob/main/.github/workflows/spelling.yml) of english-written texts -->
- [Validates Markdown](https://github.com/marketplace/actions/markdown-linting-action) format
- Renders a PDF version on _develop_ and _main_
- [Updates](./.github/workflows/publish.yml) the Amazon physical version book through their API

This repo uses a [trunk-based git workflow](./fra/README.md#workflows-git) with releases automatically triggering optional actions.

## Publishing

This book has numerous lives. Let's make sure it reflects DevOps' state of the art practices at all times with your contributions.

- "Source edition" : the original book, unique, exclusively written by the author
- "Community edition(s)" : annual versions of the book including community contributions to improve it

## Supporting the author

- ⭐ Star and share this repo
- 📓 Buy the hardcover book (soon)
- ☕ Sponsor

## Book generation

This repository has [automatic](.github/workflows/render.yml) PDF, HTML and EPUB generation thanks to Pandoc.

```bash
cd ./fra && make pdf && cd -
```

## License

Copyright © 2023 Flavien BERWICK

## Useful VSCode extensions when writing

- [Spellcheck](https://github.com/bartosz-antosik/vscode-spellright)
- [Markdownlint](https://github.com/DavidAnson/vscode-markdownlint)
- [Wordcount](https://github.com/Microsoft/vscode-wordcount)
- [Todo Tree](https://github.com/Gruntfuggly/todo-tree)
- [TODO Highlight](https://github.com/wayou/vscode-todo-highlight)
- [Markdown Footnote](https://github.com/houkanshan/vscode-markdown-footnote)

<p id="footnote-1">[1] To be translated (not planned at the moment)</p>
