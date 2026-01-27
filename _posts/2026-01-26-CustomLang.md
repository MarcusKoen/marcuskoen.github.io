---
author: Marcus Koen
title: Fuck it all. Time for a new language. weebC.
---
<style>
html, body {
  margin: 0;
  padding: 0;
  background: #0f0f0f;
  color: #e0e0e0;
  font-family: monospace, system-ui, sans-serif;
}

/* Rain container */
.rain-container {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
  overflow: hidden;
}

/* Individual raindrop */
.raindrop {
  position: absolute;
  width: 1px;
  height: 60px;
  background: linear-gradient(
    to bottom,
    rgba(200, 220, 255, 0),
    rgba(200, 220, 255, 0.35)
  );
  animation: rain linear infinite;
}

/* Falling animation */
@keyframes rain {
  from {
    transform: translateY(-120vh) translateX(0);
  }
  to {
    transform: translateY(120vh) translateX(-80px);
  }
}

/* Variation */
.raindrop:nth-child(1)  { left: 5%;  animation-duration: 0.9s; }
.raindrop:nth-child(2)  { left: 10%; animation-duration: 1.1s; }
.raindrop:nth-child(3)  { left: 15%; animation-duration: 0.8s; }
.raindrop:nth-child(4)  { left: 20%; animation-duration: 1.2s; }
.raindrop:nth-child(5)  { left: 25%; animation-duration: 0.95s; }
.raindrop:nth-child(6)  { left: 30%; animation-duration: 1.05s; }
.raindrop:nth-child(7)  { left: 35%; animation-duration: 0.85s; }
.raindrop:nth-child(8)  { left: 40%; animation-duration: 1.15s; }
.raindrop:nth-child(9)  { left: 45%; animation-duration: 0.9s; }
.raindrop:nth-child(10) { left: 50%; animation-duration: 1.2s; }
.raindrop:nth-child(11) { left: 55%; animation-duration: 0.8s; }
.raindrop:nth-child(12) { left: 60%; animation-duration: 1.1s; }
.raindrop:nth-child(13) { left: 65%; animation-duration: 0.95s; }
.raindrop:nth-child(14) { left: 70%; animation-duration: 1.05s; }
.raindrop:nth-child(15) { left: 75%; animation-duration: 0.85s; }
.raindrop:nth-child(16) { left: 80%; animation-duration: 1.15s; }
.raindrop:nth-child(17) { left: 85%; animation-duration: 0.9s; }
.raindrop:nth-child(18) { left: 90%; animation-duration: 1.2s; }
.raindrop:nth-child(19) { left: 95%; animation-duration: 0.8s; }

  /* Fix code block visibility */
pre, code {
  background-color: #0b0b0b !important;
  color: #f2f2f2 !important;
}

/* Inline code */
code {
  padding: 0.15em 0.35em;
  border-radius: 4px;
}

/* Fenced code blocks */
pre {
  padding: 1em;
  overflow-x: auto;
  border-radius: 6px;
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.08);
}

/* Optional: monospace consistency */
pre, code {
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
}

</style>

<div class="rain-container">
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div><div class="raindrop"></div><div class="raindrop"></div>
  <div class="raindrop"></div>
</div>

# In the beginning God said: "weebC is the true programming language", and there was light.
First things first: General theory and scope.
# Phase 0

# What level programming language
Essentially we have 3 options:
1. Compiled -> bytecode -> VM
2. Native code
3. Interpreted AST walker

Due to my knowledge in reverse engineering, designing custom VM is the route I will take.

# Paradigm
1. I will be using an Imperative + Functional approach.
2. Explicit memory control

# Flavour
1. Keywords in slang
2. Types named after tropes
3. Compiler errors as ( I cannot believe I am actually doing this) anime tsundere insults

Keep in mind: Syntax is anime, but the semantics are deadly serious and non-negotiable.

