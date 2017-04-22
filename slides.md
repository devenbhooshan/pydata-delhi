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
title: about me
class: img-top-center

* Deven
* Co-Founder, MindIQ
    * we use AI + Human to automate customer support
    * started in feb 2016, launched the bot builder platform in aug-2016, 10,000 + bots were build through our platform
    * featured in techinasia, venturebeat, yourstory etc - clients : smart axiata(Cambodia), hubspot, wef etcf
* ex-amazon employee
* python lover, nlp enthusiast

---
title: Agenda
build_lists: false

* introduction
* word similarity
* sentence similarity
* questions ?
---

title: key takeaways
build_lists: true


* what is semantic similarity ?
* what are the applications of it ?
* word representations
* word2vec & gensim apis
* kaggle contest - quora question pairs
---
title: introduction

* semantic similarity between two sentences
    * eg: how can I uninstall snapchat ? | what is the procedure to uninstall snapchat ? | how to uninstall snapchat ?
    * these sentences are conveying the same thing/meaning/intent
    * the idea of semantic similarity between the sentences is based on the likeness of their meaning or semantic content

* word vectors
    * representing words by vectors

---
title: word similarity
build_lists: true

* word is the most basic unit that conveys meaning
* normally a word is representation as a string - it doesn't convey any meaning by own
* this representation can help us find similarities in some specific use cases. cars-car, hands-hand etc
* but what about words which are not same at character level : beautiful-alluring
* so what can we do ?
* we need some representation which takes into account the meaning

---

title: words representation - vectors
build_lists: true

* we represent words by vectors
* if suppose two words `beautiful` and `alluring` are represented by vectors `v1` and `v2`, the idea is
    * `v1` and `v2` should be very similar because they convey the same meaning
* if suppose `dog` is represented by vector `v3`,
    * `similarity(v1, v2) > similarity(v1, v3)`

---
title: word2vec & gensim
build_lists: true

- word2vec is an algorithm for constructing vector representations of words, also known as word embeddings.
- The vector for each word is a semantic description of how that word is used in context, so two words that are used similarly in text will get similar vector represenations.
- Once you map words into vector space, you can then use vector math to find words that have similar semantics.
- gensim provides a nice Python implementation of Word2Vec
---

title: words representation - examples

* api - base `http://wv.mindiq.in/`
* vectors
    * `vector/?word=dog`
* similarity
    * `similarity/?word1=kittens&word2=cat`
* most similar
    * `most_similar/?positive=mouse&positive=kittens&negative=cat
    &topn=10`

---
title: words representation - examples


### Just few lines of code
<pre class="prettyprint" data-lang="python">
from gensim.models.keyedvectors import KeyedVectors
word_vectors = KeyedVectors.load_word2vec_format('/tmp/vectors.txt', binary=False)
....
print word_vecors['beautiful']
print word_vecors.most_similar(positive=['woman', 'king'], negative=['man'])
print word_vecors.similarity('woman', 'man')

</pre>
----


title: words vectors - how do we produce them ?

* first lets understand `Distributional Hypothesis`
    * words that occur in the same contexts tend to have similar meanings.
    * the underlying idea is - "a word is characterized by the company it keeps"
* we have three sentences
    * india won the cricket match against sri lanka
    * australia won the cricket match against pakistan
    * bangladesh beat pakistan in the final cricket match
---

title: words occurrences

* we have three sentences
    * india won the cricket match against sri lanka
    * australia won the cricket match against pakistan
    * bangladesh beat pakistan in the final cricket match
* look at these pairs
    * india  - match, india - cricket
    * bangladesh - match, bangladesh - cricket
    * australia - match, australia - cricket

---

title: words occurrences

* india, bangladesh and australia - all in the similar context
    * winning, loosing, playing a cricket match
* so this what `Distributional Hypothesis` says
    * similar words => similar neighbors => similar vectors
    * `india` - `bangladesh` - `australia` are similar(how ? country names)
    * so `india` - `bangladesh` - `australia` will have similar vectors

---

title: words vectors - how do we produce them ?

* so this what `Distributional Hypothesis` says
    * similar words => similar neighbors => similar vectors
* this is the basic idea of building word vectors
* Tomas Mikolov from google created a group of models - word2vec to produce word embeddings/vectors
---
title:  semantic similarity between sentences

* *we have word vectors now*
* we have two sentences
    * Obama speaks to the media in Illinois
    * The President greets the press in Chicago

* the above sentences are similar
    * Chicago is a city in Illinois
    * press = media
    * speaks = greets

---
title:  semantic similarity between sentences
build_lists: true

* *we have word vectors now*
* we have two sentences which are similar
* any algorithm which works on word strings would fail
* what can we do ?
    * we can find the Euclidean distance in the word2vec embedding space between corresponding pairs and then add them
    * we can do the pos tagging of both the sentences and then find the similarity between verbs/nouns etc

---
title: lets play again - word mover distance

* api
    * `word_mover_distance/?s1=Obama speaks to the media in Illinois&s2=Obama greets to the press  in chicago`
* that's why I love python

<pre class="prettyprint" data-lang="python">
from gensim.models.keyedvectors import KeyedVectors
model = KeyedVectors.load_word2vec_format('/tmp/vectors.txt', binary=False)
....
print model['beautiful']
print model.most_similar(positive=['woman', 'king'], negative=['man'])
print model.similarity('woman', 'man')
<b>print model.wmdistance(
        'documents required'.split(),
        'papers needed'.split())</b>
</pre>

---

title: semantic similarity between sentences(cont..)

* wmd and other algorithms are good starting point for semantic similarity
* what if we want to improve ?
* best would be if we have some labelled data
* something like -> q1, q2, is_similar
* we can use features like the following to train our model
    * common words
    * wmd distance
    * etc
---

title: quora question pairs - kaggle contest

* can you identify question pairs that have the same intent?
* in simple terms
    * given two sentences s1, s2 - we have to tell whether they are duplicates
* 400k of labelled data
* use above idea to build your models - use features like
    * # of common words
    * wmd distance etc

---
title: quora question pairs - sample model

<pre class="prettyprint" data-lang="python">
from gensim.models.keyedvectors import KeyedVectors
model = KeyedVectors.load_word2vec_format('/tmp/vectors.txt', binary=False)
....
print model['beautiful']
print model.most_similar(positive=['woman', 'king'], negative=['man'])
print model.similarity('woman', 'man')
<b>print model.wmdistance(
        'documents required'.split(),
        'papers needed'.split())</b>
</pre>


---
title: questions?
class: segue dark nobackground


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

