# Introduction

+ The focus of the chapter:
  + POS-tagging
  + Named Entity Recognition

These are both sequence labeling tasks. 

The importance of POS-tagging:
+ clues about sentence syntax
+ clues about neighboring words

The importance of named entity recognition
+ helps with information extraction such as question answering

# 8.1 (Mostly) English Word Classes

+ POS are focused more on *grammatical relationships* and *morphological properties* rather than semantic properties
+ POS fall into closed & open classes
+ example closed classes:
   + prepositions
+ major open classes:
   + noun, verb, adjective, adverb, interjections
+ Nouns:
  + common nouns
    +  count nouns
    +  mass nouns
  +  proper nouns
+  Verbs
  + actions
+ Adjectives
  + properties of qualities of nouns
+ Adverbs
  + modify verbs, verb phrases, other adverbs
  + directional, degree, manner, temporal
+ Interjections
  + greetings, question responses
+ prepositions
  + mark spatial or temporal relation (before a noun)
+ particle
  + resembles preposition or adverb, used in combination with a verb
  + tend to have extended meanings (beyond the prepositions they resemble) eg *she turned the paper over*
  + verb + particle = phrasal verb
    + phrasal verbs tend to be non-compositional
+ determiners
  + eg this, that
  + mark beginning of noun phrase
+ articles
  + a, an, the
+ conjunctions
  + equal status (and, or, but)
  + subordinating (that)    --> also called *complementizer*
+ pronouns
  + possessive, wh-pronouns (can sometimes act as *complementizers*)
+ auxiliary verbs
  + mark semantic features of main verb such as its tense, aspect, polarity, mood
+ example tagset: Penn Treebank 45-tag set


## 8.2 POS Tagging

+ assign a POS to each word in a text
+ input = sequence of tokenized words, output = tag for each word
+ tagging is a **disambiguation** task because words may have more than one possible tag
+ generally, POS algorithm performance is about 97% (HMM, CRF, BERT etc)
+ word types (Janet, hesitantly) are majority unambiguous, but the ambiguous word types tend to be more *frequent* in corpora
  + however, often, the different tags for a word are not equally likely so it's easy to predict (eg the determiner a is more likely than the letter)
  + so as a baseline, we can just choose the most frequent tag
  + most frequent tag baseline has an accuracy of about 92%

## 8.3 Named Entities and Named Entity Tagging
+ named entity = anything that can be referred to with a proper name (person, location, organization)
+ named entity recognition task = find spans of texts containing proper names and tag entity type
+ most common entity tags: person, location, organization, geo-political entity
+ however, we often go beyond "named entities" in "named entity tagging" and do things like dates, times
+ 
