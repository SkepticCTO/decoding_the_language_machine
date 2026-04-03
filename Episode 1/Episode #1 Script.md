### **SCENE 1: THE MANUAL MACHINE (COLD OPEN)**

**NARRATOR (V.O.)** There is no computer in this room. There is no electricity powering this computation. It's 1948\. The man with the book is Claude Shannon. He is sitting in a quiet office at Bell Labs, and he's manually simulating a mind.

He isn't writing. He isn't thinking. He is following a strict, simple algorithm: Open the book at random, find the word on his paper, write down the word immediately following it, repeat.

He is playing a game of probability, sampling from the random distribution of the English language. And yet, look at the output: "The head and frontal attack on an English writer." It sounds like a sentence. It sounds like it has meaning.

But Shannon knows it doesn't. He knows exactly where it is from. It came from a blind hop from one word to the next. He has just built the world's first large language model, and he did it with a book and a pencil.

### **SCENE 3: Series Intro**

**DR. BUTCH** If you’ve seen any AI news in the last two years, you have been told that magic has arrived. Computers can now think, plan, and possibly even feel. You’ve heard AI executives claim that Large Language Models have consciousness.

Hi. I’m Dr. Butch. I’ve done research in computer vision and machine learning. I’m a principal investigator in the NIST AI Safety initiative. And it drives me crazy when I hear AI “experts” claim that we have no idea how large language models work.

When we have no idea how a large language model works, we’ll treat it like a black box. We’ll see magic instead of technology. We’ll start to see ghosts in the machine.

The goal of this series, "Decoding the Language Machine," is to exorcise those ghosts. We’re going to open the box. And when we look inside, we’re going to find statistics. We’re going to find geometry. We’re going to find the "Unreasonable Effectiveness of Data."

The "magic" of LLMs is actually the accumulation of seventy years of engineering discoveries and mathematical insights. That history is the roadmap for our series.

Episode 1: The Stochastic Dawn. That’s this episode. Here we’ll see through Shannon’s work that statistics can cause words to emerge from letters, and sentences to emerge from words.

Episode 2: Symbolic AI and the AI Winter. We’ll look at ELIZA, the first chatbot, and the "Summer Vision Project," where scientists thought they could solve computer vision in three months. Spoiler: They didn't. But we’ll learn that symbols and logic can only get us so far, and through the “ELIZA Effect” we see that computers can "look smart" without "being smart."

Episode 3: The Learning Revolution. Here we’ll see the rise of Neural Networks and Backpropagation. At this moment we stopped telling computers the rules and started asking them to learn the rules from data.

Episode 4: The Geometric Turn. By turning words into vectors computers discovered synonyms, antonyms and analogies through statistics.

Episode 5: The Transformer Era. We’ll see how "Attention" mechanism and Scaling Laws led to the first large language models that dramatically changed what we thought was possible with AI.

Episode 6: Scale and Emergence. Here we’ll see how the amazing emergent properties of today’s LLMs continue to grow, and the potential impact of cooperative agents and improved memory systems.

By looking at these discoveries we’ll gain a better understanding of how AI works today and an intuition of where it is going.

**DR. BUTCH** But today, we go back to the source. Before the microchip. Before the internet. Before the GPU. To a time when "computer" was a job title for a human, and "information" was just a vague concept. We are going to meet the man who turned language into math. Claude Shannon.

---

### **SCENE 4: THE WORLD OF WIRES (1948 CONTEXT)**

**DR. BUTCH (V.O.)** To understand Shannon’s breakthrough, we have to understand the problem he was trying to solve. He wasn't trying to build a chatbot. He was working for Bell Labs, the research arm of the American Telephone and Telegraph company (or AT\&T). In the 1940s, communication was a physical, analog mess.

You spoke into a microphone, your voice was converted into a voltage wave, and that wave was sent down a wire. The enemy was Noise. Static. Interference. Signal degradation. The farther the signal traveled, the more it degraded. If you tried to amplify the signal to make it stronger, you amplified the noise, too. It was a losing battle against the laws of physics.

One way to battle noise is to add redundancy. Early telephone and radio operators had a hard time hearing letters “A”, “B”, “C”, “D” over noisy lines (letters sound a lot alike). So they developed spelling alphabets, “Alpha” “Bravo” “Charlie” “Delta”, the NATO alphabet, with letters that are longer and easier to differentiate in the presence of noise. 

That works for really short messages, but if I’m talking to you we can’t spell every word out\!

Enter Claude Shannon. A mathematician. A cryptographer. And a unicyclist. He looked at this mess and had a radical thought. Maybe there’s redundancy already in the words we speak. How much information really is in the message "I love you" or "The invasion begins at dawn"?

