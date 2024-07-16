# Software engineering principles

> "Put another way, I started to believe that SDEs can be (or at least, should be) orders of magnitude more productive." -- [Steve Yegge](https://sites.google.com/site/steveyegge2/tin-foil-hats)

The goal of this document is provide an outline of how I understand software engineering conceptually. This document is particularly geared to software startups, or more generally, to software companies that are focused on doing more with less.

These principles can also be expressed as hypothesis. Most of what is written here comes directly from experience; but experience can be sorely biased and limited. That's why it'd be fruitful if we considered these principles as testable hypothesis, and discover whether they actually hold.

## tl;dr

- Principle/hypothesis 1: **software delivers value only by communicating, transforming and storing data**.
- Principle/hypothesis 2: **The absolute goodness of an engineering artifact consists of its reliability; reliability is four things: correctness, security, performance and durability**.
- Principle/hypothesis 3: **In the absence of a magic wand that creates it, an engineering product must be specified and constructed**.
- Principle/hypothesis 4: **The large variability in the outcomes of a software project, and the fact that even good software has to be rebuilt and extended, makes the *how* of building software critical for the success of any software project. Said variability makes it impossible to simply throw a linear amount of money at the problem.**
- Principle/hypothesis 5: **The key to specifying and constructing a software system is that those who specify and construct it must understand the system**.
- Principle/hypothesis 6: **The key to understanding a software system is to minimize its complexity -- which is the same as maximizing its simplicity**.
- Principle/hypothesis 7: **The sequence of software development (whether on a new or existing system) can be summarized as a linear sequence of Understand, Run, Test, Deploy, Log, Change. The writing of the system emerges from its understanding.**
- Principle/hypothesis 8: **Keep the URTDLC short, but not arbitrarly short, or bound to an inflexible amount of time.**
- Principle/hypothesis 9: **Overengineering is simply bad engineering. Avoid it like the plague. Beware of devops-induced complexity.**
- Principle/hypothesis 10: **Auto-activation allows to develop software systems that converge towards perfection, through the simple practice of detecting, and collecting errors, as well as targeting their root causes.**
- Principle/hypothesis 11: **A software system runs chiefly on morale; the three sources of pure engineering morale are ownership, relative ease and inner pride.**

## What does software do?

The starting point is to understand that the purpose and operation of software is strictly concerned with data. Software instructs computers to do certain operations. But those "operations" are merely communicating, transforming and storing data. The only reason we care about computers, and build our entire economy around them, is that they're extremely good at communicating, transforming and storing data. That's it.

Without data, software makes no sense, and has no economic value. The end goal of any software system is to enable the communication, transformation and storage of data.

If we had a better way than software (and the underlying hardware which makes software possible) to communicate, transform and store data, we'd all stop writing software, except perhaps for fun. Until that happens, software is of societal importance only because it is today the main way we humans work with data.

One day, I hope to give a fuller explanation of this [here](https://github.com/fpereiro/toois).

Principle/hypothesis 1: **software delivers value only by communicating, transforming and storing data**.

## The four qualities of reliability

Imagine you need a software system and that, fortunately, you can instantaneously create it by waving a magic in your possession. Imagine that it was a single use magic wand, so you want to get your wish right. From that perspective, I can see a single quality that's central to a software system (or any engineering product, really): **reliability**.

Something reliable is something that will perform exactly how you wish it to perform. This is still too broad, so let's try to outline the angles of what makes something reliable:

- Correctness: it does what it should do.
- Security: it does not do what it should not do.
- Performance: when you ask it to do something, it will take a small amount of time to do so.
- Durability: once it's working, it will keep on working just like it did at the very beginning.

Let's illustrate this with three examples: a bridge, an AK-47 and a software system.

Bridge:
   - Correctness: it allows you to go through it.
   - Security: you don't die or get hurt when you cross it.
   - Performance: it allows a certain amount of users to go through it without causing undue delays.
   - Durability: it lasts for as long as humans want it to last, without degraded correctness, security or performance.

AK-47:
   - Correctness: when you pull the trigger, it fires a bullet to where you aimed it.
   - Security: it doesn't blow up in your hand, or fire towards an unexpected direction.
   - Performance: as soon as you pull the trigger, a bullet is fired; and you can keep the trigger pressed to deliver continuous fire.
   - Durability: it lasts for as long as humans want it to last, without degraded correctness, security or performance.

Software system:
   - Correctness: it enables the data communications, transformations and preservations that you require from it.
   - Security: it doesn't allow undue access to data (whether read or write).
   - Performance: even if multiple people are using the system at the same time, the system will execute operations reasonably quickly.
   - Durability: it lasts for as long as humans want it to last, without degraded correctness, security or performance.

We could think correctness and security as the aspects of the engineering product that are concerned with a single use: what should happen (and should *not* happen) when we use it once. Performance is about function over a small amount of time (from use to result), whereas durability is about function over a long time (over the lifetime of the product).

Notice that this doesn't include any concern for cost. You could have a highly reliable product of engineering that could take a decade and billions of dollars to build and maintain.

If we consider the purpose of engineering products to be purely functional, and if we have a magic wand to make them happen, what we want is something that will function perfectly well over time. This quality of "perfect function" I'll summarize from now on in the term *reliable*. If something works, works well, and keeps on working, I (or we, or the entire human race) can simply rely on it. And that's all that we expect from it, as long as we have that magic wand.

Principle/hypothesis 2: **The absolute goodness of an engineering artifact consists of its reliability; reliability is four things: correctness, security, performance and durability**.

## From reliability to cost

The problem is, we do not have a magic wand to create engineering products (not even software systems!). Besides its nonexistence, there are two more interesting problems concerning the magic wand:

- **Specification**: we assume that "what we want" can be either clearly explained by us in a way that can be executed -- or that it can be read or interpreted from our minds.
- **Construction**: we assume that once we have specified what we want (or if the magic wand itself figured it out), it will instantaneously materialize without incurring a cost of any sort.

Assuming that it is *possible* to build reliable products of engineering, the two problems become *specifying* the product and *building* it -- or more specifically, the *cost* of specifying and building the product.

We separate these two stages, specification from construction, since construction must follow specification. Even if one subscribes to an iterative model of development, every single action must stem from a purpose -- and the specification is what provides purpose at any level of scale. Even if you rethink the picture with every brush stroke, you think right before executing the brush stroke.

The cost can be split in three components: calendar time; human time (hours of human effort); and number of resources required (steel, machine tools, trusses, data centers, etc.).

The second and third dimensions of cost can be approximated by an amount of money (ie: the cost of hiring humans is indistinguishiable from the cost of hiring a data center), but this is much harder to do with calendar time: while it's true that if you spend more money you'll be able to get things done faster, there's a certain incompressibility of time, and it is generally **not true** that if spending x will give you a product in y time, spending 10x will give you a product in y/10 time.

So the question that underpins the practical possibility of reliability is: given the resources we have, how can we specify and build a reliable product?

Principle/hypothesis 3: **In the absence of a magic wand that creates it, an engineering product must be specified and constructed**.

## Why software is different

Here I must completely depart from general engineering and only focus on software engineering, due to my absolute ignorance of the former and only relative ignorance of the latter. Then the question becomes: given limited resources, how can we specify and build a reliable software system?

Perhaps in general engineering problems, the resources for building a bridge or an AK-47 rifle have relatively clear lower and upper bounds. Depending on your know-how and perhaps luck, you might be able to do it for less or more, but not varying that much from a certain amount.

Do you need a 10m bridge over a river? If you are building over a tranquil river, with solid land on either side, great access to infrastructure, and good engineers and workers, it'll cost you X. If you're building over a turbulent river on sandy terrain, far away from cities and with unreliable personnel, it might cost you 4X. Let's just say that the difference between minimum and maximum cannot be over 10X for something that's more or less the same.

Not so in software engineering. The reality of software is that the cost of specifying and building a software system can vary *wildly* (anywhere from 10X to 1000X), depending on your know-how and approach. Perhaps this is because we have been building bridges for millenia, but software only for eighty years. Perhaps software is harder than bridges. Perhaps both.

For practical purposes, what matters is that **how** we specify and build software can make a difference of **orders of magnitude** in the cost of building software. And not only that: the **how** affects the ultimate reliability of the software system that it produces. Some ways of specifying and building software can make it essentially impossible to achieve a certain degree of reliability. A testament to this is the fact that a bridge failure is considered to be major news, but software failure hardly so.

Hence, **how** we build software is the central question, because it matters so much not just to cost, but also to its reliability.

What exacerbates this phenomenon is that software is not built just once, but rebuilt over and over to meet changes to its requirements. We build software systems with software (and not with hardware) because we need it to change. Put in other terms, *if we had a magic wand to build software, we'd have to wave it very often*. So the process of specifying and building happens constantly, and not just once, for a software system that exists for a certain amount of time. This exacerbates the impact of the wild variability of the cost of software.

Principle/hypothesis 4: **The large variability in the outcomes of a software project, and the fact that even good software has to be rebuilt and extended, makes the *how* of building software critical for the success of any software project. Said variability makes it impossible to simply throw a linear amount of money at the problem.**

## Understanding is the key to reliability maximization and cost minimization of software systems

Building software systems, particularly today, is very different from most engineering disciplines. The limiting factor isn't access to computing resources (computation, memory, network), but actually understanding what the damn thing is supposed to do. The main difficulty in specifying and implementing a software system is that we need to **understand** it.

This is remarkable. Most of engineering is concerned with building reliable products out of unreliable and costly materials. In software, for the most part, we have extremely reliable and almost free materials (barring very specific use cases like cryptocurrencies and training large language models, where you do need eye-watering amounts of computing resources). For the workaday designer/builder of a software system, our main challenge is to understand how we can organize these materials (which, in the case of software, are processors, memory and communications) into a coherent whole.

Understanding software is difficult for a number of reasons. Here's a few I can think of:

- **Abstraction**: it deals with data, and data is generally quite abstract. Our brains work better with concretions than abstractions.
- **Linearity**: data flows concern our prefrontal cortex (or what Daniel Kahneman calls System 2), which is for the most part sequential and slow. Compare this to our visual cortex, which processes a massive amount of data constantly.
- **Conceptual immaturity**: we're still developing conceptual tools that allow us to work effectively with data.

I contend that if a team has an excellent understanding of the software system they are building (or maintaining), they will almost certainly be able to build it (and maintain it) with a small amount of resources and a maximum of reliability. Conversely, a team with poor understanding of the software system they're working on will incur great costs to generate and maintain a system of poor reliability.

The curve over this two dimensional continuum is exponential: a crystal clear understanding of the system offers almost perfect reliability at a meager cost; and a remedial understanding of the sytem offers a generally unreliable system no matter how many resources are thrown at the system.

Given our limited cognitive resources to deal with the abstractions of software systems, the key to it all is for the humans that specify and build the system to be able to understand the system. The real value is found in truly understanding the problem, as well as our solution to it. Reliability maximization and cost minimization flow from it.

Principle/hypothesis 5: **The key to specifying and constructing a software system is that those who specify and construct it must understand the system**.

## Simplicity is the key to understanding

My guiding definition of simplicity is the one that Rich Hickey gives in his [Simple Made Easy talk](https://www.youtube.com/watch?v=SxdOUGdseq4). ChatGPT kindly summarized his definition for our benefit:
- Simplicity is about the absence of interleaving (complexity). Simple systems have fewer intertwined parts.
- Complexity arises from the interweaving or intertwining of multiple elements or concerns.
- Simple is distinct from easy. Something easy is familiar and convenient, but not necessarily simple.
- Simplicity is objective and measurable. It's about minimizing the number of components and their interdependencies.
- Essential simplicity is about focusing on the core aspects of a problem without adding unnecessary layers.

In essence, a simple system is built by parts that are less intertwined. This lack of intertwining is what makes things easier to understand.

Something simple, even if unfamiliar, can be understood thoroughly. You might just have to spend a bit more of time processing the concepts you're unfamiliar with. But sooner rather than later, you'll "get" it, and that "getting it" will be reliable. Which brings in an interesting echo between what we're trying to build (reliable software systems) and what we're using to build them (reliable concepts).

Through simplicity, we can achieve **reliability**. By making the system simpler, we make it easier to understand, which means that there are less gaps in our design. And through simplicity, we make the system easier to test thoroughly.

Through simplicity, we can also achieve **cost minimization**, both upfront and for changes. If we fully understand the system, we can execute it with great speed. And we can redesign it with great speed *while* maintaining reliability.

The converse of these two statements is easier to believe:
- It is extremely difficult to ensure the quality of a complex system, because nobody really understands it, so nobody knows what's truly right or wrong (so how would you be able to tell if it was behaving correctly or not?).
- It is extremely difficult to ensure flexibility of a complex system, because in the absence of a clear understanding of the system and strong tests, it takes an extraordinary amount of effort to make sure that the changes do not break existing functionality and that they properly integrate with it.

The more I read or hear some greats of software engineering, the more I'm convinced of simplicity as the key to it all. Consider the following quotes:

- Edsger W. Dijkstra: "Simplicity is prerequisite for reliability."
- Rich Hickey: "Simple things should be simple, complex things should be possible."
- Donald Knuth: "The art of programming is the art of organizing complexity, of mastering multitude and avoiding its bastard chaos as effectively as possible."
- Alan Kay: "Simple things should be simple, complex things should be possible."

Principle/hypothesis 6: **The key to understanding a software system is to minimize its complexity -- which is the same as maximizing its simplicity**.

## Simplicity in practice: the URTDLC process

I'd like to introduce something I just made up: the URTDLC process for developing software. URTDLC stands for the following:

- Understand.
- Run.
- Test.
- Deploy.
- Log.
- Change.

These actions come in order: it is quite pointless to run a system without understanding it; you cannot test a system if you cannot run it; and you cannot (or at least should not) change a system if you cannot understand it, run it, test it, put it in front of users (deploy), and see what went wrong (log).

For each of these actions (which I'll explain in a minute), we can measure how well we're doing it using two variables:
- How well we do it.
- How much effort it takes us.

For example: I might understand the system quite well; but it might have taken me six months full-time to achieve this understanding (effort).

So, for example, the cost of understanding the system to a "quite well" level would then be six months.

*Most of our work should be targeted at reducing the effort it takes any new team member to understand, run, test, deploy, log and change the system.* It is with a view to this that we'll propose changes to our engineering practices. Indeed, the mere writing of this documentation in Github is meant as a way to lower the cost of understanding the system, for both myself and the entire team (present and future).

As for the actions, let's start with **understand**. To do anything with a software system, we need to understand it: why do we write it? What does it do? How does it do it? Without crystal clear answers to these questions, any work we might do running, testing or changing the system will 1) take much longer than it'd take if we did understand the system; 2) we will *almost certainly* make the system **worse** if we change it without understanding it.

Understanding must be concrete: that is, it must directly explain with the data flows that go through the system, and it should be done in writing, not just in one's head. Understanding can (and should) use layers of abstraction, but always starting with the concrete, and always remembering that an abstraction is just a generalization of concretions.

Once you have a solid understanding of the system, it makes sense to **run** it. By run it I mean to execute it in a computer, either local or remote, so that the system is ready to process information. Running a software system, despite decades of progress, is still nontrivial. Luckily, there are a few low-effort, high-impact actions we can take to make this as easy as possible. A lot of our technological choices will be related to the ease of running the system, particularly over a longer time period.

Once you understand the system and can run it, you're able to **test** it. Testing might be manual, automatic, or both. What matters, first and foremost, is that you know what to test in the system. By already understanding the system, you know what the system ought to do, and even if you are missing some details, you can quickly find and fit these details into your mental map of the system. Then you'll figure out the hoops you need to jump in order to check that the system works. If a team member already wrote test scripts or tests, even better: you can run those tests, either manually or automatically, and hopefully improve on them.

Once you can understand, run and test the system, you're ready to **deploy** the system. This means that the system is in a remote environment (a server) where users can actually get value from the system.

Once you can understand, run and test the system, and the system is deployed, you are in a position to **log** any potential issues or valuable information that emerges from the interactions between your users and the system. Things that can and should be logged are any errors produced by the system, as well as the collection of metrics like response time and resource usage. Those logs must be centralized and should be readily and flexibly queryable.

Finally, after you understand, run and test a system, as well as put it in front of users and collect logs, you're now able to **change** it. The reason we create information systems in software and not in hardware is because we need those systems to *constantly evolve*. This is particularly so in a startup like FuelFWD, where we're figuring out what to build it as we build it. So our systems must change, shall change, will change.

The change process is itself composed, at a microlevel, of the first five stages: understand, write/run, test, deploy and log: you first understand the change in the context of the entire system; then you write it (and run it while you write it); finally, you test it, extending the existing test suites, to demonstrate that the change is mostly correct. Then you deploy it and you log useful information.

Note that nowhere we've specified **Write** as a step in the sequence. It is also my contention that the best way to understand something is to be able to write it down; so the writing of the design or the writing of its implementation happens as a byproduct of understanding the system. The remaining steps will show bugs and omissions that can be addressed iteratively.

Principle/hypothesis 7: **The sequence of software development (whether on a new or existing system) can be summarized as a linear sequence of Understand, Run, Test, Deploy, Log, Change. The writing of the system emerges from its understanding.**

## Keep the URTDLC cycle as short as possible, but not any shorter

In general, it is a good idea to keep the development cycle as short as possible.

In the context of a new system, it usually makes perfect sense to pick a very small number of features (and rudimentary versions of those features to begin with), so that the system can be live and receiving user feedback as soon as possible.

In the context of an existing system, it also makes perfect sense to work or extend features one at a time, unless a number of features are closely related and require each other.

However, the cycle shouldn't be made any shorter that it can be. Sometimes, it pays off to work for a few weeks on just one thing. Any non-trivial software system will sometimes require more than two weeks (the so-called "sprint") to complete something. Rather than fixating on an arbitrary amount of time, it's best to focus on what matters for the iteration, for as long as it actually takes.

Principle/hypothesis 8: **Keep the URTDLC short, but not arbitrarly short, or bound to an inflexible amount of time.**

## Overengineering doesn't exist, only bad engineering

Overengineering is defined to be the making of an engineering product that's too complex or does unnecessary things. If the key to software is to maximize simplicity so that we can understand the system, overengineering is simply bad engineering. If some complexity is introduced that is not absolutely necessary, then we're potentially multiplying the cost and decimating the reliability of our software system.

Something that complicates things and adds few or no benefits, is not just unnecessary, but downright harmful; this is *exactly* what we're trying to avoid.

As of 2024, devops seems to be by far the largest harbringer of overengineering. Consider the following system type, which is highly descriptive of a large portion of all software projects:

- A system that relies on a single relational database and S3-like storage.
- Has a peak load of under 10 requests per second.
- Doesn't perform heavy I/O or CPU heavy tasks.
- Is built around HTTP or websockets calls.
- The application layer holds no state in between calls, and puts all the state in the database and S3-like storage.

For a system like this, which also usually counts with a cloud-provisioned database, scaling it is as simple as doing the following:
- Have a single entrypoint (load balancer) for all the traffic and distribute it to n nodes.
- Have a reliable way to store configuration, in a way that 1) is versionable; 2) doesn't mix the secrets with the rest of the config; 3) but brings in the secrets together with the config at runtime.
- Automatically provision and deploy an application node.
- Have a programmatic way (that can be both manually or automatically activated) to add or remove application nodes.

That's it! While you could do the above with minimal configuring in AWS with an autoscaling group and an image, most devops toolsets will use one or more of the tools below to make this happen:
- Kubernetes.
- Helm.
- Terraform.

You could make this even simpler with a control node that spins up or down application nodes.

You might not even need scaling the service, *ever*. You could simply have 2 (or 5) servers, whether virtual or dedicated, and have a script that "freshens them up" periodically.

Principle/hypothesis 9: **Overengineering is simply bad engineering. Avoid it like the plague. Beware of devops-induced complexity.**

## Auto-activation is the key to operational excellence

Auto-activation, a term from the Toyota Production System, means that a machine or process stops immediately when an error is found, instead of going on until the faults in the process make it break down completely. Let's restate this: an auto-activated machine stops on its own when it detects an error.

The purpose of auto-activation is twofold:

- No defective products are made, because every machine involved in the process checks the state of the product and will stop the whole process if any abnormality is found.
- By stopping the process on any error, the system sharply distinguishes normal from abnormal operation. The process cannot start again until that error is solved. Thus, errors are not ignored or dismissed, but rather brought into the light so that its root causes can be determined and eliminated.

By sharply distinguishing normal from abnormal operation, we can achieve an [asymptotic expectation](https://github.com/fpereiro/lite?tab=readme-ov-file#5-when-you-find-an-error-stop) towards errors, which means that they should become exponentially less likely over time; much like the approach of [aviation accident analysis](https://en.wikipedia.org/wiki/Aviation_accident_analysis). When errors emerge in a system with high quality, they won't elicit panic or annoyance, but rather wonderment: every error will teach us something new that we can immediately apply.

For this shift to happen, we need the following:

- Detect all errors.
- Collect all errors into a centralized logging system.
- Group them into coherent wholes, since errors can be related to each other.
- Target their root causes by both 1) fixing the code; 2) fixing the tests that didn't detect the errors in the first place.

