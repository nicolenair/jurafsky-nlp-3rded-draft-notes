# Chapter 21: Coreference Resolution

## Introduction

### Important Terms

+ mentions/referring expressions
+ referent
+ discourse model
+ evoked
+ accessed
+ anaphora
+ antecedent 
+ singleton
+ nesting of coreference mentions
+ main tasks in coreference resolution
+ Winongrad Schema Problems
+ event coreference
+ discourse deixis

## 21.1 Coreference Phenomena: Linguistic Background

### 21.1.1 Types of Referring Expressions
+ indefinite noun phrases
   + examples: a, an, this some etc
   + used to introduce discourse entities that are new to the learne
+ definite noun phrases
   + example: the
   + previously represented in the discourse model
+ pronouns
   + used in pronominalization (for salient entities)
   + can be "bound" (each __ her)
+ demonstrative pronouns
   + either as 
+ zero anaphora
   + anaphora that have no lexical realization (eg （私は）スーパーに行きます） 

### 21.1.2 Information Status
+ Types:
   + new NPs 
      + brand new NPs(discourse and hearer new)
      + unused NPs (discourse new, hearer old) such as Hong Kong or the New York Times
   + old NPs
      + discourse and hearer old
   + inferrables
      + neither discourse nor hearer old, but can be inferred from the existence of other entities via "bridging inference"
+ the position of an entity on a "given-new" dimension
+ a salient entity can be referred to with less linguistic material (eg pronouns)

### 21.1.3 Non-referring expressions
+ appositives: noun phrases which describe the head noun phrase eg "Victoria Chen, *CFO of Megabucks Banking*"
+ predicative and prenominal NPs: properties of the head noun eg "Shanghai is China’s *biggest city*"
+ expletives: "*it* is raining" or "hit *it* off" where "it" does not refer to anything

### 21.1.4 Linguistic Properties of Coreference Relations
+ number agreement (singular should refer to singular)
+ person agreement (first person should refer to first person) --> quotations are the exception
+ gender or noun class agreement (she/her/it)
+ 

## 21.2 Coreference Tasks and Datasets . . . . . . . . . . . . . . . . . . . 429
## 21.3 Mention Detection . . . . . . . . . . . . . . . . . . . . . . . . . . 430
## 21.4 Architectures for Coreference Algorithms . . . . . . . . . . . . . 433
## 21.5 Classifiers using hand-built features . . . . . . . . . . . . . . . . . 435
## 21.6 A neural mention-ranking algorithm . . . . . . . . . . . . . . . . 437
## 21.7 Evaluation of Coreference Resolution . . . . . . . . . . . . . . . . 440
## 21.8 Winograd Schema problems . . . . . . . . . . . . . . . . . . . . . 441
## 21.9 Gender Bias in Coreference . . . . . . . . . . . . . . . . . . . . . 442
