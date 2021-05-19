---
layout: post
title: "Six months at Styra"
date: 2021-05-19 00:22:22 +0100
categories: tech
tags: opa openpolicyagent styra
---

Wow, time really does fly! Feels like only yesterday I said [goodbye to Bisnode]({% post_url 2020-11-25-thank-you-bisnode-hello-styra %}), and hello to Styra. But that was back in December! Almost six months later and..

- OPA is now a [graduated](https://www.cncf.io/announcements/2021/02/04/cloud-native-computing-foundation-announces-open-policy-agent-graduation/) CNCF project.
- Styra has been listed as one of the [best workplaces of 2021](https://www.inc.com/best-workplaces/2021)
- ...named as a [cool vendor](https://registration.styra.com/styra-gartner-cool-vendor) by Gartner.
- ...has [raised $40 million](https://techcrunch.com/2021/05/18/styra-the-startup-behind-open-policy-agent-nabs-40m-to-expand-its-cloud-native-authorization-tools/) in series B funding.

To call the last six months eventful would be an understatement! While I'd like to believe I've played at least a tiny part in the bigger events, this also feels like a good time to note down some of my own work and experiences working with OPA at Styra for the last half of a year.

### Community

One thing that wasn't new to me was the fantastic OPA community. In fact it alone had been a major driver in my decision to work full time on OPA. Getting to work not just on open source, but one of the coolest projects around, was just insanely awesome.. and six months later, it still is. There's just so much cool going on around OPA that I can barely wait to see where we are just six months or a year from now.

Needless to say I'm somewhat biased at this point, but I believe the clear separation between OPA the open source project and Styra the company has really been well managed by Styra, and while the [Styra DAS](https://www.styra.com/pricing) is a kick-ass control plane for managing OPA at scale, I appreciate having a clear line drawn between community work and Styra the product. I've come to understand that this is something many developer advocates struggle with at other companies and communities.

### Team and Colleagues

Having worked in and around the OPA community for quite some time, and for a Styra customer even, I knew at least a handful of colleagues before joining. Though I don't work with everyone in the company I have probably had some interactions with most by now, and I've gotta say that Styra has really managed to collect some of the most competent _and_ kind people I've had the pleasure of working with in my career so far. Working with so many smart people has been a humbling experience, but since they seem to appreciate what I'm doing I guess I must be doing something good, or they're not that smart after all :)

### Coding

Already before starting at Styra I had contributed quite a few commits into OPA and the surrounding ecosystem. While I still try to write at least some code each day, I find myself prioritizing other tasks, like blogging, higher. Working closely with people who are way better coders than I am helps some with that too. Not in the sense that I don't feel like I can contribute, but I find it pretty hard to maintain a balance between my responsibilities if I let myself get too involved in bigger coding tasks or PR discussions. While I enjoy coding on OPA I've had just as fun working with side projects in the ecosystem, such as the [Clojure OPA middleware](https://github.com/anderseknert/clj-opa). Need to remind myself to work more on projects like that!

### Working From Home and Timezones

While I, like most of the people in tech during the pandemic, worked from home long before joining Styra, this is my first job where I know there won't be an office to go to later. While I feel more productive at home most days, having to share an "office" with a newborn kid has been a challenge at times. Having a real office to go to for presentations, meetups and webinars would definitely help, and after the summer and my parental leave is over I'll look into renting something like a shared workspace with private rooms for that purpose.

With the majority of my colleagues in the US west coast, the timezone difference has been a bit of a problem at times. There's only really an hour or so of natural overlap in office hours between Stockholm and Pacific Time, but with most communication taking place on Slack or over email, there hasn't been a need for that many meetings.

Timezone wise I expect things to normalize somewhat as Styra grows in Europe and more colleagues will work closer geographically. Secondly, working from home becomes truly awesome when combined with occasional traveling, as that pretty much provides the best of both worlds, and I am really looking forward able to go to non-virtual conferences, meetups and events soon.

### Blogging

While I did write the occasional internal blog at Bisnode, and certainly my fair share of wiki pages, documentation, and so on.. I've really gotten the chance to ramp up my blogging at Styra. While writing posts for blogs that are not only public, but often have quite a large number of readers, can feel quite intimidating at times, it is also extremely rewarding!

Having people, from both my own team and from Styra's fantastic marketing team, review my blog posts before they are published and provide corrections, edits and feedback has really been invaluable. I feel like I've learnt so much here these past six months and yet I feel like I've only just started. Really looking forward to keep learning in this space! Here's the blogs I've authored so far. Some for the [OPA blog](https://blog.openpolicyagent.org/), some for [Styra](https://blog.styra.com/blog) and some for external publications:

- [Open Policy Agent 2020, year in review](https://blog.openpolicyagent.org/open-policy-agent-2020-year-in-review-dc25b60308d7)
- [Integrating Identity: OAuth2 and OpenID Connect in Open Policy Agent](https://blog.styra.com/blog/integrating-identity-oauth2-and-openid-connect-in-open-policy-agent)
- [5 OPA Deployment Performance Models for Microservices](https://thenewstack.io/5-opa-deployment-performance-models-for-microservices/)
later republished on the [Styra blog](https://blog.styra.com/blog/5-opa-deployment-performance-models-for-microservices)
- [The Kubernetes Authorization Webhook](https://blog.styra.com/blog/kubernetes-authorization-webhook)
- [Linting Rego with... Rego!](https://blog.styra.com/blog/linting-rego-with-rego)
- [Dynamic Policy Composition with OPA](https://blog.styra.com/blog/dynamic-policy-composition-for-opa)
- [WTF is policy as code](https://blog.container-solutions.com/what-is-policy-as-code)
- [Community Spotlight, Grant Shively](https://blog.openpolicyagent.org/community-spotlight-grant-shively-12903674c28c)
- [Getting Open Policy Agent Up and Running](https://thenewstack.io/getting-open-policy-agent-up-and-running/)
- [What is Open Policy Agent?](https://blog.styra.com/blog/what-is-open-policy-agent)

### Meetups and Conferences

Besides blogging, presenting OPA at meetups and conferences has really been the main activity on my list of priorities. While this wasn't something new to me, and I'd much rather meet people in person than the online events we've all had to attend this last year and a half, I must say I really enjoyed this.

<img src="/assets/rosenheim.jpg">

I've talked at a couple of conferences and more than a dozen public webinars and meetups. On top of that probably as many or more internal meetups at companies. I've come to think that the meetup format has been a better fit for online/video than the (especially big) conferences have been. Another observation is that although there is nothing stopping anyone from joining local community meetups online, they have remained surprisingly... local. Presenting for a small local community of peers where almost everyone knows each other by name, that feeling really comes across even online.

### Twitter

Having worked mainly with internal development communities at companies in the past, I hadn't really had much use for Twitter. Now working full time with the larger OPA community made Twitter a great choice for interacting with the community just as much as for promoting blogs, events and meetups to people outside of it. In fact Twitter was so engaging that I eventually had to remove the app from my phone, and I'm now only checking in from my computer a couple of times per day. I've already made some great connections there and I'm looking forward to growing my network. Find [me there](https://twitter.com/anderseknert), and if we haven't already I'd be happy to connect!

### Summary

Though I, as I guess most people do, sometimes feel I could have have done more, looking back at the past six months makes me realize I've really done a lot! Most importantly, I've had a lot of fun and learnt so much along the way. Exciting times, and I'm really looking forward to growing in my role as a developer advocate here, just as much as I enjoy being part of the bigger Styra journey. If you'd like to join me on that, Styra is [hiring](https://www.linkedin.com/company/styra/jobs/)!
