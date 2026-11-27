---
layout: default
title: "They Opened the Gate. Malicious JavaScript Rode In."
date: 2026-11-23
categories: security
---

# They Opened the Gate. Malicious JavaScript Rode In.

*Originally published on [LinkedIn](https://www.linkedin.com/pulse/opened-gate-malicious-javascript-rode-robert-hines-d0fae).*

![Painting of a wooden Trojan horse being wheeled toward the city gates]({{ "/assets/images/LI-They-Opened-the-Gate-Malicious-JavaScript-Rode-In/cover.jpg" | relative_url }})

*Attribution: Seudo, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), via Wikimedia Commons*

Hope this is no surprise, but most of the code modern web pages run in your user's browser comes from someone else, a third party. According to HTTP Archive, somewhere north of 64% of that code is third-party. If that code were something you built into your codebase, it would just be a supply chain challenge. We're becoming increasingly used to managing that set of risks. Problem is, much of that third-party (3P) code is dynamically loaded from hosts owned by vendors you've chosen to trust. But SHOULD you be trusting them?

Report URI, a Content Security Policy (CSP) reporting service, wrote an excellent blog post on the November 16 drive-by JavaScript attack that rode in on Optimizely's trusted script. Optimizely says a signup flaw let the attacker impersonate users and add malicious JavaScript to customer projects. The malicious JavaScript "swapped cryptocurrency wallet addresses for the attacker's, skimmed payment cards, stole cookies and screenshots" and delivered two iOS exploit kits, Coruna and DarkSword, to vulnerable iPhones and iPads. In other words, attackers pwned the page your users trusted with their data. Perhaps I'm being repetitive, but you should NOT be trusting third-party scripts.

**Optimizely is not uniquely at fault.**

Their approach mirrors that of most vendors offering third-party code. Optimizely's earlier CSP guide pushed 'unsafe-eval' in script-src for audience targeting with custom JavaScript conditions, letting scripts execute strings as code. These vendors make it practically impossible for you to track and review every change before the JavaScript reaches your users. How would you even know the code changed? Report URI can flag a change at a trusted URL when browsers send script hashes to its CSP reporting endpoint. That gives you, the site owner, some warning.

**What to do with your newfound knowledge?**

First, recognize how prevalent third-party code is. My signed-in LinkedIn feed referenced 59 distinct external script URLs and contained three inline scripts. LinkedIn hosted 57 of those URLs, including Tealium's tag manager and six tag files. Seven outside vendors showed up across the scripts, frames, and tracking requests. You probably know Google and Adobe. Others are well known only to insiders. That's a lot of opportunity for mischief when outsiders who don't share your risk tolerance get to decide what's OK.

Second, if you have a website and you care about your users, you must be enforcing a Content Security Policy. A CSP lets you limit where the browser gets scripts, which scripts it runs, and where the page can send data. Report URI found 188 infected snippets across 178 organizations, including the BBC, CNN, and Zoom. Its CSP table covered 159 organizations, and 68 of them (43%) had no CSP at all. But what of the 91 organizations (57%) that did have a CSP? Were they saved? Well, 50 of those policies let both the payload and the data theft through. But there's hope.

![How CSP limited the Optimizely Malware Attack (data via Report URI)]({{ "/assets/images/LI-They-Opened-the-Gate-Malicious-JavaScript-Rode-In/figure-01.png" | relative_url }})

*How CSP limited the Optimizely Malware Attack (data via Report URI)*

A restrictive script-src directive can stop the external payload from downloading and keep the embedded fallback from running. The trusted snippet could pass that trust to a script it loaded under 'strict-dynamic', and 'unsafe-eval' could let the fallback run. Report URI counted 24 organizations that blocked the payload outright (15% of the 159). Another 17 let it run, but connect-src blocked the page from sending card details, cookies, and screenshots to the attacker's server. The wallet address swap could still work on those pages because changing the address a user saw or copied didn't require an outbound connection. If a user sent crypto to that substituted address from their own wallet, the attacker got the payment. In this case, the directive was a partial mitigation. Report URI didn't name all 24 protected organizations, but congratulations and thank you to those teams!

