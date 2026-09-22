---
layout: post
title: "AI, Explain Yourself!"
date: 2026-09-20 13:03 +0800
categories: [notebook, data-science, artificial-intelligence]
tags: [explainable-ai, xai, autonomous-vehicles, machine-learning]
---
This term, I’m also taking **Contemporary Works in Data Science (SC09)**, and our first topic is something I honestly didn’t know had an entire field built around it: **Explainable AI**, or **XAI**.

For our first presentation, we had to review five research articles related to Explainable AI. My presentation focused specifically on **XAI in autonomous vehicles**, which turned out to be a pretty good way of understanding why explainability matters in the first place.

## Wait… AI Has to Explain Itself?

We’re already using AI in so many parts of our lives. We use it to write, search, recommend things, generate images, help us study, analyze data, and increasingly assist with decisions.

Most of the time, we ask it something, get an answer, and move on.

But what happens when the AI is making a decision that actually matters?

Imagine sitting inside a self-driving car. The car suddenly hits the brakes.

Okay. Why?

Was there a pedestrian?

Did another vehicle cut into the lane?

Did the system misread a shadow as an object?

Or did the car just decide that stopping in the middle of the road was a great idea?

> **“Trust me bro!”**

![Inside a self-driving car with the driver's hands off the steering wheel and a speech bubble saying “Trust me bro!”](/assets/posts/xai/trust-me-bro-self-driving-car.png)

<p class="image-credit">Photo: <a href="https://www.wired.com/">WIRED</a></p>

That is where Explainable AI starts to make a lot more sense.

XAI is essentially about making the results of machine-learning systems understandable to humans. In the presentation, we described it as allowing people to **comprehend and trust the results and outputs created by machine-learning algorithms**.

And that word *trust* is important.

Not blind trust.

More like: **give me enough information so I know when I should trust you.**

## Interpretability and Explainability Aren’t Exactly the Same

One thing I learned while preparing for the presentation was the difference between **interpretability** and **explainability**.

Interpretability is more about understanding *how the model itself works*. Explainability is about understanding *why it made a particular decision*.

For example, imagine a self-driving car has a simple rule:

> If a pedestrian is closer than the safe-distance threshold, slow down.

You can inspect that rule and understand the logic behind it. That is interpretability.

But after the car brakes, it could tell the passenger:

> “I slowed down because a pedestrian was detected entering the vehicle’s path.”

That is explainability.

The distinction sounded a little academic at first, but the more I thought about it, the more useful it became.

As a passenger, I probably don’t need to know the internal architecture of the neural network controlling the vehicle.

I just want to know why the car suddenly slammed on the brakes.

## What the Five Papers Say

The five papers approached XAI in autonomous vehicles from different angles, but they pointed toward the same challenge:

- **Dong et al. (2022)**, in [*Development and Testing of an Image Transformer for Explainable Autonomous Driving Systems*](https://doi.org/10.1108/JICV-06-2022-0021), showed how a system could predict a driving action and generate an explanation for it—but a convincing explanation is not necessarily the real reason behind the decision.
- **Kuznietsov et al. (2024)**, in [*Explainable AI for Safe and Trustworthy Autonomous Driving: A Systematic Review*](https://doi.org/10.1109/TITS.2024.3474469), presented XAI as useful not only for passengers, but also for designing, monitoring, validating, and assuring autonomous-driving systems.
- **Kenny et al. (2026)**, in [*Explainable Deep Learning Improves Human Mental Models of Self-Driving Cars*](https://doi.org/10.1038/s41586-026-10950-5), connected driving decisions to human-understandable concepts, making it easier to inspect what actually influenced the vehicle’s behavior.
- **Atakishiyev et al. (2024)**, in [*Incorporating Explanations into Human-Machine Interfaces for Trust and Situation Awareness in Autonomous Vehicles*](https://doi.org/10.1109/IV55156.2024.10588812), emphasized that explanations must consider what should be explained, who needs the explanation, when it should appear, and how it should be delivered.
- **Peintner et al. (2025)**, in [*Balancing Transparency and Control: The Impact of AI Explanation Detail on User Perception in Automated Vehicles*](https://doi.org/10.1016/j.trip.2025.101742), found that the level of detail matters: more explanation can improve acceptance, but too much can reduce clarity or give passengers a false sense of control.

Taken together, the studies show that a useful explanation must be **faithful, understandable, timely, and appropriate for its audience**. It should help people recognize both when the system deserves trust and when it does not.

And that leads to one of my biggest takeaways:

**More explanation ≠ more safety.**

## Maybe the Goal Isn’t Trust

Before studying this topic, I would probably have described Explainable AI as a way of making people trust AI more.

After reading these papers, I think that description is incomplete.

The goal shouldn’t be to make us trust AI **more**. It should be to help us trust it **appropriately**.

For autonomous vehicles, the best explanation is not always the longest or most technical one. It is the one that clearly reflects what the system is doing, arrives when it is needed, and helps the passenger judge the situation correctly.

So the important question is not only:

**“Can the AI make the right decision?”**

It is also:

**“Can we understand why it made that decision—and can we trust that explanation?”**

Apparently, *“trust me bro”* isn’t quite enough.

## References

<ol class="references">
  <li>J. Dong, S. Chen, M. Miralinaghi, T. Chen, and S. Labi. “<a href="https://doi.org/10.1108/JICV-06-2022-0021">Development and testing of an image transformer for explainable autonomous driving systems.</a>” <em>Journal of Intelligent and Connected Vehicles</em>, 5(3):235–249, 2022.</li>
  <li>A. Kuznietsov, B. Gyevnar, C. Wang, S. Peters, and S. V. Albrecht. “<a href="https://doi.org/10.1109/TITS.2024.3474469">Explainable AI for safe and trustworthy autonomous driving: A systematic review.</a>” <em>IEEE Transactions on Intelligent Transportation Systems</em>, 25(12):19342–19364, 2024.</li>
  <li>E. M. Kenny, A. Dharmavaram, S. U. Lee, et al. “<a href="https://doi.org/10.1038/s41586-026-10950-5">Explainable deep learning improves human mental models of self-driving cars.</a>” <em>Nature</em>, 657(8130):114–120, 2026.</li>
  <li>S. Atakishiyev, M. Salameh, and R. Goebel. “<a href="https://doi.org/10.1109/IV55156.2024.10588812">Incorporating explanations into human-machine interfaces for trust and situation awareness in autonomous vehicles.</a>” <em>2024 IEEE Intelligent Vehicles Symposium (IV)</em>, pp. 2948–2955, 2024.</li>
  <li>J. Peintner, C. Manger, M. Berger, and A. Riener. “<a href="https://doi.org/10.1016/j.trip.2025.101742">Balancing transparency and control: The impact of AI explanation detail on user perception in automated vehicles.</a>” <em>Transportation Research Interdisciplinary Perspectives</em>, 34:101742, 2025.</li>
</ol>
