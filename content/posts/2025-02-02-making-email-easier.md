---
title: Making Email Easier for Developers
date: 2025-02-02
draft: false
author: Jeremie Bornais
--- 

Email is and always will be a pain to work with as a developer. What began as a simple and open communication channel has become a mess, thanks in part to spammers and scammers. Now, if you want to be able to reach your users, you almost always need to use some third party service to send your emails for you.

This isn't necessarily a bad thing. In produdction, the only difference is changing an environment variable to point to a third party [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) server instead of your own. What happens when you're not in production though? How should you handle emails when working on an application locally, as a developer?

This is the situation I found myself in a few months back when working on a project for the [NASA Space Apps Hackathon](https://www.spaceappschallenge.org/nasa-space-apps-2024/find-a-team/reesaholics/?tab=project). Our team was building a web application and wanted to send email reminders to our users. Simple enough - find an SMTP service, put in the credentials, and let Python take care of the rest. The annoying part, however, was the fact that all of the developers on our team needed to either share credentials to our production SMTP service, or figure out our own SMTP service to use while working locally. Using an actual SMTP service for local development can be a pain too, especially when you're waiting (sometimes several minutes) for emails to appear in your inbox.

## The Solution

It wasn't until a few months later that I discovered "fake SMTP servers". These services run locally and intercept all emails your application sends, acting as a controlled environment for testing and local development. What this means as a developer is you don't need to worry about having credentials to an SMTP service and you don't need to wait for emails to hit a real inbox. You run the fake SMTP server, point your application at it, and when your application sends an email you immediately see it in your fake SMTP server's web interface.

My favourite of these services is a project called [Mailpit](https://github.com/axllent/mailpit). You can download and run the service as a single static binary or run it as a Docker container. The configuration is super simple, and the web interface is great. My advice: if you're a software developer working on an application that needs to send emails via SMTP, use Mailpit when developing locally.

## My Version

Of course, I wouldn't be a true software developer if I didn't take a stab at making my own implementation of a similar service... Enter [fakesmtp-py](https://github.com/jere-mie/fakesmtp-py), a barebones alternative to Mailpit. See, Mailpit is probably going to be better in the majority of cases and for the majority of users, but I had a unique vision for fakesmtp-py. 

There were a few things I wanted that motivated me to make my own fake SMTP service:

1. I didn't want to have to open a web interface to see emails.
2. I wanted to be able to embed the fakesmtp service directly in my codebase.
3. I wanted to better understand how these services work.

Realistically, none of these are *that* important and I could have been fine sticking with Mailpit. However, considering how simple the end product ended up being, I'd say it was worth the time and effort.

One of the things that bugged me about working with Mailpit is having to switch browser tabs to see the contents of my emails. Seeing them appear directly in the terminal (or seeing them saved in a file in my editor) is a small developer experience improvement that I value. (Of course, if you do want to see the emails in a web interface, I have that option in fakesmtp-py, but be warned it's a lot uglier than Mailpit's).

My second motivation for making my own service, wanting to embed the service directly in my codebase, is another small detail that I wanted in my workflow. I did have other options to achieve this - I could have included/vendored the Mailpit binary in my codebase. However, as someone who often works on bare metal Windows, WSL, and Linux proper, I would have needed to include multiple binaries to achieve this. Something about doing this didn't feel quite right though... taking someone else's binary and sticking it in my codebase. Since it's a binary too, it works kind of like a black box - how exactly does this service work and how exactly should I use this? Both of these are solved by linking to the GitHub repository and documentation, but again, something just *felt off* about doing this.

I'm primarily a Python developer in my free time (though I have also been working with Go a lot recently), so implementing this in Python made the most sense to me. Not only is it written in the language I'm already developing my application in, but it's cross-platform out of the box, and it fits in one (arguably) easily-readable file that anyone can see. The only thing I don't love about my implementation is it uses packages outside of the Python standard library. There used to be projects that achieved this using the standard library (check out [this one](https://github.com/VaderZ/fakesmtp) from 2011), but unfortunately these no longer work ([RIP smtpd](https://docs.python.org/3/library/smtpd.html)). Adding a relatively-small third party library in my Python projects is a small price to pay, I guess.

My final motivation for building this, wanting to learn more about how these services work, is probably the best reason for me (and maybe you) to build a service like this. Going down the email/SMTP rabbit hole has been an interesting experience and I've learned quite a bit in the process of making fakesmtp-py. Even if no one ends up using this service (including myself), I still see it as a success, and I'm glad I spent the time working on it.

## In Conclusion

My advice to developers: don't shy away from creating your own version of an existing product. Even if your version ends up being objectively worse for most users, it might be the perfect fit *for you*. Moreover, even if you don't end up using it, you'll certainly be better off after learning how to build it. And who knows, with my new knowledge of fake SMTP services, maybe Mailpit will see a new contributor soon too.
