---
layout: post
title: Tradle software tutorial - part 1
---


I want to give a short tutorial on how to use Tradle’s trust-in-motion ([TIM](https://github.com/tradle/tim)) open source software. But before I do that, I want to give a short overview of what TIM does, and what one might use it for. But before that…a short joke to incept clarity:

> Two deaf French guys, Pierre and Jean-Paul, are talking:  
> **Pierre**: want to go fishing with me tomorrow?  
> **Jean-Paul**: can’t, I’m busy, I’m going fishing tomorrow


## Trust in motion

TIM is a peer to peer comm device with two modes:

### Walky talky

This is serverless, end-to-end encrypted (OTR*), realtime, NAT-breaking, free chat, much like secure IM. It allows you to talk “securely” peer to peer, without any intermediaries. If you’re thinking “what intermediaries?”, think about any communication method you use today.

When you call someone on the phone, your call goes through your telco. When you email someone, the email goes through your email provider. When you use your debit card, your payment goes through a number of intermediaries like PayPal, Visa/Mastercard and your bank. When you chat with someone on most IM clients, your messages go through some server or another, owned by some third party or another. When you sext over Snapchat, the Snapchat servers see your naked butt before they pass it along to its final delighted recipient.

Essentially, we live in a world where there’s a man in middle for everything.

So if you don’t make sex tapes, or you keep them on VHS, what’s so bad about having an intermediary? Just that they own your ass. Being in control of the comm channel, they can deny you service, surveil you, impersonate you, change what you say and sell you out to other third parties, to name a few. I’m not saying that they do that (some of them do), but they can. Which means you’re putting a lot of trust into them.

Now that you’re very scared, as you damn well should be, I should say that at least among chat clients, there are a number that provide good security. If you’re interested, the Electronic Frontier Foundation (EFF) keeps an updated breakdown [here](https://www.eff.org/secure-messaging-scorecard). You’ll notice that AIM, Skype, WhatsApp and Facebook chat fail miserably. Among the champions there’s Pidgin, which has been around forever, and WhisperSystems’ privacy-empowering duo of Signal and TextSecure.

If you haven’t already, have a look at the security factors EFF uses to score messengers. Just the questions they ask are a small lesson in security:

- Encrypted in transit?
- Encrypted so the provider can’t read it?
- Can you verify contacts’ identities?
- Are past comms secure if your keys are stolen?
- Is the code open to independent review?
- Is security design properly documented?
- Has there been any recent code audit?

At it’s current state of evolution, TIM will not be able to address all of these questions to the EFF’s satisfaction. But this list outlines some clear goals.

### Chained messages / “Quotable chat”**

Serverless, encrypted (ECC, AES), slow (1+ hours for delivery), relatively expensive chat (2p / message). This is arguably the more important part of TIM’s functionality. It is not meant for regular messages, but rather messages you want to be highly auditable, messages you want to be able to make provable claims about in the future:

- Claim & prove the message existed at a certain time
- Claim & prove the message’s contents haven’t changed
- Claim & prove who sent the message and to whom it was sent

There are also several special properties to the message’s existence:

- It’s stored/served by conversation participants (vs in the cloud). There’s a balance between centralization and decentralization. On the one hand messages are all hanging off the blockchain (though not stored directly in it), and on the other the blockchain is a decentralized database, unlike the typical cloud database.
- It’s encrypted to be readable only by conversation participants. Moreover, each message is encrypted with different keys***.

### With their powers combined…

The two comm modes, transient vs permanent, realtime vs don’t-hold-your-breath, deniable vs non-repudiable, work together hand in hand. When you engage in small talk, use the first one. When the message is a contract or a payment or any kind of transaction for which accountability is important, use the second (but still use the first for realtime delivery).

### What’s the point?

The idea that led to TIM’s birth is not new. The goal was and is to enable a decentralized identity, and to allow network participants to communicate and build their reputations, without those communications and reputations belonging to a third party. This “identity platform” can then be used for e-commerce, governance, etc.

### KYC: statements of trust

[![XKCD: Responsible behavior](https://imgs.xkcd.com/comics/responsible_behavior.png "Statements of trust")](https://xkcd.com/364)

The specific application we’re working on currently is KYC: statements of trust by parties with great motivation to get their facts right (banks), about parties who need reputations in order to garner trust in the global marketplace (individuals and SMEs). Using Tradle’s TIM, when banks verify companies and individuals, they then reward those individuals at the end of the KYC process by publishing statements of trust about them. Those statements, as well as the raw data consumed by the KYC process, can then be shared by the individual in global marketplace, e.g. with other banks and network operators, in the on-demand marketplace, etc.

With that in mind, the first step towards this goal is creating and publishing an identity to hang data and statements of trust on. The tutorial for doing this will appear in the next installment.

<sub>* OTR (off-the-record) provides the interesting duality of ensuring that you’re mutually authenticated with the other party, while providing deniability of the conversation. In other words, you know you’re talking to them, but you can’t prove they said anything to a third party.</sub><sub>** “Quotable chat” in quotes, pun very much intended.</sub><sub>*** The current design does not provide what’s called “perfect forward secrecy,” as keys used to encrypt links embedded in the blockchain are reused. This is a weakness in the design that we would love some help designing out.</sub>


