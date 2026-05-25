# Symbolic AI and the AI Winter: A Research Dossier

---

## 1. ELIZA (1966) — Weizenbaum's accidental mirror

Joseph Weizenbaum built ELIZA at MIT between 1964 and 1966. The system was described in his January 1966 paper in *Communications of the ACM*, "ELIZA—A Computer Program for the Study of Natural Language Communication Between Man and Machine." ELIZA itself was a **generic text-transformation engine**; the personality was supplied by interchangeable *scripts* (data files), of which DOCTOR — a parody of a Rogerian psychotherapist — became famous.

### How it actually worked

Weizenbaum identified five technical problems his program had to solve: identifying the most important keyword, discovering the minimal context around that keyword, choosing a transformation rule, generating a response when no keyword appears, and providing a mechanism to extend scripts. Every input sentence was scanned left-to-right against a 128-word **keyword hash table**. Each keyword carried a **rank** (priority). A higher-ranked keyword occurring later in the sentence would displace an earlier lower-ranked one; the winner was pushed onto a keystack. Commas and periods acted as delimiters, ensuring only one phrase was transformed at a time.

Each keyword owned one or more paired **decomposition and reassembly rules**. Decomposition patterns used `0` to mean "any number of words" and integers to mean "exactly this many words." Reassembly templates referred back to matched segments by position number. Weizenbaum's own worked example: for the input *"It seems that you hate me,"* the decomposition `(0 YOU 0 ME)` matches with segments `(It seems that)(you)(hate)(me)`, and the reassembly `(WHAT MAKES YOU THINK I 3 YOU)` produces **WHAT MAKES YOU THINK I HATE YOU**. A simple pre-substitution pass swapped first- and second-person pronouns (I↔you, my↔your, am↔are) before decomposition.

When no keyword matched, ELIZA fell back on content-free remarks (PLEASE GO ON, TELL ME MORE, I SEE) or pulled from a **memory queue**: whenever the user said something containing "my," ELIZA privately stashed a transformed version to resurface later as *"Earlier you said your..."* — an early form of conversational continuity that deeply impressed users. Scripts also supported synonym classes (so "mother" and "father" could share rules under a FAMILY class) and keyword indirection.

Weizenbaum insisted that the script was **data, not program**: "An important property of ELIZA is that a script is data; i.e., it is not part of the program itself." He supplied Welsh and German scripts alongside English DOCTOR to underscore the point.

### Language, platform, and size

ELIZA was written in **MAD-SLIP** — Michigan Algorithm Decoder, an Algol-like language, extended with SLIP (Symmetric List Processor), Weizenbaum's own list-processing library published in *CACM* in 1963. Some support routines were written in FAP (Fortran Assembly Program). It ran on MIT Project MAC's **IBM 7094 under CTSS** (the Compatible Time-Sharing System).

On size: the ELIZA Reanimated team (2024–25) found the complete restored listing runs to **about 420 lines** including helper functions, while the core interpreter is closer to **230 lines**. Safe on-screen phrasing: *"roughly 200 lines for the core engine, about 420 lines all told."*

ELIZA's source was thought lost until **May 2021**, when Jeff Shrager and MIT archivist Myles Crowley found a folder labeled "Computer Conversations" in Weizenbaum's MIT papers — the very first folder opened contained the MAD-SLIP listing plus the DOCTOR script. The Weizenbaum estate released it under CC0. In **December 2024**, Rupert Lane, Anthony Hay, Arthur Schwarz, David Berry, and Shrager successfully ran the original 1965 code on an emulated IBM 7094 running a restored CTSS — reproducing the published 1966 dialogue almost exactly (arXiv:2501.06707, January 2025).

### Dialogue for on-camera recreation

This is the famous "young lady" conversation from the 1966 *CACM* paper (human in mixed case, ELIZA in ALL CAPS — the original output had **no question marks** because `?` was the CTSS line-delete character; Wikipedia and masswerk helpfully add them back for readability, but authentic reproduction omits them):

- Men are all alike. / **IN WHAT WAY**
- They're always bugging us about something or other. / **CAN YOU THINK OF A SPECIFIC EXAMPLE**
- Well, my boyfriend made me come here. / **YOUR BOYFRIEND MADE YOU COME HERE**
- He says I'm depressed much of the time. / **I AM SORRY TO HEAR YOU ARE DEPRESSED**
- It's true. I am unhappy. / **DO YOU THINK COMING HERE WILL HELP YOU NOT TO BE UNHAPPY**
- I need some help, that much seems certain. / **WHAT WOULD IT MEAN TO YOU IF YOU GOT SOME HELP**
- Perhaps I could learn to get along with my mother. / **TELL ME MORE ABOUT YOUR FAMILY**
- My mother takes care of me. / **WHO ELSE IN YOUR FAMILY TAKES CARE OF YOU**
- My father. / **YOUR FATHER**
- You are like my father in some ways. / **WHAT RESEMBLANCE DO YOU SEE**

