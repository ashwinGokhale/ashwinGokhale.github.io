# Datadog Experience interview answers

Senior Software Engineer, Backend. 45 minutes on one project.

Anything in [square brackets] is a made-up placeholder. Replace it with what actually happened, or cut it.

Give the main answer as one STARL story (Situation, Task, Action, Result, Learning) in under 3 minutes, then stop and let the interviewer steer. Every question from Datadog's Experience prep guide is answered under it, in the guide's order. Every learning from both interviews is listed at the end.

## Main answer

**Headline:** Built the system that ships our web app separately from the backend, for 16 apps across 12 clouds. Releases went from once a week to ten a day, and global rollback went from 20 minutes to 3.

> **S - Situation:** I led the release system that ships the web app for Microsoft's incident-management product separately from its backend. On-call teams across Microsoft use it, and over 100 engineers build it. Before, its files shipped inside the weekly backend deployment, copied over the live folders on every server. So a UI fix waited up to a week, and a global rollback took about 20 minutes.
>
> **T - Task:** I owned delivery and built the Azure side. The app also had to keep working during an Azure outage, and the SRE team, which runs our servers, was supposed to build the non-Azure side.
>
> **A - Action:** I moved every build into its own version folder, with a small version list that decides which build users get. A release flips that list across three rollout rings, and rollback points it at an older build that's still there, with no rebuild. I first wanted both sides ready before launch. My manager challenged that, and I agreed to ship the Azure side first, with the old deployment path kept as a manual fallback. That meant running two release paths for a while, but engineers got the benefits sooner. With SRE, I ran weekly, then daily check-ins and escalated through both managers and my skip manager. Their engineer left, the replacement was pulled away after about a month, and SRE withdrew. So I built the non-Azure side myself.
>
> **R - Result:** Releases went from about once a week to about ten a day across 16 apps and 12 clouds, so a fix can reach users the same day. Global rollback dropped from 20 minutes to 3. The staffing gap made us months late. I run the system in production and lead the weekly frontend on-call handoff.
>
> **L - Learning:** In August, a config file inside one app's upload broke part of the Troubleshooting page before canary could catch it. My fallback folder had the same flaw: every release overwrote it while it was live, and partners had built on it. I learned that safety has to come from the system, not from people being careful. Any step that reaches users before a check will eventually hurt them, and anything other teams can see becomes a promise. So I led a redesign where nothing reaches users until it passes tests and on-call approval. That's how I'll look at every release path at Datadog.

## If they ask you to draw it

This is the redesign.

1. Build once, and promote that exact build everywhere.
2. Upload it to Azure and to our own servers in parallel, each version in its own folder. Nothing live changes.
3. Run UI tests against that exact build.
4. Promote to canary, then datacenter A, then datacenter B. The on-call engineer approves each step, and we wait 24 hours after the first two.
5. On each server, take it out of rotation, let requests finish, stop the site, update the version list, start it, run the health check, and put it back.
6. The server writes the version list into each page, and every download uses an exact version URL. In public production, the main page's code comes through Akamai, and app code comes from Azure Front Door.

Public production uses both Azure and our own servers. Europe uses only Azure. The government clouds use only our own servers, with no CDN.

## If they dig in

These follow the prep guide's order. Each heading is a section of the guide, and each bold question is one of its prompts. Extra follow-ups sit in the section they fit.

### Context

- **What problem existed?** Our web app's files shipped inside the weekly backend deployment. Every release copied them over the live folders on every server, so we released about once a week, and a global rollback took about 20 minutes.
- **Why did it matter?** A UI fix waited up to a week for the next backend release, and undoing a bad release took 20 minutes. Over 100 engineers couldn't ship on their own schedule, and on-call teams across Microsoft use the app while they handle incidents.
- **Who were the users and stakeholders?** On-call teams across Microsoft use the app. Over 100 engineers build its 16 apps. Partner teams load some of our pages inside their own tools. The SRE team runs our servers. My manager and skip manager owned the priority calls.
- **What constraints did you have?** It had to work in 12 clouds with different hosting rules. It had to keep working during an Azure outage. The non-Azure side depended on SRE, whose staffing I didn't control. And partner integrations had to keep working without changes on their side.
- **What was your role?** I led the project. I owned delivery, built the Azure side, and later built the non-Azure side when SRE withdrew. I run the system in production today.
- **Which part did you personally own?** Delivery of the whole project, the Azure hosting and release path, the shell (the main page that loads every app), the non-Azure side after SRE withdrew, the fix for the August incident, and the redesign. SRE still owns the servers, load balancers, and deployment tool.
- **What did it look like before?** One package built the backend website and the web app together. The deploy copied gigabytes of the app's files over the live folders on every server while they were serving users. There was no way to release or roll back the web app on its own.

