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

![Reinhart and Rogoff BBC Article](reinhart.png)

### Ariane 5 Rocket Launch 1996
The launch of the first Ariane 5 rocket was a 10 year development and a $7 Billion cost for the European Space Agency. On the first test launch in June 1996 the trajectory of the rocket went of course 37 seconds in and
the self destruct mechanism kicked in.

<div style='width: 507px; height: 380px; margin: auto;'>
<iframe width="507" height="380" src="https://www.youtube.com/embed/gp_D8r-2hwk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>

Investigations found that the inertial reference system had software bug, which was caused by the conversion of a 64-bit float containing the velocity into a 16-bit integer, and this caused an integer overflow. It turned out that this calculation was not even necessary on the Ariane 5, and had been inherited from software on the Ariane 4, but because this rocket reached much higher speeds, the rocket attempted to make correction for altitude deviation which hadn't happened.

This was a particularly expensive mistake!


### Supercooled Water
![Supercooled Water War](supercooled-water-1.png)
[Very recent case](https://physicstoday.scitation.org/do/10.1063/PT.6.1.20180822a/full/) - but went on for years. Researchers had conflicting results in simulations of supercooled water. Eventually, one group published all of their research software, which put pressure on the other group to do so. When they eventually did, it was found that they were using a very unconventional method of initialising their molecular dynamics simulations, which led to the spurious results.

### NHS Connecting for Health

![NHS Connecting for Health logo](NHS.gif)

Stepping away from scientific software bugs, let's look at how poor software design and oversight may hamper a different type of large software project, even when professional software developers are the ones writing it. It may surprise you to find out that in the UK, there is no national database of patient records. If you go to A&E on a Saturday night unconscious, in general, doctors will not be able to see your medical records until the Monday morning when your GP opens again.

In 2002, Tony Blair's Labour government decided to rectify this, and in 2003 and 2004 awarded contracts to Accenture, Fujitsu, BT Health and Computer Sciences Corporation between 2002 and 2004, which the intention of building a complex set of regional systems which could integrate with one another. The initial projected timescale for this project was three years. The proposed system had an expected cost 2.3 Billion and would have been the biggest government IT project in the world.

The scheme was eventually cancelled in 2011 but 16 years later costs from fallout of this project are still escalating - currently at over £20 billion. Compare this, for example, to the UK science budget which in 2018 is £5 billion. A government report "Government and IT - a recipe for rip offs" in 2011 blamed **lack of in-house technical knowledge** and a **tendency to build large complex projects that cannot adapt to changing requirements**.

### More examples

* A [trading glitch](https://www.cio.com/article/2393212/agile-development/software-testing-lessons-learned-from-knight-capital-fiasco.html) cost Knight Capital $440 Million dollars in 30 minutes.
* The Therac-25 Radiation Therapy machine bug [killed 4 patients and injured two others because of integer overflow](https://hackaday.com/2015/10/26/killed-by-a-machine-the-therac-25/) in software written by a single programmer.
* In 1998 the [Mars Climate Orbiter](https://en.wikipedia.org/wiki/Mars_Climate_Orbiter) crashed because of imperial vs metric units in interface between software.
* [Y2K](https://en.wikipedia.org/wiki/Year_2000_problem) was caused by 32-bit integer commonly used to store dates overflowing. [(Upcoming again in 2038...)](https://en.wikipedia.org/wiki/Year_2038_problem)
* A 1999 Study on suicides after natural disasters counted deaths in one year twice and [had to be retracted.](https://www.nejm.org/doi/full/10.1056/NEJM199901143400213)
*

## What are the implications of badly written software?

* It's clear that complex systems are very hard to get right. This means that starting out when writing a programme is usually not the best way of approaching it - take some time to plan.
* Getting things wrong for you means bad science and a damaged career. If you have to retract some work because of what amounts to carelessness, you're going to be known in your field for getting it wrong, and it will take a lot of work to recover your reputation. [Retractions are also becoming more visible!](http://retractiondatabase.org/)
* If you work on large projects it can mean huge costs in time and money if you have to redo analysis.
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

Think now about the requirements you're being asked to meet for research in the UK. As EPSRC funded researchers, you are already required to:
* Deposit the accepted manuscript in an institutional repository so that they are openly accessible within 3 months of acceptance.
* All of your research data must now [be made public and be available for up to 10 years after the last 3rd party access](https://epsrc.ukri.org/about/standards/researchdata/expectations/).

You need to care about these things if you want to stay in academia, because if you don't meet the requirements, your publications are not countable towards REF, which directly impacts your career path. The motivations behind these policies is that as publicly funded researchers, the general public should be able to access information you produce (with some exceptions on national security or data privacy grounds).

Moving on from funder requirements, we need to look at what publishers are starting to demand. It is becoming increasingly necessary for you to release the source code that generates your publications. See, for example, Nature Publishing Group's [publication guidelines](https://www.nature.com/documents/GuidelinesCodePublication.pdf), which are moving in this direction. Where high quality journals start, others will follow! Looking at one particularly odd example, [a 2004 paper was retracted from BMC Evolutionary Biology](http://www.sciencemag.org/news/2015/11/paper-retracted-after-scientist-bans-use-his-software-countries-welcome-refugees) after the author refused to let scientists from countries admitting refugees use of the software, as this breached the journal's guidelines on software availability.

The other thing to note is that other scientists - and not just funders and publishers - are becoming more demanding regarding access to software, which the
recognition that complex software is often not described adequately in research papers, making the results irreproducible. Government funded organisations such as the [Software Sustainability Institute](https://www.software.ac.uk/) are actively pushing for more research code to be made open and maintainable, and provide training. There is now a whole new career path for ['Research Software Engineers'](https://rse.ac.uk/) - usually former academics with strong software skills, who can provide training to academics and who are included on grant applications to work on making the research software used maintainable.  

### What will this course teach you?

Everything in the following courses is designed to make it easier for you to writing good software. In the software industry these just some starting points from which all else follows. If you are not doing any one of these things (with the exception of containerisation), you are almost certainly not writing good software. The main point is that scientific software is not some special case - it is just as complex as software in industry, where all of these are standard practice.
