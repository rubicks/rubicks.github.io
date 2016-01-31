---
categories:
- posts
date: 2014-12-19T00:00:00Z
title: autoconf git describe
url: /2014/12/19/autoconf-git-describe/
---

You don't know me, [Chris Packham][cpackham], but I owe you a debt of
gratitude. Let me explain...

I use autotools. The autotools are *The Means* by which one configures (and
builds and distributes) software. Sure, they're weird, but they work.

I also use git. Git is *The Means* by which one versions (and branches and
releases) software. I don't have to apologize for anything with git---it's
universally awesome and everything else sucks hard.

Git has the [```tag```][git-tag] and [```describe```][git-describe]
sub-commands. Provided you have at least one tag on your repository, you can
generate descriptive version names like so:

    rubicks@machine:~/code/barry$ git describe --always --dirty
    v0.2.0-1-g87dd6e9

In this example, on the current branch:

* ```v0.2.0``` is the most recent tag
* ```1``` is the quantity of commits since that tag
* ```g``` precedes the 7-character abbreviation (```87dd6e9```) for the most
recent commit

With ```autoconf```, one specifies version information as the second argument to
the [```AC_INIT```][ac-init] function. For example,

    AC_INIT([crapware],[0.1.0])

would initialize autoconf for the ```crapware``` package at version ```0.1.0```.

I got to thinking there must be a way to keep the autoconf package version in
sync with ```git describe```. There is, and it looks like this:

    AC_INIT([foobar],
            [m4_esyscmd_s([git describe --always])])

The benefit to doing it this way (as opposed to shell-substitution) is that the
working directory for the command is always the same; namely, the directory that
contains ```configure.ac```. With shell substitution, the invocation to ```git
describe``` only works as intended when the git repository is discoverable from
the build directory; i.e, in-source builds and/or out-of-source builds when the
git repo is the (eventual) parent.

Many thanks to Packham for showing this trick on the
[```configure.ac```][configure-ac] within the [```git-patch```][git-patch]
project. There were [lots of others][search], but I found Packham first.



[cpackham]: https://github.com/cpackham
[git-patch]: https://github.com/cpackham/git-patch
[configure-ac]: https://github.com/cpackham/git-patch/blob/master/configure.ac
[git-tag]: https://www.kernel.org/pub/software/scm/git/docs/git-tag.html
[git-describe]: https://www.kernel.org/pub/software/scm/git/docs/git-describe.html
[ac-init]: https://www.gnu.org/software/autoconf/manual/autoconf.html#Initializing-configure
[search]: https://github.com/search?q=git+describe+extension%3Aac&type=Code
