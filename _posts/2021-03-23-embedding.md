---
layout: default
title: Natural Language Semantics from a Noob Perspective
date: 2021-03-13
---

TODO: References

I'm a complete novice when it comes to linguistics and natural language
processing. I know nearly nothing about machine learning. I hope to change
that by writing these posts. Here, I'm going to write what I think word
embeddings should look like, and anyone with half a brain and any knowledge
is going to realize that I don't know what the hell I'm talking about and I 
should go read a book. That's what I intend to do. I want to lay out my current 
expectations here, and see how far my expectations are met when I actually 
study in depth. (I expect they will fall apart very quickly.)

I say I'm a novice in linguistics, and it's true that I have no formal 
education in the area nor have I delved very deeply. However, I often 
intellectually engage with a linguist, who explains involved linguistic
ideas to this terribly underqualified wannabe type theorist (yours truly).
I have also read scantily and scatteredly across linguistics in a depressingly
unfaithful manner. As a result, though I have little formal understanding,
I do have *impressions*, which could be wildly misinformed due the lack of 
basis. If, despite this wild disclaimer, you're intent on reading onwards, I 
can only assume that you'd like to watch me make a fool of myself. I'm happy to 
oblige.

Where Do I Begin?
-----------------

I'm familiar with the bag-of-words *model*[^1] where the meaning of a word is
interpreted as a multiset of the words in its surroundings. I believe this is
one of the simplest forms of distributed semantics, since you can think of a
multiset as a vector where each element represents the unit vector of a 
dimension in the vector space. I like this formulation for its simplicity and
intuitiveness. However, as a consequence of its simplicity, it throws out all 
the semantic information present in word order. Surely we can capture some
information from that?

Enter the other end of the spectrum, n-grams! n-grams are used to predict
words based on the preceding words. To illustrate, consider a corpus with
the word "light" appearing three times. In each case, it was followed by a 
different word: "cream", "hai", "flooded". A bigram (2-gram) model would
store "light cream", "light hai" and "light flooded" as separate entries, and
use this to calculate that the word following "light" is equiprobably "cream",
"hai" or "flooded". n-grams generalize this notion to sequences of n words.
As one can see, n-grams captures the semantic information present in 
*sequential word order*. Skip-grams are a generalization of n-grams which allow
you to predict a word that's at most k distance ahead (for some fixed k). 
Syntactic n-grams generalize n-grams to any syntactic dependency, including
part-of-speech n-grams.[^2] I'm sure syntactic n-grams probably shine in some
particular area, but I'm told that modern machine learning learns this 
syntactic structure from the sequential text. But I'm not very fond of black-
box solutions, and I think syntactic n-grams are also beautifully simple, so
I like the idea.

Given that they seem to capture different (but perhaps not completely 
distinct?) information, I would suppose that there exists work that combines 
the two. However, I don't know of any myself.[^3]

My Baby Understanding of Machine Learning and Distributed Semantics[^4]
-------------------------------------------------------------------

When machine learning joins the party, the party gets wild, but everyone gets
blackout drunk and only distinctly feel it was wild in the aftermath, and maybe 
infer so from some pictures. There exist powerful machine learning techniques
[^5] that embed words most commonly in vector spaces (though not always!), but
while they seem to work very well, and everyone can see they work well, how
they work is still poorly understood[^6]. I don't like algorithms that are not
well-understood. Black-box solutions make me uneasy, and feel like cheating.

If I were to attempt to devise a theory to embed vectors in words, I'd like a 
word vector would simply be the sum representation of the word's context in its 
many appearances. It's length could then be correlated to the number of its 
occurrences in the corpus, which gives us a cute confidence measure.[^7] We can 
extract this information from the length, and then remove the distinction due 
to confidence by normalizing the vector. I have no understanding of how 
close this is to how modern techniques work, but I suspect it's not too close
since this feels similar in naivety to bag of words. 

Since words are represented by their context in a distributed setting, I assume
a context can be embedded as a vector as well. Evaluating words in that context
may be akin to shifting the origin to that context.

Again from the innocent bag of words perspective, it's confusing to me that a 
word is represented as a vector which must be some average (mean?) 
representation of the word in its many occurrences in several contexts.
Representing a word as a vector is akin to representing it as a single point
in the space; but in order to really capture information about the distribution
representing the word, should you not be trying to represent a word as a
subspace? Wouldn't information about this distribution help inform tasks like
word-sense induction? There exists work on embedding words in manifolds,
which I don't really understand yet, but I think they make similar arguments. 
A friend who understands an epsilon more than me describes a manifold as a set
of points whose neighbors have a notion of Euclidean distance with it. There's
also something about paths. I really need to learn more about manifolds, and 
topology in general.

Compositional Semantics
-----------------------

Distributional semantics is concerned with how to embed words into structures 
so we can study them. Compositional semantics is an orthogonal concept which
talks about how words glue together to form a sentence i.e. how to typecheck
a sentence. Montague gave literal typechecking rules in his Montague grammar!
Pregroup grammars are particularly interesting, and seem to capture information
about ordering beyond the next word (and probably can be used to derive 
dependency grammars? Am I using dependency grammar correctly?).

Compositional Distributional Semantics
--------------------------------------

Bob Coecke showed that pregroups and vector spaces share an underlying 
categorical structure. He uses this to justify using pregroup grammars to
direct how to construct sentence vectors. Word application was analogous to
tensor product. (IIRC, pl confirm) This is interesting work, but is a similar
categorical structure sufficient motivation? Also, as I pointed out earlier,
are vectors good enough?

[^1]: I'm not sure if this is/isn't the formally correct term.
[^2]: I got a lot of that from Wikipedia.
[^3]: TODO Fill in with some quick finds, just for completeness.
[^4]: Complete with pretentious theories, pseudophilosophical psychobabble,
      and terrible metaphors that possibly only make sense in my head right 
      now!
[^5]: For more on this, check out word2vec, GloVe, BERT, etc. Or maybe just 
      check out the Wikipedia page for "word embedding", but don't take my word 
      on that, since I have no idea how reliable Wikipedia is here.
[^6]: TODO Double check this
[^7]: Is this valid reasoning? 
