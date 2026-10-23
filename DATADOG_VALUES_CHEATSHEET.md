# Datadog Values cram sheet

Memory aid for [DATADOG_VALUES_ANSWERS.md](DATADOG_VALUES_ANSWERS.md). Anything in [square brackets] is a made-up placeholder. Replace it with what actually happened, or cut it.

## How to answer

- **Story answers are STARL.** Situation (one line on what the story is about), Task, Action (about half the time, say "I"), Result (numbers), Learning (what I changed).
- **Q1 is CARL.** Context, Action, Result, Learning. The Learning leads into Datadog.
- **Q2 and Q3 have three parts.** My point, evidence from my work, why Datadog.
- **2 to 3 minutes, then stop.** Let them dig in.
- **Don't name Datadog's values.** Show them.
- **Your resume is open.** Glance at the bullet for numbers. Spend your memory on what it doesn't show: the decision, the trade-off, and the Learning.

## Story map

Learn this table first. If you know the story for each question, the rest comes back. "Senior", "SWE II", and "SWE I" are the Microsoft roles on your resume. Quoted text is how the bullet starts.

| Q   | Asked about                        | Story                                                  | Resume bullet to glance at                                                                                                                    |
| --- | ---------------------------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Career story                       | Building what engineers depend on                      | Summary, then each role top to bottom                                                                                                         |
| 2   | Why Datadog                        | Customer facing, bigger scale, same domain, full suite | None                                                                                                                                          |
| 3   | What you want to learn             | Noisy neighbors at scale, cross-team calls             | Summary (100+ engineers), Senior "Reduced partner onboarding" (4 organizations)                                                               |
| 4   | Ownership and scope                | Scope summary, then the SRE dependency                 | Senior "Reclaimed 317", "Scaled releases", "Corrected incident response", "Reduced partner onboarding", SWE II "Cut load time" (15 engineers) |
| 5   | Full lifecycle                     | Postmortems service, first on .NET                     | SWE II "Started the team's .NET migration"                                                                                                    |
| 5b  | Backup: cross-team delivery        | AI Copilot side panel                                  | SWE II "Shipped an AI copilot"                                                                                                                |
| 6   | Wrong technical decision           | Fallback folder                                        | Not on resume                                                                                                                                 |
| 6b  | Backup: another wrong decision     | Shell and version list                                 | Not on resume                                                                                                                                 |
| 6c  | Use in Experience round instead    | Shared repo changes                                    | Not on resume                                                                                                                                 |
| 7   | Prioritization and influence       | Telemetry visualization: what, in what order, who      | Senior "Standardized how 40+" (Led 2 engineers, 1K+ daily)                                                                                    |
| 7b  | Backup: influence and advocacy     | Module federation                                      | SWE II "Cut load time"                                                                                                                        |
| 8   | Disagreement with a coworker       | FAST disagreement                                      | Not on resume (the 40+ is in Senior "Standardized how 40+")                                                                                   |
| 8b  | Backup: pushing back on leadership | Azure Portal evaluation                                | Not on resume                                                                                                                                 |
| -   | Unclear requirements               | Azure Portal evaluation, told for ambiguity            | Not on resume                                                                                                                                 |
| 9   | Working across many teams          | Cypress to Playwright                                  | SWE II "Saved 8 hours of PR build time"                                                                                                       |
| 10  | Mentoring                          | Blocked mentee                                         | Not on resume                                                                                                                                 |

## Not on your resume: memorize these