# Phase 1
All the work is done on a seperate repository [here](https://github.com/MarcusKoen/weebC)
# Token Parsing
Essentially breaking up the code that was given to the compiler into "tokens" e.g:
```
int x=3;
```
```
becomes: ['i','n','t',...,'3',';']
```
# Lexical Analyzer
This is what actually does the token parsing. A few options are available.
1. Manually do string manipulation in language of choice (C++)
2. Lex generation
3. Flex/RE-Flex generation

Due to time constraints and depleting sanity I will for the moment be using a lexical generator.
This will be reworked in the future to a proper C++ lexical analyzer :D
Nevermind I did it manually.
# Lexical Analyzer Code
```
#include <iostream>
#include <vector>
using namespace std;

    //An enum is a special type that represents a group of constants (unchangeable values)
    enum TokenType
    {
        Number,
        Identifier,
        Equals,
        LParen, RParen,
        BinaryOperator,
        Plus,
        Minus,
        Multiply,
        Divide,

        Be,

    };


/////////////////////////////////Token Class////////////////////////////////////////
    //Can use a struct here as well, just depends on default access modifier
    class Token
    {
    public:
        std::string value;
        TokenType type;
        //Constructor for Token class.
        //Just as a reminder for constructors in C++. 1. Same name as class. 2. No return type. 3. Has to be public.
        Token(std::string Value, TokenType Type)
        {
            //Can also use this.value, this.type, Just personal preference
            value = Value;
            type = Type;
        }
    };
///////////////////////////////////////////////////////////////////////////////

/////////////////////////////////Lexer Class//////////////////////////////////
    class Lexer
    {
    public:
        std::string text;
        int pos = -1;
        char current_char = '\0';//In C++ use '\0' NOT NULL

        //Lexer Constructor
        Lexer(std::string Text)
        {
            text = Text;
            Advance();
        }

        void Advance()
        {
            pos += 1;
            if(pos<text.length())
            {
                current_char=text[pos];
            }
            else
            {
                current_char = '\0';
            }

        }

    std::vector<Token> makeTokens() //Need to use vectors since we cant use dynamic arrays like Token token =[]
        {
        std::vector<Token> tokens;
            while(current_char!='\0')
            {
                if (isdigit(current_char))
                    {
                        tokens.push_back(makeNumber());
                        continue;
                    }

                switch(current_char)
                {
                    case ' ':
                    case '\t' :
                         Advance();
                         break;

                    case '+' :
                        tokens.push_back(Token("+",Plus));
                        Advance();
                        break;
                    case '-' :
                        tokens.push_back(Token("-",Minus));
                        Advance();
                        break;
                    case '*' :
                        tokens.push_back(Token("*",Multiply));
                        Advance();
                        break;
                    case '/' :
                        tokens.push_back(Token("/",Divide));
                        Advance();
                        break;
                    case '(' :
                        tokens.push_back(Token("(",LParen));
                        Advance();
                        break;
                    case ')' :
                        tokens.push_back(Token(")",RParen));
                        Advance();
                        break;
                    default: Advance();
                }

            }

            return tokens;
        }

    Token makeNumber()
    {
        std::string numStr;
        bool hasDot = false;

        while (current_char != '\0' &&
              (isdigit(current_char) || current_char == '.'))
        {
            if (current_char == '.')
            {
                if (hasDot)
                    break; // second dot stop number
                hasDot = true;
            }

            numStr += current_char;
            Advance();
        }

        return Token(numStr, Number);

    }

    };



///////////////////////////////////////////////////////////////////////////////



int main()
{
    Lexer test("12 + 3.14 * (5 - 2)");
    auto tokens = test.makeTokens();

    for (auto& t : tokens)
        cout << t.value << " ";


}
```
# Parser

# AST

# Nodes

# Interpreter

# General Observations

# Notes and Theory

This whole excersise was really good revision for OOP principles, however I completely forgot to modularize my program. Everything was coded in a single main.c file.
