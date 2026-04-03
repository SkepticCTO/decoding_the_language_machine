Note: My approach to using the Manim scripts was to run them in this wonderful online notebook:

[https://mybinder.org/v2/gh/ManimCommunity/jupyter\_examples/HEAD?filepath=First%20Steps%20with%20Manim.ipynb](https://mybinder.org/v2/gh/ManimCommunity/jupyter_examples/HEAD?filepath=First%20Steps%20with%20Manim.ipynb) 

## Animation for Shannon Entropy Equation

%%manim \-qh ShannonEntropy

class ShannonEntropy(Scene):  
    def construct(self):  
        \# 1\. Display the Title and General Equation  
        title \= Text("Entropy").to\_edge(UP)  
        self.play(Write(title))

        \# Using split strings in MathTex helps TransformMatchingTex know what parts to animate later  
        equation \= MathTex(  
            r"H(X)", r"=", r"- \\sum\_{i=1}^n", r"P(x\_i)", r"\\log\_2 P(x\_i)"  
        )  
          
        self.play(Write(equation))  
        self.wait(2)

        \# Move the general equation up to make room for the calculation  
        self.play(equation.animate.scale(0.8).next\_to(title, DOWN, buff=0.5))

        \# 2\. Introduce the Fair Coin scenario  
        coin\_setup \= Text("Fair Coin: Heads (H) or Tails (T)").scale(0.6).next\_to(equation, DOWN, buff=0.75)  
        self.play(FadeIn(coin\_setup, shift=DOWN))

        probabilities \= MathTex(r"P(H) \= 0.5", r"\\qquad", r"P(T) \= 0.5")  
        probabilities.next\_to(coin\_setup, DOWN, buff=0.3)  
        self.play(Write(probabilities))  
        self.wait(1)

        \# 3\. Step-by-step Calculation  
        \# Step A: Substitution  
        calc\_step\_1 \= MathTex(  
            r"H(\\text{Coin})", r"=", r"- \\big(", r"0.5", r"\\log\_2(0.5)", r"+", r"0.5", r"\\log\_2(0.5)", r"\\big)"  
        ).next\_to(probabilities, DOWN, buff=0.75)  
          
        self.play(Write(calc\_step\_1))  
        self.wait(2)

        \# Step B: Evaluate the logarithm (log2(0.5) \= \-1)  
        calc\_step\_2 \= MathTex(  
            r"H(\\text{Coin})", r"=", r"- \\big(", r"0.5", r"(-1)", r"+", r"0.5", r"(-1)", r"\\big)"  
        ).next\_to(probabilities, DOWN, buff=0.75)

        self.play(TransformMatchingTex(calc\_step\_1, calc\_step\_2))  
        self.wait(2)

        \# Step C: Multiply  
        calc\_step\_3 \= MathTex(  
            r"H(\\text{Coin})", r"=", r"- \\big(", r"-0.5", r"-", r"0.5", r"\\big)"  
        ).next\_to(probabilities, DOWN, buff=0.75)

        self.play(TransformMatchingTex(calc\_step\_2, calc\_step\_3))  
        self.wait(2)

        \# Step D: Final Result  
        calc\_step\_4 \= MathTex(  
            r"H(\\text{Coin})", r"=", r"1", r"\\text{ bit}"  
        ).next\_to(probabilities, DOWN, buff=0.75)  
        calc\_step\_4.set\_color\_by\_tex("1", YELLOW)  
        calc\_step\_4.set\_color\_by\_tex(r"\\text{ bit}", YELLOW)

        self.play(TransformMatchingTex(calc\_step\_3, calc\_step\_4))  
          
        \# Add a celebratory box around the final answer  
        box \= SurroundingRectangle(calc\_step\_4, color=YELLOW, buff=0.2)  
        self.play(Create(box))  
          
        self.wait(3)  
