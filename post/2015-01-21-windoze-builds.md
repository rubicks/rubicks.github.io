---
categories:
- posts
date: 2015-01-21T00:00:00Z
title: windoze builds
url: /2015/01/21/windoze-builds/
---

Let's get one thing out of the way right now:
[Windows sucks][windows-sucks]. The reasons are myriad, but I'm not going to get
into them. We all know it sucks, just as we all know that Windows users are
legion.

Most of the time, I don't have to think about that family of operating
systems. That's because, over the course of 16 years, I learned and used various
Linux distros. It was never magical and sometimes painful, but on average, those
distros worked as advertised. Any Linux problem nearly always sprung from my
stupidity, inexperience, and/or naivete. With enough google queries and
reference documentation, a solution (or sane workaround) was possible.

Windows is different. Windows problems don't yield to the usual
google-the-error-message protocol. Just using Windows is scary. Developing
software for Windows is scarier. Developing cross-platform software that runs on
[POSIX][posix] *and* [win32][win32]---that's downright nightmarish.

In the free software world, the well-trodden path is to develop initially on
Linux (almost always Ubuntu, these days) until the product stabilizes before
trying to cross-compile with [mingw][mingw]. If this is your first such foray
into supporting multiple target platforms, then this is also your first
introduction to [The Matrix of Pain][matrix-of-pain].

To enumerate your matrix of pain, find the
[Cartesian product][cartesian-product] of every set of all compilers (and
variations of flags thereto) *for every platform*. For example, if I wish to
support `gcc` and `clang` native compilations and `mingw` cross compilation,
then my pain matrix is of size *three*. Not so bad, right? It gets so much
worse.

If I want to support release and debug builds, that necessitates two sets of
flags for each compilier. This doubles the size of the matrix. If I want to
support multiple build platforms, the matrix expands by the equivalent
factor. Within popular open-source projects, it is not uncommon to see build
matrices of dozens of elements.

That is, in short, what [Mortis69][Mortis69] and myself are attempting with
[rendera][rendera]. It's not easy. It's very, very hard. It's the reason why we
don't have automated Windows builds yet.


[windows-sucks]: https://duckduckgo.com/?q=windows+sucks
[posix]: https://en.wikipedia.org/wiki/POSIX
[win32]: https://en.wikipedia.org/wiki/Windows_API#Win32
[mingw]: http://mingw.org/
[cartesian-product]: https://en.wikipedia.org/wiki/Cartesian_product
[Mortis69]: https://github.com/Mortis69
[rendera]: https://github.com/Mortis69/rendera
[matrix-of-pain]: https://en.wikipedia.org/wiki/Matrix_of_pain

