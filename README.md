# Romanian-NLP-tools
A list of Natural Language Processing Tools for the Romanian language

![](https://www.finextra.com/finextra-images/top_pics/xl/natural-language-processing.png)

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

## Tokeniser, Lemmatiser and POS
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

# Lingvistic resources
- List of (all, I hope) romanian words - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_cuvinte.txt)
- List of prefixes - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_prefixe.txt)
- List of suffixes - from [here](https://raw.githubusercontent.com/Alegzandra/romanian_word_family/master/lista_sufixe.txt)
- **RoSentiwordnet** - download from [here](https://drive.google.com/file/d/1_MSJ9RrTalrFhZPc_KjPjfEYLReOxVRE/view?usp=sharing)

*RoSentiWordNet* is a lexical resource in which each RoWordNet synset is associated to three numerical scores Obj(s), Pos(s) and Neg(s), describing how objective, positive, and negative the terms contained in the synset are. It was created by translating SentiWordnet into Romanian using googletrans Python library.

***Any feedback to this repository is greatly appreciated.
All suggestions are welcome!***