- **Why Datadog (Q2), four reasons:** customer facing, orders of magnitude more scale, same business I work in, observability and incident management in one product suite (most companies own only part of that).
- **Noisy neighbor (Q3):** we already have one large customer whose load can slow down everyone else. Datadog has that across many customers.
- **SRE dependency (Q4):** weekly, then daily check-ins. Group chat with both managers and my skip manager. Their engineer left, the replacement was pulled away after about a month, SRE withdrew. I built it myself. Months late.
- **Postmortems service (Q5):** proposed the split. Weekly working group. Rewrote the auth library and other shared libraries.
- **AI Copilot (Q5b):** reused Fluent AI components, built the bot-framework piece. Biweekly scrums, weekly updates and demos. No reported regressions.
- **Fallback folder (Q6):** only way to tell which version was live. Every release overwrote it. Incident had a different cause: duplicate routing rule, found in the IIS logs. Kept the partner URL, routed it to an exact version.
- **Shell fix (Q6b):** old shell from ring 3 plus new app code from canary. Version list now embedded in the shell's HTML. First load 5% faster.
- **Shared repo (Q6c):** 2023. Merge windows, environment updates coordinated ahead, batched changes.
- **Telemetry (Q7):** first version answered "is anyone using this, and is it working?" [Overlay plus usage panel first. Trends, tags, leadership breakdown later.] [I took the risky data layer.] Juniors owned whole features. Put their growth ahead of the deadline: wrong call. MVP on time.
- **Module federation (Q7b):** iframes got slower with each one. Prototype on my own in one component, then a standard path. Foundation for the details page.
- **Search (planning questions):** PMs and my manager prioritized it over my performance push. Ctrl+F can't find text on closed tabs. I made my case, then committed.
- **FAST (Q8):** kept navigation and the service and team pickers. Both of us presented to both managers and my skip manager.
- **Azure Portal evaluation (Q8b):** first load about 1 second to 9. Their team of about 60 vs our five part-time maintainers. Couldn't keep working during an Azure outage. Decision tree for our org and three partner orgs.
- **Playwright (Q9):** about 7x faster.
- **Mentee (Q10):** speed roughly doubled, 3 features in 2 months.

## Q1. Career story

**Story:** Building what engineers depend on

**Resume:** walk it top to bottom: summary, SWE I, SWE II, Senior. Bloomberg for the 75K.

**Open with:** "My career has been about building things other engineers depend on."

**Cue:** internships to first React app / shared pieces / 100+ engineers / prototype first, then Datadog

- **C:** Object Edge and Bloomberg internships, service at 75,000 requests a second. Then 6+ years at Microsoft. Incident-management team: first React app, base for all 16 apps.
- **A:** Scope grew into shared repo, deployments, telemetry, backend services. Team's first ASP.NET Core service, shared code reused by ten more. Build 120 to 25 minutes. Kafka pipeline: 200,000 events an hour into 50,000 postmortem updates a day. Led the release system that lets the web app ship separately from the backend.
- **R:** Own the platform 100+ engineers build on. Releases once a week to about ten a day, 16 apps, 12 clouds. I run it in production.
- **L:** A good idea doesn't spread just because it's right. People follow what they see working, so I prototype first. Next: backend at growing load, so Datadog.

## Q2. Why Datadog

**Story:** Customer facing, bigger scale, same domain, full suite

**Resume:** none needed.

**Open with:** "I want to work at Datadog because it's the business I already work in, but customer facing and at orders of magnitude more scale."

**Cue:** same business / customer facing / orders of magnitude / one suite

- **Point:** Same business I'm in, but customer facing and at orders of magnitude more scale.
- **Evidence:** Datadog's customers are engineers, and so are mine. Every Microsoft team uses our incident tool when something breaks. I run our release system in production and traced a production incident on it through the server logs. But our tool is internal: one company.
- **Why Datadog:** Outside customers, and every new customer sends more data. Backend must keep up and stay fast for engineers debugging an outage. Observability and incident management in one suite, incidents next to metrics, traces, and logs. Most companies own only part of that. Domain knowledge on day one, much bigger systems.

## Q3. What you want to learn

**Story:** Noisy neighbors at scale, cross-team calls

**Resume:** summary (100+ engineers), Senior "Reduced partner onboarding" (4 organizations).

**Open with:** "I want to learn how to design backend systems for load that grows with every new customer, and I want to grow into leading technical decisions across several teams."

**Cue:** growing load / one large customer already / orders of magnitude / calls teams build around

