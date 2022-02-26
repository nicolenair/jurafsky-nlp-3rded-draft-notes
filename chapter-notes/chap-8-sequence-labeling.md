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


# 8.2 POS Tagging

+ assign a POS to each word in a text
+ input = sequence of tokenized words, output = tag for each word
+ tagging is a **disambiguation** task because words may have more than one possible tag
+ generally, POS algorithm performance is about 97% (HMM, CRF, BERT etc)
+ word types (Janet, hesitantly) are majority unambiguous, but the ambiguous word types tend to be more *frequent* in corpora
  + however, often, the different tags for a word are not equally likely so it's easy to predict (eg the determiner a is more likely than the letter)
  + so as a baseline, we can just choose the most frequent tag
  + most frequent tag baseline has an accuracy of about 92%

# 8.3 Named Entities and Named Entity Tagging
+ named entity = anything that can be referred to with a proper name (person, location, organization)
+ named entity recognition task = find spans of texts containing proper names and tag entity type
+ most common entity tags: person, location, organization, geo-political entity
+ however, we often go beyond "named entities" in "named entity tagging" and do things like dates, times
+ sometimes in *specific applications* there will be special entities such as proteins, genes
+ there is a **span recognition problem** that is not present in POS tagging, because we are tagging *spans* rather than individual tokens
+ there is **type ambiguity** eg JFK can be a person or an airport
+ the **span recognition problem** is often resolved via BIO/IO/BIOES tagging, where each token is tagged with the entity type AND the position in a span (begin = B, in = I)

# 8.4 HMM POS Tagging

## 8.4.1 Markov Chains
+ Markov assumption: if we want to predict the future, it only depends on the current state
+ components of a Markov chain
  + Q = set of N states
  + A = transition probability matrix specifying probability of transitioning from one state to another
  + $\pi\   = initial probabilities of states

## 8.4.2 The Hidden Markov Model
+ Markov chains can be used directly for observable events
+ But often, the states we are interested in are HIDDEN (eg we cannot directly observe POS tags)
+ We can think of the POS tags as "causing" the words
+ Components of a HMM:
  + Q = a set of N states
  + A = transition probability matrix
  + O = a sequence of T observations, each drawn from vocabulary V
  + B = a sequence of observation likelihoods/ "emission probabilities" probability of an observation being emitted from a state
  + $\pi\ = initial probability distribution
+ First order HMM simplifying assumptions:
  + probability of a state depends only on the previous state
  + probability of observation i depends only on state i

## 8.4.3 Components of a HMM tagger
+ A transition probabilities and B emission probabilities are the two major components
+ They are estimated using a tagged training corpus
+ a_titj = count(tag i followed by tag j)/count(tag i)
+ b_tjwj = count(tag t which generates word w)/count(tag t)
+ From a Bayesian perspective, we can view a_ij as the prior probability, and b_tw as the likelihood --> if we multiply, we get the unnormalized posterior of the tag at time t
  + p(t_j) * p(w_j | t_j) = p(t_j | w_j)

## 8.4.4 HMM tagging as decoding
+ Decoding = task of determining the hidden variable sequence, given the sequence of observations
+ Basically repeats the earlier explanation, and provides equations (good for reviewing!)

## 8.4.5 The Viterbi Algorithm
+ summary: 
  + at each step take the v * a * b where v is the previous state which maximizes v * a * b, a is the transition probability and b is the emission probability
  + at the termination step, take the maximum probability path *by following backpointers

## 8.4.6 Working through an example
+ basically provides an example of using the Viterbi algorithm to do HMM tagging


# 8.5 Conditional Random Fields
+ HMMs are useful but require augmentations
+ Example HMM problems
  + unknown words
+ Can be considered a discriminative sequence model based on log-linear models
+ basic CRF = linear chain CRF
+ HMMs are generative and used Bayes rule, but CRFs compute the posterior P(tags | words) directly
+  


