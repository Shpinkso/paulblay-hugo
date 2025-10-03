+++
title = "The agility Challenge for Embedded Software"
date = "2020-12-02T11:46:20+01:00"
tags = ["agile"]
categories = ["embedded","delivery"]
banner = "img/banners/banner-4.png"
authors = ["Paul Blay"]
+++

If you’ve ever worked for a business that has it’s core focus in the embedded software space, I suspect you are more likely to have had to tolerate software development practices from 20 years ago. If you’ve read many books on Agile software development, DevOps or other modern practices, you may also have noticed that they almost all talk about software that targets a server or website, possibly a PC. But unless you’re reading a very different library to me, you’ll not have seen much talk about embedded software. Why is this?

First of all, “Embedded software” is a little nebulous (a mobile phone could be considered an embedded platform, but these days has modern PC rivalling specs & connectivity) – for this article, a platform can be considered more “Embedded” the more resource constrained it is (I’m talking low-cost, low power devices with minimal or no UI) and/or the more application specific the hardware is (i.e. ASICs “Application Specific Integrated Circuit”).
Embedded Software is (unfortunately, as I’m such an Agile nerd) what the majority of my career has focussed on. But I’m lucky, I’ve experienced life outside this world too. Working in IoT you start to see how software for a cloud platform can operate when done well – suddenly all those great ideas touted by the books, conferences and blogs can be seen in action.

THIS is how I got hooked. THIS is the way things should be done.

Effective agility is a major challenge for the embedded software world though…. Probably not an insurmountable one, but a much bigger one than the platforms they write the books about.

In this article I’ll identify the core reasons why I think it’s such a challenge, based on my experience of driving Agile transformations in the teams I’ve managed and businesses I’ve worked for.
# Hardware Production Timelines and Costs
Software agility relies on the fact that software is, as it’s name suggests, “soft”. It can be changed easily (architectural and readability considerations aside) and cheaply. Hardware on the other hand is “hard” – usually time consuming and expensive to change.
For those in the cloud space, hardware has become almost invisible, abstracted far away from your software with the use of virtual machines and containers. You need another server? No need to gear up a production line, nor even place an order with a retailer – it’s yours, to your specification, in literal seconds and at miniscule cost.
With embedded, this is a very different story. If you’re developing a new product, that product will be painfully expensive and time consuming to build. As a result, the company is going to be very twitchy about everything being ready according to a long, rigid, hardware project plan. The software timeline is often intrinsically tied to the hardware timeline.

# Inflexible Customer Contracts
Certainly not limited to embedded, but more likely due the closely coupled hardware aspect. Customers for your new embedded offering may be more likely to put in place heavy, up front, contracts with late-delivery penalties – this renders business agility void which, I’d argue, thwarts technical agility for all intents and purposes (if, indeed, those two concepts can be separated).
Lest we forget: customer collaboration over contract negotiation

# Resource Limitations
I’m cheating a bit here as I’m using this as a literal definition of “embedded”, but embedded systems are often extremely resource poor due to the heavy focus on BOM (Bill Of Materials) costs. The BOM is a serious consideration for any new electronic device. Every cent on the BOM is multiplied several times to get to a list price, as the product navigates its way from the production line onto the shelves. This isn’t the only pressure, there’s also the fact that these devices are often portable and reliant on a small battery, with precious limited power, to function.

The power, memory, and processing limitations that embedded platforms face are often seen as a significant challenge when developing embedded applications. The focus tends to be on how many features can be included and how the device manages these in various power states, but the implications are far wider than this.

In order to squeeze performance out of highly resource constrained devices, certain decisions can be made that make agility difficult. Some examples include:

### Development Language Selection
No software developer in their right mind would be choosing assembler or C as the language of choice for anything other than performance reasons. C++ is the highest level development language I’ve seen used for an ASIC.
The impact of this choice, while understandable, is low readability and a lack of support for modern development tools and techniques.

### Architecture and Code Cleanliness
I’m certainly not saying that it’s impossible to develop cleanly architected code on an embedded system, but there does seem to be such a focus on resource limitations that often code readability and efforts to ensure low coupling are de-prioritised in order to squeeze that extra bit of performance out of the device. I’m sure this is not limited to embedded systems, but it is a pervasive pressure on them.

Why does this create a challenge for agility? Low readability impacts the speed at which code can be understood and changed, high coupling reduces the safety of making changes without unwanted side effects. Effective agility requires that you can make software changes with maximum speed and minimum uncertainty.

 