**What NOT to do?**

Whatever you do, don't let third-party providers talk you into running their code in the context of your users' most sensitive data. Google's reCAPTCHA Enterprise was the only vendor-hosted JavaScript I found referenced in LinkedIn's same-origin preload frame. A script running there can read or change the feed content already loaded on the page. LinkedIn is probably reasoning, "If Google can't be trusted, nobody can."

Most egregious, IMO, are audience and ad trackers. Most often they insist, "We can't accurately identify your user's behavior without tracking every movement and nuance in the browser. You'll lose revenue." Product managers, rightfully intent on making their numbers and keeping their jobs, push hard to accept the risk. They have a point when they say, "Everybody is doing it."

**Pssst, hey USER!**

Now, I want to address users of websites rather than operators.

*Dear user,*

*Website owners prioritize their interests and then yours. This drive-by attack lets thieves steal the card number you typed at checkout without ever touching the company's customer database. They could even change the wallet address you copied for a crypto payment. They could steal your logons, read your email, and see your photos.*

*The website owner chose which scripts to trust. You could spend months cleaning up after that choice.*

*All the best, Me*

That's the last and most important point. Should we be happy to live in a world where "everybody is doing it"? Why should well-meaning website operators who do right by their users have to compete with bottom-of-the-barrel organizations that don't care enough to do the same? Should we require websites to limit the personal data they process by default to what's necessary for each purpose, as Article 25 of the EU's GDPR requires? Should we raise our expectations regarding security, privacy, and data ownership overall? Smart people wonder. Smart people like Bruce Schneier. His November 20 Guardian column calls for changing the incentives that let companies profit from systems that barely work and "push the costs of failure on to all of us."

Until those incentives change, users have good reason to block ads and trackers.

**You decide.**

**References:**

[HTTP Archive, 2019 Web Almanac, "Third Parties" (JavaScript requests and bytes).](https://almanac.httparchive.org/en/2019/third-parties#byte-weight)

[HTTP Archive, 2024 Web Almanac, "JavaScript" (first-party and third-party mobile medians).](https://almanac.httparchive.org/en/2024/javascript#first-party-versus-third-party-javascript)

[Bruce Schneier, The Guardian, "Don't blame cyber-attacks for recent outages. The real villain is the US economy" (November 20, 2026).](https://www.theguardian.com/commentisfree/2026/nov/20/cyber-attacks-outages-blame-economy)

[Scott Helme, Report URI, "World's Largest Brands Infected With Malware Via Optimizely" (November 16, 2026).](https://blog.report-uri.com/worlds-largest-brands-infected-with-malware-via-optimizely/)

[Optimizely, "Security Advisory: Web Experimentation Security Incident" (updated November 19, 2026).](https://support.optimizely.com/hc/en-us/articles/50521849710605-Security-Advisory-Web-Experimentation-Security-Incident-Updated-November-19-2026)

[Mark Stott, "Lessons From the Optimizely Web Experimentation Compromise" (November 17, 2026), on the earlier 'unsafe-eval' guidance.](https://world.optimizely.com/blogs/mark-stott/dates/2026/11/lessons-from-the-optimizely-web-experimentation-compromise/)

[Optimizely, "Update your site's Content Security Policies (CSP)" (current Web Experimentation guide).](https://docs.optimizely.com/web-experimentation/docs/update-your-site-s-content-security-policies-csp)

[Report URI, "Script Watch" (script fingerprints and change alerts).](https://docs.report-uri.com/setup/script-watch/)

Author's signed-in LinkedIn For You feed capture and JavaScript inventory, November 19, 2026.

[European Union, General Data Protection Regulation, Article 25(2), on data protection by default.](https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?from=EN&uri=CELEX%3A32016R0679#page=48)

#ThirdPartyRisk #SoftwareSupplyChainSecurity #WebSecurity #JavaScript #DataPrivacy
