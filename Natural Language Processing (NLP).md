# Natural Language Processing (NLP)

Credits: Hjalmar Turesson, IBM

### What is it?

As defined by IBM, "Natural language processing (NLP) is a subfield of computer science and artificial intelligence (AI) that uses machine learning to enable computers to understand and communicate with human language.".

### What do we use it for?

NLP is used for a variety of tasks, at its core its purpose is to allow computers to understand the natural language that humans communicate in. It can be used to create chatbots, draw insights from media containing natural text, and to apply other subfields of AI to media that contains natural text.

### How does it work?

To begin working with NLP, you would often times need to assemble a corpus (a dataset of sorts) of text that you will be working on. Once the corpus has been assembled, some preprocessing must be applied to it. There are several different types of pre-processing, including the removal of stop words, tokenization, text normalization and n-grams. These will not be discussed in depth here, in the future they may each receive their own entry in the data science dictionary.

Once the corpus has been preprocessed, then two analytical paths can be followed, a syntactical and semantical analysis of the corpus. The syntactical method attempts to define the meaning of a text passage (could be a word, phrase or sentence) by parsing the syntax of the text and using hard-coded grammar rules. The semantical method then uses the output of the syntactical method to interpret the meaning of the text passage within the greater text structure (for example, the meaning of a word within a sentence, or the meaning of a sentence within a paragraph).

Within these analytical methods, there are two parsing methods that can be utilized: Dependency and Constituency parsing. Dependency parsing focuses on the relationships between words (i.e. locating nouns and related verbs), whereas constituency parsing builds a tree starting from a root word/token and builds outwards following the syntactic structure of text.

There are 3 main approaches to NLP: Rule-Based, Statistical and Deep Learning.

* Rule Based NLP: This approach utilizes no AI or Machine Learning methods. It is solely based upon hard-coded rules to respond to specific inputs. Therefore, it is only suited to complete the specific task it was built for.

* Statistical NLP: This approach does utilize Machine Learning. The main benefit of this approach is that it introduced the concept of storing natural language through vector representations. This allowed for statistical and mathematical analyses for vectors to now be applied to natural language.

* Deep Learning NLP: This approach utilizes Deep Learning models. The models are passed large volumes of un-processed media containing natural language, this allows them to become extremely accurate at predicting and understanding natural language. It does utilize some of the methods of Statistical NLP to accomplish this. This is currently the dominant approach seen in NLP today and is the approach utilized by Large Language Models (LLMs).