# Testability
A critical element of agility is having high confidence in the robustness of your software at all times. In order to achieve this confidence, you need effective automated testing.
Embedded suffers with several significant testability challenges.

### Speed
How quickly can you run a test for new code on the target device? Typically the device needs to be re-programmed before you even start the test, this can take significant time depending on the size of the application the NAND (common low-cost non volatile memory used in embedded systems) write speed and a host of other potential bottlenecks.

On top of this, you typically can’t run the test framework on the device itself due to resource constraints, so a test machine will be poking at it over various IO interfaces and polling on responses.

This may only increase test run time by a matter of milliseconds per test, but these milliseconds quickly add up.
For effective agility, we’re going to want to complete a build, setup, test and teardown within a reasonable time to enable continuous integration.

### On-Target Testing Reliability
What is worse than slow test suites when trying to establish continuous integration? Flaky tests!
What’s the most infuriating cause of flaky tests? Flaky hardware.

You’re likely to be running on-target testing using numerous 3rd party devices such as Flash programmers, signal generators, USB hubs, programmable power sockets, adaptors, wires and a host of other ad-hoc hardware that may not be designed for prolonged test robustness. On top of this, for the most critical phase of your project you’ll be running tests on pre-production hardware – highly likely to be less than flawless.

### Write Cycle Limitations
Partially due to the nature of NAND flash, but exacerbated by the likelihood that you’ll be using close to 100% of it due to the resource constraints we covered earlier, plus the limited wear-levelling options you have when programming devices for test.

For those not familiar with NAND flash, it’s typically the non-volatile memory used in SSDs, USB flash drives, memory cards and other embedded devices. It’s low cost and decently fast, but suffers from some drawbacks like memory wear. Memory wear is, as it’s name suggests, is a limitation in which any particular block of memory has an average number of write/erase cycles before it becomes unusable. The limit is large, but CI runs a lot.

It’s not unusual to see target hardware start failing well within a year due to this limitation, in my experience.

# Customer Feedback Hurdles
What is agility without feedback? The ideal place to get this feedback is from customers. We suffer on this front with embedded development too, here are a few of the key reasons.

### Your Customer Needs Your Hardware
In order to be any use at all, the customer(s) need your hardware in order to try the product and provide feedback. Unfortunately, the time you could really use this the most is before you’ve hit mass production. Your walking skeleton is ready, but you only have a dozen devices from a short, low cost (high cost per unit, low cost in total) pre-production run.

No one has this problem with PC software, a website or a cloud service – all the hardware required for those are ubiquitous.

### Connectivity Limitations
A device without connectivity can’t be updated. This is becoming less of a problem over time as IoT takes off (replaced with a myriad of other problems), but even if a device has an active connection to the internet, there are significant constraints around the connectivity needed to provide software updates.
Is it acceptable to drain a bunch of battery power or interrupt functionality to perform a SW update & how often?

### UI Limitations
How do I get the customer feedback once we’re out in the field? How can we check with the user if it’s ok to accept a SW update and reboot?

# Nice Rant - So What Are Our Options?
I think there is some value in just raising awareness of the challenges & opening it up for debate; but it’s fair to say that it’s even more useful to suggest ways to address these challenges, so here are my 2 cents:

### Hardware Production Timelines and Costs
Probably the most challenging aspect as agility is only valuable when change is low cost. Technically, though, there is very little difference between long term planning for hardware and long term planning for marketing/key demos/investors. There key here is to identify your options for iterative HW development early.

This may be achieved with Emulation, Simulation, mimicking functionality by strapping existing hardware together, and/or finding a manufacturing partner that specialises in rapid prototype development (they do exist).
Each of these options come with nuanced limitations as to how well they can simulate your targeted product along with differing benefits to you and your customers.

Identify your priorities for Hardware agility (e.g. Verifying software logic, demoing real world use, the importance of form factor, key areas for feedback) and choose the most appropriate options.

### Inflexible Customer Contracts​
Although a common challenge for agility in other fields, I do believe embedded is particularly hard hit on this one.
The most affective approach you can employ here is to try to work with your customer(s) to take a step back from the detailed requirements list. What are the outcomes that the customer wants to achieve, and how would they prioritise them? This can be a tough conversation, but your goal is to understand the real business value of the product, from your customers view.