### Action

- **What did you design or significantly influence?** The release model: every build in its own version folder, and a small version list that decides which build users get. The shell. The three-ring rollout. And, after the incident, the redesign where uploading never changes what users see.
- **Which technical decisions did you make, and why?** Version folders that never change, so rollback is just pointing at an older build, with no rebuild. Azure first with the old path as a fallback, so engineers got faster releases sooner. Building the non-Azure side myself when SRE withdrew, because waiting had no end date. And after the incident, separating upload from going live.
- **What alternatives did you consider, and why reject them?** A custom C# proxy that rewrites the page, which we'd maintain on every request. Separate builds per environment, which breaks "build once." Routing all downloads through our servers, which loads the portal machines when a CDN already does this. A catch-all fallback folder, which hides failures and can mix builds. Sorting users into rings in our own code, when Front Door's traffic weights already do it. And waiting for both sides before launch, which would have held back every benefit until the slowest part was done.
- **Which trade-offs did you make?** Azure first meant running two release paths for a while. The redesign trades production speed for safety, with 24-hour holds and on-call approval. And the fleet doesn't switch all at once, so we keep each page on one build instead. Each one is broken out under Trade-offs below.
- **Which technologies did you pick, and how did they fit?** Azure Storage behind Front Door for app files, because Front Door splits traffic across rings by weight. IIS rewrite maps on our own servers, because those servers already run IIS and a rewrite map can pick a version with no new code. Akamai in front of our servers in public production, so users far from our US datacenters, like in India, aren't slow. Module federation, so each app loads into the shell at runtime with its own version.
- **What went wrong or changed direction?** My manager challenged my plan to wait for both sides, and I shipped Azure first. SRE withdrew, so I built their part myself, months late. And the August incident showed that an upload could change what users see, which led to the redesign.
- **How did you handle rollout, monitoring, and operations?** Every release goes ring by ring, starting with canary. Rollback points the version list back at a build that's still on the servers, in about 3 minutes globally. In the redesign, every step also needs on-call approval, with a 24-hour wait after the first two. [We watch page-load errors, portal error rates, and new incidents after each step.]
- **How did you work with, influence, or unblock other teams?** With SRE, I ran weekly, then daily check-ins and escalated through both managers and my skip manager, then built their part when they withdrew. For partners, I kept their URL working while I changed what was behind it. For on-call engineers and app developers, I wrote the release steps and the local testing guide.
- **How did your approach change as you learned more?** I started out wanting the complete design before launch, and learned to ship a safe piece first. I started out trusting steps that weren't meant to change anything, and learned to check what each step can actually reach. And after the incident, I moved from fixing the instance to fixing the class of problem.

### Result

