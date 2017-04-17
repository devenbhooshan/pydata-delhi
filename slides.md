% title: semantic similarity between sentences
% subtitle: word vectors
% author: Deven Bhooshan
% author: Founder - MindIQ Solutions Pvt Limited
% thankyou: Thanks everyone!
% thankyou_details:
% contact: <span>github</span> <a href="http://github.com/devenbhooshan">/devenbhooshan</a>
% contact: <span>twitter</span> <a href="http://twitter.com/devenbhooshan">@devenbhooshan</a>
% favicon: http://www.stanford.edu/favicon.ico

---
title: Content/Agenda
build_lists: false

* about me
* topic discussion
* language
* words
* gensim
* demo
* quora Question Pairs - Contest
* know your limits
* questions ?

---

title: about me
class: img-top-center

* Co-Founder, MindIQ
    * started in February 2016, launched the bot builder platform in aug-2016, 10,000 + bots were build -
    * featured in techinasia, venturebeat, yourstory etc - clients : smart axiata(Cambodia), hubspot, wef etc
    * we use AI + Human to automate customer support
* ex-amazon employee
* python lover, nlp enthusiast
* love travelling(anybody who hates?)
---

title: topic discussion

* semantic similarity between two sentences
    * Semantic similarity is a metric defined over a set of documents or terms, where the idea of distance between them is based on the likeness of their meaning or semantic content as opposed to similarity which can be estimated regarding their syntactical representation (e.g. their string format).
    * IS-A relation

---

title: language

* ambiguous
    * I saw a man on a hill with a telescope.
    * Look at the dog with one eye.

---

title: words

* what is the meaning of 'bank'

---

title: words occurrences

* what is the meaning of 'bank'

---

title: Simple matrix of co - occurrences

* what is the meaning of 'bank'

---

title: word representations

* what is the meaning of 'bank'

---

title: word embeddings

* what is the meaning of 'bank'

---
title: word2vec & gensim
build_lists: true

- word2vec is an algorithm for constructing vector representations of words, also known as word embeddings.
- The vector for each word is a semantic description of how that word is used in context, so two words that are used similarly in text will get similar vector represenations.
- Once you map words into vector space, you can then use vector math to find words that have similar semantics.
- gensim provides a nice Python implementation of Word2Vec

---

title: lets play

* what is the meaning of 'bank'

---

title: quora question pairs - contest

* what is the meaning of 'bank'


---

title: know your limits

* what is the meaning of 'bank'

---

title: questions?
class: segue dark nobackground
* what is the meaning of 'bank'

---

title: 3 similarities

* semantic similarity?
* structure/syntactic similarity ?
    * If sentences contains similar words as well as structure  is also similar, then there exist structural similarity between sentences.
* relatedness ?
    * how related two concepts are, using any kind of relation

---
title: training your own model

<pre class="prettyprint" data-lang="python">
>>> from gensim.models import Word2Vec
>>> from nltk.corpus import brown
>>> b = Word2Vec(brown.sents())

>>> b.most_similar('money', topn=5)
[('pay', 0.6832243204116821), ('ready', 0.6152011156082153),
 ('try', 0.5845392942428589), ('care', 0.5826011896133423),
 ('move', 0.5752171277999878)]

>>> b.most_similar('great', topn=5)
[('new', 0.6999611854553223), ('experience', 0.6718623042106628),
 ('social', 0.6702290177345276), ('group', 0.6684836149215698),
 ('life', 0.6667487025260925)]

>>> b.most_similar('company', topn=5)
[('industry', 0.6164317727088928), ('technical', 0.6059585809707642),
 ('orthodontist', 0.5982754826545715), ('foamed', 0.5929019451141357),
 ('trail', 0.5763031840324402)]

</pre>

