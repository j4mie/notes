# Questions about software and energy efficiency

This post is full of questions. It does not contain any answers. It is a set of notes to serve as starting point for further research and consideration.

In general, do professional software developers ever consider the energy footprint and efficiency of their algorithms and tool choices? Should they?

Is spending time trying to reduce the energy consumption of software a worthwhile endeavour? Or is it so insignificant that remembering to turn off a lightbulb would make a bigger contribution to reducing climate breakdown?

Does the energy used in the process of developing and supporting software (powering developer laptops, office heating and air conditioning, commuting, boiling the kettle etc) dominate over the long-term energy usage of hosting and operating the software in production or vice versa? Does the answer to this question affect the choice of programming language and tooling? Should we be optimising for developer productivity or runtime efficiency? How does energy usage scale with complexity or number of users? What about different desktop and server operating systems?

How would one usefully measure the energy usage of a running process on a server? What units might the measurement be given in? Does the answer change if the server is virtualised? Should the embodied energy of the servers and data centres be taken in account? Could we borrow any measurement techniques from other industries, such as building design? Could infrastructure providers publish real-time metrics on hardware utilisation and redundancy?

Is there any low-hanging fruit? Is the goal of improving energy efficiency always aligned with other goals such as performance, bandwidth use or budget? Are there any practices which would save power at the cost of making the software slower or less pleasant to use in some way? Would this be a worthwhile trade-off?

Would it be possible for compilers or interpreters to consider the power-saving characteristics of modern CPUs when deciding how code should be executed? Do they already do this?

> Programmers waste enormous amounts of time thinking about, or worrying about, the speed of noncritical parts of their programs, and these attempts at efficiency actually have a strong negative impact when debugging and maintenance are considered. We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil. Yet we should not pass up our opportunities in that critical 3%.

*Donald Knuth, “Computer Programming as an Art”,  1974*

If we replace the word “speed” in this ubiquitous programming mantra with “energy efficiency” or “carbon footprint” or “contribution to the extinction of all life on Earth” does it affect the conclusion? Does it change the 97% vs 3% split?