Shannon had the insight to think of “information” in terms of probability. With this he opened the floodgates to the information age we enjoy now. But what is “information”?

---

### **SCENE 5: THE BIT AND THE SURPRISE**

**DR. BUTCH** Shannon defined information as the Resolution of Uncertainty. Imagine I flip this coin. Right now, you are uncertain. It could be Heads, it could be Tails. 50/50. When I lift my hand, I resolve that uncertainty. I have just transmitted exactly 1 Bit of information to you

A "Bit", a term Shannon popularized, is a binary digit. 1 Bit is a choice between two equally likely alternatives. Now, imagine I have a coin with Heads on both sides. I flip it. You know it’s going to be Heads. There is zero uncertainty. When I show you it’s Heads, how much information have I transmitted? Zero.

Because you were not surprised. Information is Surprise. This is the core intuition of Information Theory. The more predictable a message is, the less information it contains.

This is Shannon’s formula for Entropy – the measure of Information. It calculates the average amount of "surprise" in a message. Armed with this definition, Shannon then asked a weird question: What is the entropy of the English language?

If I send you a letter... say, the letter 'Z'... how surprised are you? Well, if English letters were truly random (a monkey banging on a typewriter) every letter would be equally likely. A 'Z' would be just as common as an 'E'. But English isn't random. English has Structure.

We know that letter 'E' appears about 12% of the time (1 out of every 8 letters you read in English is the letter ‘E’). 'Z' appears less than 0.1% of the time (1 out of 1300). This means 'Z' carries more "surprise", more information, than 'E'.

But Shannon went deeper. He realized that letters depend on the letters that came before them. This is the Stochastic nature of language. "Stochastic" means "random" but having patterns that we can be analyze statistically.

If I write the letter 'Q'... what is the next letter going to be? You know it’s going to be 'U'. The probability of 'U' given 'Q' is nearly 100%. This means the letter 'U' when it appears with “Q”  carries almost zero information. It’s redundant.

Shannon played guessing games with wife Betty, who was also a mathematician, and together they calculated that English letters are about 50% redundant. Take a look at this sentence (feel free to pause)  Do you understand it? To me it says “You can remove half the letters in a sentence and you can still read it.”

But how? Because our brains are Prediction Machines. We are constantly predicting the world around us. Shannon thought: if humans do this... could a machine do it?

---

### **SCENE 6: THE N-GRAM EXPERIMENT**

**DR. BUTCH** So he designed an experiment called "Approximations to English". He wanted to see if he could generate text that looked like English, purely by using statistics. He looked at what he called “N-Grams”. An "N-Gram" is just a sequence of N items. Let’s recreate his experiment, step by step, to see how structure emerges from chaos.

Level Zero. The Monkey at the Typewriter. Symbols are independent and equiprobable. Each letter has a 1 in 26 chance. Let's see what we get.

Gibberish. High entropy. Maximum surprise. This looks nothing like English. It’s unpronounceable. So let’s introduce the First Constraint: Frequency.

Level One. We select letters independently, but we weight our letter dice rolls to match English frequency. 'E' comes up 12% of the time. 'T' 9%. 'Z' almost never. We respect the population statistics, but not the order.

Better. "OCRO". "NMIELWIS". It’s still nonsense, but it looks more pronounceable. We see vowels appearing between consonants. We see the "shape" of English emerging. But it’s still not language. So let’s introduce the  Second Constraint: Context.

Level Two. Let’s look at letter pairs: the Digram. Now, the choice of the next letter depends on the previous letter. If the last letter was 'T', we don't roll the generic letter dice. We roll the "What comes after T?" dice.

Shannon didn't have a computer to calculate these probabilities. So he used the hack from the intro. He used a book. To find the letter after 'T', he opened the book at random, scanned for a 'T', and recorded the letter immediately following it. He was sampling from the distribution of the English language itself.

Look at that. "ON". "ARE". "BE". Real words are forming. Shannon’s machine didn't know the word "ARE". It didn't have a dictionary. The word "ARE" emerged from the statistics of letter pairs. 'A' likes to be followed by 'R'. 'R' likes to be followed by 'E'. Structure is emerging from probability.

Level Three: Let's consider groups of three letters. The Trigram. The probabilities now depend on the last two letters.

"DEMONSTURES". That’s not a word. But it should be a word. It sounds like "Demonstrate" mixed with "Gestures." The machine is creating plausible words because it has learned the local rules of English morphology. It has learned how to sound English, without knowing English.

---

### **SCENE 7: THE STOCHASTIC PARROT**