- **What changed, in numbers?** Releases went from about once a week to about ten a day across 16 apps and 12 clouds. Global rollback went from about 20 minutes to 3. Moving the version list into the page made first load 5% faster.
- **What did it mean for users and engineers?** A fix can reach users the same day instead of waiting a week. Engineers can load their local code or a branch build against real test data and share a link to it, so they get feedback before they merge.
- **Was it a full success?** No. The staffing gap made us months late, and the August incident exposed a gap in how uploads worked.
- **What's still unresolved, and why?** The redesign isn't in production yet, because we designed it after the August incident. [It's built and tested in code, and PPE is next.] The old fallback URL stays for older partner integrations until they move.

### Learning

- **What would you do differently if you started again?** I'd decide on day one the few rules the system must never break, like "nothing reaches users before it's checked," and test every design choice against them. I only had that rule after an incident. I'd also turn cross-team risk into a decision as soon as it appeared, instead of tracking it. [And I'd pin down requirements that differ by environment, like which clouds need which hosting, before building.]
- **Which assumption proved wrong?** That a step was safe because it wasn't meant to change anything. Uploading wasn't supposed to affect users, so nothing checked it, and it did. I also assumed two parts of the system would always match, and in the middle of a rollout they didn't. Failures hide in the steps nobody watches and in the in-between states.
- **Which skills did you develop?** Technically, designing changes so they can be checked and undone before they reach users. Operationally, debugging production from evidence, starting with the server logs instead of guesses. As a leader, shipping a useful piece early when there's a safe way back, and turning a stalled dependency into a decision for the people who can fix it.
- **How did production differ from what you expected?** People and systems used it in ways I didn't plan. Partners built on a folder I meant only as a backup, and browsers mixed servers in ways I hadn't designed for. Production finds every path you leave open, so I design for how a system can be used, not just how I meant it to be used.
- **What did you learn about users, scale, reliability, or collaboration?** Users: anything they can reach, they'll build on, so it's a promise whether I meant it or not. Scale: every special case multiplies across environments, so keep the parts simple and the same everywhere. Reliability: make undoing a change fast and routine, and don't depend on people being careful. Collaboration: escalation gets attention, not people, so bring leaders a decision, not just a status.
- **How did it change your engineering approach?** I keep "it's built" separate from "users have it," so every change can be checked and undone before it matters. I ship the smallest useful piece that's safe to undo instead of waiting for the full design. And I treat other teams' work as the biggest risk in a plan from day one.
- **Where have you applied it since?** In the redesign, where nothing reaches users until it passes tests and an on-call approval, and partners get a supported way to see what's live instead of relying on internals. And in how I plan cross-team work, with dependencies named at kickoff and tracked by milestone. Those are the habits I'd bring to any system Datadog customers rely on.

### Technical challenges

- **What made it hard?** Twelve clouds with different hosting rules. A browser can load the page from one datacenter and scripts from another, so every server needs a build's files before any server switches to it. The app has to keep working when Azure is down. And the redesign had to leave the Portal's code alone, because we're retiring it.
- **Scale, traffic, or data volume?** 16 apps across 12 clouds, [about 100,000 page loads a day across about 40 servers]. The old deploy copied gigabytes to every server. The hard part isn't raw traffic. It's the number of places a release has to land correctly.
- **Reliability, availability, or disaster recovery?** The app has to keep loading during an Azure outage, which is exactly when people need an incident tool. If an app's first download from Azure fails, the browser retries once from our servers with the same build. If Azure is fully down, on-call switches the default source to our servers.
- **Distributed coordination, concurrency, or consistency?** There's no global switch. Servers update one at a time, so for a while the fleet runs two builds. We keep that safe by keeping each page on one build: the server writes the exact versions into the page, and every download uses an exact version URL. Each server is out of rotation while its version list changes, because those writes aren't coordinated across servers.
- **Performance bottlenecks or resource constraints?** The old deploy copied gigabytes to every server on every release. Now each build uploads once to its own folder. Files served straight from our US servers were slow for users far away, so public production puts Akamai in front. Embedding the version list in the page removed a request and made first load 5% faster. [After a failed deployment, I also tuned our uploads to Azure Storage.]
- **Operational complexity?** Two release paths while the old one stayed as a fallback, 12 clouds with three hosting setups, and partners on an old integration path. I kept it manageable by making every source a plain file server and keeping one version list as the only source of truth.
- **Migration or backward compatibility?** There was no cutover day. The old deployment kept running as a manual fallback until the new path was proven. Partners kept their old URL, which I pointed at an exact version instead of a copied folder.
- **Ambiguous requirements?** "Keep working during an Azure outage" didn't say how. I first read it as "both sides ready before launch." My manager and I agreed that the old path with a manual switch met the requirement for the first release. [Which clouds needed which hosting also took a while to settle.]
- **Unfamiliar technologies or systems?** IIS rewrite maps and server variables, Front Door routing rules and ring weights, and the Portal's ASP.NET code. I learned them from the docs and by testing changes in PPE.

### Personal contribution

- **What did you do yourself?** I built the Azure side, then the non-Azure side when SRE withdrew. I wrote the redesign and presented it to the team leads. [I also wrote the deployment scripts and the browser loading changes, and I'm adding the UI test stage.] SRE owns the servers, load balancers, and deployment tool.
- **Which decisions did you personally make?** Version folders plus a version list. Shipping Azure first after my manager's challenge. Building the non-Azure side myself. Pointing the partner URL at an exact version instead of making partners move. Rejecting the custom proxy for IIS routing. And putting the version list in the page instead of a separate file.
- **Which components or interfaces did you design?** The shell, the version list, the Azure hosting and release pipeline, the routing behind the partner URL, and the redesign's promotion steps. I also added the ring parameter on-call uses to ask a specific ring which build it's running.
- **Which hard problems did you personally solve?** The August incident: I traced a generic server error through the IIS logs to a duplicate routing rule and removed it. The mismatched versions, by moving the version list into the page. And the non-Azure side, after the team that owned it withdrew.
- **Which trade-offs did you evaluate or change?** I changed my own definition of done, from both sides ready to Azure first with a fallback. I changed the fallback folder from a copy to routing. And in the redesign, I chose slower production releases with approvals and holds over speed.
- **What leadership, influence, or mentoring did you provide?** I led the project across my team, SRE, and partner teams. I escalated the SRE gap with a written record. I presented the redesign to the team leads. And I wrote the release steps for on-call and the local testing guide for app developers.
- **Which outcomes were you accountable for?** Delivery, including the delay. The release and rollback numbers. The system's health in production, including the August incident and its fix.

### Design decisions

- **What does the redesign change?** We upload each build everywhere, run UI tests against that exact build, and then promote it one group of servers at a time, with on-call approval at each step. Going live only updates the version list on each server, and the server writes that list into each page.
- **Why this architecture over another?** Version folders plus a version list make release and rollback the same cheap step. The alternative was keeping the app in the backend package, which kept us at weekly releases. For the redesign, routing on the server beat picking versions in the browser, because the server can pin every page to one build, and the browser doesn't need to know about rings.
- **Why these technologies and data model?** The data model is just a version list: for each app, which source and which exact version. It's tiny, so the server can write it into every page. It lives in the new site's own IIS config, because a database or new service is one more thing to keep up during an outage. The technology choices are under Action.
- **What was the hardest decision?** Where to store which version is live. A database or new service is one more thing to keep up during an outage. The Portal's config gets wiped by its weekly deployment. The server-wide IIS config is shared with the Portal and API, so a bad write hurts them too. We chose the new site's own IIS config and accepted that writes aren't coordinated across servers. That's why each update happens out of rotation.
- **Which alternatives did you consider, and why reject them?** The full list is under Action: a custom proxy, per-environment builds, routing everything through our servers, a catch-all fallback folder, sorting users into rings ourselves, and waiting for both sides. Each one either added code we'd have to maintain, broke "build once," or put load or failure risk where we didn't want it.
- **How did requirements and constraints shape the design?** The outage requirement meant two sources and nothing at runtime that depends on a database or new service. "Build once" meant one build promoted everywhere, so anything that differs by cloud lives on the server, not in the build. And 12 clouds meant no per-cloud code, just different sources in the version list.
- **How did the design change after testing or production feedback?** The fallback folder became routing to an exact version. The separately fetched version list moved into the page. Two copies of the version list became one. In testing, a timed-out script could still run later, so timeouts don't trigger a retry. And after the incident, upload and promotion became separate steps.
- **Any recent design change?** We kept the version list in two places, a public JSON file and the server's routing setting, and every script had to keep them in sync. We made the routing setting the only copy. The JSON is generated from it on each request, and neither browsers nor the CDN cache it.
- **Why not health-check or retry everything?** A health check adds a request to every healthy page and still doesn't guarantee the next download. A blanket retry can load an app twice after a timeout, or retry an app that already half-started. So we retry only when the first download fails outright, and a timeout doesn't trigger a retry.
- **Are the apps fully independent?** Mostly. Each app has its own version, but shared libraries load once from the main page, so a shared change ships the main page too.
- **Open tab during a release?** It keeps its old versions until it refreshes. We don't automatically delete old builds, so its files are still there.
- **Is the switch atomic?** On one server, effectively yes, because it's out of rotation while we change it. Across the fleet, no, but each page sticks with one build, so no page mixes two.

### Trade-offs

- **Simplicity versus flexibility?** I chose simple. Every source is a plain file server, and the server picks versions with built-in IIS rewrite rules instead of custom code. We give up custom ways to split users across rings, but Front Door's traffic weights already do that.
- **Performance versus cost?** Akamai in front of our servers costs money, but users far from our US datacenters would otherwise be slow. Keeping old builds on disk costs storage, but it means rollback needs no upload.
- **Consistency versus availability?** Across the fleet we favor availability, and within a page we keep consistency. Servers update one at a time, so the fleet runs two builds for a while, but each page sticks with one. If an app's download from Azure fails, we retry from our servers with the same build, never a different one.
- **Build versus buy?** We used what already existed wherever we could: Azure Storage, Front Door, Akamai, and IIS's built-in rewrite rules. We built only the thin parts: the shell, the version list, and the release scripts. I rejected a custom C# proxy because it would rebuild what IIS already does.
- **Delivery speed versus maintainability?** Shipping Azure first was faster, but it meant maintaining two release paths for a while. I accepted that because engineers got the benefits sooner, and the old path doubled as our fallback.
- **Short-term mitigation versus long-term redesign?** During the incident, I removed the bad config file with a script to restore the page. Then I fixed the build so an app's output can't include that file. The long-term fix is the redesign, where uploading never touches what's live.
- **Reliability versus operational complexity?** The redesign adds on-call approvals, 24-hour holds, and per-server rotation steps, and we keep old builds on disk. That's more work per release. I accepted it because rollback is still fast, and a bad build on every server costs more than a day's wait.
- **How do 24-hour holds fit with ten releases a day?** The ten a day is the current system. [In the redesign, changes still ship to PPE all day, and production gets a daily batch that goes through the holds.]

### Production ownership

- **Monitoring and alerting?** [We watch page-load errors, portal error rates, and new incidents after each promotion.] Front Door logs go to Log Analytics, and I've used them to debug blocked requests. Our UI components also report usage and errors automatically through our telemetry library.
- **Meaningful service-level indicators?** [The share of page loads where every app's code loads. We alert when it drops after a promotion, split by app and by source.] On the release side, I track rollback time and how often we release.
- **On-call responsibilities?** I lead the weekly frontend on-call handoff. [I'm also on the rotation.] In the redesign, on-call approves each promotion and can switch sources if Azure is down.
- **Production debugging?** In the August incident, the browser only showed a generic server error. The IIS logs had the specific one, a duplicate config entry, and that led me to a config file inside one app's folder.
- **Root-cause analysis?** Three things lined up. A build change started putting a server config file into one app's output. The upload copied it to every server before canary, so canary couldn't contain it. And our checks were blind: the partner's old path was already broken in our test environment, and UI automation wasn't running.
- **Reliability improvements?** Rollback from 20 minutes to 3. A retry from our servers when an app's Azure download fails. The version list in the page, so a page never mixes builds. And in the redesign, uploads that never touch what's live, UI tests on the exact build, and on-call approval at each step.
- **Capacity planning?** [About 100,000 page loads a day across about 40 servers.] Public production puts Akamai in front of our servers, so most downloads come from its cache, not our machines. The government clouds already serve everything from our own servers.
- **Load testing and scaling limits?** [We haven't load-tested a full public failover yet. That's the next test I'd run, because the limit is our own servers if Akamai has to fetch everything from them at once.]
- **Deployment, rollback, and migration strategy?** Build once, upload everywhere, test that exact build, then promote ring by ring. Rollback is the same promotion pointed at an older build that's still on the servers, with no rebuild and no upload. [In an emergency, the on-call engineer can skip the 24-hour holds.] We migrated with the old path kept as a manual fallback until the new one was proven.
- **Failure recovery?** Fast rollback covers a bad release. A second source covers outages:
    - **One app's download from Azure fails:** In public production, the main page comes from our own servers, and app code comes from Azure. If an app's first download from Azure fails outright, the browser retries once from our servers with the same build. A timeout doesn't trigger a retry, because in testing a timed-out script could still run later and load the app twice.
    - **Azure is fully down:** The on-call engineer switches the default source to our own servers. New page loads pick it up, and open pages need a refresh. This keeps the app's code available. Our APIs and sign-in have their own recovery plans.
- **How do you know a release is bad?** UI tests run on the exact build, a person approves each step, and we wait 24 hours after the first two. [We watch page-load errors, portal error rates, and new incidents.] Each server must pass its health check to rejoin.
- **Why no automatic rollback?** [A bad frontend release usually shows up as a few broken pages, not a clean health signal. So we keep a person in the loop and make rollback fast instead.]
- **Where does the redesign stand?** [It's built and tested in code, and PPE is next.]

#### The August incident

- **What happened?** In August, part of the Troubleshooting page failed for about three hours. One app's files returned server errors, because a config file inside its folder duplicated a routing rule the server already had.
- **How were users affected?** The retrospective counted 150 affected customers. They couldn't use that part of the Troubleshooting page. The rest of the portal, including the other Troubleshooting tabs, kept working.
- **How did you diagnose it?** I used the IIS logs to get past the generic server error. They showed a duplicate config entry, which led me to a config file inside one app's folder.
- **How was it resolved?** I removed that file from the affected servers with a PowerShell script, then checked the page and APIs by hand to confirm recovery. We also redeployed the app's files.
- **Which immediate and long-term changes followed?** Immediate: the cleanup script, and a build fix so the app's output no longer includes that config file. Long-term: the redesign, where uploads never touch what's live, UI tests run on the exact build, and every promotion needs on-call approval.
- **Why didn't your checks catch it?** A partner was still using an old integration path that was already broken in our test environment, so testing couldn't catch a new break on it. Our UI automation wasn't running. And the upload copied files, including that config, to every server before canary.
- **What prevents it from happening again?** I fixed the build so an app's output no longer includes that config file. The redesign covers the wider problem. Uploads go to new folders that no live page uses, UI tests run against that exact build, and each promotion needs on-call approval. So a bad file breaks a build no user is on yet, and the tests should catch it there. [The partner has also moved off the old integration path.]
- **What did the incident teach you?** To fix the class of problem, not just the instance. Removing the bad file fixed that day. The lasting fix was making sure no single step can reach users before a check, and that the checks actually run. I'd treat incidents at Datadog the same way: the follow-up isn't done until the same kind of failure can't happen the same way again.

### Collaboration and technical leadership

- **What happened with SRE?** Their engineer left, the replacement got pulled away, and they withdrew. I escalated through both managers and my skip manager, then built it myself. A dependency I don't control is still my risk, and escalating gives visibility, not people. Now I break big projects into milestones, name every dependency on another team at kickoff, and report by milestone. If a dependency's staffing changes, I act on the first change and ask the managers to choose: more people, less scope, a later date, or I take it over.
- **Influencing decisions without authority?** SRE didn't report to me. I made the gap visible with weekly, then daily check-ins and a group chat with both managers and my skip manager, so status and escalation were on record. When that didn't produce people, I took the work on myself.
- **Working across team or organization boundaries?** SRE for the servers, partner teams for the old URL and integration path, and the app teams that ship on the platform. For each, I kept the interface they depended on working while I changed what was behind it.
- **Mentoring engineers?** On this project, I taught through what I wrote and ran: the on-call release steps, the local testing guide, and the weekly on-call handoff. My main mentoring story is from another project, Values Q10.
- **Raising engineering standards?** The redesign sets rules for every release: uploading never changes what users see, UI tests run on the exact build, and each promotion needs on-call approval. I also fixed the build so an app's output can't carry server config.
- **Handling disagreement?** My manager disagreed with my plan to wait for both sides. I listened, saw that the old path with a manual switch covered the outage requirement for now, and changed my plan.
- **Building consensus?** After the incident, I wrote the design and presented it to the team leads. [The main pushback was the 24-hour holds, and we settled on a daily production batch.]
- **Creating clarity in ambiguous situations?** "Keep working during an Azure outage" was vague, so I turned it into specific behavior: retry one app from our servers if its Azure download fails, and switch the default source if Azure is fully down. I also wrote down how on-call can see which build each ring is running.
- **Balancing stakeholder needs with engineering constraints?** Partners needed their URL to keep working. I needed releases that don't copy over live files. So I kept the URL and changed what's behind it.
- **Helping others make better technical decisions?** I wrote the on-call release steps, including how to check which build each ring is running. I also wrote the guide for loading your local code against real environments, so engineers can test with real data before they merge.

### Learning and reflection

- **What did you learn, and what would you do differently today?** The biggest lesson is that safety has to come from the system, not from people being careful. I'd set the rules the system must never break on day one, ship a safe partial version sooner, and turn cross-team risk into a decision early. Those carry straight to Datadog, where a bad release reaches many customers at once.
- **Would you choose a simpler architecture?** Yes, in places. My fallback folder was an extra moving part that every release had to update, and it added more risk than it removed. I've learned to be suspicious of safety features that bring their own moving parts. The simpler design, plain file servers and one source of truth for what's live, is also the safer one.
- **Would you add observability earlier?** Yes. We leaned on tests and people noticing problems, and our UI tests weren't even running when the incident hit. I'd decide on day one what "healthy" means for users, measure it from the first release, and make sure the checks themselves are watched. [For this system, that's the share of page loads where every app loads, split by app and source.]
- **Would you change the rollout or migration strategy?** I'd make every step before the final switch harmless to users, with a person approving each step to production. Our rollout looked staged, but one early step already reached everyone, so the stages didn't protect us. The lesson is to check what each step can actually reach, not what it's called.
- **Would you test more failure scenarios?** Yes, the in-between ones. I tested before and after, plus the obvious outage, but not a half-finished rollout or a bad file inside an upload. Real failures tend to happen in those middle states, so that's where I'd test first, [including a full failover under real load].
- **Would you validate assumptions sooner?** Yes. Two of my assumptions, that an upload couldn't affect users and that two parts would always match, went untested until production proved them wrong. Now I list the assumptions a design depends on and try to break the riskiest ones early.
- **Would you involve stakeholders earlier?** Yes. I'd ask the teams that use a system how they use it before I decide what's public, so nothing turns into a promise by accident. And I'd get a firm commitment from teams I depend on at kickoff, with a date and an owner, not just a person's time.
- **Would you make different performance, cost, or reliability trade-offs?** I'd pay for safety earlier. Approval steps and waits slow releases down, but a bad release that reaches everyone costs far more. I'd rather start safe and speed up with evidence than start fast and add safety after an incident.
- **Would you lead or collaborate differently?** I'd turn risks into decisions sooner. When a dependency first slipped, I'd go to the managers with a choice, more people, less scope, a later date, or I take it over, instead of more check-ins. And I'd define "done" as the smallest useful piece that's safe to undo, not the full design.
- **What did you learn as a lead?** That "done" isn't my complete design. It's the smallest piece that solves the real problem and can be safely undone. My manager pushed me on that, and shipping Azure first got engineers faster releases while the rest was still being built. I'd lead the same way at Datadog: get value to people early, with a safe way back.
- **How did the lesson change a later decision?** The redesign is the clearest case. I didn't just patch the incident. I changed the system so a mistake gets caught before it reaches users, no matter who makes it. That's the habit I'd bring to Datadog: fix the class of problem, not just the instance.

## AI in your workflow

Use this if they ask how you use AI. Same shape, about 2 minutes.

**Headline:** Used an AI coding agent to compare options for the release redesign, then rejected its custom proxy for a simpler design built on IIS routing and our CDN.

> **S - Situation:** After the August incident, I had to redesign how builds go live across Azure, our own servers, and 12 clouds. I also wanted to leave the Portal's code alone, because we're retiring it.
>
> **T - Task:** I wanted to compare designs quickly across the Portal, IIS, and Front Door. I own this system in production, so every idea still had to hold up under my review.
>
> **A - Action:** I gave an AI agent our code and the constraints and asked for options. One draft was a custom handler in the Portal that fetched each page itself and passed every file through. I rejected it. It rebuilt what IIS already does, served every file from our US datacenters, which is slow for users in India, and tied releases back to the Portal. I asked for a server-side design using built-in features, and we got to IIS rewrite maps for the version, with Akamai in front of our servers. It also drafted on-call steps that said to read the public version file to see what's live. That was wrong. Front Door splits traffic across three rings, so you'd get a random ring's file. I had it undo that and added a ring parameter so on-call can ask a specific ring. Nothing it writes merges without my review, lint, and tests.
>
> **R - Result:** I had the design in front of the team leads [within two days]. It's simpler than the first drafts: no custom proxy, no new Portal code, and every source is a plain file server. The on-call steps now check the right ring.
>
> **L - Learning:** AI is fast at reading code and listing options, but it doesn't know our constraints, like which app we're retiring or how traffic splits across rings. So I give it those up front, treat what it writes as a draft, and check it against how the system actually behaves. At Datadog, AI-written code would get the same reviews, tests, and rollout as anything else.

### How you use AI today

- **Exploring implementation or design approaches?** For the redesign, I had it lay out ways to pick versions, then pushed it from a picker in the browser to routing on the server with IIS rewrite maps.
- **Generating boilerplate or routine transformations?** Moving admin pages from Angular to React. I have it write a migration plan first, get the plan reviewed as a PR, then implement from the plan in a fresh session.
- **Writing, expanding, or reviewing unit tests?** It drafts tests, and I cut the ones that prove nothing, like tests for a simple pass-through API call. For flaky-test fixes, I have a second agent review the first one's changes and explain why each is needed.
- **Understanding unfamiliar APIs, codebases, or technologies?** The Portal's ASP.NET code, IIS rewrite maps, and Front Door rules for the redesign. I point it at the code and docs and ask it to explain how a request flows.
- **Refactoring code?** Upgrading our shared repo's build tool to a new major version. It reads the release notes and makes the changes. I run the full validation in CI, because building every app at once won't fit on a laptop.
- **Identifying simplification opportunities?** It's weaker here than people expect. Left alone, it tends to add code, like a new helper next to an existing one. So I ask for less code directly and check for reuse in review.
- **Debugging issues?** Failing builds and flaky tests. I give it the pipeline logs and have it find the cause. I don't accept fixes that just add timeouts, because that hides the real timing problem.
- **Generating investigation hypotheses?** I pull an incident's details and customer impact into the chat through our incident tool's connector and ask what could explain the symptoms. [Each idea is a lead to check in the logs, not an answer.]
- **Summarizing documentation?** Release notes before a tool upgrade, Azure docs like the storage upload performance guide, and our own design docs before I change related code.
- **Comparing technical alternatives?** For the redesign: Front Door backup origins versus our own servers behind Akamai, and picking versions in the browser versus on the server.
- **Accelerating investigation of complex systems?** Tracing how a request moves through Front Door, IIS, and the shell, so I could write correct on-call steps. It got the ring split wrong the first time, which is exactly why I check.

### How you stay in control

- **Do you review AI-generated code?** Every diff, the same as a teammate's. I've thrown away a whole agent-built branch and restarted from a written plan, using the old branch only as a reference.
- **Tests, static analysis, and security checks?** Lint and tests run through the repo's normal commands, and the PR pipeline runs them again [with security scans] before anything merges.
- **Benchmarking performance?** I measure performance claims myself instead of trusting them. [The 5% first-load gain from moving the version list into the page came from measuring before and after.]
- **Validating resource usage?** When it planned to build every app in parallel for the build tool upgrade, I moved that validation to CI. It also set a test worker limit inside one app, and I moved it into the shared test config instead.
- **Checking assumptions against docs and system behavior?** It assumed the public version file showed what's live, but Front Door splits traffic across rings. It also insisted we were on an older version of our build tool than we were. I check claims like these against the docs and the running system.
- **Rejecting suggestions that don't fit?** The custom proxy in the Portal. A duplicate query helper when one already existed. And changes to our shared telemetry setup that the task never needed.
- **Protecting confidential data?** [I use only company-approved tools inside our own repos, and I don't paste secrets or customer data anywhere else.]
- **Following security and AI-usage policies?** [I use the approved coding assistant and internal connectors, and AI-written code goes through the same review, pipeline, and rollout as any other code.]
- **Treating AI as an assistant, not an authority?** It proposes, and I decide. On the redesign, the key choices, routing on the server and leaving the Portal's code alone, were mine.

### How your workflow has evolved

- **How did you start using AI?** [I started with inline autocomplete for small functions and tests.]
- **How has your use become more selective or sophisticated?** Now I start with a written plan, get it reviewed like any PR, and then have the agent implement it. When a review catches something, I update our repo instructions so the next session gets it right. Before it goes deep, I ask it to step back and check whether we're headed the right way. For risky changes, a second agent reviews the first one's work.
- **How do you keep it consistent with your codebase?** I added repo instructions for our React patterns, like which form and component libraries to use, so the agent follows them without being told each time.
- **Where does AI save meaningful time?** Reading code I don't know yet, first drafts of scripts, tests, and docs, and turning a bug into a small repro another team can act on. [It gets me to a reviewable first draft in about half the time.]
- **Where do you deliberately avoid it?** [I use only approved company tools with internal data, and I don't let it make design calls or run production changes. It drafts, and I decide.]
- **A poor suggestion you rejected?** The custom handler in the Portal, from my main AI answer. Another: a flaky-test fix that only added timeouts, which would have hidden the real timing problem.
- **How do you validate AI-generated work?** I read every diff and run lint and tests the same way CI does. For risky changes, I have a second agent review the first one's work and explain why each change is needed. For UI changes, I load the branch build against our test environment and try it myself.
- **How has AI changed how you investigate, implement, or review?** Investigate: I get a first map of unfamiliar code much faster. Implement: I write the plan and constraints first, because that's what the agent needs. Review: I review more code than I write, so I've gotten stricter about reuse and size.

### Your view on the future

- **Where is this going?** AI will write more of the first draft. Engineers still own the requirements, the design, and what reaches production. So checking work matters more: good tests, careful review, and releases you can stop and roll back fast. That's the same thinking behind the redesign.
- **Who owns requirements, architecture, and decisions?** Engineers. AI can propose a design, but it didn't know which project we're retiring or how our traffic splits. The person who's on call for the system has to make the call.
- **Does human review still matter?** More than before, because there's more code to review and it often looks right. The on-call steps it wrote read fine and were wrong.
- **Do production, security, and quality standards still apply?** Yes. Same pipeline, same rollout, same on-call. AI-written code doesn't get a faster path to production.
- **How do you decide when to use it?** By risk and by how well I can check the result. Work with good tests, like a page migration, I hand off more. For the release path, I use it to explore and draft, and I make the calls.

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

- "What's a recent production problem that made your team rethink part of its design?"
- "Where does Datadog work well for debugging your own services, and where do you still reach for other tools?"
- "What separates a strong senior engineer on your team from someone who's just good at shipping features?"
