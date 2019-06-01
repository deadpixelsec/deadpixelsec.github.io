---
layout: post
title: How Combat Sport Psychology and Strategy apply to the Red vs. Blue dynamic of Cyber Security Competitions
---

[@CharCharBonkles](https://twitter.com/CharCharBonkles)

*Author’s note: The last portion of this article relies heavily on my personal experiences “in the ring” of collegiate taekwondo sparring and “in the pit” of the Mid-Atlantic Regional CCDC.  Many of the fighting strategies are ‘coach-isms’ and are not from an official source.  Sources are linked inline.*

A recruiter at the 2019 MACCDC Regional competition noticed that I listed a karate black belt as an achievement on my resume, and asked me if I thought there were correlations in the respective strategies of physically attacking someone and attacking a network.  My original answer involved an explanation of how varying the speed, direction, and height of a physical attack makes the defender’s job very difficult, and similar variety in a network attack likewise makes the defender’s job more difficult.

That discussion led me to investigate the similarities in underlying psychology and strategic similarities between combat sports and my experiences at MACCDC.  Four areas of psychological similarity are mental toughness, focus, stress management, and the role of practice and preparation.  These areas impact performance in both sparring matches and cyber defense competitions.

Two important components of mental toughness are resilience and how one handles failure. Merriam-Webster defines resilience as "[an ability to recover from or adjust easily to misfortune or change](https://www.merriam-webster.com/dictionary/resilience)." In a sparring match, misfortune can consist of an opponent landing a devastating head kick.  In a cyber defense competition, such misfortune takes the form of downed services and the appearance of [nyancat instead of a bootloader](https://github.com/brainsmoke/nyanmbr).  The ability to recover from these events by handling failures properly is critical to success in both sparring and cyber defense competitions.

Two [tips for maintaining resilience](https://www.peaksports.com/sports-psychology-blog/if-your-mental-toughness-only-improved-one-percent/) during a stressful situation are:
1.	Decide ahead of time how you will react in adverse situations.  See yourself responding positively at critical moments in competitions.
2.	Choose a motto that will guide your behavior during adverse times.  Repeat it to yourself as you meet your challenging situations.

These two tips are incredibly useful, I do both of these things (although I didn’t realize it until I started writing this).  Regarding the second tip, my personal motto is “no plan survives first contact”, which is a paraphrased form of a [quote from Helmuth von Moltke the Elder](https://en.wikiquote.org/wiki/Helmuth_von_Moltke_the_Elder).  The contact can be either an unexpected punch to the face (in Mike Tyson’s case), or the decimation of your team’s network by the red team.

<img align="right" width="400" height="200" src="https://github.com/cpbarker/deadpixelsec.github.io/blob/master/images/AnalysisParalysis.jpg" alt="Analysis Paralysis? Aint nobody got time for that!">

Focus is incredibly important to success in both combat sports and cyber defense competitions.  The type of focus required for combat sports can be defined as “[a state of being both simultaneously alert and relaxed with an effective, yet empty mind](https://rough.asia/analysis/focus-the-psychology-of-fighting/).”  The same type of focus aids in the problem solving process and teamwork required to defend a network.  Focus is a combination of alertness and analysis, without analysis paralysis.

When asked how I was dealing with the stress of the CEO interview portion of MACCDC, I replied, “I’m always stressed out and out of my comfort zone, so this is normal.”  I am comfortable and incredibly focused in highly stressful situations, and I do some of my best thinking and work under higher-than-normal levels of stress.  Stress is a large part of life, like it or not.  However, how stress levels are managed in incredibly stressful environments can make or break reactions and decision-making processes.

<img align="right" width="400" height="200" src="https://github.com/cpbarker/deadpixelsec.github.io/blob/master/images/ImproviseAdaptOvercome.jpg" alt="Your services died? Improvise, adapt, overcome.">

Stress can be defined as “[the strains on our physiological and psychological well-beings that occur because of the taxing of emotions that arise because of our appraisals of events, situations, or occurrences that are threatening to our sense of well-being](https://www.researchgate.net/publication/226135997_Sport_Psychology_in_Combat_Sports).”  However, research demonstrates that complete elimination of stress does not increase performance.  Rather, a “[zone of optimal stress […] is associated with peak performance]().”  This zone of stress is different for everyone, which explains how some thrive under immense stress and pressure and others fold.

Stress is high in competitive situations, including both collegiate taekwondo sparring and MACCDC Regionals.  Learning how to diffuse stress and carry on with the task at hand is important for longer events, especially those which require high degrees of collaboration and teamwork.

<p align="center">
*cough* MACCDC *cough*
</p>

I’ve noticed that as my level of stress rises, it becomes more difficult to interact with those around me without raising their stress level as well.

Finally, practice and preparation are where the foundations for mental toughness, focus, and stress management are built.  One of my favorite “coach-isms” is “you play how you practice.”  The more like the 'real deal' practice sessions are, the better!  Although it is difficult to re-create the stress of a competitive atmosphere, it pays off.  Practice is a safe place to try new things, be it a new kick combination or a risky registry key edit.  I see practice as an opportunity to refine skills and master the basics, not drudgery (although it can be repetitive).  A word of warning: don’t practice in a way that forces you to commit to one single reaction to an event.  In fighting, this makes your moves very predictable.  In cyber defense competitions, this lack of flexibility can result in an inability to act when the conditions are not the same as the ones you practiced under.

<p align="center">
--------------------------------
</p>

Now for the part that I really wanted to write but decided I needed to provide background for!  The aforementioned psychological categories/aspects are foundational to many fighting principles that also apply to cyber defense strategy.  Behold, a list of fighting principles and their correlated cyber security principles!

* Set up your attack: OSINT/ Recon
* Know your enemy – observe, and go for the weakest link: OSINT / Recon
* Protect your head: Know and protect valuable assets on your network
* Know your own weaknesses: Internal audits and awareness of likely targets
* Use your surroundings to your advantage: Get to know the ‘lay of the LAN’
* Not everything works on everyone: Not every network has the same vulnerabilities
* Don’t telegraph your moves: Remove all of an attacker’s access at the same time
* Don’t bring a gun to a knife fight: Verify a threat before acting, and then respond appropriately
* When you enter the ring, the only thing you can control is your own conditioning: Practice, have a plan in place, and do your due diligence.  It’s too late to worry about what you should have done when you’re in the ring!

Many of these principles are different sides of the same coin.  Attack and defense go hand in hand, in both combat sports and cyber security!  The better you understand one, the better you understand the other.

Setting up attacks is incredibly important in competitive sparring.  An opponent is expecting an attack, so it is important to observe their fighting style, reaction time, attack patterns, and any other useful information and factor it into an attack.  For example, an opponent might have a habit of dropping their left hand right after they throw a certain technique.  Knowledge of this pattern might enable an attacker to score a head kick.  Open Source Intelligence (OSINT) and network reconnaissance serve a similar purpose: familiarity with an opponent eventually enables an attacker to identify and exploit weaknesses.  These weaknesses can be anything from poor physical security and vulnerability to social engineering to system or network level vulnerabilities.

Protecting your head is critical in a competitive fight.  Not only are successful head kicks worth more points than any other techniques, but they can lead to serious injuries like concussions.  Your head is a valuable target in sparring, like valuable information, critical network infrastructure, and privileged accounts are valuable targets on a network.  In both fights and network security, protecting high value targets is important!  This is along the same vein as knowing your weaknesses and building a strategy around them.

The concept that not everything works on everyone in a fight also applies to network security.  In self-defense, there are several common techniques (think swift kick to the balls).  These techniques will not work on every single person, because each person is different, and an attacker may be on drugs that makes them relatively immune to pain.  Networks are like humans, they are complex and have similarities, but are almost never the same.  So, it follows that not every exploit will work on every network.  So, if something that usually works doesn’t work, don’t give up, and keep trying!

The ‘coach-ism’ to not telegraph your moves is also relevant to cyber security, specifically attack-defend competitions such as CCDC.  As a network defender, when I spot a suspicious process on the windows server I’m monitoring during the competition, my first inclination is to delete the process and move on with whatever I was doing before.  However, this action can be counterproductive to the defense of the system and network.  In my experience, red team is like hydra – cut off one head and two more grow in its place.  So, in order to remove red team’s access to a system, removing one method of persistence at a time won’t cut it.  Doing so “telegraphs” my next moves – I’ve found one method of persistence and removed it, and it’s likely that I’m in ‘hunt mode’ searching for other persistence on the box.  So, before red team loses all access and must break in again, they can disable or mess with the tools that I need to remove their access, as well as implant stealthier methods of persistence.  To avoid this, I typically round up as many persistence methods as I can find, and remove them all within a small time span.  In a perfect world, the red team is focusing on a different system at that time and will come back to find a bunch of dead shells and no persistence on the system.  (The world is rarely perfect, and sometimes this just makes the red team target the system more aggressively if they still have a persistence method.)

The phrase “don’t bring a gun to a knife fight” represents a tendency to over-react to stressful situations.  In my experience, it’s easy to see every little thing that looks out of place on a CCDC network as an indicator of compromise and go down the rabbit hole when it may just be a configuration change required to run a required service.  So, it’s important to properly assess the situation and react appropriately.  The same concept is valuable in self defense; assessing a situation can allow you to diffuse it before it turns into a fight, or be prepared to use acceptable levels of force to defend oneself.

Finally, my favorite words of wisdom from my collegiate taekwondo coach are the following: “When you enter the ring, the only thing you can control is your own conditioning.”  What this boils down to is that once you’re in the ring, you have to rely on all of the time and training to carry you through – you can’t bow out and go practice a specific technique or go get in better shape.  This would be akin to taking time off of an actively attacked system to google how to do something.  Sure, sometimes you have to go look things up, but it’s too late to worry about what you should have done and do what you can.  Save those thoughts for the after action review!
