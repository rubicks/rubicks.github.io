---
categories:
- posts
date: 2015-01-17T00:00:00Z
title: rendera resource files
url: /2015/01/17/rendera-resource-files/
---

Remember when I was [all excited](2014-12-14-barry.html) about [`barry`][barry]?
Remember how I was going to turn all those PNG images into byte-arrays and
compile them directly into the `rendera` executable? What ever happened with
that?

The short story is that it didn't work out that way. The reasons for this
include (but are not limited to) the following:

* [recursive automake][automake-manual-recurse] is *really hard* to get right
* [recursive autoconf][autoconf-manual-recurse] is *even harder* to get right

This is not to say that such things are impossible. Recall that I managed get
automake subdirectories working when I
[started using autotest](2015-01-04-autotest.html). That little job, however,
was mostly copypasta---I had some (not many) examples from which to steal.

Building the `barry` executable as a subproject of [`rendera`][rendera] to then
use the former to generate source code for the latter---that is what I set out
to do.

I couldn't find a single example implementation---not *one*. After many
faltering attempts, I discovered that such a thing it is actually
possible. Unfortunately, for someone with my meager [m4][m4] skills, the effort
required is completely unjustified.

So, I did something else.

It started as a directory path problem; i.e., the directory hierarchy of build
(automake's `$(builddir)`) didn't match that of the installation (autoconf's
`$(prefix)`). So, if they don't match, we'll just make symlinks until do. How,
exactly? Why, in `configure.ac`, of course:

    ...
    
    AC_PROG_LN_S
    AC_PROG_MKDIR_P
    
    ...

    (
      $MKDIR_P share/rendera && \
      cd share/rendera       && \
      $LN_S ../../"${srcdir}"/data
    )

I should probably change that relative path to its absolute equivalent, but, for
the moment, it's working.

Update: I deleted the __submod_barry__ branch on my rendera repo, but I did
manage to get a __submod_fltk__ branch working.

Update: I deleted the __submod_fltk__ branch on my rendera repo. The git
submodule stuff was working. The cross compilation of FLTK was not.


[autoconf-manual]: https://www.gnu.org/software/autoconf/manual/autoconf.html
[autoconf-manual-recurse]: https://www.gnu.org/software/autoconf/manual/autoconf.html#Subdirectories

[automake-manual]: https://www.gnu.org/software/automake/manual/automake.html
[automake-manual-recurse]: https://www.gnu.org/software/automake/manual/automake.html#Subdirectories

[m4]: https://www.gnu.org/software/m4/
[barry]: https://github.com/rubicks/barry
[rendera]: https://github.com/Mortis69/rendera
