+++
title = "A Policy for AI-enhanced software development"
date = "2025-10-07T08:52:20+01:00"
tags = ["LLM","AI"]
categories = ["delivery","people"]
banner = "img/banners/ai_in_sw_dev.jpg"
authors = ["Paul Blay"]
+++

The DORA research group at Google recently came out with an [AI capabilities model](https://cloud.google.com/blog/products/ai-machine-learning/introducing-doras-inaugural-ai-capabilities-model) and capability number 1 is to have a "Clear and communicated AI stance".
Given my experience so far talking to other leaders and on the ground, here's my proposal for what an effective AI stance could look like:

## Core Philosophy

> LLMs should amplify engineering cognition, not automate it

* **Human Ownership**: Engineers must remain the authors and owners of production logic.
* **Knowledge Retention**: We preserve and grow organisational understanding rather than outsource it.
* **Cognitive Augmentation**: Use LLMs to compress the time between _problem recognition_ and _informed decision making_.

## Effective Augmentation Patterns

### 1. Knowledge Synthesis & Search
Turning documentation into an accessible, converstaional knowledge layer.
**Examples**

* Semantic search across wikis, task management systems, souce control systems, document management systems, emails, instant messaging, etc.

* Summarising incident reports, design docs, and architecture reviews into digestible insights.

* Building an “Engineering Assistant” that answers: “Where is this handled?” or “Has anyone done this before?”

**Outcome**: Reduced onboarding time, less re-work, faster decision-making.


### 2. Engaged Pairing Partner
LLMs as a _thinking mirror_ rather than a co-author.

**Examples**

* Reviewing an engineer’s reasoning, not their syntax — “What assumptions am I making?”

* Prompting for test cases, corner conditions, or design trade-offs.

* Acting as a “silent peer reviewer” for PR descriptions, design proposals, or ADRs.

**Outcome**: Improves reasoning quality and self-awareness without diminishing problem-solving ability.

### 3. Organisational Memory & Context Capture

LLMs can observe patterns and generate summaries that humans rarely have time to maintain.

**Examples**:

* Weekly digest of code changes → mapped to system components and owners.

* Summaries of retrospective actions or recurring issues across teams.

* Change intelligence — “These systems are often affected when X changes”.

**Outcome**: Improved cross-team learning loops and system understanding.

### 4. Coaching & Skill Development

LLMs trained on internal standards can coach individuals on:

* Design quality (SOLID, clean architecture, readability).

* Security and compliance guidelines.

* DORA or generative culture principles (e.g. “How could you make this safer to experiment with?”).

**Outcome**: Scalable, personalised mentorship and continuous improvement.

## Guardrails

* **Transparency**: Always track when and how AI contributed to an artefact.

* **Verification**: Treat all LLM outputs as drafts requiring review.

* **Ethics & Trust**: No generation of source code, credentials, or proprietary data.

* **Learning over Delegation**: Encourage reflection: “What did this tool help me realise?” rather than “What did it produce for me?”.

Finally, an example framing for a narrative from the leadership team:
> “We treat AI as a cognitive amplifier. It doesn’t replace our engineers’ judgement — it makes their insight visible sooner. Our focus is not faster typing, but faster thinking.”

---

I'd like to see the wider industry focus less on how to get LLM's to generate more code and more on how to augment the capabilities and skills of existing staff and internal processes.

Thanks for reading!