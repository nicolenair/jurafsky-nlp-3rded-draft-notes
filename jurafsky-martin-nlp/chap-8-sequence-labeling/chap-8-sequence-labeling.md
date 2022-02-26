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
+ CRFs 
  + do not compute a tag probability at each time step, instead, only a *log linear function over a set of relevant features* is computed
  + the features are then aggregated and normalized to produce a global probability over the whole sequence
+ CRF Feature Function
  +  based on logistic regression
    + in logistic regression, the feature is f(x, y)
  + in CRF, the feature function is also f(x, y) BUT x and y are entire sequences
  + we can have k different feature functions(X, Y) and corresponding weights w_k and then use the weighted sum of these global features in a softmax-like manner
  + the global feature functions are computed by taking a summation over local features where global = entire sequence, local = one token
  + features can use:
    + current output token yi
    + previous output token yi-1
    + entire input string x
    + current position i
  + the constraint to only depend on yi and yi-1 is what defines a *linear chain crf*
    + linear chain crf enables the usage of viterbi, forwards-backwards algorithms
    + if we depend on other output tokens (eg yi-4) then we have to use more complex decoding algorithms
## 8.5.1 Features in a CRF POS tagger
+ the reason to use a discriminative sequence tagger is that it's easy to incorporate a lot of features. Here are some examples:
  + example 1: xi = the, yi = determiner
  + example 2: yi = proper noun, xi+1 = Street, yi-1 = number
+ the system designer decides on features, and then the features are automatically populated using a *feature template* (chapter 5)
+ features which help with unknown words are also helpful
  + eg *word shape* features which represent letter pattern of the word [lower = x, upper = X, number = d]
  + prefix features
  + suffix features
+ REMEMBER that these local/word-level features are not multiplied by weights, they are only multiplied after we have summed across the sequence to get the global feature
  + so there is always a set of K features with K weights, even if the sequence length differs


## 8.5.2 Features of CRF Named Entity Recognizers
+ similar features to POS tagging
+ some other features:
  + presence in gazeteer
  + presence in census list
  + POS tag

## 8.5.3 Inference and Training for CRFs
+ Viterbi can be used for linear chain CRF decoding, due to dependence only on previous output!
+ But the method of filling the N x T lattice is different:
  + the a transition probabilities and b emission probabilities are replaced
  + we will instead use the sum of weight_k * feature_k
+ can use the same supervised learning algorithms as logistic regression
+ L1, L2 regularization is important
+ forward-backward algorithm can be used to compute derivatives wrt the loss function



Remaining Confusions:
+ why is the decoding computation still apparently using local features, rather than global features in CRF
  + when we loop through T time steps, is this the equivalent of summing over T???



## 8.6 Evaluation of Named Entity Recognition
+ POS taggers usually use accuracy, but NER models usually use recall, precision & f1
+ To compare f1 of two NER systems, we can use a paired boostrap test or a randomization test (section 4.9)
+ complications due to segmentation portion of NER:
  +  we train using words, but evaluate using entire entities, so there is a train-test mismatch 


# 8.7 Further Details
+ labeled data is essential for training and test

## 8.7.1 Bidirectionality
+ in Viterbi, we *indirectly* use future tag information, but it would be helpful to *directly* use it
+ can use multiple passes to address this
+ neural models are often bidirectional

## 8.7.2 Rule-based Methods
+ in commercial applications, rules and lists are often used in place of CRF for NER
    + example: IBM System T specifies declarative constraints for tagging task in a formal query language (using regex, dictionary, semantic constraints etc)
  + it is also possible to use high precision rules to extract NER at first, and then use that as an input to another ML system
    + this method was first used for coreference
+  rule-based methods were also used for POS tagging
  + English Constraint Grammar system
    +  step 1: morphological analysis + return all POS tag entries for a given word
    +  step 2: use a large set of constraints to rule out inconsistent POS tags for a word given a sequence 

## 8.7.2 POS Tagging for Morphologically Rich Languages
+ examples; Czech, Hungarian, Turkish
+ productive word formation processes produce a *large vocabulary*
+ large vocabularies --> many unknown words --> performance degradation
+ inflections (masculine, feminine) or (accusative, nominative, genitive) can impact tasks like parsing and coreference resolution
  + so POS taggers for morphologically rich languages tag case & gender info
  + so we use a **morphological parse sequence** for such languages instead of single POS tags
  + so the tagsets for these languages tend to be much larger than English
  + so we will first morphologically analyse the word, and then the annotator will disambiguate between the possible POS tags for the analysed word
  + we can deal with unknown words because morphological parsers can deal with an unknown stem and segment the affixes correctly

# Chapter 8 Exercises

# 8.1

## My answer:

1. Atlanta/NN
2. dinner/NNS
3. have/VB
4. can/VBP

# 8.2

## My answer:

