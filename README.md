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

Many organizations have begun their digital transformation but are struggling to establish a clear or effective strategy. They then call on many experts in the hope of success. What they have been looking for for so many years and what they did not know the name of is described in this book : DevOps.

This book aims to introduce you to this movement rooted in the largest and most successful organizations in the world.

Accessible, this practical and illustrated guide will allow you to discover the range of possibilities offered by state-of-the-art DevOps technologies, what organizational prerequisites they ask and how to implement them at your scale.

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
