---
title: How to organize your computational projects
date: 2020-10-10 16:08:00 +0800
categories: [Skills]
tags: [organization, computational biology, project management, graduate school, research]     # TAG names should always be lowercase
math: true
toc: true
---

> Anyhting that can go wrong will go wrong.

If you're engaged in any sort of scientific work, Murphy's law should be your mantra. Scientific work should be virgoriously documented, and it one of the most essential habits that a scientist should have. Always be critical, even towards your own work. If you're going to be a scientist, be a conscientious one.

## What my 'pseudo-system' used to look like

Back in my undergraduate days, I was working as a summer intern for a bioinformatics project in a wet lab. The set up I had was the typical paper notebooks, printed graphcs and gels photographs. But I obviously cannot print every code out (even though one of the RAs actually did that), so what I ended up doing was nothing! Yes, I was naive and dumb (maybe I sitll am) and I didn't know better. I got by because that was more of a one-off project, we ended up publishing it 2 years later and if you ask me how I did some of those parts, I probably won't remember. When I interned in another more computational based lab, I started using remote servers and Github, but my stuff was still a mess. I would manually edit scripts in some of the lines and change those every time I wanted to run something a little differently. I have number named scripts `(RNASeq1.R, RNASeq2.R, ...)`, a ton of tmps that are just sitting there, multiple copies of GDC downloaded data, chunks of copied code in almost every scripts etc. You get the idea, it was a mess. When I wanted to collaborate, others had no clue what happened. We've spent so much time during meetings just 'looking' for the proper result directory or script. It was a total disaster. 


## (Speaking from personal experience) Why you should document your work well:
1. Avoid last minute surprises
    
    Do you want to find out about a bug that would have ruined your entire analysis moments before you're about to submit your manuscript?

2. Reproducabiltiy

    I guess I'm not the first one who can't get the same results generated months ago... I will also quote David Quigley's [post on Biostar](https://www.biostars.org/p/8434/#843)

    > If you don't know how the data were transformed, you will get bitten by it. In my experience, the more systematic and hard-core you are about it, the more dividends it pays over time.

3. Communications

    You can never do science alone! Discussion and collaboration is the key to success, and in order to do so effectively, you need to be able to show others what **exactly** you did to generate such results. It's never a good idea to pull everything from your memory, it's not reliable. It happened to me very often that I would tell my supervisor "I think I used $\alpha=0.05$ for this script". You "think" or you "reckon" are not good enough, details about your work needs to be displayed properly in context with time stamp.

4. Personal branding

    As computational based (I would say even for wet-lab based) researchers, it's more important than ever to have an online presence! Let's be honest your latest Google Scholar entry is probably unrelated to your current interest, and you want interested collaborators/friends/potential supervisors to see what you're up to in one place. Linkedin is overrated and doesn't offer much flexibility in terms of showing who you are as a scientist. Yes, you put as many Cousera courses on there as you like, just like everybody else. Good documentation and recording is a good yardstick for competency, don't say you're a good scientist, show it.

5. Legal uses

    If you got so successful that one day you created a patentable software/product, congrats! (Or if someone acusses you of copyright infrignement) You will need your documentations.

## What I think a good set up should offer

So the set up I'm talking about here isn't just about your documentation, code or workspace, it's everything altogether. Where you would run your code, where the results go to, where your output logs go to, where to find your written documentation about why you chose this particular method etc. So here goes:

