---
layout: default
title: "Equifax Breach - Not Technical?"
date: 2019-01-02
categories: security
---

# Equifax Breach - Not Technical?

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/equifax-breach-technical-robert-hines-cissp-csslp-pmp-pe).*

![Collage of the Equifax breach notice, congressional testimony, and a stock chart]({{ "/assets/images/LI-Equifax-Breach-Not-Technical/cover.png" | relative_url }})

Application security and devops leader, [Troy Marshall, recently suggested the Equifax 2017 breach report by the House Oversight Committee Majority as required reading](https://www.linkedin.com/feed/update/urn:li:activity:6481267471138508800). He's absolutely correct. Yet, the lesson we should learn might surprise you.

Recall Equifax, one of the three large credit reporting agencies (CRAs), announced in September 2017 the theft of private data affecting 148 million consumers, 56% of American adults. Attackers leveraged out-of-date software to pillage Equifax's internal network for 76 days. If only those IT folks patched...right? That's what their now "retired" CEO, Richard Smith, said to Congress.

> No.

### Assessing Organizational Security

As it turns out, 70% of what organizations actually do to "be secure" comprise non-technical activities such as educating stakeholders, inventorying assets, defining acceptable vs unacceptable security, and providing business process support to ensure everything that should happen actually does. Sure...but isn't 70% a bit high?

> No.

Find a security framework and look carefully at the components. NIST Cybersecurity Framework (CSF) is one and another I'm familiar with is the Build Security In Maturity Model (BSIMM). BSIMM considers IT Security Risks with software risks in the center of view. The model outlines 116 activities firms have been observed to perform during observational studies conducted over the last 10+ years. Classify each activity and you'll find a 70/30 ratio between organizational activities and those technical things we normally attribute to "doing security". Great...but what does this mean for Equifax? Well, we can estimate a bottoms-up score for Equifax and try to understand the probable root of their problem. Hint...the 70/30 ratio kinda gives away the answer.

### Take Out the Ruler on Pseudo Equifax

Though we can't accurately measure Equifax from the outside, one can make educated guesses based on the CEO's Congressional testimony as well as other governmental and journalistic sources. Let's play the game for a fictional company called "Pseudo Equifax". The exercise is useful for several reasons. First, both CSF and BSIMM are public models so you CAN try this at home. For BSIMM, summary measurements have been published so you can see how Equifax might have scored, how you might score, and decide whether the resulting indicator is ok...or not.

![BSIMM9 score distribution with markers for Pseudo Equifax and Fine-Firm]({{ "/assets/images/LI-Equifax-Breach-Not-Technical/figure-01.png" | relative_url }})

Documenting the full Pseudo Equifax BSIMM score is too much for this space but the brief explanation gives credit for activities observed in 1/2 of BSIMM participants. The resulting Pseudo Equifax score is in the 17-26 range. The estimate is generous since there are clearly activities in this common set that could not have been observed. For example, an activity covering "host and network security basics" is observed 87% of the time but given Equifax's patching performance and their CEO-reported reliance on senior VPs forwarding vulnerability alerts by email, there's just no way they earn that observation (House Report, page 4). In any case, a score in the indicated range places Pseudo Equifax in the 16-30 BSIMM9 Score Bucket as shown in the diagram. At best, Pseudo Equifax's maturity is on par with fewer than 43% of 120 firms in the data pool - that is, the bottom 40%. On the BSIMM9 Score Buckets diagram, Pseudo Equifax is represented in orange. Each bar pair corresponds to the number of firms in that scoring bucket (blue bar) and the aggregate number of firms in that bucket and below (purple bar). All data to be found on BSIMM.com.

### What Should Pseudo Equifax Hope to Be?

As an objective, where SHOULD Equifax-like companies seek to place themselves in terms of BSIMM activity accomplishment? This answer can be had by introducing activities to overcome obvious shortcomings. One example to start, we'd enable Equifax to know where the out-of-date software components were used so that specific audits could be performed. These actions are embodied in activities identifying and controlling open source software. In BSIMM terms, controlling open source risk in their large inventory of legacy software requires requires automated identification of open source components and better processes than senior VP emails to ensure compliance. In fact, CI/CD and DevOps would properly leverage existing tool chains with no critical path load on developers. Making this all happen is a management responsibility. Overall, after looking at failures described in sources such as the Congressional report, a rebuilt Equifax security program might earn a BSIMM score in the 46-60 range placing it in the top 20% of participants. Pause on that. <u>Reasonable assurance comes by shooting to be the in the top 20%</u>...

### tl;dr Three Lessons to Learn

Three lessons I hope everyone gathered. First, a sound measurement framework is essential. Second, most of the activities involved in assuring good technology are not technical, they are management. Third, average isn't good enough for firms handling valuable, private, and sensitive data.

### Does Security Matter?

![Stock chart comparing Equifax, TransUnion, and Experian after the breach]({{ "/assets/images/LI-Equifax-Breach-Not-Technical/figure-02.png" | relative_url }})

And...because I can't resist, one wonders what financial and perceptual impact the breach had on Equifax. It's fair to view Equifax's stock price against the other CRAs; TransUnion and Experian. Technically, the diagram means nothing without supporting analysis but the picture doesn't look to be in favor of the business prioritizations Equifax made prior to September 2017. Whereas other Credit Reporting Agencies are up 17-20% for the period September 2017 to December 2018, Equifax is down 34%.

### Disclaimers:

1. I have no inside knowledge of Equifax. Estimated score was created from public information and might/or might not resemble an accurate picture of Equifax's actual, internal state. Think like: "This is a work of fiction. Names, characters, businesses, places, events, locales, and incidents are either the products of the author’s imagination or used in a fictitious manner. Any resemblance to actual persons, living or dead, or actual events is purely coincidental."
2. All expressed notions are mine.

### Useful references:

1. BSIMM: https://www.bsimm.com/
2. Congressional Report: https://oversight.house.gov/wp-content/uploads/2018/12/Equifax-Report.pdf
3. CEO Testimony: https://energycommerce.house.gov/hearings/oversight-equifax-data-breach-answers-consumers/
4. NIST CSF: https://www.nist.gov/cyberframework
