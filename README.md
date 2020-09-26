# Romanian-NLP-tools
A list of Natural Language Processing Tools for the Romanian language

## Stemmer

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install nltk.

```bash
pip install nltk
```

### Usage

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

### Usage

```python
import stanza
from spacy_stanza import StanzaLanguage

snlp = stanza.Pipeline(lang="ro")
nlp = StanzaLanguage(snlp)

doc = nlp("Această propoziție este în limba română.")
for token in doc:
    print(token.text, token.lemma_, token.pos_)
print(doc.ents)
```

For more info visit [Spacy-stanza](https://spacy.io/universe/project/spacy-stanza).

