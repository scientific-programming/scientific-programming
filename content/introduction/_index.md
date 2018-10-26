---
date: 2018-10-25T17:11:13+01:00
draft: false
author: Ryan Pepper
date: October 29th 2018
title: "Software Engineering in Science"
weight: 10
---

## Why is it needed?

The expectation is that your scientific code must be error free, within reason. However, there are many places where errors can creep in, and in general, scientists do not perform basic software engineering techniques which are designed to minimise "stupid" mistakes. Sources of errors can either be conceptual - a mistake in understanding of the theory - or in the implementation of the software used to solve problems. Here, we're going to focus on the mistakes that come in from implementation issues, which really, are the easier ones to deal with. Let's try and think about the issues that might happen when when things go wrong with software, both scientific and general.

There are a number of high profile examples which can illustrate for us the issues that might occur from coding errors.

### Geoffrey Chang

![Geoffrey Chang](chang_jeff.jpg)

Geoffrey Chang and coauthors published a series of papers in high profile journals which attempted to determine the structure of molecules through analysing X-Ray crystallography data. The research groups papers were very highly cited and influential. However, in 2006 Kasper Locher performed a similar technique to Chang to determine the structure for what should have been a similar crystal to one studied by Chang's group. Instead, he found a 180&deg; flip in the orientation of one helix, which suggested that the results were incorrect. Chang went back and looked at his software, and realised that two columns of data had been accidentally transposed, which resulted in the signs of charges in the molecular structure being flipped. In total, this led to retraction of 6 papers, and around five years of work.

You can read more about the impact of this [here](https://dx.doi.org/10.1126/science.314.5807.1856).

### Reinhart and Rogoff

Two economists, Reinhart and Rogoff published an influential paper \"Growth in a time of Debt\" on the topic of government debt to gross domestic product ratios.
The results from their study showed that growth declined once the ratio reached around 60%, the growth in countries historically had begun to decline.
The paper was notable for it's use in political circles; it was cited by government figues in the UK, EU and US as the basis for reducing government spending.

A PhD student in the US, Herndon, struggled to reproduce the results of the study, and eventually contacted the original authors of the paper requesting the non-public data that the study was based on.
The authors passed this on, but Herndon and found a number of spreadsheet errors which meant that certain countries were not included in the historical data. On inclusion of these countries, the results from the paper still showed a decline in growth, but one which was substantially lower than as originally presented.

### Ariane 5 Rocket Launch 1996
The launch of the first Ariane 5 rocket was a 10 year development and a $7 Billion cost for the European Space Agency. On the first test launch in June 1996 the trajectory of the rocket went of course 37 seconds in and
the self destruct mechanism kicked in.

<div style='width: 507px; height: 380px; margin: auto;'>
<iframe width="507" height="380" src="https://www.youtube.com/embed/gp_D8r-2hwk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>

Investigations found that the inertial reference system had software bug, which was caused by the conversion of a 64-bit float containing the velocity into a 16-bit integer, and this caused an integer overflow. It turned out that this calculation was not even necessary on the Ariane 5, and had been inherited from software on the Ariane 4, but because this rocket reached much higher speeds, the rocket attempted to make correction for altitude deviation which hadn't happened.

This was a particularly expensive mistake!

### NHS Connecting for Health

Stepping away from scientific software bugs, let's look at how poor software design and oversight may hamper a different type of large software project, even when professional software developers are the ones writing it. It may surprise you to find out that in the UK, there is no national database of patient records. If you go to A&E on a Saturday night unconscious, in general, doctors will not be able to see your medical records until the Monday morning when your GP opens again.

In 2002, Tony Blair's Labour government decided to rectify this, and in 2003 and 2004 awarded contracts to Accenture, Fujitsu, BT Health and Computer Sciences Corporation between 2002 and 2004, which the intention of building a complex set of regional systems which could integrate with one another. The initial projected timescale for this project was three years. The proposed system had an expected cost 2.3 Billion and would have been the biggest government IT project in the world.

The scheme was eventually cancelled in 2011 but 16 years later costs from fallout of this project are still escalating - currently at over £20 billion. Compare this, for example, to the UK budget which in 2018 is 5 billion. A government report "Government and IT - a recipe for rip offs" in 2011 blamed **lack of in-house technical knowledge** and a **tendency to build large complex projects that cannot adapt to changing requirements**.

### More examples

* Trading glitch cost Knight Capital \$440 Million dollars in 30 minutes.
* Therac-25 Radiation Therapy machine bug killed 4 patients and injured two others because of integer overflow in software written by a single programmer.
* Mars Orbiter crashed in 1998 because of imperial vs metric units in interface between software.
* Y2K bug was caused by 32-bit integer commonly used to store dates overflowing.
* 1999 Study on suicides after natural disasters counted deaths in one year twice and had to be retracted.
* Sainsbury's wrote off \$526 Million investment in 2004 because of software bugs.

## What are the implications of badly written software?

* It's clear that complex systems are very hard to get right. This means that starting out when writing a programme is usually not the best way of approaching it - take some time to plan.
* Getting things wrong for you means bad science and a damaged career. If you have to retract some work, youre
* If you work on large projects it can mean huge costs.
* Wasted time and money dealing with fallout of mistakes.
* Poorly designed software is just as bad as bugs in well designed software!

## What should we draw from this?
* Clear that even professional software developers can get it wrong.
* Scientists in particular are not generally good programmers and are mostly self taught.
* Scientists do not have the resources to use all of the techniques from industry to avoid problems.

## Reproducibility and Repeatability
* **Reproducibility - Gaining results which are close in agreement using the same methodology described**
* Key concept of the scientific method
* **Often scientific papers cannot be reproduced** solely from the paper alone.
* How many of you have ever struggled to reproduce a result from a computational paper?
* Often this comes from inherent assumptions in modelling which are not discussed in the research literature itself.
* Very challenging to write a paper which is complete.
* Large and well discussed \"reproducibility crisis\"

### A Changing Landscape?
* Increasing pressure from funders - all UK research data must be made public. Similar story in other countries.
* However, papers and the data are still are not generally enough to reproduce methods.
* Organisations like the Software Sustainability Institute and Software Carpentry have been leads in giving scientists better software development training.
* Well written open projects in Python/C/Fortran like AstroPy, SciPy and NumPy are well documented and serve as great examples for writing well tested and usable software.
* Time commitment to getting there is hard at first but leads you to do better science and have more confidence in your results.

### A Changing Landscape?

It is becoming increasingly necessary for you to release the source code that generates your publications. It is highly likely you won't be able to decline in future! See, for example, Nature Publishing Group's [publication guidelines](https://www.nature.com/documents/GuidelinesCodePublication.pdf), which are moving in this direction. Where high quality journals start, others will follow!

Everything in the following courses is designed to make it easier for you to writing good software. In the software industry these just some starting points from which all else follows. If you are not doing any one of these things (with the exception of containerisation), you are almost certainly not writing good software. The main point is that scientific software is not some special case - it is just as complex as software in industry, where all of these are standard practice.
