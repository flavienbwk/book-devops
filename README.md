# Scaling Institutions with DevOps - The Book

<p align="center">
    <a href="https://github.com/flavienbwk/book-devops/actions/workflows/render.yml">
        <img src="https://github.com/flavienbwk/book-devops/actions/workflows/render.yml/badge.svg?branch=main" alt="Build" />
    </a>
    <a href="https://github.com/flavienbwk/book-devops/actions/workflows/markdownchecks.yml">
        <img src="https://github.com/flavienbwk/book-devops/actions/workflows/markdownchecks.yml/badge.svg?branch=main" alt="Markdownlint" />
    </a>
</p>

<h4 align="center">:us:</h4>
<h3 align="center"><a href="./eng/README.md" alt="Access the book in english version">Scaling Institutions with DevOps</a><sup></sup></h3>
<p align="center"><i>The pragmatic decision-makers' guide to understanding and acting.</i></p>
<p align="center" style="color: gray; font-size: 0.9em;">Paperback and ebook with foreword</p>

<p align="center">
    <img src="./eng/images/cover_a5_source_thumb.png" width="128px"/>
    <img src="./eng/images/fourthcover_a5_source_thumb.png" width="128px"/>
</p>

<h4 align="center">:fr:</h4>
<h3 align="center"><a href="./fra/README.md" alt="Accéder au livre en version française">Le DevOps pour transformer les institutions</a></h3>
<p align="center"><i>Le guide des décideurs pragmatiques pour comprendre et agir.</i></p>
<p align="center" style="color: gray; font-size: 0.9em;">Livre broché et ebook préfacés</p>

<p align="center">
    <img src="./fra/images/cover_a5_source_thumb.png" width="128px"/>
    <img src="./fra/images/fourthcover_a5_source_thumb.png" width="128px"/>
</p>

<br/>

## What is it ?

This repository hosts a comprehensive guide to implementing DevOps in large organizations, addressing the challenges from fostering cultural shifts to navigating technical and HR transformations.

_Scaling Institutions with DevOps_ was written from [my SRE/DevOps experience](https://berwick.fr/en) to benefit enthusiasts, mainly from the public sector, to overcome these technical and transformational challenges.

As a DevOps advocate, I had to make this book GitOps-compliant, this is why it is hosted here. I hope it will be **community-driven** to fill it with good resources and make improvements as practices evolve. Please contribute through _Pull Requests_ and _Discussions_.

Here are the different ways to access this writing :

| Type             | French                                                                                                                      | English                                                                                                                                                                       |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web version      | [Lire maintenant](https://book-devops.berwick.fr/fra/index.html)                                                            | [Read now](https://book-devops.berwick.fr/eng/index.html)                                                                                                                     |
| Markdown version | [Lire maintenant](./fra/README.md)                                                                                          | [Read now](./eng/README.md)                                                                                                                                                   |
| Ebook version    | [Amazon](https://www.amazon.fr/dp/B0CKHV5QB7) / [Google Books](https://play.google.com/store/books/details?id=3u_bEAAAQBAJ) | [Amazon](https://www.amazon.com/dp/B0CT8RY844) / [Google Books](https://play.google.com/store/books/details/Flavien_BERWICK_Scaling_Institutions_with_DevOps?id=bxvwEAAAQBAJ) |
| Paperback book   | [Amazon](https://www.amazon.fr/dp/B0CKJ6SLV3)                                                                               | [Amazon](https://www.amazon.com/dp/B0CT6ZF5GZ)                                                                                                                                |
| Hardcover book   | [Amazon](https://www.amazon.fr/dp/B0CKJ651K9)                                                                               | N/A                                                                                                                                                                           |
| Audiobook        | N/A                                                                                                                         | [_Soon_](./eng/AUDIOBOOK.md)                                                                                                                                                  |

> The original book was written in French. The English version was reworked to include america-related examples and use cases.

## Summary

Numerous organizations have embarked on their journey towards digital transformation, yet find themselves grappling to develop a coherent and effective strategy. In their quest for improvement, they often turn to a plethora of experts, harboring hopes of achieving success.

Confronted with the imperative necessity to evolve and sustain their operational momentum, a pervasive sense of fatalism begins to take hold. In this situation, the DevOps movement emerges as a beacon of hope. Rooted in the principles that govern the world's most successful and expansive organizations, DevOps seeks to provide viable solutions to these pressing challenges.

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

## Supporting the author

- ⭐ Star and share this repo
- 📓 Buy the [paperback](https://www.amazon.fr/DevOps-pour-transformer-institutions-pragmatiques/dp/B0CKJ6SLV3) or [hardcover](https://www.amazon.fr/DevOps-pour-transformer-institutions-pragmatiques/dp/B0CKJ651K9) book (including foreword)
- 📘 Buy the [ebook](https://www.amazon.fr/DevOps-pour-transformer-institutions-pragmatiques-ebook/dp/B0CKHV5QB7) (including foreword)
- ❤️ Sponsor me

## Contributions and publishing process

This book has numerous lives. Let's make sure it reflects DevOps' state of the art practices at all times with **your** contributions.

- **Source edition** (1.x.x) : the original book, unique, exclusively written by the author.
- **Community edition(s)** (>1.x.x) : annual versions of the book including community contributions to improve it.

## Licenses

- **Source edition** : Copyright © 2023 Flavien BERWICK
- **Community edition(s)** : GNU General Public License v3.0 + Commons Clause License

    <details>
    <summary>Details about the community license.</summary>

    After the initial source edition' hard cover book gets publicated and as soon as there are accepted contributions to this repo's writing (`fra/README.md` or `eng/README.md`) through a pull request, the license will be updated to [GNU General Public License v3.0](https://choosealicense.com/licenses/gpl-3.0/) + [Commons Clause License](https://commonsclause.com/).

    The Commons Clause License was added so any book version officially published totally reflects community's contributions, with no parts adapted or removed by someone trying to partially publish it.

    What this means is that you can use this project (blogs, podcasts, presentations), while citing its source, but not sell it as-is in a (e)book.

    The name in the GitHub profile of contributors will be published if granted. To grant authorization to include your name, please include the following sentence in the description of your _Pull Request_ : "I hereby declare allowing the original author of the book publishing the following edition of this book with my contribution and name.". If you want to be published with another name that your GitHub's one, please specify it at the same place.
    </details>

## Book generation

This repository has [automatic](.github/workflows/render.yml) PDF and HTML generation from Markdown files thanks to Pandoc.

```bash
mkdir -p "$HOME/.local/share/fonts"
cp ./fra/templates/fonts/* "$HOME/.local/share/fonts"
cp ./eng/templates/fonts/* "$HOME/.local/share/fonts"
cd ./fra && make pdf && cd -
```

- Other formats available : EPUB (requires you to clone this repo or buy the digital version to support the author).

## Useful VSCode extensions when writing

- [Spellcheck](https://github.com/bartosz-antosik/vscode-spellright)
- [Markdownlint](https://github.com/DavidAnson/vscode-markdownlint)
- [Wordcount](https://github.com/Microsoft/vscode-wordcount)
- [Todo Tree](https://github.com/Gruntfuggly/todo-tree)
- [TODO Highlight](https://github.com/wayou/vscode-todo-highlight)
- [Markdown Footnote](https://github.com/houkanshan/vscode-markdown-footnote)
