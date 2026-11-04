---
title: 'LLMaaO (LLM as an Oracle)'
linkTitle: 'LLMaaO (LLM as an Oracle)'
excerpt: The case for asking an LLM "yes or no" instead of "how".
date: 2026-11-04
permalink: /posts/2026/11/llm-as-an-oracle
images:
  - /images/consulting-the-oracle.jpg
tags:
  - learning
  - llm
---
More to pedagogy than nice visuals. AI usage needn't be all-or-nothing. Close
open loops. Free thyself.
<!--more-->

I've lately been having fun using LLMs as teaching assistants in a different way
from the usual "generate me a nice HTML explaining X" seen in `/teach` and other
skills.

This all started when I took a stab at the ["Original Performance Take
Home"](https://github.com/anthropics/original_performance_takehome) that
Anthropic published, a take-home challenge that was previously used in their
hiring process for performance engineers.[^1]

Having committed to not using any AI assistance at all, I spent quite a few hours
getting the solution down to 4,974 cycles (still not as good as Opus
4.5, which managed to reach 1,363 cycles). This was very stimulating and a lot
of fun, even though it revealed just how bad and slow I am. I would've blasted
through the challenge with AI assistance restricted to only the coding parts,
not the high-level optimization ideas, but I use LLMs too much at work and
needed a change of scenery.

At some point I got stuck and, while I had quite a few ideas, I wasn't sure
which direction was the most promising. I had reached the point where even
evaluating the feasibility of an idea required effort.

Having stagnated, with the novelty having worn off and not much motivation to
beat the challenge, I got concerned that I'd just end up quitting and missing
out on some learning opportunities. At the same time, I did not want to just
look at a solution, say "ah, obviously," and pretend I learned anything.

So, I decided to rely on AI assistance of a very restricted kind. I wanted two
things:

1. to avoid going down dead ends
2. to accelerate (but not entirely delegate) writing the code

(Granted, the second point does not reflect the title of this post, but I needed
something catchy.)

If you think of problem-solving as navigating a large space of possible
approaches, where only a few paths lead to the solution, it's very easy to go
down a dead end: there are many more dead ends than correct paths. Moreover,
it's not just the size of the search space that makes a problem hard (and
interesting) in the first place, but the difficulty of being able to tell which
path is feasible.

{{< figure class="diagram-wide" src="many_paths.svg" alt="Search space with one viable path" >}}

Thus, having access to an _oracle_, an entity that can answer with a simple yes
or no to the question of the feasibility of a direction, would drastically
reduce the time needed to find the right solution. (The term _oracle_ was
borrowed from complexity theory; see for example Section 9.2
in Sipser [[1]](#References).)

The other difficulty, of course, is having ideas in the first place![^2] And so
I decided that, having a few ideas but not the time to try them all out, I could
still experience much of the intended learning effect by using an LLM as an
oracle.


Naturally, some of that learning would be lost. Wrong turns teach you things
too: what not to do, what something is not, when to quit, how to start anew
without letting the failed attempt linger in your head. (_Unlearning_ is hard.)

I accepted this trade-off.

{{< figure class="diagram-wide" src="path_back_learning_and_forgetting.svg" alt="Path back from a dead end showing learning and forgetting" >}}

Reducing the exploration time was one dimension; translating the ideas into code
was also a bit hairy as generating the assembly was not nicely abstracted in the code, but was rather just raw string generation. All useful abstractions needed to be built. So I decided to let LLMs help
me out there too. I was now operating almost entirely at the level of ideas.

I decided to trust myself to use the LLM in this restricted way, still not
letting it generate ideas or explain finer details. It went delightfully
well!

I got down to 2,000 cycles and still felt like I'd learned a lot.

For example, at some point I realized that the next big improvement would likely
be automating the packing of instructions into bundles. Up to that point, I had
done that locally within one loop iteration and gotten quite close to the
limit. So, although I had a strong suspicion that doing this globally would be quite
productive, I had the oracle confirm that for me.

Once confirmed, I was able to use the LLM as a Socratic dialogue partner to
flesh it out, again without becoming overly reliant. At this point it would've
been trivial to just say "hey, now just implement instruction packing," feeling
proud that "I had gotten the idea right." But I wanted more.

I was doing much of this work on my phone, without access to pen and paper (or
some other "scratch space"), so using the LLM as a conversational partner was
quite helpful. I started off by saying:

> ok, now let me think about what's necessary to make a better scheduler.
> i think the number one thing is data dependencies. so we should be able to,
> when emitting, also list a dependency.
>
> now i wonder what the right way to do this is
> 
> one thing i was thinking is for emit to return an id (could be arr idx, could
> be something else), and then that can be used as an arg in the emit of the
> instruction that depends on this.
> 
> what do you think? discuss

The LLM was eager to give me way too much hand-holding here, so I had to
prompt it to

> be socratic with me and don't reveal the answer immediately

That worked decently well. (I had to repeatedly tell it to tell me less and
less, as it often liked to give me the benefit of the doubt and fill the gaps
for me.)

It walked me through the different steps to determine how to build the
dependency relationships. Granted, it was a bit _too_ helpful, as I certainly
would've made some wrong decisions here, but that's no different from any
teacher.

Naturally, this method is easier than deriving the rules alone, and I realized
as much. I told the LLM:

> Hmm this is really clean and nice. I'm worried I wouldn't have come up with
> this. I am worried that my approach would've been very different, that
> I wouldn't have explored the cases so cleanly and thoroughly, that I would've
> written some of the "easy" dependencies and used the actual instructions to
> try to derive the rules, instead of thinking abstractly and from first
> principles.

I want to be honest and not delude myself. Yes, this was not nearly as fruitful
as a solo effort would have been. Even so, the entire endeavor was ultimately
productive. I managed to get unblocked and make progress, freeing up time to
work on other things instead of adding yet another project to the graveyard. At
the same time, it's clear to me this is qualitatively different from a purely
vibe-coded project. The gap is not small at all. I feel confident that I learned
quite a lot.

My takeaway is that I get the best out of LLMs when I start without them at
all, and this is something I want to carry over to my work as well.

## <a name=References id="References"></a>References
[1] M. Sipser, _Introduction to the Theory of Computation_. Cengage Learning, 2012.



[^1]: Tristan Hume wrote a nice
    [article](https://www.anthropic.com/research/AI-resistant-technical-evaluations)
    back in January 2026 on why Anthropic stopped using this challenge and what
    makes a good technical evaluation. I presume this looks vastly different today,
    just 10 months later.


[^2]: In complexity theory this isn't considered difficult because ideas can
    just be naively enumerated, and the massive cost is exploring the search
    space! So an oracle suffices, as long as it can tell you whether a solution
    lies down a given branch.