**DR. BUTCH** Shannon realized that doing this letter-by-letter was tedious. So he took it to the next level. He switched to N-Grams using words. Instead of predicting the next letter from previous letters, predict the next word from previous words. Let’s look at Shannon’s Second-Order Word Approximation.

Here, each word is chosen based on the probability of following the previous word. Read that sentence. "The head and in frontal attack on an English writer that the character of this point is therefore..." It sounds profound, doesn't it? It sounds like a literary critic analyzing a novel. But this sentence was generated by a lookup table of word pairs.

It doesn’t really have meaning. It’s a “Stochastic Parrot”. Even then we find phrases and sentence structure.

From Shannon’s experiments we get our first flash of intuition about artificial intelligence: Stochastic systems have emergent properties. When we explore relationships between letters, we discover words. When we explore relationships between words, we discover phrases and sentences.

So intuitively, what if we can somehow replace Shannon’s single book with a whole library, or maybe the whole internet? What if we could increase our 2 word n-grams to hundreds or thousands of words?

Maybe we can write English text just from statistics. Maybe we can answer questions. Here is the key insight: “LLMs are stochastic parrots with capabilities that emerge from human language.” When LLMs surprise us, we learn more about ourselves.

---

### **SCENE 8: CONCLUSION – THE BRIDGE TO 2026**

**DR. BUTCH** So, if Shannon figured this out in 1948, why didn't we have ChatGPT in 1950? Three reasons.

One: Data. Shannon had one book. Today, we have the entire internet.

Two: Stochastic systems. How can we capture the statistics of n-grams in the thousands? Modern LLMs estimate these distributions using deep neural networks, which we’ll encounter in Episode 3\.

Three: Representation. Shannon treated words as text symbols. LLMs use vectors for words, which have amazing properties that we’ll encounter in Episode 4\.

But in the next episode, we’ll see that for the next 25 years after Shannon’s experiments, computer scientists would try a different path. They would try to write down the rules of English by hand. They would try to teach computers grammar, logic, and syntax. They would build "Expert Systems" and "Symbolic AI."

And they would discover that there are things that humans do that are really hard for symbolic logic. They missed the fundamental truth of the Stochastic Dawn: Language is not a set of rules. Language is a distribution. Why would language be that way? Because we humans are incredible at pattern matching.

So next time, we’re going to look at the Symbolic AI and the AI Winter. We’re going to meet ELIZA, the first chatbot, and the scientists who thought they could solve computer vision in a single summer.

We’re also going to see that humans are easily fooled by machines that can talk... and why "looking smart" is very different from "being smart." Thank you for watching, and I look forward to seeing you in the next episode.

## 

## Credits

The writer, editor, and speaker is Robert Buccigrossi, Ph.D. (“Dr. Butch”)

The video “Decoding the Language Machine \- Episode 1” is Copyright 2026 SkepticCTO, LLC.

With the exception of the likeness and vocals of speakers and guests, most of the material is provided under a Creative Commons License. Please see [https://www.decodingthelanguagemachine.com](https://www.decodingthelanguagemachine.com) for more information.

A significant portion of the graphics, diagrams, and songs were created with AI or the Python library “manim”. Source code and prompts will be made available at [https://www.decodingthelanguagemachine.com](https://www.decodingthelanguagemachine.com) .

The theme song for “Decoding the Language Machine” is a variation of the Jazz riff known as “The Lick” (shout out to Adam Neely)..

Other sources include:  
Distribution of English Letters  
 \- By Nandhp \- Own work; en:Letter frequency., Public Domain, https://commons.wikimedia.org/w/index.php?curid=9971073

Unreasonable Effectiveness of Data  
 \- Alon Halevy, Peter, Norvig, and Fernando Pereira, Google

Eliza Terminal \- https://www.masswerk.at/elizabot/eliza.html  
 \- Norbert Landsteiner

Summer Vision Project \- MIT Report  
 \- https://people.csail.mit.edu/brooks/idocs/AIM-100.pdf

Image of Bell System Telephone Switchboard  
 \- https://catalog.archives.gov/id/1633445

Approximations to English ("A Mathematical Theory of Communication")  
 \- https://people.math.harvard.edu/\~ctm/home/text/others/shannon/entropy/entropy.pdf

Many thanks to:  
 \- Daniel Turner (CEO of TCG, Inc.) \- For encouraging me to go on sabbatical and start this project  
 \- Jennifer Buccigrossi \- For patient support  
 \- Sarah Buccigrossi \- For artistic guidance  
 \- The Rogues of “The Skeptic’s Guide to the Universe” \- For being an inspirational voice of scientific reason  