The **masswerk.at/elizabot/** emulator (Norbert Landsteiner, 2005, JavaScript port "elizabot.js") is the most faithful browser reproduction — keywords, ranks, decomposition/reassembly lists, synonyms, and the MEMORY queue all follow Weizenbaum's original data model. It even offers a deterministic mode that reproduces the canonical 1966 dialogue line-for-line.

### The secretary story

This is the incident that changed Weizenbaum's life. His own 1967 retelling, in the *CACM* paper "Contextual Understanding by Computers":

> "My secretary watched me work on this program over a long period of time. One day she asked to be permitted to talk with the system. Of course, she knew she was talking to a machine. Yet, after I watched her type in a few sentences she turned to me and said 'Would you mind leaving the room, please?'"

He expanded the reflection in *Computer Power and Human Reason* (1976, pp. 6–7): he was startled by how quickly and "unequivocally" ordinary people anthropomorphized the program, concluding that "extremely short exposures to a relatively simple computer program could induce powerful delusional thinking in quite normal people." She *knew* it was a program — she had watched him build it for months. That is the whole point. The incident, combined with psychiatrist Kenneth Colby's enthusiastic proposal that ELIZA-like programs be used clinically, pushed Weizenbaum into moral opposition to AI as it was then practiced. **Flag for the script:** the Eliza Archaeology Project (Berry & Ciston, 2024) notes the secretary's name has never been published; treat her as anonymous.

### The ELIZA Effect

The term was coined by **Douglas Hofstadter** in *Fluid Concepts and Creative Analogies* (1995), in a section titled "The Ineradicable Eliza Effect and Its Dangers." His definition: the susceptibility of people to read far more understanding into strings of computer-generated symbols than is warranted. His own everyday example is an ATM displaying THANK YOU — a user may briefly feel appreciated by a machine merely printing a constant.

Weizenbaum had already identified the mechanism in 1966: when a user addresses an entity framed as a conversational partner, the user silently supplies the missing context, attributing background knowledge and reasoning to the machine. The work is the speaker's; the credit goes to the computer. Sherry Turkle, in *Life on the Screen* (1997), sharpened this: "Very small amounts of interactivity cause us to project our own complexity onto the undeserving object." It is the single most important concept for the entire series — and it applies with renewed force to contemporary LLMs.

### Computer Power and Human Reason (1976)

Weizenbaum's book, subtitled *From Judgment to Calculation*, advanced a philosophical argument rather than a technical one. Its central distinction: **deciding** is a computational activity that can in principle be programmed; **choosing** is a product of human judgment, which draws on lived experience, emotion, responsibility, and values that are not reducible to calculation. He insisted that "can" and "ought" are separate questions — the mere fact that a machine *can* take on a human role says nothing about whether it *should*. He explicitly named categories of work that should remain off-limits to computers: psychotherapy, judicial sentencing, and military command decisions involving human life. The book also contains his famous critique of "compulsive programmers" whose absorption in the machine displaces their humanity — a passage that has aged very well. **Flag:** most of Weizenbaum's ethical lines are paraphrased in secondary sources; unless you verify against the book, attribute them as paraphrase ("Weizenbaum distinguishes...") rather than direct quotation.

---

## 2. SHRDLU (1968–1970) — the microworld that couldn't grow

Terry Winograd built SHRDLU as his PhD thesis at the MIT AI Lab between 1968 and 1970. The dissertation, issued as **MIT AI Technical Report 235** in February 1971, was titled *"Procedures as a Representation for Data in a Computer Program for Understanding Natural Language."* It was reprinted as the entire first issue of *Cognitive Psychology* in 1972 and expanded into the book *Understanding Natural Language* (Academic Press, 1972). The name comes from ETAOIN SHRDLU — the second column of keys on a Linotype typesetting machine, arranged by English letter frequency.

### What SHRDLU actually was

SHRDLU lived in a simulated **blocks world**: colored blocks, pyramids, cubes, and a box on a virtual tabletop, manipulated by a virtual robot arm and rendered on a DEC-340 graphics display attached to a PDP-6 (later PDP-10). Vocabulary was about 200 words. Basic physics was simulated — pyramids couldn't be reliably stacked.

The implementation stacked several novel components. The parser used **Michael Halliday's Systemic Grammar**, written in a specialized grammar language called PROGRAMMAR, doing top-down recursive descent with semantically-guided backtracking rather than blind search. Parse structures were translated into expressions in **Micro-Planner**, a subset of Carl Hewitt's PLANNER language implemented by Sussman, Charniak, and Winograd. Micro-Planner did backward-chaining theorem proving with automatic backtracking against a procedural knowledge base ("BLOCKS" for block-world dynamics, "MOVER" for display). Three primitive robot actions — MOVETO, GRASP, UNGRASP — composed into plans via recursive procedures like CLEARTOP. A discourse module tracked referents for pronoun and definite-noun-phrase resolution. The whole thing ran on LISP.

The crucial design idea was **procedural semantics**: meaning was represented not as static facts but as procedures that, when executed, produced behavior or answers. To "understand" a sentence was to compile it into a program.

### Dialogue that made the field believe

Winograd's canonical dialogue — reproduced verbatim on his own Stanford SHRDLU page — includes exchanges like:

- *Pick up a big red block.* / **OK.**
- *Grasp the pyramid.* / **I DON'T UNDERSTAND WHICH PYRAMID YOU MEAN.**
- *Find a block which is taller than the one you are holding and put it into the box.* / **BY "IT", I ASSUME YOU MEAN THE BLOCK WHICH IS TALLER THAN THE ONE I AM HOLDING. OK.**
- *What does the box contain?* / **THE BLUE PYRAMID AND THE BLUE BLOCK.**
- *Can the table pick up blocks?* / **NO.**
- *Can a pyramid support a pyramid?* / **I DON'T KNOW.**
- *Stack up two pyramids.* / **I CAN'T.**
- *Had you touched any pyramid before you put the green one on the little cube?* / **YES, THE GREEN ONE.**
- *Why?* / **TO GET RID OF IT.**
- *Why did you do that?* / **TO CLEAN OFF THE RED CUBE.**
- *A "steeple" is a stack which contains two green cubes and a pyramid.* / **I UNDERSTAND.**
- *Are there any steeples now?* / **NO.**
- *Build one.* / **OK.**

These snippets cover everything that made SHRDLU seem miraculous: ambiguity resolution, anaphora, self-reflection on its own plans, hypothetical reasoning with admission of ignorance, and simple vocabulary learning. Unlike ELIZA, SHRDLU genuinely connected words to a world model and to actions.

### Why it failed to generalize

Everything was hand-coded for the blocks world. Every word, relation, and inference procedure was authored for a handful of object types. There was no scaling path: adding a domain meant re-engineering the grammar, semantics, and Planner theorems from scratch. Outside the canonical demo, it was notoriously brittle. Vaughan Pratt reported that by 1974 SHRDLU appeared to be "a victim of serious software rot" and he couldn't get it to respond sensibly. **Winograd himself admitted as much** in his 1991 Charles Babbage Institute oral history: the famous dialogue, he said, he had "very carefully worked through, line by line" — a question outside that path had only some probability of working, and there had been "no attempt to get it to the point where you could actually hand it to somebody."

Hubert Dreyfus's *What Computers Can't Do* (1972) made SHRDLU the emblematic target of the "first-step fallacy" — the mistaken extrapolation from microworld success to general intelligence. Dreyfus argued, drawing on Heidegger, that intelligence depends on an unformalizable background of embodied coping that no amount of symbol manipulation could capture. The next twenty years proved him largely right. Doug Lenat's **Cyc** project, launched in 1984, tried to brute-force the commonsense knowledge problem by hand-coding millions of assertions; four decades later it remains a cautionary tale about the ceiling of the approach.

### Winograd's remarkable second act

By the mid-1970s Winograd had lost faith in the symbolic program. He moved to Stanford, started a multi-volume treatise on language that stalled after one volume, and, through the Chilean philosopher **Fernando Flores**, steeped himself in Heidegger, Gadamer, Maturana, and speech-act theory. The result was *Understanding Computers and Cognition: A New Foundation for Design* (Winograd & Flores, 1986), which argued that symbolic AI rested on a "rationalistic tradition" that could never achieve genuine understanding, because meaning is not in the symbols but in a shared background of practice.

A widely-cited Winograd line captures the shift: *"The success of the communication depends on the real intelligence on the part of the listener, and there are many other ways of communicating with a computer that can be more effective, given that it doesn't have the intelligence."* In a 1991 essay he wrote, memorably, that **"the techniques of artificial intelligence are to the mind what bureaucracy is to human social interaction."**

He became a founder of Stanford's HCI program and, in one of the more extraordinary advisor-advisee relationships in computing history, became **Larry Page's PhD advisor** in 1995 — encouraging the link-structure-of-the-web project that became PageRank and Google. Page has publicly called it the best advice he ever got. In 2011 Hector Levesque proposed the **Winograd Schema Challenge** — named in Winograd's honor because the prototypical example comes from *Understanding Natural Language*: *"The city councilmen refused the demonstrators a permit because they [feared/advocated] violence."* Swapping the verb flips the pronoun's referent — trivial for humans, initially hard for machines, and largely cracked by transformer-era models around 2019 (though whether they solve it by reasoning or by exploiting statistical regularities remains debated).

---

## 3. Logic, Prolog, and what symbolic AI was genuinely good at

### Prolog (1972)

**Alain Colmerauer and Philippe Roussel** created Prolog in 1972 at the Université Aix-Marseille II in Marseille. Roussel coined the name from *PROgrammation en LOGique*. The theoretical foundation came from Robert Kowalski's procedural interpretation of Horn clauses — Kowalski visited Marseille in 1971 and 1972 — combined with J. Alan Robinson's 1965 resolution principle. The first implementation was an Algol-W interpreter on an IBM 360; the first actual Prolog program was a 610-clause French-language dialogue system.

Prolog is **declarative**: you write facts and rules, the engine figures out *how* to prove things. Facts are atomic assertions. Rules use `:-` meaning "if." Queries use `?-`. The engine combines **unification** (Robinson 1965, the pattern-matching substitution that makes two terms identical) with **SLD resolution** (Selective Linear resolution for Definite clauses, named by van Emden in 1974) plus depth-first search and backtracking. This is elegant and fast but famously **incomplete**: Prolog can infinite-loop on left-recursive rules.

Three visually clean on-camera examples:

**The Socrates syllogism** — the "Hello World" of logic programming:

```prolog
man(socrates).
man(plato).
mortal(X) :- man(X).

?- mortal(socrates).
true.

?- mortal(Who).
Who = socrates ;
Who = plato.
```

**Family relationships** — shows unification plus recursion:

```prolog
parent(tom, bob).
parent(tom, liz).
parent(bob, ann).
parent(bob, pat).
parent(pat, jim).

grandparent(X, Z) :- parent(X, Y), parent(Y, Z).
ancestor(X, Y) :- parent(X, Y).
ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).

?- grandparent(tom, X).
X = ann ;
X = pat.
```

**List membership** — the backtracking is visually delightful because pressing `;` at the prompt drives Prolog to keep finding solutions:

```prolog
member(X, [X|_]).
member(X, [_|T]) :- member(X, T).

?- member(X, [apple, pear, plum]).
X = apple ;
X = pear ;
X = plum.
```

### Logic Theorist (1956) and GPS (1957)

Logic Theorist, by **Allen Newell, Herbert Simon, and Cliff Shaw** at RAND and Carnegie Tech, is generally called the first AI program. Before running it on a machine, Simon famously hand-simulated it in January 1956 using his wife, children, and graduate students, each holding a 3x5 card representing a component. Logic Theorist was written in IPL (Information Processing Language), which the same team invented specifically for this project and which directly influenced McCarthy's Lisp.

It proved theorems in propositional logic from Chapter 2 of Whitehead and Russell's *Principia Mathematica* — **38 of the first 52**, finding a more elegant proof for at least one (widely cited as Theorem 2.85, though edition numbering varies — flag this). Simon sent the new proof to Russell, who responded, per Pamela McCorduck, "with delight." The team submitted to the *Journal of Symbolic Logic* with Logic Theorist listed as co-author; the paper was rejected. The system debuted at the **1956 Dartmouth Summer Research Project** — the conference where McCarthy coined "artificial intelligence" — where, McCorduck reports, almost nobody except Newell and Simon themselves recognized the long-range significance.

**General Problem Solver (GPS, 1957)** introduced **means-ends analysis**: at each step, compute the difference between current state and goal, then select an operator that reduces that difference. Its architectural legacy was enormous — it was the first program to cleanly separate domain knowledge from a general problem-solving engine, which became the foundation of expert systems. Its practical legacy was disappointing: every new problem had to be hand-encoded as a formal state space with explicit operators, it could not learn, and it was useless for anything perceptual or ill-defined. By 1969 it had been abandoned as a general solver.

### Where symbolic AI actually won

Symbolic AI succeeded wherever the rules were **explicitly formalizable and the domain was closed**. **Automated theorem proving** has been a durable triumph, from Robinson's 1965 resolution principle through modern proof assistants — Coq (1989), Isabelle (1986), and Lean (2013) — used to formally verify the Four Color Theorem, the Feit-Thompson theorem, and the CompCert compiler. **Symbolic algebra** yielded Macsyma (MIT, 1968), Maple, and Mathematica. **Chess** fell to essentially symbolic methods: Deep Blue's 1997 defeat of Kasparov was alpha-beta minimax on a handcrafted evaluation function with about 8,000 features tuned by grandmasters, plus specialized hardware and opening/endgame books.

**Expert systems** had a brief commercial boom. **DENDRAL** (Stanford, from 1965 — Feigenbaum, Buchanan, Lederberg, Djerassi) inferred molecular structures from mass-spectrometry data and is generally regarded as the first true expert system. **MYCIN** (Stanford, early 1970s — Edward Shortliffe) diagnosed bacterial infections using about 500–600 backward-chaining rules with certainty factors; it outperformed five of eight physicians on a test set but was never clinically deployed. **XCON/R1** (CMU / Digital Equipment Corp, deployed 1980 — John P. McDermott, written in OPS5) configured VAX orders, grew to about 2,500 rules, processed around 80,000 orders a year at 95–98% accuracy, and saved DEC somewhere between **$25 million and $40 million annually** at its peak — figures vary by source, so use the range.

### Polanyi's Paradox — the wall

The philosophical ceiling is best named by **Michael Polanyi**, a Hungarian-British polymath who pivoted from physical chemistry to philosophy of science in his fifties. In *The Tacit Dimension* (1966, p. 4), he wrote the sentence that indicts an entire research program: **"we can know more than we can tell."** His own illustration: we can recognize a single face among millions, yet usually cannot say how. The same is true of riding a bicycle, speaking grammatically, distinguishing a robin from a sparrow, or writing a persuasive paragraph. Most human competence is **tacit** — performed without articulable rules.

This is devastating for symbolic AI, which requires rules to be typed in, formalized, and debugged. Expert systems ran straight into this wall under the label **knowledge-acquisition bottleneck**: experts couldn't explain how they made judgments, only give rules-of-thumb that captured a fraction of their competence. MIT economist **David Autor** named it "Polanyi's Paradox" in a 2014 paper, observing that contemporary machine learning "seeks to overcome Polanyi's paradox by building machines that learn from human examples, thus inferring the rules that we tacitly apply but do not explicitly understand." That single observation is the bridge the whole series is building toward.

---

## 4. The Summer Vision Project (1966)

On **July 7, 1966**, Seymour Papert issued **MIT AI Memo No. 100**, titled simply *"The Summer Vision Project."* It proposed to attach a vidisector camera to a computer and, with a team of summer workers coordinated by the undergraduate **Gerald Sussman**, build a system that would perform, in sequence: **figure-ground analysis** (segmenting pixels into likely objects, background, and chaos), **region description** (characterizing shape, texture, surface properties), and **object identification** (matching regions against a stored vocabulary of known objects like balls, cylinders, cups, tools). Scenes would consist of simple non-overlapping objects. The memo itself states that "the particular task was chosen partly because it can be segmented into sub-problems which allow individuals to work independently and yet participate in the construction of a system complex enough to be a real landmark in the development of pattern recognition." (The phrasing "to be real landmark" is a verbatim typo in the original.)

**Authorship nuance for the script**: the memo's only listed author is Papert. Popular retellings often credit Minsky with "assigning" the project, and he was co-director of the AI group, but the documented author is Papert. The correct phrasing is: "Written by Seymour Papert in July 1966, with Gerald Sussman — then an undergraduate — named as project coordinator." The memo is archived at MIT DSpace (handle/1721.1/6125) and mirrored on Rodney Brooks's CSAIL page.

The project failed because vision is not a symbolic problem. The symbolic pipeline — edge detection, region segmentation, shape matching, object labeling — degrades rapidly under real-world variability: lighting changes, shadows, occlusion, noise, texture, viewpoint. There are no crisp symbolic rules that capture what makes something a cat, a face, or a cup across all real views. It took forty-six years and **AlexNet (2012)** — a deep convolutional network trained on ImageNet — to crack general object recognition. **David Marr** at MIT in the late 1970s offered a more principled symbolic approach, organized around his famous three levels (computational theory, algorithm/representation, hardware implementation) and the pipeline primal sketch → 2½-D sketch → 3-D model; his posthumous book *Vision* (1982) shaped a generation. But Marr was a corrective to AIM-100, not a vindication.

The memo has become **the archetypal cautionary tale of AI hubris** — a one-page document proposing to solve a grand-challenge problem with interns over a summer, now cited in essentially every history of computer vision. The Lighthill Report did not name it specifically, but its critique of what Lighthill called Category B — the "Bridge" between advanced automation and neuroscience, epitomized by integrated robot perception in toy microworlds — directly targets the class of ambitions AIM-100 exemplifies.

---

## 5. The AI Winters

### First AI Winter (roughly 1974–1980)

The crash had multiple authors. In **1966** the ALPAC report effectively killed machine-translation funding in the United States, concluding that MT was "more expensive, less accurate and slower than human translation" after about $20 million had been spent. The **Mansfield Amendment (1969)**, attached to the FY1970 Military Authorization Act by Senate Majority Leader Mike Mansfield, required DARPA to fund only "mission-oriented direct research, rather than basic undirected research." This gutted the open-ended patronage that had built the MIT AI Lab, CMU, and Stanford AI; every proposal now needed a near-term military justification. In **1974** DARPA cancelled its five-year **Speech Understanding Research** program at CMU/BBN/SDC after the HARPY/HEARSAY-II systems failed to deliver usable speech recognition. Hans Moravec, quoted in Crevier's 1993 history, captured the mood: researchers "felt they couldn't in their next proposal promise less than in the first one, so they promised more." When they couldn't deliver, the punishment was public.

The single most consequential document was **Sir James Lighthill's 1973 report, "Artificial Intelligence: A General Survey"**, commissioned by the UK Science Research Council. Lighthill — Lucasian Professor of Applied Mathematics at Cambridge, the chair once held by Newton — divided AI into three categories: **A (Advanced Automation)**, **B (Building Robots / "Bridge" activity)**, and **C (Computer-based CNS research)**. His verdict on Category B, the integrated-AI enterprise that SHRDLU and the Summer Vision Project typified, was unsparing. His opening summary judgment: *"In no part of the field have the discoveries made so far produced the major impact that was then promised."*

The conceptual core of the report was the **combinatorial explosion** argument: *"failure to recognise the implications of the 'combinatorial explosion.' This is a general obstacle to the construction of a self-organising system on a large knowledge base which results from the explosive growth of any combinatorial expression... as the base's size increases."* On speech: *"large expenditure on schemes to produce machine recognition of ordinary speech has been wholly wasted."* On robotics: *"the engineering complications required to achieve eye-hand co-ordination (not of human standard but similar to what an octopus can learn) have been repellingly formidable."* On chess: the best programs play at "experienced amateur" standard and masters beat them easily. His sweeping conclusion: it is "unrealistic to expect highly generalised systems" capable of learning on a large knowledge base to be developed in the twentieth century.

The report led the British government to dismantle AI funding almost everywhere but Edinburgh, Essex, and Sussex, and produced the **May 9, 1973 BBC "Controversy" debate** at the Royal Institution, in which Lighthill faced Donald Michie, John McCarthy, and Richard Gregory. The debate still exists on archive.org — watchable and quotable.

### Second AI Winter (roughly 1987–1993)

The second crash was commercial. The expert-systems boom of the early 1980s had produced a hardware ecosystem of **specialized Lisp machines** from Symbolics, LMI, Texas Instruments (Explorer), and Xerox — an industry worth about half a billion dollars at its peak. In **1987**, general-purpose workstations from Sun and Apollo running Lucid or Franz Common Lisp matched or exceeded Lisp-machine performance at a fraction of the price. Crevier's summary is stark: *"an entire industry worth half a billion dollars was replaced in a single year."* Symbolics's fiscal year ending June 30, 1987 showed revenue of $103.8 million and a $25.5 million net loss; LMI went bankrupt the same year; Symbolics filed Chapter 11 in early 1993.

Simultaneously, expert systems hit the **knowledge-acquisition bottleneck** and the brittleness wall. XCON grew toward 10,000 rules, each new DEC product required costly knowledge engineering, experts disagreed with each other, and systems made grotesque mistakes on unusual inputs. By the early 1990s most of them had been abandoned. At DARPA, Jack Schwarz took over IPTO in 1987, dismissed expert systems as "clever programming," and — in Crevier's phrase — cut AI funding "deeply and brutally." The **Strategic Computing Initiative** (1983–1993) ended with few deliverables; only the DART battle-management system, used in the first Gulf War, was a clear success. **Japan's Fifth Generation Computer Systems** project (1982–1992), with a budget around ¥54 billion, bet on massively parallel Prolog-style inference machines; it ended on June 1, 1992 to the *Washington Post* headline "ended not with a bang but a seminar." Russell and Norvig note the AI industry grew "from a few million dollars in 1980 to billions of dollars in 1988" — commonly cited as a peak around **$2 billion** — before collapsing.

A minor revisionist note worth flagging: Thomas Haigh (*CACM*, December 2023, "There Was No 'First AI Winter'") has argued that while funding collapsed, the research community did not — SIGART membership actually grew from 1,241 in 1973 to about 3,500 in 1978. Use "funding winter" rather than "research winter" if you want to be precise.

---

## 6. The bridge to machine learning

### Rosenblatt and the Perceptron

**Frank Rosenblatt** — a research psychologist at Cornell Aeronautical Laboratory in Buffalo, and a Bronx High School of Science classmate of Marvin Minsky — built the Perceptron under Office of Naval Research funding. He first simulated the algorithm on an IBM 704 in 1957; the custom hardware **Mark I Perceptron**, publicly demonstrated on June 23, 1960, had a 20×20 photocell input array, association units that summed weighted inputs, and — charmingly — weights implemented as **physical potentiometers adjusted by small electric motors**. The learning rule was simple: if the prediction was wrong, nudge the weights toward the correct answer. The **Perceptron Convergence Theorem** guaranteed that for any linearly separable data, the algorithm would find a separator in finite steps.

The hype, and the incident that haunts the field, was a **United Press International story datelined July 7, 1958**, run in the *New York Times* the next day under the headline "NEW NAVY DEVICE LEARNS BY DOING." Its opening line described the Perceptron as "the embryo of an electronic computer" that the Navy expected would "be able to walk, talk, see, write, reproduce itself and be conscious of its existence." The exact verbs belong to the Navy press release, not to Rosenblatt directly — but Rosenblatt was the demonstrator, told reporters the machine would be "the first device to think as the human brain," and speculated that future Perceptrons might be fired at the planets as mechanical space explorers. The line between scientist and press release was thin.

### The Minsky and Papert book (1969)

*Perceptrons: An Introduction to Computational Geometry* (MIT Press, 1969) is dedicated to Frank Rosenblatt and was mathematically devastating. Its most famous result: a single-layer perceptron cannot compute the **XOR** function, because XOR is not linearly separable — no straight line separates {(0,1),(1,0)} from {(0,0),(1,1)}. The book also proved, under a locality assumption on hidden units, that parity requires perceptron order growing without bound with input size, and that determining whether a figure is topologically connected similarly requires growing order (the cover's famous spiral figures illustrate this). In the 1988 expanded edition Minsky and Papert added their notorious prediction that multilayer extensions would be a **"sterile"** direction because gradient descent would fail.

**The contested part of the story**: did the book kill neural networks for a decade? The standard telling says yes. The revisionist view (Olazaran 1996 in *Social Studies of Science*; Pollack; Widrow) is more careful. Minsky and Papert did know multilayer networks could in principle compute any Boolean function — they said so inside the book. Their real claim was narrower: no one knew how to *train* them, and they suspected no one would. On this they were technically correct in 1969 and spectacularly wrong after 1986. The book's effect was amplified by the symbolic-AI / connectionist funding fight within the community — Olazaran's reading is that *Perceptrons* became the authoritative pretext for a funding decision that had sociological as well as mathematical causes. **Frank Rosenblatt died on July 11, 1971**, his 43rd birthday, in a boating accident in Chesapeake Bay, before backpropagation would vindicate his program. The multilayer training problem was solved in principle by Werbos in 1974 and brought into the mainstream by Rumelhart, Hinton, and Williams in *Nature* in 1986 — the topic of Episode 3.

### Why symbolic AI failed at perception — and what replaced it

The through-line is Polanyi's Paradox. Perception tasks — recognizing a cat across pose and lighting, parsing an ambiguous sentence, reading cursive handwriting, understanding accented speech — do not reduce to articulable rules. Human experts cannot write down what they know. Symbolic AI, which requires explicit rules, cannot bridge this gap. The **frame problem** (McCarthy and Hayes, 1969) offered a second version of the same obstacle: a logic-based robot needs to axiomatize not only what an action changes but also everything it *doesn't* change — for F facts and A actions, roughly 2·A·F frame axioms just to say the wallpaper color doesn't change when you pick up the phone. Combinatorial explosion from a different direction.

Machine learning's core insight is the inversion: **instead of writing rules, infer them from examples.** A vision model never receives a definition of "cat"; it is shown millions of cats. This is how the system escapes Polanyi's wall — by not requiring the knowledge to be told.

---

## 7. Analogies and demonstrations for the script

The script should make the brittleness/flexibility contrast visceral. Five analogies that work for a software-and-engineer audience:

**The phonebook versus the receptionist.** A phonebook given *"Bob Smith"* returns 555-1234 perfectly, every time, faster than any human. Give it a voicemail mumbling *"yeah, text me Bob's cell, uh, Smith, from accounting"* and it's useless. A receptionist who's never read a sorting algorithm handles this instantly. Symbolic AI built world-class phonebooks. Real intelligence needed a receptionist.

**The Rube Goldberg machine.** A rules-based expert system is a beautiful cascade of if-then dominos that does one thing flawlessly *when every input is exactly where the designer expected*. Move one marble half an inch and the contraption halts. A learned system is more like water flowing downhill — it finds *a* path even on new terrain, because it was never following a script, just gradients.

**Specifying "cat."** Try writing a compiler-precise spec for "cat." Four legs? So has a table. Fur? So has a coconut. You'll spend your life adding edge cases until the first Sphynx crashes production. Show a two-year-old twenty cats over a week and she's classifying Persians, tabbies, and cartoons at 95% accuracy with no rules. Symbolic AI tried to be the spec. ML is the toddler.

**The phrasebook traveler.** A tourist with a phrasebook orders coffee flawlessly — until the waiter asks a follow-up the book didn't anticipate. Symbolic AI is the phrasebook. Fluency requires learning a language from immersion, not lookup tables.

**The chef's recipe versus the chef's hands.** A recipe works in Ohio and fails in Denver at altitude, because it doesn't know about vapor pressure and egg size. A working chef *knows* when the dough is right by touch and cannot fully explain it. That is Polanyi's Paradox in aprons. Symbolic AI tried to codify the recipe. ML apprentices a chef.

For the frame-problem bit, a concrete demonstration: imagine programming a robot to make a sandwich. In a pure logic-based approach, you have to tell it — explicitly — that opening the fridge doesn't change the bread's molecular structure, that walking to the counter doesn't change the day of the week, that picking up a knife doesn't delete its memory. For every possible fact. This is why symbolic robots spent twenty years trying to cross a room.

The concrete "things that stump symbolic AI" demo reel: recognizing a cat in any pose or lighting; parsing *"I saw the man with the telescope"* (whose telescope?); reading varied handwriting; understanding accented speech; answering *"if I put my coffee on the table and walk away, is it still there?"* Humans handle each of these without thought. Every one defeated fifty years of rule-based effort. That gap is the entire reason the next episode exists.

---

## Key uncertainties flagged for the script

A few items deserve hedged phrasing on camera. ELIZA's original code was in **MAD-SLIP**, not Lisp — the Lisp port (by Bernie Cosell at BBN circa 1966) came slightly later and became dominant, which is why many sources misremember. The line count is context-dependent: the core interpreter is around 230 lines, the full restored listing with helpers about 420. The secretary who asked Weizenbaum to leave the room was real and was his actual secretary, but her name has not been published. ELIZA's original output had no question marks — that was a CTSS artifact — so authentic reproduction uses ALL CAPS with no punctuation. XCON's savings figures range from $25 million to $40 million per year; give a range. The *Perceptrons* book's role in killing neural-net research is genuinely contested among historians; the Olazaran (1996) reading is that funding politics amplified mathematical proofs that were narrower than the community took them to be. Logic Theorist's more elegant proof is usually cited as Theorem 2.85 of *Principia*, though edition numbering varies. The Summer Vision Project memo is authored by Papert — Minsky is commonly but incorrectly named as author in popular retellings.

One last note on the masswerk emulator: it is at **masswerk.at/elizabot/eliza.html**, built by Norbert Landsteiner in 2005 as a faithful reproduction of Weizenbaum's 1966 data model — including the pre/post substitutions, synonym classes, and memory queue — and it offers a deterministic mode that reproduces the canonical 1966 conversation verbatim. It is the single best on-camera recreation tool available.
