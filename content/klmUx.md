+++
title = "KLM UX or how to be terrible at user experience"
description = "How terrible KLM user experience is"
date = 2021-02-26
draft = false
+++

Recently I've been trying to check in via web to my Zagreb - Dublin flight. For some reason, I didn't get the usual mail which reminds you about it. I've logged in to KLM web, still nowhere to check in. Couldn't find an explanation either. Finally, I've downloaded KLM app, added my flight and saw a warning - _If traveling via Netherlands, you need to bring negative PCR test_

The thing was, I did check the restrictions on Irish government page and  KLM's [traveldoc](https://klm.traveldoc.aero/) page.My first thought was - _Was the restriction added in last few days?_. Turns out it was added 2 weeks before. Then how did I miss it? Is there and error on [traveldoc](https://klm.traveldoc.aero/)?

So I went to the page and the moment I saw it, I realized what happened.

![Klm](/images/klm_traveldoc.png)

I've used the one-way tab, when I should have used the transit one. My first thought was: how did I miss that, am I blind? My second thought was: Can this design be any worse?

I'm not a UI or UX person, I've read one [book](https://mitpress.mit.edu/books/design-everyday-things) on the subject and that's it. I'm don't claim any sort of expertise. Yet I had several ideas of how to improve this immediately:
1. Using precise language.
2. Short description below the tab.
3. Using flight number as input rather than city starting point of departure/destination.
4. Warning

#### Using precise language

_Return_ flight or _one-way_ flight can be both direct flight or layover flight. Other than _"Transit"_ Tab there's nothing to suggest that _one-way_ flight doesn't include layover flights.
If tabs were simple _Direct return_ and _Direct one-way_ it would be obvious there is a different tab for transit tabs.

#### Short description below the tab

Simple clarifying description like "Enter your direct flight" would prevent any confusion.

#### Using flight number as input 

Flight numbers are per direct flight. So if you have a connection you'll have flight number for each flight. Using flight number as input would immediately show you there's only one place to input it while you have multiple numbers. Seeing something doesn't fit would make you look around the page to see if you missed something. And then you would notice the inconspicuous _Transit_ tab.

#### Warning 

Adding a warning shouldn't be too hard either. They could have add a bar on the top of the page, or a popover when choosing selection, or a short text below _Your trip_ heading. And considering KLM is Dutch company, I suspect they don't have too many flights that aren't under Dutch laws. So warning would be useful for almost all users.

After all, they found it appropriate to add it to their mobile app:

![Klm Mobile](/images/klm_mobile.png)


#### Bad design or a purposeful design

Arthur C. Clarke coined Grey's law: _Any sufficiently advanced incompetence is indistinguishable from malice._ Website with terrible UX, not providing something as basic as e-mail for reaching out to support, not replying to phone calls or replying on what's app every 2 to 4 days... I know how incompetent we can be, but it's hard to believe any company can be as incompetent as KLM. 
