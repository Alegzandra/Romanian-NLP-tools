# Romanian-NLP-tools
A list of Natural Language Processing Tools for the Romanian language.   
I try to keep this list up-to-date, as technologies evolve over time.

***Any feedback to this repository is greatly appreciated.
All suggestions are welcome!***


## Stemmer

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install nltk.

```bash
pip install nltk
```

#### Usage

```python
from nltk.stem.snowball import SnowballStemmer
stemmer = SnowballStemmer("romanian")
print(stemmer.stem("alergare"))
```

## Tokeniser, Lemmatiser and POS (Part-Of-Speech)
Use the package manager [pip](https://pip.pypa.io/en/stable/) to install spacy and spacy-stanza.

```bash
pip install spacy spacy-stanza
```

#### Usage

```python
import stanza
from spacy_stanza import StanzaLanguage

snlp = stanza.Pipeline(lang="ro")
nlp = StanzaLanguage(snlp)

doc = nlp("Această propoziție este în limba română.")
for token in doc:
    print(token.text, token.lemma_, token.pos_)
```

For more info visit [https://spacy.io/universe/project/spacy-stanza](https://spacy.io/universe/project/spacy-stanza).

## SpaCy
### Create Doc objects and play with its tokens:
```python
from spacy.lang.ro import Romanian
nlp = Romanian()
doc = nlp("Aceasta este propoziția mea: eu am 7 mere, ce să fac cu ele?")
print("Index: ", [token.i for token in doc])
print("Text: ", [token.text for token in doc])
print("is alpha: ", [token.is_alpha for token in doc])
print("is punctuation: ", [token.is_punct for token in doc])
print("is like_num: ", [token.like_num for token in doc])
```
Output:
```output
Index:  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
Text:  ['Aceasta', 'este', 'propoziția', 'mea', ':', 'eu', 'am', '7', 'mere', ',', 'ce', 'să', 'fac', 'cu', 'ele', '?']
is alpha:  [True, True, True, True, False, True, True, False, True, False, True, True, True, True, True, False]
is punctuation:  [False, False, False, False, True, False, False, False, False, True, False, False, False, False, False, True]
is like_num:  [False, False, False, False, False, False, False, True, False, False, False, False, False, False, False, False]
```

### Search for POS and dependencies:
```python
import spacy
from spacy.lang.ro.examples import sentences
#load pre-trained romanian model
nlp = spacy.load("ro_core_news_sm")
doc = nlp("Ea a mâncat pizza")
for token in doc:
    print('{:<12}{:<10}{:<10}{:<10}'.format(token.text, token.pos_, token.dep_, token.head.text))
```
Output:
```output
Ea          PRON      nsubj     mâncat    
a           AUX       aux       mâncat    
mâncat      VERB      ROOT      mâncat    
pizza       ADV       obj       mâncat 
```
### Predict Named Entities:
```python
import spacy
from spacy.lang.ro.examples import sentences

nlp = spacy.load("ro_core_news_sm")

doc = nlp("Iulia Popescu, cea din Constanta, s-a dus la Lidl să cumpere pâine. Pe drum și-a dat seama că are nevoie de 50 de lei așa că a trecut și pe la bancomat înainte.")

for ent in doc.ents:
    print(ent.text, ent.label_)
```
Output:
```output
Iulia Popescu PERSON
Constanta GPE
Lidl LOC
50 de lei MONEY
```
### Rule-based Matching
Matching can be done by handlers: LEMMA, POS, TEXT, IS_DIGIT, IS_PUNCT, LOWER, UPPER, OP.  
The OP handler can have the following values:
- '!' = never
- '?' = never or once
- '+' = once or more times
- '*' = never or more times
```python
import spacy
from spacy.matcher import Matcher
#load pre-trained romanian model
nlp = spacy.load('ro_core_news_sm')
#create matcher
matcher = Matcher(nlp.vocab)
#create doc object
doc = nlp("Caracteristicile aplicației includ un design frumos, căutare inteligentă, etichete automate și răspunsuri vocale opționale.")
#create pattern for adjective plus one or two nouns
pattern = [{'POS': 'NOUN'}, {'POS': 'ADJ'}, {'POS': 'ADJ', 'OP': '?'}]
#add the pattern to the matcher
matcher.add('QUALITIES', [pattern])
#apply mather on doc
matches = matcher(doc)
for match_id, start, end in matches:
    matched_span = doc[start:end]
    print(matched_span.text)
```
Output:
```output
design frumos
căutare inteligentă
etichete automate
răspunsuri vocale opționale
```
## RoWordnet
Use the package manager [pip](https://pip.pypa.io/en/stable/) to install rowordnet.

```bash
pip install rowordnet
```

#### Usage

```python
import rowordnet

wordnet = rowordnet.RoWordNet()
word = 'arbore'
synset_ids = wordnet.synsets(literal=word)
wordnet.print_synset(synset_ids[0])
```
For more info visit [https://github.com/dumitrescustefan/RoWordNet](https://github.com/dumitrescustefan/RoWordNet).

# BERT for Romanian
```python
from transformers import BertModel, BertTokenizer
# load tokenizer and model
tokenizer = AutoTokenizer.from_pretrained("dumitrescustefan/bert-base-romanian-cased-v1")
model = AutoModel.from_pretrained("dumitrescustefan/bert-base-romanian-cased-v1")
# tokenize a sentence and run through the model
input_ids = torch.tensor(tokenizer.encode("Acesta este un test.", add_special_tokens=True)).unsqueeze(0)  # Batch size 1
outputs = model(input_ids)
# get encoding
last_hidden_states = outputs[0]  # The last hidden-state is the first element of the output tuple
```
For more info visit [https://huggingface.co/dumitrescustefan/bert-base-romanian-cased-v1](https://huggingface.co/dumitrescustefan/bert-base-romanian-cased-v1).

# Word Vectors

## fastText
```python
import fasttext.util
fasttext.util.download_model('ro', if_exists='ignore')
ft = fasttext.load_model('path/to/cc.ro.300.bin')
```
or download from [here](https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.ro.300.bin.gz).  
More info on usage here: [https://fasttext.cc/docs/en/crawl-vectors.html](https://fasttext.cc/docs/en/crawl-vectors.html).  
## word2vec
from here: [https://github.com/senisioi/ro_resources](https://github.com/senisioi/ro_resources).  
# Other Lingvistic resources
- List of (all, I hope) romanian words - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_cuvinte.txt)
- List of prefixes - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_prefixe.txt)
- List of suffixes - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_sufixe.txt)
- **RoSentiwordnet** - download from [here](https://drive.google.com/file/d/1_MSJ9RrTalrFhZPc_KjPjfEYLReOxVRE/view?usp=sharing)

*RoSentiWordNet* is a lexical resource in which each RoWordNet synset is associated to three numerical scores Obj(s), Pos(s) and Neg(s), describing how objective, positive, and negative the terms contained in the synset are. It was created by translating SentiWordnet into Romanian using googletrans Python library.