Principle/hypothesis 10: **Auto-activation allows to develop software systems that converge towards perfection, through the simple practice of detecting, and collecting errors, as well as targeting their root causes.**

## Three human metrics to track simplicity

A software system runs only incidentally on computers, but chiefly on the morale of those who specify and implement it. Morale can have many sources and many sinks. Here I'm interested only in sources and sinks of morale that are "pure engineering" -- that is, that don't have anything to do with the purposeof the system, or the organization that makes it.

The three "pure engineering" morale boosters I've found are:

1. Ownership
2. Relative ease
3. Inner pride

The more of the above, the more "pure engineering" morale will be available. This morale translates into further reliability increases as well as cost reductions.

For any reasonably motivated engineer, understanding is the main driver of ownership. When the system is understood, and the reasons for its shape are clear to everyone involved, that all-too-common "throw up my hands in the air" disappears from sight. It's hard to feel ownership of something that, even if you fully built it yourself, you don't really get. The converse is true: when you've built something and you truly understand it, it is almost impossible to not feel that you own it.

Relative ease is how difficult it is to implement something, given a certain level of "baseline difficulty" of the task itself (Fred Brooks calls this baseline difficulty "inherent complexity"). A system that makes nontrivial features relatively easy to implement will boost the morale of those who implement those features; conversely, a system that makes trivial changes a nontrivial undertaking is surely a morale destroyer.

