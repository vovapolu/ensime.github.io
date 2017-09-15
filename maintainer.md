---
layout: page
title: New Maintainer Needed
---

by @fommil  
15th September 2017

In December, when my first child is due, I will give up my online
hobbies to be with my family, and finish my book, [Functional
Programming for Mortals with Scalaz](https://leanpub.com/fpmortals).
Of most relevance to ENSIME is that I will, sadly, no longer have the
time to maintain this project.

I have anticipated this over the last couple of years and automated as
much as possible (e.g. the server, Emacs, docker and website release
processes) to make it easy for any motivated user to contribute
features, bug fixes, and code reviews.

My real hope was that [the sponsorship programme](/sponsor) would
generate enough revenue to pay somebody to take this role. But even
with the exceptionally generous donations from our core userbase, our
funds are orders of magnitude lower than necessary.

ENSIME still needs a maintainer who is able to do the basic job of
assigning authority roles (such as merge rights, publishing to
Sonatype), cutting stable releases of the various components, keeping
the servers ticking and taking responsibility for code / build
quality.

The ENSIME contributor base is absolutely fantastic and it is a
genuine pleasure to hack with the great people who come through these
revolving doors. There is an energy in the center of a loved part of
the scala ecosystem, whilst being a banner for [Free (libre)
Software](https://www.gnu.org/philosophy/floss-and-foss.en.html), and
empowering users to hack their workflow to their exact requirements.

It is addictive to contribute to a project where **you are the
customer**, not somebody else. Unlike at your day job, where projects
can live or die by the quality of communication between the customer
and developers, with ENSIME you know exactly what you want to do and
you are in the unique position to be excited about the possibilities
of what can be done AND the implementation details.

That said, there are a lot of additional burdens that you, as the
future maintainer, will have thrust upon you unless you actively
identify the lures and choose not to get involved.

In the interests of being completely open, this is some of what you
can expect and if I was to do it again, you can probably guess what
I'd have done:

1. keeping a mental picture of the overall project: server, all build
   tool plugins and all editor plugins. You will be expected to have a
   plan for what the next milestone looks like and be aware that any
   pull request you accept can break somebody's workflow. Like the
   maintainer before you, tests will be your best friend. I actually
   quite liked this architectural bit. I've created a plan for the 3.0
   series, feel free to do what you want with it.
1. being expected to review every pull request and give advice on
   implementing features that you're not really excited about.
   Sometimes this might mean finishing off the PR yourself because the
   contributor is stuck. Be harder than me, just park the PR.
1. deciding your stance on backwards compatibility and how much effort
   you will spend on ensuring that you don't break the workflow of
   somebody who is not contributing to the project. Before making any
   large breaking changes, we have in the past cut a stable release so
   that nobody is left without the ability to use ENSIME. This is a
   burden to you, but it will save you from having to deal with angry
   users.
1. being aware of upstream developments in scalac, dotty and sbt, and
   getting involved in the scoping of those projects to ensure that
   they don't result in irretrievable situations where ENSIME is no
   longer viable. e.g. writing requirement documents for those
   developers.
1. continually upgrading ENSIME to support the latest scalac, dotty
   and sbt even if these things are not part of your daily usage.
   Although the community is good at the occasional bugfix or feature,
   the larger issues like this require a larger commitment.
   ensime-server was at one point part of the scala Community Build,
   but it became too burdensome to maintain. Be aware that nobody
   upstream checks for ENSIME compatibility before releasing and you
   will be expected to fix it if it breaks.
1. telling contributors that they cannot add any more dependencies
   because it makes upgrading to newer versions of scala and sbt much
   harder. Remember that you will pay the cost if you listen to them.
1. keeping the documentation up to date on the website. Be prepared
   for lots of passive aggressive insults if there is even a single
   sentence that is wrong or it didn't make sense to somebody who just
   skims it. Don't be afraid to point out that `[edit]` button that I
   added to every single page.
1. being available 24/7 to spoon feed your documentation to random
   dudes on the internet who feel like you owe them something, and
   don't know how to use a browser. If you don't decorate your advice
   with salutations and graciously thanking them for trying out
   ENSIME, be prepared to be called arrogant, lazy and rude. My advice
   is to shut these people out of the project and not to tolerate
   them, but you **will** be ostracised by other groups in the scala
   ecosystem who wish to encourage such privileged behaviour. You will
   need thick skin to deal with both of these types of people.
1. having a Code of Conduct. If you do not have one, you will be
   pressured by people until you put one in place. Their primary
   weapon is emotional blackmail, they will claim that you are
   excluding people until you put *their* code of conduct in place.
   They will exclude you from the social gang until you agree with
   them. You're between a rock and a hard place: no matter what you
   do, there will always be somebody who complains about it, for
   example, it seems we now need to have a stance on ["actual
   Nazis"](https://github.com/typelevel/general/issues/74), and you
   need to prove your commitment to the cause by punching a Nazi, or
   something. This is why [we have a simple code of conduct](/conduct)
   which asserts that users should be respectful of the contributors'
   time and help each other out. ENSIME is a technical project and the
   only politics we subscribe to are those of the Free Software
   Foundation.
1. Everything you say publicly will be criticised by the twitter mob
   and you could suffer the same witch-burning fate as [Ashley
   Williams or Rod
   Vagg](https://theoutline.com/post/2206/the-node-js-code-of-conduct-diversity-tech).
   I have personally experienced blocking / muting / "polite" ignoring
   / tone-policing by prominent people in our Scala community who
   believe in the imaginary Nazi revolution, because I have opposed
   their paternalistic approach to community management. For example,
   there are some in the wider community who feel it is appropriate to
   contact employers over a twitter argument. The mobs are real, they
   can impact your livelihood, don't get involved, this is just a
   hobby.
1. managing the sponsorship programme and the cash funds available
   there. We are currently generating about $350 / month, which means
   we can afford to hire a part time student for two months a year. By
   December, the funds will be depleted. It'll be your responsibility
   to basically do all the management and admin around this, including
   finding the person in the first place (do you have any idea how
   **hard** it is to find good Scala developers?). The effort involved
   in doing this is quite high, although the payback is good. You may
   want to consider canning the sponsorship programme because of the
   admin burden, and give what little remains to the Free Software
   Foundation.
1. This position is obviously so desirable that you are expected to
   contribute financially. The cost of appveyor (Windows CI) is $300 /
   year. Your choice of CI and worker agents varies, currently running
   at about $350 / year plus Chip's machine (which does the lion's
   share of the work). You may be expected to top up the sponsorship
   funds if they are running low and the developer needs to be paid
   because of timing. I recommend canning the Windows CI and letting a
   Windows user contribute the funds and effort to keep the Windows
   build running, unless the gratis AppVeyor service has improved in
   the last two years (which you will need to spend a weekend
   investigating). I will try to move us over to gitlab before my
   tenure is up so that the CI cost is removed, but we will still be
   reliant on Chip's machine doing the work.

Applicants need not apply, I will grant admin permissions to some core
contributors over the coming months and somebody will eventually step
up out of necessity. There will be no handover, you will (re)discover
and (re)invent everything as you need it, much as the incumbent earned
his scars.