From this, collaboratively build a contract that identifies the required outcomes, rather than specific, detailed outputs. This both gives you the required wiggle room to manage scope, build an early walking skeleton and provides you with an opportunity to get creative on the work not done, all while addressing the customers real value rather than ticking off a requirements list.
This will not be perfect and is not the end of the story, of course, close customer collaboration and feedback needs to be maintained throughout.

No doubt this is a poor second place to a rolling service contract & requires a customer that’s willing to collaborate, but will be a step in the right direction.

### Resource Limitations
This is a challenge that most embedded product developers are fully aware of and will typically create early evaluation prototypes with increased resources to allow for a smoother software development process.

This does not address the issues around selection of programming language and adherence to good architectural & development practice in order to enable agility. The first question to ask ourselves is “Are we really improving efficiency when we sacrifice clean architecture and code?”, how good is our compiler at optimising for us? These are not questions that can be answered wholesale, but consider refactoring some area of the application and comparing code size and execution clock cycles before and after. No doubt some areas are more efficient in assembler, but how would an OO structure actually compare to Functional?

The ASICs that a certain company I worked for designed had the vast majority of the firmware written in C++ instead of C – these ASICs were all about efficiency, powering USB hubs supporting multiple displays and other peripherals at lightening speed. It can be done.

### Testability
There really is no substitute for testing on target, but you can look at ways to ensure it’s not throttling your software development pipeline.

At an embedded security company I worked for, we suffered with 30+ minute CI pipelines even after spending significant time and effort refactoring and parallelising the jobs. The target hardware were third party prototypes and we lacked simulation & quantity. We ended up taking the approach of building a framework with cross compiled firmware to run on a PC in order to test basic code logic and segregated the testing coverage between commit and overnight runs.

Commit testing included what we defined as ‘core features’, which included the functionality behind our core offering to the market. Overnight testing checked compatibility and performance across less typical configurations.

As for reliability issues with target test setups, I have considered setting up a website where those maintaining embedded CI rigs can suggest and review various hardware that offers good reliability and features relevant for CI. In my experience, there are a lot of shared needs across companies using embedded test setups. As for now, the best advice I can offer is ask the wider community, review what places like kernelci are using and other boardfarms for public domain software. Don’t pick cheap equipment, you’ll lose far more than you save on maintenance and debugging (and probably buying something else in the end).

### Customer Feedback Hurdles
Finally, then, how do we get the feedback we need?
To be honest, if your device does not have some form of data connection to the outside world, a lot of what I am about to suggest is not possible and it’s not within my expertise to advise on that, unfortunately. However, for those that do…
It can’t be overstated how important it is to design in a secure software update mechanism if at all possible – this is not just for providing customers with updates, but also to mitigate the huge security risks that IoT devices face (and I believe, these days, it’s written into law in many jurisdictions).

If you’re here are lacking the expertise locally, there are specialist companies now that offer solutions to enable secure software updates on embedded devices, along with IP protection and more. SecureThingz is one that I’m aware of.
Next up, logging. For any connected device, prioritise the ability to log the state transitions and accompanying timestamps of your device to a location that you can access. There are some legal considerations around this once the devices are in the field, so have a legal team advise you on what can and can’t be done. Your CI and local testing can help you hone your logging to be as useful as possible.

Finally, ensure you build a customer portal for capturing feedback, if your on-device options are limited. Ensure that for bugs and/or unexpected behaviour you’re able to identify the corresponding log and time in order to investigate.
Getting customers interacting with your product:

### If you’re working B2B

It seems obvious, but budget for and get early prototypes out to customers as well as to your engineers. There’s often a fear around showing something to a customer that isn’t polished, I believe this fear needs to be confronted and become fearless prototyping to be a standard way of working.
If it’s not possible to send physical hardware to customers, consider if there is a way to sensibly mimic the user experience of the product using simulation. If you anticipate this product to evolve on your roadmap, it will be a worthwhile investment.

### If you’re working B2C

It’s a little harder to manage, but getting early beta trials out is important. I’ve worked with companies like CenterCode that will manage the selection, distribution and contact with members of the public that are keen to try out new devices on the understanding that they won’t be polished. In my experience, you will get reasonably high quality, candid feedback from people who are engaged and understand that you are in development and want to help you deliver a great product.

So that is my overview of the challenges for embedded software development adopting Agile, I hope that some of it has been helpful. I’m very interested in differing opinions and options. I do think that this industry could benefit heavily from addressing some of these challenges and identifying any others that hold us back too.
Thanks for reading.