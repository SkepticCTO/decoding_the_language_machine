Note: My approach to using the Manim scripts was to run them in this wonderful online notebook:

[https://mybinder.org/v2/gh/ManimCommunity/jupyter\_examples/HEAD?filepath=First%20Steps%20with%20Manim.ipynb](https://mybinder.org/v2/gh/ManimCommunity/jupyter_examples/HEAD?filepath=First%20Steps%20with%20Manim.ipynb) 

### Standard manim import for jupyter:

import manim as mn  
from manim import \*

config.media\_width \= "75%"  
config.verbosity \= "WARNING"

print(mn.\_\_version\_\_)

### Simple Animation of title:

%%manim \-qm DecodingText  
import random  
import string

class DecodingText(Scene):  
    def construct(self):  
        \# 1\. Set the final target text  
        final\_text\_str \= "Decoding the\\nLanguage Machine"  
          
        \# 2\. Create a placeholder Text mobject  
        \# We use a monospace font like 'Consolas' or 'Monospace' to prevent   
        \# the text from jumping around as character widths change.  
        decoding\_text \= Text("".join(random.choices(string.ascii\_letters \+ string.digits, k=len(final\_text\_str))),   
                             font="Monospace").scale(1.2)  
          
        self.add(decoding\_text)

        \# 3\. Flash through random characters  
        \# Each iteration updates the text with a new random string of the same length  
        for \_ in range(15):  \# Adjust the range for longer/shorter flashing  
            random\_str \= "".join(random.choices(string.ascii\_letters \+ string.punctuation, k=len(final\_text\_str)))  
            new\_text \= Text(random\_str, font="Monospace").scale(1.2)  
            decoding\_text.become(new\_text)  
            self.wait(0.08) \# Speed of the "flicker"

        \# 4\. Final reveal  
        \# Transform the last random mess into the actual final string  
        final\_text\_mobject \= Text(final\_text\_str, font="Monospace").scale(1.2)  
        self.play(Transform(decoding\_text, final\_text\_mobject), run\_time=0.5)  
        self.wait(2)

### More Complex version of Title Animation:

%%manim \-qh DecodingTitle  
import random  
import string

class DecodingTitle(MovingCameraScene):  
    def construct(self):  
        \# Configuration  
        target\_string \= "  Decoding the Language Machine  "  
        font\_style \= "Monospace"   
        text\_color \= WHITE  
        run\_time \= 6   
        czoom \= 16  
        fps \= 24  
          
        \# 1\. Create the final target text object (Hidden)  
        target\_text \= Text(target\_string, font=font\_style, color=text\_color)  
        \# target\_text.arrange(RIGHT, buff=0.05)  
        target\_text.scale(1)  
        target\_text.move\_to(ORIGIN)  
          
        \# 2\. Create the "Display" text (Visible)  
        \# We will only create Mobjects for NON-SPACE characters to match target\_text's structure  
        display\_text \= VGroup()  
          
        \# We need to track which Mobject corresponds to which character  
        \# because 'target\_text' does not have entries for spaces.  
        for char in target\_string:  
            if char \== " ":  
                continue \# Skip spaces to avoid the IndexError  
              
            rand\_char \= random.choice(string.ascii\_uppercase \+ string.digits)  
            letter \= Text(rand\_char, font=font\_style, color=text\_color)  
            letter.scale(1.5)  
            display\_text.add(letter)  
              
        \# Align the starting random letters to the target text positions  
        \# Now len(display\_text) \== len(target\_text), so this works safely  
        for i, letter in enumerate(display\_text):  
            letter.move\_to(target\_text\[i\].get\_center())

        self.add(display\_text)

        \# 3\. Setup the Camera (Zoomed In)  
        \# We grab a letter near the middle. Since we skipped spaces, we safely grab a valid index.  
        focus\_index \= len(target\_text) // 2   
        self.camera.frame.move\_to(target\_text\[focus\_index\])  
        self.camera.frame.set\_width(target\_text\[focus\_index\].width \* czoom) 

        \# 4\. The Animation Loop  
        frames \= fps \* run\_time  
        dt \= 1 / fps  
          
        for frame in range(frames):  
            alpha \= frame / frames  
              
            \# \--- Camera Movement \---  
            current\_zoom\_width \= interpolate(  
                target\_text\[focus\_index\].width \* czoom,   
                target\_text.width \* 1.2 \+ 2,          
                rate\_functions.ease\_in\_out\_cubic(alpha)  
            )  
              
            current\_center \= interpolate(  
                target\_text\[focus\_index\].get\_center(),  
                target\_text.get\_center(),  
                rate\_functions.ease\_in\_out\_cubic(alpha)  
            )  
              
            self.camera.frame.set\_width(current\_zoom\_width)  
            self.camera.frame.move\_to(current\_center)

            \# \--- Text Decoding Logic \---  
            num\_solved\_chars \= int(len(target\_string) \* rate\_functions.ease\_out\_quad(alpha))  
              
            new\_group \= VGroup()  
              
            \# We must maintain a separate counter for the Mobject index  
            mob\_idx \= 0   
              
            for i, char in enumerate(target\_string):  
                if char \== " ":  
                    continue \# Skip logic for spaces completely  
                  
                target\_pos \= target\_text\[mob\_idx\].get\_center()  
                  
                \# Check if this specific character index (i) should be solved  
                if i \< num\_solved\_chars:  
                    new\_char \= Text(char, font=font\_style, color=text\_color)  
                else:  
                    \# Random scrambling  
                    if frame % 4 \== 0:  
                        rand\_char \= random.choice(string.ascii\_letters \+ string.digits)  
                        new\_char \= Text(rand\_char, font=font\_style, color=GREEN)  
                        new\_char.set\_opacity(1)  
                    else:  
                        \# Copy the existing character from the previous frame  
                        new\_char \= display\_text\[mob\_idx\].copy()

                \# new\_char.scale(1.5)  
                new\_char.move\_to(target\_pos)  
                new\_group.add(new\_char)  
                  
                \# Increment Mobject counter only when we processed a real letter  
                mob\_idx \+= 1  
              
            display\_text.become(new\_group)  
            self.wait(dt)

        self.wait(2)

### Animation for Digram Instructions

%%manim \-qh TextGenerationAlgorithm

class TextGenerationAlgorithm(Scene):  
    def construct(self):  
        \# Set the background color to white  
        self.camera.background\_color \= WHITE  
          
        \# Create the title (Bold, Black)  
        title \= Text("Text Generation", weight=BOLD, color=BLACK, font\_size=36)  
          
        \# Create the individual lines of text (Black)  
        subtitle \= Text("(Start by writing a random word)", color=BLACK, font\_size=24)  
        step1 \= Text("1) Open the book at random", color=BLACK, font\_size=24)  
        step2 \= Text("2) Find the last word you wrote down", color=BLACK, font\_size=24)  
        step3 \= Text("3) Write down the next word in the book", color=BLACK, font\_size=24)  
        step4 \= Text("4) Repeat", color=BLACK, font\_size=24)  
          
        \# Group and arrange the steps to be left-aligned  
        steps \= VGroup(subtitle, step1, step2, step3, step4)  
        steps.arrange(DOWN, aligned\_edge=LEFT, buff=0.4)  
          
        \# Group the title and the steps, which centers the title automatically above the left-aligned steps  
        text\_block \= VGroup(title, steps)  
        text\_block.arrange(DOWN, buff=0.6)  
          
        \# Scale the text block to fit strictly within the left 25% of the screen  
        \# We use 22% (0.22) to leave a small visual buffer near the screen edge  
        max\_width \= config.frame\_width \* 0.22   
        text\_block.scale\_to\_fit\_width(max\_width)  
              
        \# Move the entire block to the center of the left 25% region  
        \# The x-axis spans from \-frame\_width/2 to \+frame\_width/2.   
        \# \-3/8 (or \-0.375) places the center exactly in the middle of the left-most quarter.  
        left\_center\_x \= \-config.frame\_width \* 0.375  
        text\_block.move\_to(\[left\_center\_x, 0, 0\])  
          
        \# \--- Animation Sequence \---  
          
        \# Unveil the title first  
        self.play(Write(title))  
        self.wait(0.5)  
          
        \# Loop through the remaining steps, unveiling them one line at a time  
        for step in steps:  
            self.play(Write(step))  
            self.wait(0.5)  
          
        \# Hold the final frame for a moment before finishing  
        self.wait(2)

## Animation for episode years

%%manim \-qm YearSequence

class YearSequence(Scene):  
    def construct(self):  
        years\_data \= \["1948", "1966", "1986", "2013", "2017", "2026"\]  
          
        \# Calculate offscreen positions based on the camera frame width.  
        \# Adding a buffer ensures the text starts completely out of view.  
        start\_pos \= RIGHT \* (config.frame\_width / 2 \+ 2\)  
        end\_pos \= LEFT \* (config.frame\_width / 2 \+ 2\)  
          
        \# Create a list of Text mobjects for each year  
        year\_mobjects \= \[\]  
        for year in years\_data:  
            text \= Text(year, weight=BOLD, font\_size=96)  
            text.move\_to(start\_pos) \# Place offscreen right initially  
            year\_mobjects.append(text)  
              
        \# Generate the movement animations for each year.  
        \# We use rate\_func=linear so the speed is constant (no slowing down at the edges).  
        \# A run\_time of 4 seconds gives a nice, readable cruising speed.  
        slide\_animations \= \[  
            year.animate(run\_time=4, rate\_func=linear).move\_to(end\_pos)   
            for year in year\_mobjects  
        \]  
          
        \# LaggedStart staggers the animations.   
        \# A lag\_ratio of 0.5 means the next animation starts when the current one is 50% done.  
        \# Because we use a linear speed, 50% of the time equals exactly 50% across the screen.  
        self.play(LaggedStart(\*slide\_animations, lag\_ratio=0.5))  
          
        \# Give the final year a brief moment to finish clearing the screen  
        self.wait(1)  