1. Flexibility

    A good system should offer enough freedom to accommodate any issues/edit/add-ons that arises from your day to day code-running. This means it should have places for both static (source code, functions etc.) and dynamic files (logs, run script, bash files etc.) You should also be able to include your written documentations in it. I like to keep everything in the same place, which is one of the main reasons why I shy away from many wonderful yet limited note taking systems and [electronic lab notebooks](https://www.nature.com/articles/436020a).


2. Accesibility

    Freedom is great, yet it should be structured just enough to keep everyting tidy and accessible. Anyone going into your directory should know right off the bat where everything is, what each files are for. Every directory or folder naming should make sense, no `tmp1.R`, no `script_ver2.1.R` or any bullshit like that. Every script and every documentation should be as verbose as possible, since my memory is not reliable.

3. Disaster-proof

    That means *cloud sync* and *version control*. All your important scripts and results should be online and backed up. I used to store things on my local laptop because it was just easier for me, and we didn't have servers. I understand not everybody has this luxury of cloud storage, but storing essential project files on local pc not only puts them at risk of hard disk apocalypse and coffee spills on keyboards, it gets really messy when you accidentally replaced an older version with the current copy (I've been there, you don't want re-write your scripts halfway.) There are many free cloud storage services and I am looking into [Nextcloud](https://nextcloud.com/) for hosting my own stuff, they seem to offer reasonably priced plans.

4. OS integration

    I'm a huge (GNU) Linux fan, and obviously I want everything I use on a day to day basis to be well integrated to my native Linux environment. So some of the really well designed systems like Onenote or Evernote are out of the quetsion. I also don't want to run anything with Wine, my Tux is sober. So citation systems like EndNote are not welcomed here. Given that I play with my system frequently, I also want the whole set up to be easily transferred.


## What my current reserach set up looks like

I used a combination of ready-made products and 'home-brew' systems that I feel comfortable using. I will talk about the general structure of my workspace here, but I have a separate post about how exactly I set this up if you're interested.

### Code, scripts and results

Github is the to-go platform for me to host all my scripts and analysis realted notes. We have two separate servers for our lab and sometimes files transfer analysis done on different servers could get messy. The basic format of my project follows what was posted by [RIL Labs](https://rillabs.com/posts/organizing-compbio-projects). Each project should adhere to this structure strictly.


```
├── bin  <-------------------# Binary files and executables (jar files & proj-wide scripts etc)
├── cfg <--------------------# Project-wide configuraiotn
├── doc  <-------------------# Any documents, such as manuscripts being written
├── exp  <-------------------#  The main experiments folder
│   ├── 2000-01-01-example <-# An example Experiment
│   │   ├── audit  <---------# Audit logs from workflow runs (higher level than normal logs)
│   │   ├── bin   <----------# Experiment-specific executables and scripts
│   │   ├── cfg  <-----------# Experiment-specific config
│   │   ├── dat  <-----------# Any data generated by workflows
│   │   ├── doc   <----------# Experiment-specific documents
│   │   ├── log   <----------# Log files from workflow runs (lower level than audit logs)
│   │   ├── raw   <----------# Raw-data to be used in the experiment (not to be changed)
│   │   ├── res  <-----------# Results from workflow runs
│   │   ├── run   <----------# All files rel. to running experiment: Workflows, run confs/scripts...
│   │   └── tmp   <----------# Any temporary files not supposed to be saved
├── raw  <-------------------# Project-wide raw data
├── res  <-------------------# Project-wide results
└── src  <-------------------# Project-wide source code (that needs to be compiled)

```

`bin`, `cfg`, `doc` and `src` are shared between servers and version controlled, whereas the `exp` folders are only partially shared and pushed to my Github repository.

### Log, lab notebook and other notes

I thought about using a separate system for these documents, but since not all of my results are hosted online, I think it's a better idea to keep the realted notes or otuput logs together with the scripts and data I used to generate those results. It's also a good idea to put why I chose a particualr formula or theory to work with in my scripts side by side. I used to use Joplin as my electronic labnotebook, but it's a huge hassle to cross reference the noteobok and the result on the servers, so I will slowly get rid of my old Joplin setup.


### Formal texts and citation management

I read a lot of papers and I use Zotero to manage them. I have offline access to all the full texts and they are synced on MEGA, so I can basically fetch any papers I want anytime with the Zotero + MEGA combo. What's really great about Zotero is the biblatex plugin that can be installed on it. I write .tex files with VSCode while keeping a live .bib file that automatically updates whenever I added new entries to it. I could collaborate with others if I added them to my git repository for this document, but I suppose not all collabroators have the same set up. So I think I should start looking into Overleaf.


## Final thoughts

I think I should have learnt all this on day 0! This would have saved me a lot of time when trying to publish or communicate with others.

> Science is not about making predictions or performing experiments. Science is about explaining. ― Bill Gaede

I knew I was in deep trouble when I wrote my thesis, but for some reason I dind't end up getting this stuff together. I should really thank Larry from my lab for inspiring me to do so, and pointing me to the resources by [Prof. Karl Broman](https://kbroman.org/). I think this kind of training should be made mandatory in every graduate program (wet-lab, dry-lab included), those safety classes are less important.

## Further reading