# Your computer is leaking: a defence of dynamic types

I’ve been writing Python code for at least 15 years, and full-time for 10. Early on, I remember hearing Python described as “executable pseudocode”. That really stuck with me.

Pseudocode is not real code intended to be run by a computer. It’s a way of describing the code we might later write. It’s a tool for allowing humans to communicate the shape of an algorithm to each other without actually implementing it in any particular programming language. It’s a simplified, roboticised, code-alike version of plain English, readable even by people who aren’t really programmers.

Readability counts. It’s right there in the [Zen of Python](https://www.python.org/dev/peps/pep-0020/). Python has always been about giving humans priority over machines. “Programs are meant to be read by humans and only incidentally for computers to execute” has never been more baked into the bones of a language than it is with Python. Python is pseudocode with just enough of a grammatical skeleton to make it something that could actually run.

Python came from a time when “dynamic” was not a dirty word: it was the future. No longer did we need to submit to the tyranny of telling a dumb box of wires precisely what to do. We just described the solution to our problem and let the layers of abstraction figure out how to push the ones and zeroes around. This included types: Python is strongly typed but the type checking happens dynamically at runtime on the values that actually exist in the running program.

It’s an incredibly productive way to work. It allows for exploration of the design space, starting with little more than a sketch and iteratively approaching a “perfect” solution. The programmer gets to choose when to stop: to decide where to strike the balance between a perfectly architected, beautifully designed masterpiece and a quick hack that just about works, depending on budget and intended use. The design of the language allows it to scale smoothly between the two.

But time is a flat circle and in 2021 none of that is cool any more. Static typing is the new (old) hotness. All the kids are TypeScripting and even Python folks seem to be drunk on type annotations. After all, the argument goes, why would anyone possibly want to let the computer figure things out at runtime when you can tell it in no uncertain terms what it’s supposed to be doing before it even starts?

Well, because I usually don’t know what I want a program to do when I start writing it. And if I have to define exactly what sort of thing goes in and out of all the parts of the algorithm while I’m still trying to write it, my brain ties itself in a knot and falls over. Writing statically-typed code feels like being asked to design the intricate inner workings of a five-lever mortice lock before figuring out what a door is, or even why it might be nice to leave the house.

Static types encourage over-engineered difficult-to-change codebases because the first design approach you thought of becomes solidified, fossilised, like quick-drying cement, while the rest of the program is built around it. It’s like trying to make something with Lego but gluing all the bricks together as you go.

And that’s just the writing part. Reading code with static types feels like my train of thought is constantly being derailed by all the line noise, looping on itself to figure out where it’s just been.

> In the beginning (a Time Period) God (a Supernatural Deity) created the heaven (a Mythical Place) and the earth (a Habitable Planet).  

I don’t think literature would have got very far if it worked like that.

Python’s static typing is “optional”, except it isn’t really, is it? If your part of the program is type annotated and mine isn’t, then your part can’t meaningfully be type checked, so there is pressure on me to type-annotate my code. Also, if your code is using type annotations then I am forced to subject my eyeballs to them when I’m trying to read it (unless you’ve hidden the annotations in a separate stub file, which nobody does). The plague of static typing infects everything it touches.

And another thing: async. Async Python is great: it lets Python go as fast as Node! Except Node is JavaScript and JavaScript is all async, balls to bones. Python isn’t. Python’s standard library isn’t. So an entirely different language was bolted on to the side of Python, with different kinds of functions that do async kinds of things. Moving between async land and sync land is perilous: all it takes is one CPU-bound operation and your entire program grinds to an inscrutable halt. Good luck with that.

Now, please don’t think that I’m arguing that static  typing and async Python are always bad. Of course I’m not. I’m saying that they are both failures. They’re failures of the ideal of writing code for humans to read and only incidentally for computers to execute. They’re concessions to the machine. It’s no longer enough to describe your solution: now you have to tell the computer exactly what to do. The computer is leaking.

Sure, if you have a crusty old five-million-line spaghetti codebase with hundreds of engineers working on it every hour of every day, maybe static type checking could help you. If you’re writing code that needs to move network packets around between thousands of connected clients, then you probably need async. But at least be aware of what you’re doing: you’re making concessions. You’re writing code to tell the computer more about precisely what it needs to do, at the cost of it being less understandable by humans, and at the cost of foregoing the wildly productive technique of exploratory software design. Like everything in life, it’s a trade-off.

So please, just because you can, it doesn’t mean you should. My intuition is that 99% of all Python code written by anyone anywhere for any reason should not be using static type annotations and should not be async. Maybe 99.9%. In Python, dynamic, synchronous code should be the default. Don’t let your computer leak unless you are absolutely sure that you have to.
