# Introduction

+ focuses on context-free grammars (CFGs) which serve as a backbone for syntactical models of natural and computer languages
+ CFGs play a role in many computational applications inclusing grammar checking, semantic interpretation, dialogue understanding, machine translation
+ can express sophisticated relations between words in a sentence, while being computationally tractable (algorithms discussed in Chapter 13)
+ **lexical grammars** are also introduced
+ as an alternative to constituency grammars, dependency grammars also exist (chapter 16)

# 12.1 Constituency

+ syntactic constituency = the idea that groups of words can behave as single units/constituents
+ building a grammar involves building an inventory of constituents in the language
+ example: noun phrases as constituents:
  + Harry the Horse
  + a spot like Mindy's
+ what is the evidence for constituency --> 
  + evidence 1: the ability to appear in similar syntactic contexts
    + eg the entire NP can appear before a verb, while each individual word cannot necessarily do that
    + constituency is needed to make rules like "noun phrases can occur before verbs"
  + evidence 2: preposed/postposed constructions
    + a phrase like "on September seventeenth" can be inputted at different points in the sentence (beginning, end, middle)
    + but we cannot break the phrase up and place individual words at different points in the sentence
      + "on September seventeenth" must appear as a unit, regardless of location

# 12.2 Context-Free Grammars
+ 
