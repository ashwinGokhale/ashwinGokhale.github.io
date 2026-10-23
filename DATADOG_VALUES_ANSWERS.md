# Datadog Values interview answers

Senior Software Engineer, Backend. 45 minutes of behavioral questions.

Anything in [square brackets] is a made-up placeholder. Replace it with what actually happened, or cut it.

Datadog's values are owner, excellence, pragmatic, honest, humble, enthusiastic, and friendly. Don't name them. Show them through what you did.

Story answers use STARL (Situation, Task, Action, Result, Learning), the career story uses CARL (Context, Action, Result, Learning), and each answer runs 2 to 3 minutes at most. Stop there and let them dig in. End with what you learned and what you did differently afterward. Every learning from both interviews is listed at the end.

## 1. Career story

Recruiter's question: _work history and motivations. career to date. can you tell me a high level story_

**Headline:** Backend internships at Object Edge and Bloomberg, then 6+ years at Microsoft, growing from our platform's first React app to owning the shared platform 100+ engineers ship on. Took releases from once a week to ten a day.

> **C - Context:** My career has been about building things other engineers depend on. I started with backend internships at Object Edge and Bloomberg, where I built a service that handled 75,000 requests a second. At Microsoft, I joined the team behind the company's incident-management product and built the first React app on our new web platform. It became the base for all 16 apps we run today.
>
> **A - Action:** From there, my scope grew into the shared pieces other engineers need: the shared repo, deployments, telemetry, and backend services. I built our team's first ASP.NET Core service and rewrote the shared code it needed, and ten more services later reused that code. In the shared repo, I cut the build from 120 minutes to 25. I built a pipeline that turns about 200,000 Kafka events an hour into 50,000 postmortem updates a day. And I led the release system that lets our web app ship separately from the backend.
>
> **R - Result:** Today I own the platform that more than 100 engineers build on. The release system took us from one release a week to about ten a day across 16 apps and 12 clouds, and I run it in production.
>
> **L - Learning:** The biggest thing I learned is that a good idea doesn't spread just because it's right. People follow what they can see working, so before I ask a team to change how they work, I build a prototype and make the new way easy to follow. Next, I want to build backend systems that engineers depend on at a scale where the load keeps growing, and that's why I'm talking to Datadog.

## 2. Why Datadog

Recruiter's question: _why are you interested in datadog? be more specific and talk about what datadog is actually working on._

> **My point:** I want to work at Datadog because it's the business I already work in, but customer facing and at orders of magnitude more scale.
>
> **Evidence:** Datadog's customers are engineers, and so are mine. Every team at Microsoft uses our incident-management tool when something breaks, so I know what engineers need in the middle of an incident. I also run our release system in production, and I've traced a production incident on it through the server logs. But our tool is internal. It serves one company.
>
> **Why Datadog:** Datadog builds for outside customers, and every new customer sends more data. The backend has to keep up with that load and still stay fast for engineers debugging an outage. Datadog also has observability and incident management in one product suite, with incidents next to the metrics, traces, and logs engineers use to find what went wrong. Most companies in this space own only part of that. So I'd bring domain knowledge on day one, and I'd work on much bigger systems than mine.

## 3. What you want to learn

Recruiter's question: _what things are you looking to learn and how do you want to grow and how will datadog do that for you?_

> **My point:** I want to learn how to design backend systems for load that grows with every new customer, and I want to grow into leading technical decisions across several teams.
>
> **Evidence:** My current system serves one company, so its load doesn't keep climbing. We already have a version of the hard part: one large customer can create a noisy-neighbor problem, where their load slows down everyone else. And today I set technical direction for a platform that more than 100 engineers and partner teams in four organizations build on.
>
> **Why Datadog:** At Datadog, every new customer sends more data, so noisy neighbors and cost show up across many customers at orders of magnitude more scale. I want to get good at those problems. I also want to make the calls that several teams build around, on systems much bigger than mine. In a year, I'd like to [have led a design that changed how a system handles growth or cost, and be someone other teams pull into their design reviews].

## 4. Ownership and scope

Recruiter's question: _ownership. talk them through your recent scope of your responsibilities. what systems do you own? are you mentoring or coaching junior engineers? what do you do outside of your immediate team. how do you prioritize tasks, plan, etc._

**Headline:** Own the shared repo, build pipeline, and release system for 100+ engineers, plus backend pipelines for incident data. Mentored 15 engineers. Plan by milestones with outside dependencies named at kickoff.