Inner pride is how proud (or not proud) does a builder of the system feel, in their own self, towards the quality of the system they build. External displays of pride (or shame) are irrelevant, because they are distorted by myriad with cultural traits and incentives. The internal feeling of pride that a maker has towards what they build is what counts, because it is much more sincere, and it doesn't expect anything: it is pure perception. All too often, makers of software find it hard to feel proud about the software that they build. But those who achieve this feat, more often than not, are those who will go farthest.

Principle/hypothesis 11: **A software system runs on morale; the three sources of pure engineering morale are ownership, relative ease and inner pride.**

## Appendix: URTDLC checklist

- Understand means that you fully know the following:
   - Which system components exist (frontends, backends, databases, s3-like third party services).
   - Which calls each of the components do, including the concrete implementation of its payloads.
- Run means the following:
   - The commands to run the system in a reasonable base environment are specified.
   - Also how to get all the required environment variables, including the secret ones.
- Test
   - For each of the calls implemented by the system, try all possible families of incorrect payloads and assert that the proper errors are returned and no further changes are generated.
   - For each of the calls implemented by the system, implement all possible families of correct payloads and assert that the proper return values are returned and the proper state transformations have happened.
- Deploy
   - Any branch or commit of the code can be triggered by any human with enough privileges to do it.
   - The deploy happens automatically as soon it is triggered, without further manual intervention.
- Log
   - All logs produced by the application are directed to a centralized and queryable location.
   - All error logs from the application are logged.
   - Some interesting behaviors that it makes sense to log, are logged.
   - Metrics like response time and resource usage are also logged.
- Change
   - No steps of the above are skipped. The change must be first understood, then run, then tested, then deployed, then logged.
