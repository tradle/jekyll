---
layout: post
title: Tools of growth
featured: true
image: "/content/images/2016/08/construction-work-carpenter-tools1.jpg"
date: '2016-08-21 00:00:15'
tags:
- startup
- governance
- technical
---
![](/content/images/2016/08/construction-work-carpenter-tools1.jpg)
There is a school of thought on managing growth - you need good managers to manage it, ideally the best managers we can get, right? As we are building the world class organization, we are told by our advisors, whom we love and extremely grateful to, that we need to create an org structure, a matrix structure perhaps, proper policies, and the industrialized processes. But before we fall into the common pattern of adding more people..
![](/content/images/2016/08/project-managment.jpg)

..let's recall the Startupbootcamp's mini-MBA course on company building: [Lean Startup](http://theleanstartup.com/) and [Business Model Canvas](http://www.businessmodelgeneration.com/canvas/bmc).

In this spirit of openness let's discuss what we need now before we rush to add structure that can stifle experimentation, which is the essence of Lean Startup.

Let's see if we find the tools to manage our growth.

##Tools we use already
1. Google Apps for mail, calendar, docs, sheets, slides, diagrams.
i. Everyone's work calendar should be made open to the whole Tradle team.
ii. Google sheets are used until the migration to proper CRM
1. [Github](https://github.com) for public and private code and docs repositories.
i. We share private code and docs with customers by asking them to give us their github IDs (which they often do not have - ideas?)
1. [Travis Ci](https://travis-ci.com/) for automated testing
1. NPM for publishing software modules so that they can be installed
1. [Docker Hub](https://hub.docker.com/) for deployment of Tradle servers
1. [Webex](webex.com) for video meetings with customers. It is the only video chat, dial in, and screensharing tool excepted in most all firewalls in banks and other Enterprises.
1. [Zoom](https://zoom.us) for internal video meetings
1. Blog: we use Ghost, it is self-hosted and simple (simplistic? - e.g. you must use markdown to write posts, and have to click 'save draft' to avoid losing what you have typed.
1. [eShares](https://esharesinc.com/) for cap table management
1. [Gusto for payroll](https://gusto.com/product/payroll)

##Tools we need to choose

###Internal instant communications
Contenders are:
1. slack (supports mobile & desktop, presence management)
2. whatsapp (supports SMS, voice, end-to-end encryption developed with Open Whisper Systems)

Slack has taken startup world by storm, it managed to achieve the unachievable - it replaced a lot of email conversations, so it deserves careful consideration.

####Here is my past experience with Slack
We used Slack a lot before and although it is extremely well crafted and feature rich, I felt it had significant issues, so before we start using it we need to consider them carefully and institute policies to address them:

1. it is not a web product, is not indexable by Google so does not work for SEO. Note that Ethereum is using [discussion forums](https://vanillaforums.com/) quite well for SEO and support: https://forum.ethereum.org/
2. it promotes group chat and becomes super super super chatty - I wasted hours and days and felt helpless
trying to follow group conversations, especially if were not part of them and are trying to catchup, as on Slack there is no division into threads, just topics, so 5 conversations become intertwined.
i. The alternative we are considering for long form conversations is https://nodebb.org/
ii. Simon: Mark has installed NodeBB on http://forum.tradle.io for experimentation, it needs a lot of customization. re:email support, notifications, replacing nodebb branding with ours, figuring out internal forums vs external forums (and the ability to move an existing thread between them)
1. Slack app on Mac was (is it still?) a major CPU killer, not always, but often. I had to stop it, and then would miss messages.
1. Slack is costly if you need access to old messages (beyond 10K limit). It is $12 per user.

Does anyone know remedies or can suggest how to handle above issues?

####Best parts of Slack

1. instant communications - the forum (e.g. NodeBB) is no match, thus we will always relegate to skype chat or messaging
1. presence - it is very important for a team that is on all continents to know if you can bother someone - as you see them online/away/offline
1. multitude of integrations with other tools (e.g. you can get notified on slack regarding customer issue, technical problem, etc.)


###Support (customer and developer):
1. instant: slack group
2. async (delayed response): [NodeBB] forum
3. tickets/issues: issue tracker provides a lot more structured functionality than the forum. Github issue tracker is quite rudimental and requires understanding which module is at fault, which might be ok for developers but not for customer facing complaints and suggestions.

###Work planning
1. project/task managers: trello (latest darling of startups using a slightly more visual board style)

###Sales tools
1. CRM: salesforce (powerful platform but complex, expensive), SuiteCRM (open source, self-hosted), Zoho (10 free licenses). But before choosing the tool, [let's transform the way we sell](http://blog.hubspot.com/sales/inbound-sales-transforming-the-way-you-sell#sm.0001ailorbm9reqju5y1gram9xhd3).

###Event planning
1. shall we use the CRM for that? It could help with collecting all the leads.
1. card scanner: today I use CamCard app for scanning business cards, which I get by the dozens. I am told Evernote is miles better, and even connects to LinkedIn, but could not get it to work on my android.
1. sadly we need to print business cards. Ideally they should have person's photo, and [Tradle] QR code, to connect electronically using Tradle app.

###Newsletter
1. Ghost blog allows to get connected to a newsletter. TODO.
2. Many companies use Mailchimp, shall we?

###Marketing
This section needs a lot of work, as we have not started our strategic marketing yet
####Tracking mentions
1. We need to know when press writes about us and we need to know when to react on social media mentions. Today we  use http://mention.net, should we continue?
####Posting
1. we use http://buffer.com to tweet at the preferred time, should be continue?
#### Journalist relationships
Shall we use CRM for this?

### Funding
Shall we use CRM for managing all engagements?

###Governance
Let's explore the possibilities:

1. Buffer is [pushing the envelope](https://buffer.com/transparency) with the radical transparency of their governance.
1. Corporate actions. We use eShares for cap table management, but it is a glorified excel. We preach to the corporates the corporate actions on blockchain. Time to create them and eat our own dogfood.