> I own the platform more than 100 engineers build on: the shared repo, its build pipeline, and our web app's release system. I cut the build from 120 minutes to 25, and I run releases and rollbacks across 16 apps and 12 clouds. [I'm on its on-call rotation and run the weekly on-call handoff.] I also own a backend pipeline that turns 200,000 Kafka events an hour into 50,000 postmortem updates a day, fixing incident metrics like time to mitigate. Outside my team, a colleague and I built a plugin model so four partner organizations ship six plugins on their own, and onboarding dropped from three weeks to one hour. And I've mentored 15 engineers through our move to React.
>
> When work competes, whatever is blocking users or other teams goes first. [If the shared build breaks for 100 engineers, that beats my own project that day.] Here's how I plan, and where I learned it.
>
> **S - Situation:** Our release system depended on another team. The SRE team, which runs our servers, was supposed to build its non-Azure side.
>
> **T - Task:** I led the project, so their part was still my delivery risk, even though I didn't control their staffing.
>
> **A - Action:** I ran weekly, then daily check-ins with their engineer, who sometimes went weeks without responding. I set up a group chat with both managers and my skip manager, so the escalation and status were on record. Then their engineer left, the replacement was pulled away after about a month, and SRE withdrew. So I built the non-Azure side myself.
>
> **R - Result:** It shipped, and releases went from once a week to about ten a day. But we were months late.
>
> **L - Learning:** I own the outcome even when part of the work belongs to another team, and escalating gets attention, not people. So I treat other teams' work as the biggest risk in a plan. I name it at kickoff, track it by milestone, and when it slips, I bring the managers a decision: more people, less scope, a later date, or I take it over. At Datadog, where many teams own parts of the same product, that's how I'd run cross-team work.

## 5. Owning the full lifecycle

Recruiter's question: _what role did you have in the full software development lifecycle? (ex. you identified an issue, you proposed it, and implemented it)_

**Headline:** Started our team's move to .NET by proposing and building its first ASP.NET Core service, for postmortems. Ran the design working group and rewrote the shared libraries, including auth. The service grew to 60K requests a day, and ten more services moved over on that shared code.

