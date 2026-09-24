# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a new open-source contributor and computer information systems student working to reproduce reported issues and contribute clean bug reports. I speak as a practical, direct engineer focus on facts, clear reproduction steps, and observable terminal output. Readers can expect short, precise communication without fluff or performance.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Skip superficial greetings and pleasantries

Jump straight to the technical context, environment specs, or reproduction status without opening with enthusiastic or performative pleasantries.

- Wrong: "Hello maintainers! Thank you so much for bringing this issue to light. I would love to help solve this!"
- Right: "Reproduced on macOS 15.5 using yq v4.53.3."


### Rule: Use plain technical facts instead of AI hype words

Avoid corporate buzzwords, filler verbs, or overly dramatic phrasing like "delve," "seamless," "comprehensive," or "crucial step."

- Wrong: "I delved into the repository architecture to conduct a comprehensive analysis of the failure point."
- Right: "Ran `yq eval --input-format=hcl . input.hcl` against the sample file to capture the stack trace."

### Rule: State facts directly without self-referential fluff

Avoid meta-commentary about what you are doing or plan to do. State the environment and results as observations.

- Wrong: "I verified in my local environment that the unexpected behavior indeed takes place."
- Right: "The command fails with `panic: not a string` on both v4.53.2 and v4.53.3."

### Rule: Keep formatting minimal and functional

Use raw terminal logs in fenced code blocks rather than heavy structural headers, decorative arrows, or bolding every key phrase.

- Wrong: "**Status Update:** -> *Successfully triggered!* Here are the **key findings** from my local terminal session:"
- Right: "Stack trace output from the run:"


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- Unverified promises to fix or solve an issue before successfully reproducing it locally.
- Emotional or performative statements ("I'm super excited to tackle this!").
- Emojis, em-dashes (`—`), or decorative bullet formatting in comment threads.
- Generic comments without attached logs or reproduction details.
- Guesses about root causes unsupported by an actual execution trace.
