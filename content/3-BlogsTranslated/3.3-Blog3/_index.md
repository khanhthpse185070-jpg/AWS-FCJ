---
title: "Blog 3"
 
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# Deliver Faster by Limiting Work in Progress

by Matthias Patzak on 04 MAR 2025 in Best Practices, DevOps, Enterprise Strategy| Permalink|  Comments | Share

Software development teams have always struggled to deliver features within the timeframe that businesses and customers expect. A recent BCG study found that over a third of respondents’ internal software development projects were delayed. Late delivery delays ROI and frustrates everyone involved.

Organizations face numerous challenges when accelerating software delivery, but one stands out for its outsized impact and relatively simple fix: working on too many things at once.
## The Multitasking Trap
A team has three six-week projects:

  * Project A: a customer-facing mobile app update
  * Project B: a critical security enhancement
  * Project C: a new API for partner integration

If the team context switches between projects, they get bogged down. You’ve probably been there, attending constant meetings and managing different stakeholder expectations. The team eventually completes all three projects around the same time:

  * Project A: 16 weeks
  * Project B: 17 weeks
  * Project C: 18 weeks

The impact is disastrous. The mobile app launches long after the peak shopping season. The delayed security update creates stakeholder anxiety, and the late API postpones partner onboarding opportunities.
![picture 1](/images/image3.3.1.png)
But if the team focuses on one project until they complete it, they can deliver the mobile app in just 6 weeks. They complete the security update by week 12 and the API by week 18. They still finish all the work in 18 weeks, but they give customers a valuable update 10 weeks sooner than if they context switched between projects. They fix security concerns 5 weeks sooner, and the overall process is more efficient.

## The Simple Solution: Work in Progress (WIP) Limits
You can shorten time to market with work in progress (WIP) limits—i.e., limiting how many items your teams work on at once.

When development teams at Siemens Health Systems started using WIP limits, they reduced delivery cycle time from 71 days to 43 days—a 42% improvement. The teams didn’t add resources or work longer hours. The same teams, completing the same amount of work, delivered value to customers nearly a month earlier. And quality improved significantly—the first-pass testing success rate rose from 75% to 95%. Focusing on fewer items at once leads to faster delivery and better results.

Little’s Law, which describes the average number of items in a stationary system over time, mathematically proves that delivery time increases with more WIP:

![picture 2](/images/image3.3.2.png)
where:

  * L = the average number of items in the system (WIP);
  * λ = the average number of items arriving per unit of time (throughput); and
  * W = the average time an item spends in the system (cycle time).

If 10 items are in progress (L) and there are 2 completions per week (λ), then each item takes 5 weeks (W):
![picture 3](/images/image3.3.3.png)
Double the WIP to 20 items, and delivery time doubles to 10 weeks—even with the same completion rate:
![picture 4](/images/image3.3.4.png)
If you want faster delivery, you have two choices: increase throughput (which requires more resources) or reduce WIP (which requires greater focus). You don’t need a large investment or complex transformation to start using WIP limits; it’s one of the most cost-effective improvement tools available.

## Use WIP Limits Where They Matter Most
WIP limits are most effective on bottlenecks. According to the theory of constraints, the throughput of any process is limited by its slowest step.

Value stream mapping helps you identify these constraints. It visualizes your entire development process— from concept to production—making it clear where work accumulates and bottlenecks form. You might discover a backlog of untested code or features waiting for deployment approval. These bottlenecks act as constraints that limit your overall delivery speed.

By strategically placing WIP limits at these bottleneck stages, you create a “pull” effect that regulates the entire system. When the bottleneck stage hits its WIP limit, upstream stages naturally slow down because they can’t push more work forward. This prevents work from piling up at the constraint and reduces the total amount of WIP in your system. Meanwhile, downstream stages can only process work as fast as it flows through the bottleneck.

In a typical development process, testing is the bottleneck. Without WIP limits, you might see 10 features being developed simultaneously, 6 waiting for code review, 8 stuck in testing, and 3 pending deployment—that’s 27 items in progress. By setting a WIP limit of 4 items at testing, you create a ripple effect: code review can’t push more than 4 items forward, so development focuses on fewer features at once. Now you might have 4 features in development, 4 in review, 4 in testing, and 2 in deployment—just 14 items total. With the same completion rate of 3 features per week, you’ve cut your cycle time nearly in half, from 9 weeks to less than 5 weeks.

## Getting Started: Your First 12 Weeks with WIP Limits
To start using WIP limits in your organization, choose a pilot team. Look for one that embraces change and struggles with their current workload—they’ll be your best partners in this effort. Gather the team and their stakeholders to outline each step from concept to production deployment in a value stream map. Pay special attention to stages where work tends to pile up—these areas will gain the most advantage from your initial WIP limits.

Find the bottleneck. Then set initial WIP limits to 70% to 80% of the current workload to create productive tension without disrupting delivery. In the example above about the typical development process, you would set an initial limit of six items in testing.

Measure the pilot team’s cycle time for four weeks. Count how many days each work item takes to finish. Track how many items the team completes each month (throughput). Time each step, like development and testing, then reduce the WIP limits at the bottleneck as teams adapt.

After the first 4 weeks, reduce limits by 10% to 20%. This range balances progress with practicality—hard limits cause resistance, but soft ones don’t drive enough behavioral change. Consider your team’s needs. A 10-person development team might start with 8 concurrent items and reduce to 6 as their completion rate improves.

Keep measuring the same things for 8-12 weeks. Look at the difference. Teams will complete work faster with fewer items in progress but finish the same number of items per month. A team that finishes three items per week would show the results in figure 2.
![picture 5](/images/image3.3.5.png)
Figure 2. Impact of WIP limits over 8-week period

When teams hit WIP limits, they should support active work (fixing bugs, improving code, updating tools, or sharing knowledge) instead of starting new tasks. Individual contributors may feel they’re working slower, but teams complete work faster and speed up overall delivery.

## Scaling Success Beyond the Pilot Team
Roll out and scale WIP limits across your organization. After a successful pilot phase, scale WIP limits, beginning with teams that regularly interact with your pilot team. They’ll already see the benefits through their daily collaboration. These teams face similar challenges and work under comparable requirements, making them ideal candidates for adoption.

Scale WIP limits gradually. Teams work at the story level, but larger initiatives often span multiple teams. Apply WIP limits at these higher levels too. Department leaders should limit active initiatives. When teams deliver consistently with WIP limits, leaders will use them at the portfolio level.

Extend WIP limits across your delivery process. Map the journey from the initial concept through production deployment. Many organizations discover that their process starts long before any team writes code. Apply WIP limits at each stage to maintain smooth flow throughout your entire delivery process.

## Stop Starting; Start Finishing
WIP limits don’t just deliver faster software today; they position your organization for tomorrow’s challenges. Organizations that use WIP limits to deliver software quickly can maintain speed as they scale.

Your development teams already have the capacity to deliver faster. WIP limits unlock that potential.

## About Authors
![picture 6](/images/image3.3.6.png)
Matthias Patzak joined the Enterprise Strategist team in early 2023 after a stint as a Principal Advisor in AWS Solutions Architecture. In this role, Matthias works with executive teams on how the cloud can help to increase the speed of innovation, the efficiency of their IT, and the business value their technology generates from a people, process and technology perspective. Before joining AWS, Matthias was Vice President IT at AutoScout24 and Managing Director at Home Shopping Europe. In both companies he introduced lean-agile operational models at scale and led successful cloud transformations resulting in shorter delivery times, increased business value and higher company valuations
