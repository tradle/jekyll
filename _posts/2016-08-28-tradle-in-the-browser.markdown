---
layout: post
title: Tradle in the browser
image: "/content/images/2016/08/nature-laptop-outside-macbook.jpg"
date: '2016-08-28 00:55:00'
tags:
- technical
---

The project I'm currently working on is getting the Tradle app working in the browser. As you may already know, we use React Native + magic spells to achieve a Node.js-like environment on iOS and Android. This way the overwhelming majority of our codebase can be reused on all platforms.

If you read "overwhelming majority" carefully, you probably thought to yourself: "Ha! So there *is* some platform-specific code. I bet that's where the engineers get their gray hair." You got me.

Capabilities and APIs differ from environment to environment. Here are some questions we ask ourselves whenever we consider adapting the Tradle app for a new environment:

- Security:
  - Who has access to this device?
  - Where do we store private keys? (cross fingers for dedicated secure hardware, e.g. Secure Enclave on iOS)
  - Where do we store data, and how safe is it there, e.g. can other users/apps access it, can it get wiped by a mis-flick of the wrist?
  - What cryptography is available? E.g. is there a secure RNG? Will signing/encryption be performant enough or will the app be running at 3 fps?
- Camera support
  - Can we take photos of documents here / scan QR codes? If not, can we upload files?
- Feasibility
  - How much work will it take to prep the environment? For example, the React Native universe of both core and userland components is much richer on iOS than Android, but Android is catching up quickly.
- ...plenty more

The end-result in a perfect world is an as-clean-as-possible separation of environment-specific adaptations from the app itself, a VM so-to-speak for the Tradle app to run in. Then application code doesn't need three toppings of environment checks. Most of the time, the app shouldn't know whether it's running on an iWatch or on neural interface that projects pixels straight into the mind of a dog.

The browser is not the most secure environment in the world. You can inadvertently wipe out storage, your curious spouse, her private investigator, and your favorite daughter (you know which one's your favorite) often have access to it, you install all kinds of browser extensions and blithely click "Yes" under "I understand that I'm allowing this extension to fill my life with regrets." At the same time, its convenience is unmatched. App updates can happen almost invisibly, you're not limited to your thumbs when filling out forms, there's room for more than a button and that ketchup stain on the screen, and the CPU has more horsepower.

So Tradle in the browser is an experiment. After a week of breathing life into it, the latest checkpoint is end-to-end messaging with a Tradle server, with most of the UI working. But there is still plenty of work to do.

Todo:

- react-native-accordion (fixed today)
- vector icons (fixed today)
- react-native-gifted-messenger - fix scroll handler
- back button / forward button sometimes don't work (need to figure out what generates bad history)
- chat messages that should show up, don't after back/forward (not related to browser history)
- password view on login/registration - gesture password is good for touch screens but not a mouse
- home page loses logo on re-render after splashscreen