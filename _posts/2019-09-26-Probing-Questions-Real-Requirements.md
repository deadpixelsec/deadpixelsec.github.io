---
layout: post
title: Asking Probing Questions to get to the "Real Requirements"
---

25 September 2019

[@CharCharBonkles](https://twitter.com/CharCharBonkles)

My grandpa was an engineer and a farmer, and as a kid I spent many summer weeks at my grandparents’ farm.  I was introduced to centrifugal and centripetal forces as a youngster while helping my grandpa feed the many farm cats – after filling up their bowls with calf milk replacer, he’d fill the bucket with water and spin it in a vertical circle.  To my amazement, the water didn’t come pouring out even though the bucket was upside down! (Add that to your list of ways to blow a child’s mind!)

My dad is a mechanical engineer.   I grew up in an environment where inquisitive questions, dinner conversations about the doppler effect and circuit breakers were the norm.  In the winter, when the woodstove in the corner of the living room was lit, my dad, brother, and I huddled around and discussed the three modes of heat transfer.

I’m an inquisitive science nerd, and I’m pretty sure I know where I got it from…  These discussions and experiences not only made perpetually curious about the world around me, but also taught me how to ask the right questions to get to the bottom of whatever I was curious about.

<div style="text-align:center">These days, I'm curious about requirements gathering!</div>

This summer, I designed a database schema for a friend (and absolute genius of a coder - [@capnspacehook](https://twitter.com/capnspacehook)) to use as a backend for the project he’s working on.  We had many interesting conversations about how to design the schema.  During these conversations, I noticed a pattern: my friend would mention an idea he had for the database schema.  Then, partially because I had a hard time grasping the full context of the idea and partially because I had an inkling that there was a more efficient way to implement it, I would ask one or more probing questions:
* Why do you want a many to many relationship between table x and table y?
* Can you tell me more about _______ and why you want it that way?
* A more efficient way to do the same thing might be to _______.
* Do you think ______ would work?  Is there something I didn’t consider?
* So what I think you’re saying is _______.  Is that right?

Most of these questions are pretty open ended.  Asking the right kind of question in the right way is just as important as asking the question in the first place!  These questions are crafted in such a way that when the client answers, they are providing context and a deeper understanding of the problem at hand.

All these questions are aimed at the same thing – gaining context and understanding what I call the ‘real requirement’.  Oftentimes, a requirement is what the customer thinks they want.  A real requirement is the best solution to the underlying question, issue, or sometimes even misunderstanding that led the customer to state their initial requirement.  Determining the real requirement involves understanding why the customer suggested the requirement that they did.

Understanding the why behind an initial request will lead you to the real requirement – the best solution for the customer’s problem.  And the best way to understand the why?  Ask probing questions.  Never assume you understand what the customer actually needs until you’ve asked enough questions and the customer has affirmed your restatement of their need.  This is difficult, because the client doesn’t always know exactly what they want or need.  Helping the client figure that out is the hard part of the requirements gathering process.

According to my dad, who sometimes travels to customer sites to troubleshoot circuit breakers says that “The company says the customer is always right... But in the real world you get half of the story and only half of that is true.”  He tells the story better (and with much more technical detail), but once a customer kept rejecting a circuit breaker because of an error with a certain register.  After visiting the client site and asking probing questions, my dad discovered that the client was concerned about the integrity of a *different* set of registers because of the issue with the certain register, and that was why they rejected the product.  After explaining the differences between the two sets of registers and assuaging the customer’s concerns, he was able to move forward with the project.

It’s tempting to take the customer’s request at face value and turn it into a requirement, but it’s important to ask probing questions, get to the bottom of the problem, and make sure the customer gets the best solution possible!
