---
layout: post
title: "Choose Collective Code Ownership"
published: true
excerpt: "Strong Code ownership, or development silos, is often seen as a good practice. How come it's also one of the most counterproductive project management techniques in an agile team?"
image: /images/Ralls_Texas_Grain_Silos_2010.jpg
popular: true
---

<a title="Silos by Leaflet (Own work) [CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ARalls_Texas_Grain_Silos_2010.jpg"><img src="/images/Ralls_Texas_Grain_Silos_2010.jpg" class="postImage"/></a>

Most developers "own" portions of the applications they work on. Also known as "Strong Code Ownership", or simply "Code Ownership", this is often seen as a good practice. How come it's also one of the most counterproductive project management techniques in an agile team?

## Code Ownership Makes Sense

For a new music player project, a company gathers a team of 3 web developers:

* Alice excels at frontend development, HTML5 and MV* frameworks
* Bob understands the project domain perfectly and knows all about RESTful / HATEOAS
* Charles is very good with complex algorithms, optimization, and system administration. 

For the first sprint, three user stories sit on top of the backlog:

<ol>
<li>Display a player GUI with playback controls</li>
<li>List songs available for playback from the server</li>
<li>Display the top 10 songs of the week</li>
</ol>

The optimal choice is pretty obvious:

* Alice should work on the complex playback UI components (#1)
* Bob should work on exposing a Songs JSON API and consuming it in the app (#2)
* Charles should work on storing playback metadata in a NoSQL database, aggregating top 10 statistics, and displaying it in the app (#3)

So far, so good. For the following sprint, the product owner prioritizes three new user stories:

<ol start="4">
<li>Allow to arrange several songs into a playlist</li>
<li>Display artist name when playing a song</li>
<li>Display recommendations based on similar artists</li>
</ol>

From a skills and experience point of view, it makes perfect sense to let each developer work on what they already know the best.

* Alice should keep on working mostly on the UI and add playlist management (#4)
* Bob should keep on working mostly on the backend API and add an Artist JSON API (#5)
* Charles should keep on working mostly on the BigData engine and build a basic recommendation engine (#6)

Consequently, each team member starts developing a strong sense of ownership on certain portions of the code. This will undoubtedly lead to a better productivity, right?

<a title="Silos by SimonP (Own work) [CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0) or GFDL (http://www.gnu.org/copyleft/fdl.html)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AVictory_Silos.JPG"><img alt="Victory Silos" src="//upload.wikimedia.org/wikipedia/commons/thumb/2/27/Victory_Silos.JPG/512px-Victory_Silos.JPG"/></a>

## Code Ownership Prevents Business-Driven Priority

After a careful review of Key Performance Indicators, the product owner decides to prioritize the three following stories for the third sprint:

<ol start="7">
<li>Display album art during song playback</li>
<li>Display lyrics during song playback </li>
<li>Display song metadata (year, genre, # of playbacks) during song playback</li>
</ol>

Alice can work on the UI controls of all three user stories. Bob can also develop the API for all three new models. As for Charles, he never worked either on the frontend app or on the API, so he can't really develop any of the stories.

Even though these user stories bring the most business value at that point of the project, the development team is already too specialized to develop them in this order. This forces the product owner to adjust priorities and push a nice to have feature instead of a must have feature.

## Code Ownership Reduces Velocity

So the product owner rearranges the backlog, and proposes the following instead:

<ol start="7">
<li>Add album art during song playback</li>
<li>Add lyrics during song playback </li>
<li>Display the top 100 songs of all time</li>
</ol>

Now Charles has an obvious choice: he'll work on the playback data aggregation for the top 100 (#9). As for Alice and Bob, they will work together on the album art and lyrics stories (#7 and #8), Alice in the frontend part, and Bob in the backend part.

When she starts the album art GUI, Alice is blocked because the corresponding API is not yet ready. She can't switch to the lyrics GUI either, because Bob works on both APIs. So Alice ends up redeveloping part of the Album Art API logic inside the frontend application.

At the end of the sprint, neither story 7 or story 8 are finished. Bob and Alice couldn't handle a single user story on their own, and their dependence on each other's work slowed down the overall development.

## Code Ownership Puts the Schedule At Risk

<div style="width:256px;float:right;margin: 10px 0 10px 10px"><a title="Silos by Dwight Burdette (Own work) [CC-BY-3.0 (http://creativecommons.org/licenses/by/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AHarvestore_Silos_Britton_Michigan.JPG"><img style="vertical-align: text-top" width="256" alt="Harvestore Silos Britton Michigan" src="//upload.wikimedia.org/wikipedia/commons/thumb/b/b7/Harvestore_Silos_Britton_Michigan.JPG/256px-Harvestore_Silos_Britton_Michigan.JPG"/></a></div>

For the following sprint, an unpleasant event happens: Alice catches the flu. She's seriously sick, and she's also seriously contagious. Her doctor puts her on medical leave for two weeks.

Unfortunately, the product owner had prioritized user stories with a GUI part. So Bob and Charles end up looking at the frontend code for the first time. It takes them a few days to understand how Alice organized her code. They don't understand it all (because they didn't follow Alice's work before), but with a few copy and paste they manage to somehow implement the frontend features - in twice the time it would take Alice to do it.

Had they worked on that part of the code before, Bob and Charles would be able to handle frontend development tasks much faster, and meet the product owner expectations on schedule.

## Code Ownership Reduces Quality

When Alice comes back, Bob goes on holidays. After all, it's Christmas time, and Bob has been working for the company long enough to take a well-deserved two weeks holidays. He flies to the French Alps for a joyful skiing session.

This time, the product owner decides to push a user story concerning genres. This obviously requires an update to the JSON API, so Alice and Charles dive in Bob's code. They soon realize that Bob forgot to document some methods, and left certain use cases untested. Since nobody ever reviewed his code before (after all, he's the API expert), nobody realized that he also took dreadful shortcuts.

Charles could have given Bob advice if he had reviewed his code from the beginning. But it's already too late. At that point, it is clear that strong code ownership has lead to an increase in technical debt.

## Code Ownership Prevents Mutual Assistance

<div style="width:256px;float:left;margin: 10px 10px 10px 0"><a title="Silos by Jordi Boggiano, courtesy of the author" href="https://twitter.com/seldaek/status/439315419065618433"><img style="width:256px" src="/images/jordi_silo.jpg"/></a></div>

Bob comes back from holidays with a nice tan. He's surprised that his colleagues feel much less relaxed than him.

The team is complete again, and the product owner decides that it's time for the first deployment to production. The first real users discover new bugs that weeks of Q&A never revealed. The backlog quickly fills up with urgent issues. 

Alice, Bob and Charles review the issues and try to determine who's responsible for each bug. More often than not, nobody feels entirely responsible for a given bug - maybe because the bug results from an edge case of the communication between the frontend and the backend, or because it's triggered by the analytics script, which is neither frontend, or backend, or Big data.

The product owner gets nervous about some bugs not being resolved. He asks again the team to collectively fix them quickly. Alice thinks Bob and Charles should fix them - it's not her domain. She doesn't understand why they don't volunteer, and she despises them for not helping the product owner. She takes the initiative to fix a bug with implications all around the codebase. At one point, Charles asks Alice to stop breaking his code.

After an entire sprint dedicated to fixing bugs, the mood of the team is quite dark. Each developer feels abandoned by the others, and is determined to stop helping them in the future. Collaboration is dead - if it ever existed.

The rest of this project story doesn't need to be told. Suffice to say that it ends badly.

## The Solution: Collective Code Ownership

This project went wrong right at the beginning of sprint 2. Alice should have worked on story #5, Bob on story #6, and Charles on #4. Or another rotation. But they should have gained in expertise on another part of the application instead of increasing the fences around their own code. 

This is called "Collective Code Ownership", and it's simple to put in place:

* Encourage rotation of developers on all components and features so that they all know the entire application
* Enforce systematic peer review (code written for other eyes is always more maintainable that code written just for an interpreter)
* Unit test a lot to avoid accidental code breaks
* Schedule regular meetings to share the domain design and expertise among the entire team
* Don't hire over-specialized developers ("frontend devs" and "backend devs" already makes 2 silos)
* Prompt developers to challenge each other
* If it still doesn't work, consider pair programming

If it's impossible to promote collective code ownership because the application is too big, or because the technologies are too far from each other (for instance, a native iOS app interacting with a Clojure API), there are solutions, too. Break the team into smaller teams, dedicated to sub-apps; forbid strong code ownership in a single team.

And if you think that it's a waste of time to ask a frontend dev to learn backend techniques (or vice-versa), we don't see the job of web developer the same way. Learning a new language or framework will always make developers more productive *in general*, including in their language of choice. 

## Conclusion

In an agile context, the drawbacks of strong code ownership outweigh the benefits. This is a controversial point of view (see [other](http://swreflections.blogspot.fr/2013/04/code-ownership-who-should-own-code.html) [opinions](http://c2.com/cgi/wiki?CodeOwnership) on the matter), but my experience leads me to think that Collective Code Ownership is the solution. Every developer should feel responsible for the entire application developed by their team. The entire team should be proud of the work accomplished. It makes the developers, and the product owner, happy in the long run.
