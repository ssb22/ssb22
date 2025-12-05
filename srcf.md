
from https://ssb22.user.srcf.net/access/srcf.html (also [mirrored on GitLab Pages](https://ssb22.gitlab.io/access/srcf.html) just in case)

# How the Cambridge Student-Run Computing Facility started

The SRCF “about us” page says:

> The SRCF was formed in 1999 to provide services which the University Administration could not, including web hosting, standards-compliant email, shell servers, mailing lists, and other computing resources for student societies. The UIS simply does not provide or has decommissioned their similar services, such as DS-web

While this is a good summary of what the SRCF has done, my own memory does have a slightly different version of what happened in 1999. Perhaps I’m remembering it wrongly (so disclaimers apply), but in case anyone’s interested, here is my version of how the SRCF got started, in what is probably more detail than is appropriate for the modern About page.

## Student web hosting before 1999

When I was an undergraduate, the on-site options for hosting our websites were:
1. Registered student societies were given space under `cam.ac.uk` (I remember maintaining the pages for the now-defunct Cambridge University Computer Society there)—static files only, copied from the networked filestore by an hourly cron job to a long URL. This space was not available to non-registered societies or to individuals.
2. Research students were often given Web space by their departments, and all graduate students had Web space on a machine called the Central Unix Service (CUS, a Solaris cluster which ran from 1991 to 2008)—again static files only. This was not available to undergraduates.
3. Undergraduates in Computer Science, and Physics from their third year onwards, had accounts on a cluster called Thor, which also provided a home page service (again static files only). This system closed in the early 2000s.
4. If you wanted to run CGI services like my [Web Access Gateway](https://ssb22.user.srcf.net/access/) (which helped work around limitations of the browsers available in the university in those days), the only way to do this was via a student-run server.

Most colleges allowed their students to run servers in their rooms, *if* you didn’t mind running a computer 24/7—not many PCs were quiet in those days, and although some rooms had a separated-off sleeping area, not all did, so running a server at night could sacrifice some sleep quality. I didn’t regularly run my server at night until 1999 when I got a room with a partition, just in time to help bootstrap [CCS](ccs.md) with it, and it was from carefully running that box to the point of checking system source before turning anything on that I later discovered a Linux kernel security flaw which was fixed in CVE-2001-0851. Before 1999 I was saying people are welcome to use my server but only when I’m awake, which made it unsuitable for general Web hosting.

The other option was to ask nicely for an account on the server of *another* student. Some student machines became quite popular (Excession, Epona, BanJoh, PickSel...) and in at least one case a college computer officer kindly allowed one to be located in his office. The most-used GNU/Linux distribution was Debian, which had Cambridge people in its development team (one of whom also started the `ucam.org` domain for unofficial aliases to student servers within the University of Cambridge) and it seemed a good option for newcomers to pick the distribution that would most likely be supported locally, although there were instances of servers running something else. Student machines could do just about anything you agreed with their admins to enable (like running my Access Gateway before I had my own 24-hour server which I just called “Access”), but they did have the downside of disappearing when their owners graduated—or in some cases when they went on holiday.

## Convergence into the SRCF

Trinity Hall student Julian T J Midgley, an early supporter of my Access Gateway on his “Excession” server (a pun on “X session” which was at that time the way to get a graphical desktop on GNU/Linux), kindly decided to donate Excession to a student society to carry on running it after he graduated.

As the Computer Society was struggling (not least because its constitution said a committee quorum was the square root of the *life* membership, which meant we had to get about 20 people into a room to get anything done), we thought the best way forward was to start a new society for the sole purpose of owning and running the server (and I didn’t join the committee myself this time, as they seemed to have enough capable volunteers already, but I still talked about it with some of them).

We knew about the Tardis Project at Edinburgh (which had started in 1988 on an old minicomputer donated by their department), and we wanted to set up a similar project for Cambridge. We discussed its implications with the Computing Service (this was before they renamed themselves to University Information Services, and it wasn’t so many years after they’d split from the Computer Laboratory, which formerly handled both the infrastructure *and* the Teaching and Research side of things)—the CS was generally supportive, although it took us a few attempts to come up with a club name that addressed everyone’s concerns (the SRCF was to be a central facility but not with the official up-time guarantees of the CS’s own systems, and for this and other reasons it was important to put its student-run aspect into the name). The SRCF was run from a central location, which was an improvement on running it from a student bedroom, and most importantly it wasn’t going to disappear just because one student graduated. The Jesus College Student Union server “Zeus” (shut down around 2016) had been running shell accounts since end-1998 although generally for only that one college (but they *did* let me run my Access Gateway there even though I was at St John’s); they helped set up the simple, flexible structure of the new SRCF club.

It didn’t take long for Julian’s ex-Excession machine to be retired in favour of a larger system funded by donations from SRCF members. His original machine was still used for training new sysadmins for a while. In time, the SRCF came to have a cluster of rack-mounted machines. Those of us who were around at the beginning have taken a very “hands-off” approach: the current students need the experience more than we do, so we let them get on with it, but that’s not to say we wouldn’t try to help if the club were to run into serious problems (which thankfully hasn’t happened).

## DS-Web

The official “about us” text mentioned the DS-Web service, which the SRCF did indeed replace, but that wasn’t what we were thinking in 1999 because DS-Web hadn’t even started in 1999. The SRCF was around *before* DS-Web (and the DS, the MCS and MCS Linux, although their precursors were there in the form of the PWF and PWF Linux without a Web service). The SRCF also continued to be around after DS-Web and MCS Linux shut down. In its heyday, the DS gave users more quota than the SRCF, but DS-Web was still limited to static files while the SRCF allowed CGI and other dynamic services.

Similarly, although the SRCF has always supported standards-compliant email, in 1999 we didn’t realise that the university’s own “Hermes” email service would be shut down in 2021 in favour of a Microsoft Exchange subscription. In 1999 we didn’t plan on the *specific* outcome of the SRCF one day having to take on the role of on-premises email processing for those unable to connect to Exchange, but we *did* plan on the SRCF being flexible enough to serve whatever server-related need future members would have.

We didn’t see exactly what was coming, but early services like my Access Gateway had shown that there was value in running a server which had more flexibility than that of the university’s official systems, and it turns out there still is. The SRCF has also given students valuable administration experience on a larger system than they’d be able to run individually.

Copyright and Trademarks:
All material © Silas S. Brown unless otherwise stated.
CVE is a registered trademark of The MITRE Corporation.
Debian is a trademark owned by Software in the Public Interest, Inc.
Linux is the registered trademark of Linus Torvalds in the U.S. and other countries.
Microsoft is a registered trademark of Microsoft Corp.
Unix is a trademark of The Open Group.
Any other [trademarks](https://ssb22.user.srcf.net/trademarks.html) I mentioned without realising are trademarks of their respective holders.