> **S - Situation:** I proposed splitting postmortems out of our incident system into their own service, and I built it as our team's first ASP.NET Core service. The two workflows were tangled together in one system. We wanted postmortems to change on their own schedule without breaking incident behavior users relied on.
>
> **T - Task:** I owned it from proposal to production, and I was the first on the team to move to the new stack.
>
> **A - Action:** [We considered changing the existing system in place, but every postmortem change would still have shipped with the whole incident system.] The hard part was agreeing on where an incident ends and a postmortem begins. I ran a weekly working group with [product managers and the teams that write postmortems] to settle that, and I changed the design as we answered questions. [For example, what happens if an incident changes after its postmortem has started? We walked through real cases and agreed that incident details can update, but never overwrite the team's written analysis. That gave us a rule we could build and test.] Going first also meant our shared code didn't work on the new stack, starting with our auth library. I rewrote it, along with our other shared libraries, so later services could reuse them.
>
> **R - Result:** We shipped the first APIs to production. The service grew to 60K requests a day, and ten more services later moved to .NET on the shared code I wrote, including that auth library.
>
> **L - Learning:** Real examples settle design questions faster than debate. Arguing about behavior in the abstract went in circles. [Now I start design discussions from real scenarios and turn the answers into rules we can build and test.] With as many kinds of customers as Datadog has, I'd ground design questions in real customer cases.

**Backup if they want a cross-team delivery story:**

**Headline:** Took an AI Copilot's portal integration to private preview in two months with no reported regressions, leading two junior engineers and coordinating six teams in four organizations. The product later reached 18K monthly users.

> **S - Situation:** I led the portal side of an AI Copilot integration. Its side panel showed up on every page, across modern and legacy frameworks, so it changed the layout of pages owned by six teams in four organizations.
>
> **T - Task:** I owned the portal integration, not the model or the backend.
>
> **A - Action:** I gathered requirements, scoped the work, and wrote the design. I reused the Fluent AI components instead of building our own, so our time went into the integration, and I built the bot-framework piece they were missing. I wrote most of the integration code and led two junior engineers. I worked closely with a junior engineer who was new to React. She ended up building [a real piece of the integration], and later that year she was helping new engineers on her team get started. I coordinated page owners on all six teams to check their pages and fix layout problems, with biweekly scrums and weekly stakeholder updates and demos.
>
> **R - Result:** We were ready for private preview in two months with no reported regressions. The product later reached 18,000 monthly users.
>
> **L - Learning:** [Reusing someone's work saves time, but it doesn't move the responsibility. I still owned how the panel changed every page, so now I bring the owners of affected areas in to test early.]

## 6. A technical decision you got wrong

Recruiter's question: _did you make a technical decision that you later realized wasn't correct or could have made a better one. how did that impact your decision making later and how did you grow from it? what action did you take to correct it moving forward?_

**Headline:** Designed a fallback folder that every release overwrote while users could be loading from it. I replaced it with routing to exact versions, kept the partner URL working, and led a redesign where uploading a build never changes what users see.

> **S - Situation:** I designed an emergency fallback folder for our release system, and it broke the safety rule the system was supposed to follow. When we first separated our web app's releases from the backend, every build went into its own version folder. I also added one fixed "last known good" folder as a fallback. I didn't mean for anyone to depend on it, but it was the only way to tell which version was live, and partner teams started using it as a stable URL.
>
> **T - Task:** It was my design, so fixing it without breaking partners was on me.
>
> **A - Action:** It came up after a production incident with a different cause. I traced that one through the IIS logs to a duplicate routing rule in a config file and removed it. In the review afterward, we agreed on a rule: uploading a build should never change what users see. My fallback folder broke that rule, because every release copied the new build over it, even while users could be loading from it. I could have asked partners to switch to a new URL, but they depended on that one. So I changed the server's routing to point that URL at an exact version instead of a copied folder. Then I led a redesign that goes further. Normal pages won't use that URL at all, because each page gets its exact versions when it loads. The old URL stays only for older integrations until they move.
>
> **R - Result:** Partners didn't have to change anything, and automated tests cover the routing. [The redesign is built and tested, and PPE is next.]
>
> **L - Learning:** Anything other teams can see, they'll build on, whether I meant to offer it or not. I added that folder as a backup and never asked who else would use it, so it became a promise I had to keep. In the redesign, I gave partners a supported way to see what's live, [and now I decide up front what I'm willing to support before I expose anything]. At Datadog, customers build on every API and behavior they can reach, so I'd treat anything visible as a promise.

**Backup if they ask for another decision you got wrong:**

**Headline:** Designed our shell to fetch its app version list after loading, which let an old shell load new app code during a rollout. Moved the version list into the shell's HTML so every page gets matching versions, removing a network request and a file on disk, and making first load 5% faster.

> **S - Situation:** I designed our web app's shell, the main page that loads every app, to fetch a separate version file after it loaded. That let mismatched code run together.
>
> **T - Task:** It was my design, so the fix was mine.
>
> **A - Action:** During a deployment, we roll out one ring of servers at a time, starting with canary. A user could get the shell from ring 3, which still had the old version, while the app code came from the canary ring, which had the new one. An old shell running new app code could fail at runtime. So in the redesign, I dropped the separate fetch and had the server embed the version list in the head of the shell's HTML. Now whichever ring serves the shell also sends the app versions that go with it. If a user's first request lands on ring 3, they get ring 3's app versions too.
>
> **R - Result:** Each page gets app versions that match its shell. First load got 5% faster, with no extra request and no version file on disk to maintain. [The redesign is built and tested, and PPE is next.]
>
> **L - Learning:** When two parts have to match, the riskiest moment is the middle of a rollout, when old and new run side by side. I'd designed for before and after, not the in-between. [Now I check what a user gets halfway through a rollout before I ship a change like that.] At Datadog's scale, rollouts take longer and reach more customers, so that in-between state is where I'd look first.

**If you use this story in the Experience round, use this one instead:**

**Headline:** Rolled out large shared-repo changes without enough notice and cost other engineers time. Proposed a process for large shared changes: merge windows, environment updates coordinated ahead of time, and batching.

> **S - Situation:** In 2023, I rolled out a set of large changes to our shared repo without enough notice, and it cost other engineers time while they were trying to ship.
>
> **T - Task:** The changes were mine, so the disruption was mine to fix, along with how the next big change would land.
>
> **A - Action:** [It was a dependency upgrade.] The code was fine, but people had to fix their local setups by hand. [I helped them fix it and wrote down the steps.] My manager pushed me to give more notice and write better docs, and that was the right call. So I proposed a process for large shared changes: scheduled merge windows, environment updates coordinated ahead of time, and changes batched together.
>
> **R - Result:** [On the next upgrade, I picked a merge window, sent the steps ahead of time, and had someone outside my team try them first. It needed much less hands-on help.]
>
> **L - Learning:** A change to something others depend on isn't done when it works for me. It's done when the people using it can pick it up without losing a day. At Datadog, platform changes reach many teams, so I'd plan how people adopt a change as carefully as the change itself.

## 7. Prioritization and influence

Recruiter's question: _prioritization. tell them about a time when they have to prioritize certain things over another. influencing in your team. how did you influence your teams technical roadmap. when did you proactively advocate for a solution to a problem_

**Headline:** Led two junior engineers to show engagement metrics inside the app for a framework 40+ Azure products use. Decided what made the first version, in what order, and who built each piece. Shipped the MVP on time, and it's now used daily by 1K+ engineers, PMs, designers, and Microsoft's C-suite.

> **S - Situation:** I own a shared framework that more than 40 Azure products use to measure how people use their pages. [The data was there, but to see it, a team had to write its own queries in a separate tool.] I led a project to show those numbers right inside the app, next to the part of the page they measure. I had two junior engineers and a tight deadline.
>
> **T - Task:** There was far more we wanted to build than we could finish by the deadline. I owned deciding what made the first version, in what order, and who built each piece.
>
> **A - Action:** I started from the question users most needed answered: is anyone using this part of the page, and is it working? [So the first version was the overlay that marks each measured section, plus a panel with usage, time on screen, and success and failure rates. Trends, tag filters, and the breakdown by leadership org could wait.] [Reading the data straight from the browser, with sign-in and permissions, was the riskiest piece, and everything depended on it. So I took it first myself.] I gave each engineer whole features to own, [like separate cards in the panel], instead of fragments of mine.
>
> I made one call I'd change. I put their growth ahead of the deadline and gave them a lot of room, and the first milestone got hard to hit. [So I broke the remaining work into smaller pieces with check-ins every few days,] and we got back on track.
>
> **R - Result:** We shipped the MVP on time. [Trends, tag filters, and the leadership breakdown came after.] Today it's used daily by more than 1,000 engineers, PMs, and designers, and by Microsoft's C-suite.
>
> **L - Learning:** Prioritizing is mostly deciding what not to build yet. I start from the question users most need answered and build the smallest version that answers it, [with the riskiest piece first so surprises show up early]. I also learned that growing people has to fit inside a commitment, not compete with it. At Datadog, I'd plan the same way: answer the customer's main question first, and put stretch work where there's slack.

**If they ask how you influenced the team's roadmap or advocated for a solution:**

**Headline:** Bet early on module federation, prototyped it on my own, and made it the team's way to move off AngularJS. My migration standards spread from 4 teams to 9, and it became the foundation for rebuilding our most used page, where load time fell from 6 seconds to 1.5 and monthly satisfaction rose from 3.62 to 4.10 out of 5.

> **S - Situation:** Our AngularJS portal loaded some components in iframes, which were slow and got slower with each one we added. The team needed a faster way to bring React in.
>
> **T - Task:** Nobody assigned this to me. I'd found a better approach and wanted to prove it before asking anyone to change.
>
> **A - Action:** I found module federation while it was still new. It lets a page load code from another app at runtime, so a React component can sit directly inside an AngularJS page. My manager trusted me to try it, so I rewrote one iframed component in React and loaded it straight into the AngularJS page. I demoed it to the team and built a standard path for others to move their components the same way.
>
> **R - Result:** It was much faster than iframes, kept up as we added more, and became the team's plan. My migration standards spread from four teams to nine. It also became the foundation for rebuilding our incident details page, about 65,000 daily users, where I led five engineers. Once the last workflows moved to React, load time dropped from six seconds to 1.5, and monthly satisfaction went from 3.62 to 4.10 out of 5.
>
> **L - Learning:** People follow what they can see working. A small, real prototype changed the team's direction faster than any argument could have. At Datadog, I'd make the case for a new approach the same way: build a small working version, show it, and make it easy to copy.

## 8. Disagreement with a coworker

Recruiter's question: _tell me about a time you disagreed with your coworkers._

**Headline:** Disagreed with a coworker about adding FAST to a shared framework used by 40+ teams. We presented both cases to our managers, who decided not to expand FAST. We kept what already depended on it instead of paying for a rewrite, and he later joined my team.

> **S - Situation:** I disagreed with a coworker who wanted to build shared UI components in Microsoft FAST for Elixir, the framework more than 40 Azure product teams use. He had a real point. [Our product mixed several frameworks, and a FAST component could work in all of them without being written more than once.]
>
> **T - Task:** My concern was the cost for everyone else, and I needed to make that cost clear without brushing off his point.
>
> **A - Action:** I told him directly why I disagreed. Our stack was already fragmented, few people had deep frontend experience, and FAST would give every Elixir team another way to write, test, and maintain components. The Elixir team declined the proposal, but FAST components kept landing in our own product, and we kept going back and forth on whether to add more. [So we agreed to ask for a decision.] We each presented our case to both our managers and my skip manager, and they decided not to expand FAST. That didn't mean ripping out what was there. Our navigation and our service and team pickers depended on those components, and rewriting them would have cost too much. So we kept them and stopped adding new ones.
>
> **R - Result:** We got a clear decision, with no costly rewrite of features people relied on. He later joined my team, and [I've reviewed and helped fix the FAST components we kept].
>
> **L - Learning:** Adding something and replacing it are different decisions. "Would I add this today?" and "Should I replace what people already depend on?" have different answers. [Now I push for a clear decision early, because every change that lands makes the choice harder to undo.]

**If they ask about pushing back on leadership:**

**Headline:** Tested leadership's proposal to move our portal onto the Azure Portal framework. First page load went from 1 second to 9, and it couldn't keep working during an Azure outage. Recommended against it and built a decision tree for our org and three partner orgs.

> **S - Situation:** Senior leadership asked me to evaluate moving our whole portal onto the Azure Portal framework. [They were leaning toward it because it would cut what our team had to maintain.]
>
> **T - Task:** I owned the evaluation and the recommendation.
>
> **A - Action:** I gave their option a fair test. It had real strengths. It came with deployment and monitoring built in, and it had a dedicated team of about 60. Our current framework had five part-time maintainers. Then I tested it with our pages. In the setup we evaluated, our first page load went from about one second to nine. It also couldn't keep working during an Azure outage, and that's exactly when incident responders need our tool. Asking the Portal team to build that support would have been too much work to justify the move, so I recommended against it. [I wrote up the numbers and walked leadership through them in a review.] I didn't want the answer to just be no, so I built a decision tree that our org and three partner orgs could use to tell when the framework is a good fit.
>
> **R - Result:** [Leadership agreed, and we stayed on our framework.]
>
> **L - Learning:** When I push back on leadership, I give their option a fair test and show the cost in terms users feel. One second versus nine was much harder to argue with than my opinion.

## 9. Working across many teams

Recruiter's question: _time when you had to collaborate with a lot of different teams. what were some of the challenges, how did you overcome them_

**Headline:** Moved 418 end-to-end tests from Cypress to Playwright across 11 apps, five teams, and three organizations within the milestone. Tests ran about seven times faster, saving about eight build hours a day and two weeks of manual accessibility audits a quarter.

> **S - Situation:** I led moving 418 end-to-end tests from Cypress to Playwright, across 11 apps owned by five teams in three organizations. We wanted faster tests, automatic accessibility checks, and one consistent test setup.
>
> **T - Task:** I needed five teams to do work I couldn't assign.
>
> **A - Action:** I made that harder than it needed to be. I brought up the migration after milestone planning, when the other teams had already committed their time. Since I didn't manage those teams, a good technical case wasn't enough. I focused on making the work easier for them to take on. I met with each team about their apps. I wrote a detailed migration guide so every team followed the same steps. And instead of only asking them to migrate, I did some of the migration and code reviews myself.
>
> **R - Result:** We finished within the milestone. Tests ran about seven times faster, which saved about eight hours of build time a day across PRs. The automated accessibility checks replaced about two weeks of manual audits a quarter, and everyone moved to one test setup.
>
> **L - Learning:** Even a clearly good change costs other teams time, and they plan that time in advance. [Now I get cross-team work into other teams' plans before planning closes.] And I make it cheap to do with guides and hands-on help, because that's what made this one workable.

## 10. Mentoring

Recruiter's question: _mentoring and coaching. tell them about a positive experience and what worked. learning and growth and concerned with having your colleagues grow. you helped someone overcome a challenge they had. what challenges did you have and how did you overcome them. you give them the tools instead of doing it for them._

**Headline:** Coached my most recent mentee, an engineer who kept getting blocked, with one-on-one training and direct feedback on every PR. She roughly doubled her development speed and shipped three features in two months. Applied what I learned from giving two juniors too much room on a tight telemetry deadline.

> **S - Situation:** The mentoring I'm proudest of is my most recent, with an engineer who kept getting blocked. [She was new to our platform and would get stuck for days.]
>
> **T - Task:** I wanted her to grow without me doing her work, and she still had deadlines to hit.
>
> **A - Action:** I matched my support to her and the deadline from the start. My aim was to teach her how to get unstuck instead of clearing the blocks for her. I set up one-on-one training on the areas she kept hitting. I reviewed her code closely and gave direct feedback on every PR. [When she got stuck, I asked what she'd tried and pointed her where to look, instead of writing the fix.]
>
> **R - Result:** Her speed roughly doubled [by PRs merged per sprint], and she shipped three features in two months.
>
> **L - Learning:** I learned that balance on our telemetry visualization project, where I gave two junior engineers a lot of room so they'd own the work, and with a tight deadline our first milestone got hard to hit. [I stepped back in with smaller tasks and check-ins every few days,] and we still shipped the MVP on time. Now I match how hands-on I am to the person and the deadline, and I judge my mentoring by what they can do without me.

## Planning and project management

Questions about how you plan: what to work on, in what order, who does what, and how you keep it on track. Use the general answer when they ask how you work, and a story when they ask for a time you did it.

### "How do you plan a project?"

About a minute, no story needed.

> I start from the outcome and the date, not the task list. First I pin down the main problem the work has to solve and define the smallest version that solves it. Everything else waits. Then I put the riskiest piece first, usually the one everything else depends on, so surprises show up while there's still time. I break the rest into pieces one person can own end to end and match them to people: well-defined pieces for newer engineers, and the ambiguous or cross-team pieces for me. I name every dependency on another team at kickoff. I set checkpoints where something has to work, and I send a short regular update: what we're doing, why it matters, where we are, what's next, and when it'll be done. When the facts change, I re-plan out loud instead of letting the date quietly slip.

### Questions they might ask, and what to say

- **"How do you decide what to work on first?"** Use the telemetry project (Q7). Start from the question users most need answered, and build the smallest version that answers it, [with the riskiest piece first]. [On telemetry, the first version was the overlay and the core usage panel, and trends and filters waited.]
- **"How do you decide who works on what?"** Use telemetry (Q7) and the AI Copilot integration (Q5 backup). I give people whole pieces they can own, matched to their experience. [On telemetry, I took the risky data layer and gave the two juniors well-defined features.] On the Copilot integration, I wrote the design and most of the integration code and split the rest with two junior engineers, including one new to React who later helped new engineers on her team. Telemetry also taught me that growth has to fit inside the deadline.
- **"Walk me through how you planned a project from start to finish."** Use the AI Copilot integration (Q5 backup). I gathered requirements, scoped and estimated the work, and wrote the design. I reused existing components instead of building our own, so our time went into the integration. I split the work with two junior engineers, ran biweekly scrums, and sent weekly stakeholder updates with demos. Because the panel touched every page, I had page owners on six teams check their pages before preview. We reached private preview in two months with no reported regressions.
- **"Tell me about a time you cut scope to hit a deadline."** Use the release system (Experience answers). I wanted both the Azure side and the non-Azure side ready before launch. My manager challenged that, and we shipped Azure first with the old path as a manual fallback. That meant running two release paths for a while, but engineers got faster releases while the rest was still being built. "Done" is the smallest piece that's useful and safe to undo.
- **"Tell me about a project that fell behind. What did you do?"** Use telemetry (Q7) for a slip I caused, or the SRE dependency (Q4) for one I didn't control. On telemetry, I gave the juniors too much room and the first milestone got hard to hit. [I broke the work into smaller pieces with check-ins every few days,] and we shipped on time. On the release system, another team's staffing fell through. I escalated, then built their part myself. We were months late, and I learned to bring managers a decision, not just a status.
- **"How do you handle dependencies on other teams?"** Use the SRE dependency (Q4). I treat another team's work as the biggest risk in my plan. I name it at kickoff with a date and an owner, track it by milestone, and when it slips, bring the managers a choice: more people, less scope, a later date, or I take it over.
- **"Tell me about a time priorities changed, or you disagreed with a priority."** Use the search feature on our incident details page. The on-screen parts were already React, but workflows like mitigating an incident were still AngularJS, so the page loaded both and took about six seconds. I wanted to fix performance next. But customers we were onboarding were upset, because we'd moved content onto tabs and Ctrl+F can't find text on a tab that isn't open. The PMs and my manager made search the priority. I made my case for performance, [then saw their point: load time would come down as we finished the migration anyway, but search wouldn't exist unless we built it]. [I re-planned the five engineers' work around search.] It finds content on every tab, even ones that haven't loaded, and jumps to it. Once the last workflows moved to React, load time dropped from six seconds to 1.5. The people closest to customers often see the priority I'm missing. I make my case, and once the call is made, I commit to it fully.
- **"How do you keep stakeholders informed?"** Use the early-career feedback and the Copilot integration. A manager once told me good work isn't enough if people can't see it. So I send regular, structured updates to a wider audience: what I'm doing, why it matters, where it stands, what's next, and how long it'll take. On the Copilot integration, that meant weekly stakeholder updates with demos, so nobody was surprised at preview.
- **"How do you estimate? Tell me about an estimate that was wrong."** Use the SRE dependency (Q4). My biggest miss was the release system. The plan depended on another team's capacity, and when their staffing fell through, we were months late. An estimate that depends on another team is only as good as their commitment, so I get that commitment at kickoff and track it like my own work. On the Copilot integration, I scoped and estimated the work up front, and we reached private preview in two months.
- **"How do you balance features against tech debt or reliability work?"** Whatever is blocking users or other teams goes first. Otherwise, I make the case for the work in terms users and engineers feel, and fit it into planning. The Playwright move saved about eight hours of build time a day and two weeks of manual audits a quarter, which made it easy to justify. After the August incident, I led the release redesign, because a bad release that reaches everyone costs more than fixing the process.
- **"How do you know a project is on track?"** I don't rely on status alone. I set checkpoints where something has to work, and I look at those. On telemetry, the first milestone is what showed me my approach wasn't working, while there was still time to fix it. On the Copilot integration, the weekly demos did the same job for stakeholders.
- **"How do you run a project across several teams?"** Use Cypress to Playwright (Q9). I make the work cheap for them: a detailed guide, a meeting with each team about their apps, and doing some of the migration and reviews myself. And I get it into their plans before planning closes, which I learned the hard way on that project.

## Unclear requirements

Same story as Q8 backup, told for a different question. If they've already heard it, say "This is the Azure Portal evaluation I mentioned," and spend the time on how you turned an open question into requirements, a prototype, and a decision.

They might ask:

- "Tell me about a time you worked on something with unclear requirements."
- "Describe a time you were given a vague or open-ended task."
- "Tell me about a decision you made without all the information."
- "How do you get up to speed on a technology you've never used?"
- "Tell me about a time you had to define what success looked like."

**Headline:** Turned an open-ended ask from senior leadership into clear requirements, a working prototype, and a side-by-side list of trade-offs. Found first page load went from 1 second to 9 and the framework couldn't keep working during an Azure outage, recommended against the move, and turned the findings into a decision tree for our org and three partner orgs.

> **S - Situation:** Senior leadership asked me to evaluate moving our whole portal onto the Azure Portal framework. The ask was just "evaluate it." Nobody had said what a good answer looked like, and I'd never built on that framework.
>
> **T - Task:** I owned the evaluation and the recommendation. So my first job was deciding what we actually needed to find out.
>
> **A - Action:** I started with what our users couldn't give up. They're incident responders, so the portal has to load fast, and it has to keep working during an Azure outage, because that's when they need it most. Then I listed what the move would gain us: built-in deployment and monitoring, much wider adoption, and a dedicated team of about 60, compared with our five part-time maintainers. That gave me must-haves and nice-to-haves to test against. I researched the framework, then built a prototype that ran our pages on it, because a working version answers questions the docs can't. The prototype showed what the move would really cost. It loaded extensions in iframes and used an older module system, it had few reusable components, and its components didn't capture the usage data we rely on. In the setup we built, first page load went from about one second to nine. And keeping it working during an Azure outage would have needed a lot of new work from the Portal team. I listed the benefits and costs side by side, so leadership could see the trade-off, not just my conclusion.
>
> **R - Result:** I recommended against the move, because two must-haves failed with no practical fix. [Leadership agreed, and we stayed on our framework.] Instead of a one-time no, I turned what I'd learned into a decision tree our org and three partner orgs could use to tell when the framework is a good fit. [It's now used by about 20,000 engineers.]
>
> **L - Learning:** When requirements are unclear, I don't wait for someone to define them. I pin down what users can't lose, build the smallest prototype that turns open questions into facts, and leave behind something the next team can reuse. At Datadog, I'd handle an open-ended problem the same way.

### Follow-ups

- **How did you decide what "good" looked like?** From the users. Fast load and working through an Azure outage were must-haves, because incident responders can't do their job without them. Deployment, monitoring, and a bigger support team were real benefits, but nice-to-haves. A failed must-have meant no, unless there was a practical way to fix it.
- **What did the prototype tell you that research couldn't?** How our real pages behaved on it. The docs said how the framework was meant to work. The prototype showed what our users would actually get, like a nine-second first load in the setup we built.
- **How did you learn a framework you'd never used?** Its docs and architecture pages first, then building on it. Building surfaced the details that mattered, like the iframes and the older module system, faster than reading did.
- **How did you know when to stop exploring?** Once a must-have failed with no practical fix, more research couldn't change the answer. [I'd also set a time limit up front.]
- **How did you keep leadership in the loop while it was still unclear?** [I sent short updates on what I'd learned, what was still open, and when I'd have an answer.]
- **What would have changed your recommendation?** A practical way to keep it working during an Azure outage, and acceptable load time. Then the bigger support team and built-in deployment would have been worth weighing against the cost of moving.
- **Wasn't staying put risky too?** Yes. Our framework still had five part-time maintainers, and saying no to the move didn't fix that. [I called it out as a risk we still had to solve.]

## Other questions Datadog's guide lists

These aren't in the recruiter's ten, but the Values guide names them. Reuse a story you already have.

- **A mistake or failure:** the fallback folder (Q6), or the telemetry project (Q7).
- **Feedback that changed how you work:** Two managers told me to back my proposals with data and context. I did that in the Azure Portal evaluation (Q8 backup), where one second versus nine made the case.
- **A production issue you owned:** the August incident from the Experience answers.
- **Learning a new technology quickly:** module federation (Q7 backup), or the Azure Portal framework (Unclear requirements).
- **Simplifying a system:** I replaced a custom pipeline of five Azure resources with built-in Data Share. P99 latency went from 5 seconds to 1, moving 1 million documents a day with 100% uptime over 18 months.
- **Delivering under a tight deadline:** the AI Copilot integration reached private preview in two months with no reported regressions and now has 18,000 monthly users.
- **Using data to make a decision:** the Azure Portal evaluation (Q8 backup).
- **How you measure success:** the details page's load time and satisfaction scores (Q7 backup), or the release system's ten releases a day and 3-minute rollback.

## "What would you do if..." questions

1. Ask what you'd need to know: the goal, who's affected, how urgent it is, and what's missing.
2. Say what you'd weigh. Usually that's user impact first, then how easy it is to undo, then cost.
3. Say what you'd do and who you'd involve.
4. Say how you'd know it worked and what would make you change course.

### Practice: "Your team wants to release before a deadline, and you think it's risky"

- Find out what makes it risky and what the deadline actually protects.
- Look for a smaller safe version, or ship it behind a feature flag that's turned off.
- If it ships, agree on what to watch and who can turn it off.
- Raise it early with whoever owns the decision. Don't block it quietly.

### Practice: "An alert wakes on-call up every night, and people want to mute it"

- Look at the last few pages. Did any of them matter?
- If none did, change the threshold or turn it into a ticket instead of a page.
- If some did, figure out what it's really catching and alert on that instead.
- Write down the change so the next on-call engineer knows what happened.

## All learnings, both interviews

Every lesson from the Experience and Values answers, by story. Each one is stated so it applies anywhere, with how it changed the way I work and how I'd use it at Datadog.

### Release system (Experience main story, Values Q4 and Q6)

- **Safety has to come from the system, not from people being careful.** (August incident, Experience)
    - **How I grew:** I used to trust steps that weren't supposed to change anything. After the incident, I didn't stop at removing the bad file. I led a redesign so nothing reaches users until it's tested and approved, no matter who makes the mistake. I fix the class of problem, not just the instance.
    - **At Datadog:** Customers rely on Datadog during their own outages, so a bad release hurts them at the worst time. I'd look at every release path I touch for steps that can reach customers before a check, and make sure the checks actually run.
- **Anything other teams can see becomes a promise.** (Fallback folder, Experience and Values Q6)
    - **How I grew:** I added a backup folder without asking who else would use it, and partners came to depend on it. In the redesign, I gave them a supported way to see what's live. [Now I decide up front what I'm willing to support before I expose anything.]
    - **At Datadog:** Customers build on every API and behavior they can reach. I'd be deliberate about what we expose and plan how we'd change it later.
- **The riskiest moment is the middle of a rollout.** (Shell and version list, Experience and Values Q6 backup)
    - **How I grew:** I designed for before and after, not the in-between, so an old page could load new code. I fixed it by having each page get matching parts from one place. [Now I check what a user gets halfway through a rollout before I ship a change like that.]
    - **At Datadog:** At that scale, rollouts take longer and reach more customers, so the in-between state is where I'd look first.
- **"Done" is the smallest piece that's useful and safe to undo.** (Shipping Azure first, Experience)
    - **How I grew:** I wanted both sides finished before launch. My manager pushed back, and shipping Azure first with the old path as a fallback got engineers faster releases while the rest was still being built. I stopped holding value back for my complete design.
    - **At Datadog:** I'd ship in small, reversible steps and learn from real usage early.
- **I own the outcome, including the parts other teams build.** (SRE dependency, Experience and Values Q4)
    - **How I grew:** Escalating got attention, not people. Now I treat other teams' work as the biggest risk in a plan. I name it at kickoff, track it by milestone, and when it slips, I bring the managers a decision: more people, less scope, a later date, or I take it over.
    - **At Datadog:** Many teams own parts of the same product, so I'd surface cross-team risk early and turn it into a decision while there's still time to act.
- **Set the rules a system must never break before building it.** (What I'd do differently, Experience)
    - **How I grew:** I only wrote down "nothing reaches users before it's checked" after an incident. Now I'd start a design with those few rules and test every choice against them. [I'd also pin down requirements that differ by environment, like which clouds need which hosting, before building.]
    - **At Datadog:** I'd put those rules at the top of every design doc and use them in reviews.
- **AI speeds up the draft, not the judgment.** (Using AI on the redesign, Experience)
    - **How I grew:** It's fast at reading code and listing options, but it doesn't know the constraints that matter. I give it those up front, treat what it writes as a draft, and check it against how the system actually behaves.
    - **At Datadog:** AI-written code would get the same reviews, tests, and rollout as anything else.

### Other stories (Values)

- **People follow what they can see working.** (Career, Q1, and module federation, Q7 backup)
    - **How I grew:** A good idea doesn't spread just because it's right. Before I ask a team to change how they work, I build a prototype and make the new way easy to follow.
    - **At Datadog:** I'd earn buy-in for a design the same way, by showing it working first.
- **Real examples settle design questions faster than debate.** (Postmortems service, Q5)
    - **How I grew:** Arguing about behavior in the abstract went in circles. [Now I start design discussions from real scenarios and turn the answers into rules we can build and test.]
    - **At Datadog:** With so many kinds of customers, I'd ground design questions in real customer cases.
- **Reusing someone's work doesn't move the responsibility.** (AI Copilot integration, Q5 backup)
    - **How I grew:** [I still owned how the panel changed every page, even though the components weren't mine. Now I bring the owners of affected areas in to test early.]
    - **At Datadog:** I'd bring in the teams my change touches before it ships, not after.
- **A shared change is done when others can adopt it.** (Shared repo changes, Q6 Experience-round alternate)
    - **How I grew:** My change worked, but it cost other engineers time. After my manager pushed me on notice and docs, I proposed merge windows, setup changes coordinated ahead of time, and batched changes for big shared updates.
    - **At Datadog:** Platform changes reach many teams, so I'd plan how people adopt a change as carefully as the change itself.
- **Prioritizing is mostly deciding what not to build yet.** (Telemetry visualization, Q7)
    - **How I grew:** I start from the question users most need answered and build the smallest version that answers it, [with the riskiest piece first so surprises show up early]. I also put two junior engineers' growth ahead of the deadline, and that was the wrong call. Growing people has to fit inside a commitment, not compete with it.
    - **At Datadog:** I'd plan around the customer's main question first and put stretch work where there's slack.
- **The people closest to customers often see the priority I'm missing.** (Search on the incident details page, planning questions)
    - **How I grew:** I wanted to fix performance next. The PMs and my manager prioritized search, because customers couldn't find content across tabs. [I came to see their point.] I make my case, and once the call is made, I commit to it fully.
    - **At Datadog:** I'd bring my view to priority calls, listen hardest to the people talking to customers, and back the decision once it's made.
- **Adding something and replacing it are different decisions.** (FAST disagreement, Q8)
    - **How I grew:** "Would I add this today?" and "Should I replace what people already depend on?" have different answers. [Now I push for a clear decision early, because every change that lands makes the choice harder to undo.]
    - **At Datadog:** I'd raise a disagreement before code lands and get a decision from the people who own it.
- **Data beats opinion when I push back.** (Azure Portal evaluation, Q8 backup, and manager feedback)
    - **How I grew:** Two managers told me to back proposals with data and context. When I pushed back on leadership, I gave their option a fair test, and one second versus nine made the case better than my opinion could.
    - **At Datadog:** I'd bring measurements in terms users feel to any disagreement about direction.
- **When requirements are unclear, pin down what users can't lose, then prototype to get facts.** (Azure Portal evaluation, unclear requirements)
    - **How I grew:** I didn't wait for someone to define the requirements. I wrote down what our users couldn't give up, built a prototype to answer the open questions, and turned the answer into a decision tree other teams could reuse.
    - **At Datadog:** I'd handle an open-ended problem the same way: pin down what customers can't lose, build the smallest version that gets real facts, and leave behind something the next team can use.
- **Other teams plan their time in advance.** (Cypress to Playwright, Q9)
    - **How I grew:** Even a clearly good change costs other teams time. [Now I get cross-team work into other teams' plans before planning closes.] And I make it cheap to do with guides and hands-on help.
    - **At Datadog:** I'd line up cross-team work at planning time, not after.
- **Match support to the person and the deadline.** (Mentoring and the telemetry project, Q10)
    - **How I grew:** On the telemetry project, I gave two junior engineers a lot of room on a tight deadline, and the first milestone got hard to hit. Now I adjust how hands-on I am to the person and the deadline, and I judge my mentoring by what they can do without me.
    - **At Datadog:** I'd bring that to mentoring and onboarding newer engineers.

## Questions to ask your interviewer

- "How do engineers on your team decide when reliability work should take priority over planned features?"
- "What does a senior engineer own after a launch?"
- "What's something your team changed because of a postmortem?"