- **Point:** Design backend for load that grows with every customer. Lead technical decisions across several teams.
- **Evidence:** My system serves one company, so its load doesn't keep climbing. We already have one large customer whose load can slow down everyone else. Today I set technical direction for a platform 100+ engineers and partner teams in four organizations build on.
- **Why Datadog:** Noisy neighbors and cost across many customers, at orders of magnitude more scale. Make the calls several teams build around. In a year: [have led a design that changed how a system handles growth or cost, and be someone other teams pull into their design reviews].

## Q4. Ownership and scope

**Story:** Scope summary, then the SRE dependency

**Resume:** the scope list is your Senior bullets: "Reclaimed 317" (build), "Scaled releases" (16 apps, 12 clouds), "Corrected incident response" (Kafka), "Reduced partner onboarding" (plugins). 15 engineers is in SWE II "Cut load time". The SRE story is not on it.

**Open with:** "I own the platform more than 100 engineers build on: the shared repo, its build pipeline, and our web app's release system."

**Cue:** scope / blockers first / SRE side / my risk / escalated, built it / months late / name dependencies at kickoff

**Scope (about 50 seconds):**

- Shared repo, build pipeline, release system for 100+ engineers
- Build 120 to 25 minutes. Releases and rollbacks across 16 apps, 12 clouds
- [I'm on its on-call rotation and run the weekly on-call handoff.]
- Backend pipeline: 200,000 Kafka events an hour into 50,000 postmortem updates a day, fixing incident metrics like time to mitigate
- Outside my team: plugin model with a colleague. Four partner organizations ship six plugins on their own. Onboarding three weeks to one hour
- Mentored 15 engineers through the move to React

**Priority rule:** whatever blocks users or other teams goes first. [If the shared build breaks for 100 engineers, that beats my own project that day.] Then say: "Here's how I plan, and where I learned it."

- **S:** Release system depended on the SRE team to build its non-Azure side.
- **T:** I led the project, so their part was my delivery risk, even though I didn't control their staffing.
- **A:** Weekly, then daily check-ins with their engineer, who sometimes went weeks without responding. Group chat with both managers and my skip manager, escalation on record. Engineer left, replacement pulled away after about a month, SRE withdrew. Built the non-Azure side myself.
- **R:** Shipped. Releases once a week to about ten a day. But months late.
- **L:** I own the outcome, even the parts other teams build. Escalating gets attention, not people. Name other teams' work at kickoff, track by milestone, and when it slips, bring managers a decision: more people, less scope, a later date, or I take it over. At Datadog: many teams, same product.

## Q5. Owning the full lifecycle

**Story:** Postmortems service, first on .NET

**Resume:** SWE II "Started the team's .NET migration" (60K, 10 more). Working group and auth library are not on it.

**Open with:** "I proposed splitting postmortems out of our incident system into their own service, and I built it as our team's first ASP.NET Core service."

**Cue:** tangled / first on new stack / working group / 60K and ten services / real examples

- **S:** Incident and postmortem workflows tangled in one system. Postmortems needed to change without breaking incident behavior.
- **T:** Owned it from proposal to production. First on the team on the new stack.
- **A:** Hard part: where an incident ends and a postmortem begins. Weekly working group with [product managers and the teams that write postmortems]. Changed the design as we answered questions. Shared code didn't work on the new stack: rewrote the auth library and other shared libraries.
- **R:** First APIs in production. 60K requests a day. Ten more services moved to .NET on my shared code, including auth.
- **L:** Real examples settle design questions faster than debate. [Now I start design discussions from real scenarios.] At Datadog: real customer cases.

**Trade-off:** [We considered changing the existing system in place, but every postmortem change would still have shipped with the whole incident system.]

### Q5 backup. Cross-team delivery

**Story:** AI Copilot side panel

**Resume:** SWE II "Shipped an AI copilot" (2 months, 18K, 2 engineers, 6 teams, 4 organizations).

**Cue:** every page, six teams / portal only / reuse and coordinate / two months / [owners test early]

- **S:** AI Copilot side panel on every page changed layouts owned by six teams in four organizations.
- **T:** Owned the portal integration, not the model or the backend.
- **A:** Requirements, scope, design. Reused Fluent AI components instead of building our own, built the missing bot-framework piece. Wrote most of the code, led two junior engineers. Worked closely with a junior new to React, who later helped new engineers on her team get started. Page owners on all six teams checked layouts. Biweekly scrums, weekly updates and demos.
- **R:** Private preview in two months, no reported regressions. Later 18,000 monthly users.
- **L:** [Reuse doesn't move the responsibility. Bring the owners of affected areas in to test early.]

## Q6. Wrong technical decision

**Story:** Fallback folder

**Resume:** not on it. Senior "Scaled releases" is the system it belongs to.

**Open with:** "I designed an emergency fallback folder for our release system, and it broke the safety rule the system was supposed to follow."

**Cue:** only live-version signal / my design / exact-version routing / partners unchanged / unplanned contract

- **S:** Added a fixed "last known good" folder as a fallback. Didn't mean for anyone to depend on it, but it was the only way to tell which version was live. Partners used it as a stable URL.
- **T:** My design, so fixing it without breaking partners was on me.
- **A:** Came up after an incident with a different cause: duplicate routing rule, traced through the IIS logs. Review rule: uploading never changes what users see. Every release overwrote my folder, even while users could be loading from it. Kept the partner URL, routed it to an exact version. Led a redesign: pages will load exact versions, old URL only for older integrations until they move.
- **R:** Partners changed nothing. Automated tests cover the routing. [The redesign is built and tested, and PPE is next.]
- **L:** Anything others can see, they'll build on, so it's a promise. Gave partners a supported way to see what's live. [Decide up front what I'll support.] At Datadog: customers build on every API and behavior.

**Trade-off:** Rejected asking partners to switch to a new URL. They depended on that one.

### Q6 backup. Shell and version list

**Story:** Shell and version list

**Resume:** not on it, including the 5%. Senior "Scaled releases" is the system it belongs to.

**Cue:** late version fetch / my design / embed in HTML / 5% faster / must match

- **S:** Shell (main page that loads every app) fetched a separate version file after loading. Mismatched code could run together.
- **T:** My design, so the fix was mine.
- **A:** Rollout goes one ring at a time, canary first. Old shell from ring 3 plus new app code from canary could fail at runtime. Dropped the fetch. Server embeds the version list in the head of the shell's HTML. Whichever ring serves the shell also sends matching app versions.
- **R:** Each page gets app versions that match its shell. First load 5% faster, no extra request, no version file on disk. [The redesign is built and tested, and PPE is next.]
- **L:** When parts must match, the riskiest moment is mid-rollout, old and new side by side. Designed for before and after, not the middle. At Datadog's scale, rollouts last longer and reach more customers.

### Q6 alt (use in the Experience round). Shared repo changes

**Story:** Shared repo changes

**Resume:** not on it. Same repo as Senior "Reclaimed 317" (Nx monorepo).

**Cue:** too little notice / my disruption / merge windows / [next upgrade] / done means adopted

- **S:** 2023: large shared-repo changes without enough notice. Cost engineers time while they were shipping.
- **T:** My changes, so the disruption was mine to fix, plus how the next big change lands.
- **A:** Code was fine, but people fixed local setups by hand. Manager pushed for more notice and better docs. Right call. Proposed merge windows, environment updates coordinated ahead, batched changes.
- **R:** [On the next upgrade, I picked a merge window, sent the steps ahead of time, and had someone outside my team try them first. It needed much less hands-on help.]
- **L:** A change others depend on is done when they can adopt it without losing a day, not when it works for me. At Datadog: plan adoption as carefully as the change.

## Q7. Prioritization and influence

**Story:** Telemetry visualization: what to build, in what order, who builds it

**Resume:** Senior "Standardized how 40+ Azure products" (Led 2 engineers, 1K+ daily, C-suite). The scoping and order are not on it.

**Open with:** "I own a shared framework that more than 40 Azure products use to measure how people use their pages."

**Cue:** more than we could build / users' main question first / [riskiest piece mine] / whole features to juniors / growth vs deadline / MVP on time

- **S:** Framework 40+ Azure products use to measure usage. [Teams had to write their own queries to see the data.] Show the numbers inside the app, next to what they measure. Two junior engineers, tight deadline.
- **T:** More to build than time. I owned what made the first version, the order, and who built what.
- **A:** Started from users' main question: is anyone using this, and is it working? [First version: overlay plus usage panel. Trends, tags, leadership breakdown waited.] [Took the risky data layer, sign-in and permissions, myself.] Juniors owned whole features. Put their growth ahead of the deadline, and the first milestone got hard to hit. [Smaller pieces, check-ins every few days.]
- **R:** MVP on time. Used daily by 1K+ engineers, PMs, designers, and the C-suite.
- **L:** Prioritizing is mostly deciding what not to build yet. Main question first, smallest version, [riskiest piece first]. Growth fits inside a commitment. At Datadog: customer's main question first, stretch work where there's slack.

**Trade-off:** [Gave up trends and filters in the first version to hit the date.]

### Q7 backup. Influence and advocacy

**Story:** Module federation

**Resume:** SWE II "Cut load time" (6 to 1.5, 3.62 to 4.10, 5 engineers, 65K, 4 teams to 9). Module federation is not on it.

**Cue:** slow iframes / on my own / prototype and demo / 4 teams to 9, 6 to 1.5 / show it working

- **S:** AngularJS portal loaded some components in iframes. Slow, and slower with each one.
- **T:** Nobody assigned it. Prove a better approach before asking anyone to change.
- **A:** Found module federation early. Rewrote one iframed component in React, loaded it straight into AngularJS. Demoed it, built a standard path.
- **R:** Much faster than iframes, kept up as we added more, became the team's plan. Standards 4 teams to 9. Foundation for the details page (65K daily, led 5 engineers): load 6 to 1.5 seconds, satisfaction 3.62 to 4.10.
- **L:** People follow what they can see working. A small, real prototype beat argument. At Datadog: build it small, show it, make it easy to copy.

## Planning questions

**"How do you plan a project?"** outcome and date / smallest version / riskiest piece first / whole pieces matched to people / dependencies at kickoff / checkpoints and regular updates / re-plan out loud

| If they ask...                                | Use                                                                                           |
| --------------------------------------------- | --------------------------------------------------------------------------------------------- |
| What to work on first                         | Telemetry (Q7): users' main question first, smallest version                                  |
| Who works on what                             | Telemetry (Q7) and Copilot (Q5b): whole pieces matched to experience                          |
| A project you planned start to finish         | Copilot (Q5b): requirements, scope, estimate, design, biweekly scrums, weekly demos, 2 months |
| Cutting scope for a deadline                  | Release system: Azure first, old path as fallback                                             |
| A project that fell behind                    | Telemetry (my slip, recovered) or SRE (Q4, not mine, months late)                             |
| Dependencies on other teams                   | SRE (Q4): name at kickoff, track by milestone, bring a decision                               |
| Priorities changed, or you disagreed with one | Search: PMs and my manager chose it over my performance push. Made my case, then committed    |
| Keeping stakeholders informed                 | What, why, where it stands, what's next, when. Copilot weekly demos                           |
| An estimate that was wrong                    | SRE: an estimate is only as good as the other team's commitment                               |
| Features vs tech debt or reliability          | Blockers first. Playwright savings. Release redesign after the incident                       |
| Knowing it's on track                         | Checkpoints where something has to work. Telemetry's first milestone showed the problem       |
| Running work across several teams             | Playwright (Q9): make it cheap, get into their plans early                                    |

## Unclear requirements

**Story:** Azure Portal evaluation, told for ambiguity (same story as Q8 backup)

**Asked as:** unclear requirements, a vague task, deciding without all the information, learning a new technology, defining success.

**If they've already heard it:** "This is the Azure Portal evaluation I mentioned." Then spend the time on how you turned an open question into requirements, a prototype, and a decision.

**Headline:** Turned an open-ended ask from senior leadership into clear requirements, a working prototype, and a side-by-side list of trade-offs. First load 1 second to 9, no outage support, recommended against, decision tree for our org and three partner orgs.

**Open with:** "Senior leadership asked me to evaluate moving our whole portal onto the Azure Portal framework. The ask was just 'evaluate it.'"

**Cue:** just "evaluate it" / users' must-haves first / research, then prototype / 1 to 9 seconds, no outage support / decision tree / prototypes turn questions into facts

- **S:** Leadership: evaluate moving the whole portal onto the Azure Portal framework. No definition of a good answer. Never built on it.
- **T:** Own the evaluation. First job: decide what we need to find out.
- **A:** Must-haves from users: fast load, works during an Azure outage. Nice-to-haves: built-in deployment and monitoring, wider adoption, team of about 60 vs our five part-time. Researched it, then prototyped our pages on it. Iframes, older module system, few reusable components, no usage data from its components. First load about 1 second to 9 in our setup. Outage support needed a lot of new work from the Portal team. Benefits and costs side by side.
- **R:** Recommended against: two must-haves failed with no practical fix. [Leadership agreed.] Decision tree for our org and three partner orgs. [About 20,000 engineers use it.]
- **L:** Don't wait for requirements. Pin down what users can't lose, prototype to turn questions into facts, leave something reusable. At Datadog: same for open-ended problems.

**Follow-ups:**

- **What "good" looked like:** from users. Fast load and working through an Azure outage were must-haves. Deployment, monitoring, bigger team were nice-to-haves. A failed must-have meant no, unless there was a practical fix.
- **What the prototype told you:** how our real pages behaved. Docs said how it was meant to work. Prototype showed what users would get: nine-second first load in our setup.
- **Learning a framework you'd never used:** docs and architecture pages, then building on it. Building surfaced iframes and the older module system faster than reading.
- **When to stop exploring:** once a must-have failed with no practical fix, more research couldn't change the answer. [Time limit up front.]
- **Keeping leadership in the loop:** [short updates: what I learned, what's still open, when I'd have an answer.]
- **What would have changed your mind:** a practical way to work during an Azure outage, plus acceptable load time. Then weigh the bigger team and built-in deployment against the cost of moving.
- **Wasn't staying put risky too:** yes. Five part-time maintainers, and saying no didn't fix that. [Called it out as a risk to solve.]

## Q8. Disagreement with a coworker

**Story:** FAST disagreement

**Resume:** not on it. The 40+ is in Senior "Standardized how 40+ Azure products".

**Open with:** "I disagreed with a coworker who wanted to build shared UI components in Microsoft FAST for Elixir, the framework more than 40 Azure product teams use."

**Cue:** FAST for Elixir / make the cost clear / managers decide / keep, stop adding / add vs replace

- **S:** Coworker wanted shared FAST components for Elixir, the framework 40+ Azure product teams use. He had a real point.
- **T:** Make the cost to everyone else clear without brushing off his point.
- **A:** Told him directly: fragmented stack, few frontend experts, another way to write, test, and maintain. Elixir team declined, but FAST kept landing in our product. We each presented to both managers and my skip manager. They decided not to expand FAST. Kept navigation and pickers, stopped adding new ones.
- **R:** Clear decision, no costly rewrite. He later joined my team. [I've reviewed and helped fix the FAST components we kept]
- **L:** Adding something and replacing it are different decisions. [Push for a clear decision early, because every change that lands makes it harder to undo.]

**Trade-off:** Didn't rewrite navigation and the service and team pickers. Too costly, people depended on them.

### Q8 backup. Pushing back on leadership

**Story:** Azure Portal evaluation

**Resume:** not on it. Memorize 1 second to 9, and about 60 vs five part-time.

**Cue:** leadership's proposal / own the call / fair test / recommend against / cost users feel

- **S:** Senior leadership asked me to evaluate moving our whole portal onto the Azure Portal framework.
- **T:** Own the evaluation and the recommendation.
- **A:** Fair test: built-in deployment and monitoring, team of about 60 vs our five part-time maintainers. On our pages, in the setup we evaluated, first load went from about 1 second to 9. Couldn't keep working during an Azure outage, when responders need us. Built a decision tree for our org and three partner orgs.
- **R:** Recommended against. [Leadership agreed, and we stayed on our framework.]
- **L:** Give their option a fair test and show the cost users feel. 1 second vs 9 beat my opinion.

**Trade-off:** Asking the Portal team to build outage support was too much work to justify the move.

## Q9. Working across many teams

**Story:** Cypress to Playwright

**Resume:** SWE II "Saved 8 hours of PR build time" (418 tests, 11 apps, 5 teams, 3 organizations, 2 weeks of audits). "About 7x faster" is not on it.

**Open with:** "I led moving 418 end-to-end tests from Cypress to Playwright, across 11 apps owned by five teams in three organizations."

**Cue:** 418 tests / can't assign the work / make it easy / 7x faster / teams plan ahead

- **S:** 418 end-to-end tests, Cypress to Playwright. 11 apps, five teams, three organizations.
- **T:** Get five teams to do work I couldn't assign.
- **A:** Made it harder: raised it after milestone planning, their time already committed. Made the work easier: met each team about their apps, wrote a detailed migration guide, did some migrations and code reviews myself.
- **R:** Within the milestone. About 7x faster. About 8 build hours a day and about 2 weeks of manual accessibility audits a quarter saved. Everyone on one test setup.
- **L:** A clearly good change still costs other teams time, and they plan it in advance. [Get cross-team work into their plans before planning closes.] Make it cheap with guides and hands-on help.

**Trade-off:** Didn't just ask teams to migrate. Not my teams, so a good technical case wasn't enough.

## Q10. Mentoring

**Story:** Blocked mentee

**Resume:** the mentee is not on it. The two telemetry juniors are "Led 2 engineers" in Senior "Standardized how 40+ Azure products".

**Open with:** "The mentoring I'm proudest of is my most recent, with an engineer who kept getting blocked."

**Cue:** kept getting blocked / grow and hit deadlines / training and PR feedback / doubled, 3 features / match the person

- **S:** Most recent mentee kept getting blocked. [She was new to our platform and would get stuck for days.]
- **T:** Help her grow without doing her work. She still had deadlines.
- **A:** Matched support to her and the deadline from the start. Taught her to get unstuck instead of clearing blocks. One-on-one training on the areas she kept hitting. Close review, direct feedback on every PR.
- **R:** Speed roughly doubled [by PRs merged per sprint]. Shipped 3 features in 2 months.
- **L:** Learned it on telemetry: gave two juniors lots of room, tight deadline, first milestone got hard to hit, still shipped the MVP on time. Now I match hands-on to the person and the deadline. Judge mentoring by what they can do without me.

## Question router

| If they ask...                     | Use                                                                                                                                                             |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A mistake or failure               | Fallback folder (Q6), or telemetry project (Q7)                                                                                                                 |
| Feedback that changed how you work | Two managers: back proposals with data and context. Azure Portal evaluation (Q8 backup), 1 second vs 9 made the case                                            |
| A production issue you owned       | August incident from the Experience answers                                                                                                                     |
| Learning a new technology quickly  | Module federation (Q7 backup), or the Azure Portal framework (Unclear requirements)                                                                             |
| Unclear requirements, vague task   | Azure Portal evaluation, told for ambiguity (Unclear requirements)                                                                                              |
| Simplifying a system               | Data Share (Senior "Cut ingestion"): replaced a custom pipeline of 5 Azure resources. P99 5 seconds to 1, 1 million documents a day, 100% uptime over 18 months |
| Delivering under a tight deadline  | AI Copilot: private preview in 2 months, no reported regressions, 18,000 monthly users                                                                          |
| Using data to make a decision      | Azure Portal evaluation (Q8 backup)                                                                                                                             |
| How you measure success            | Details page load time and satisfaction (Q7 backup), or the release system (Senior "Scaled releases"): ten releases a day, 3-minute rollback                    |

## Questions to ask them

- "How do engineers on your team decide when reliability work should take priority over planned features?"
- "What does a senior engineer own after a launch?"
- "What's something your team changed because of a postmortem?"

## Self-test

1. Cover everything below the story map. For each row, name the story and its key number.
2. For each card, say the "Open with" line, then the five cue words, then the Learning.
3. Answer three random questions aloud in under 3 minutes each, with your resume open. Check anything not on it against "Not on your resume: memorize these."
