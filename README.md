# Preprocessing Text Python Package

This python package is made by Nakshatra Singh.

Dependencies
```
---------------------------------------
pip install spacy==2.2.3
python -m spacy download en_core_web_sm
pip install beautifulsoup4==4.9.1
pip install textblob==0.15.3
---------------------------------------

```

Install 

`pip install git+https://github.com/nakshatrasinghh/Preprocess_Nakshatra.git`

Uninstall

`pip uninstall Preprocess_Nakshatra`

#### How to use it for preprocessing
You have to have installed spacy and python3 to make it work.

```
----------------------------------------------------------
def get_clean(x):
    x = str(x).lower().replace('\\', ' ').replace('_', ' ').replace('.', ' ')
    x = pn.cont_exp(x)
    x = pn.remove_emails(x)
    x = pn.remove_urls(x)
    x = pn.remove_html_tags(x)
    x = pn.remove_rt(x)
    x = pn.remove_mentions(x)
    x = pn.remove_accented_chars(x)
    x = pn.remove_special_chars(x)
    x = pn.remove_dups_char(x)
    return x
----------------------------------------------------------
```

Use this if you want to use them one by one
```
---------------------------------------
import pandas as pd
import numpy as np
import Preprocess_Nakshatra as pn

df = pd.read_csv('imdb_reviews.txt', sep = '\t', header = None)
df.columns = ['reviews', 'sentiment']

# These are series of preprocessing
df['reviews'] = df['reviews'].apply(lambda x: pn.cont_exp(x)) #you're -> you are; i'm -> i am
df['reviews'] = df['reviews'].apply(lambda x: pn.remove_emails(x))
df['reviews'] = df['reviews'].apply(lambda x: pn.remove_html_tags(x))
df['reviews'] = df['reviews'].apply(lambda x: pn.remove_urls(x))

df['reviews'] = df['reviews'].apply(lambda x: pn.remove_special_chars(x))
df['reviews'] = df['reviews'].apply(lambda x: pn.remove_accented_chars(x))
df['reviews'] = df['reviews'].apply(lambda x: pn.make_base(x)) #ran -> run,
df['reviews'] = df['reviews'].apply(lambda x: pn.spelling_correction(x).raw_sentences[0]) #seplling -> spelling
---------------------------------------
```

Note: Avoid to use `make_base` and `spelling_correction` for very large dataset otherwise it might take hours to process.


#### Extra

```
----------------------------------
x = 'lllooooovvveeee youuuu'
x = re.sub("(.)\\1{2,}", "\\1", x) ## remove_dups_char
print(x)
---
love you
----------------------------------
```
