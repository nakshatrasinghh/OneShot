# OneShot is all you need

Tired of creating text preprocessing pipelines all the time? Don't worry, we got you covered! **OneShot** is a python textual data preprocessing library made just for you. Just import and feel the power ⚡. Oneshot doesn't only provide you with functionality to clean your data, it also provides with numerical information present in the data. Many of the processes required for cleaning text is accessible. If you have any suggestions to make, you can connect with me by clicking the icons below. PR's are most welcome. ❤️

<p align="left" align='right'>
<a target="_blank"href="https://www.linkedin.com/in/nakshatrasinghh/"><img alt="LinkedIn" src="https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white"/></a>
<a target="_blank"href="mailto:iamnakshatrasingh@gmail.com"><img alt="LinkedIn" src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/></a>
</p>

### Dependencies 🚒
```
---------------------------------------
pip install spacy==2.2.3
python -m spacy download en_core_web_sm
pip install beautifulsoup4==4.9.1
pip install textblob==0.15.3
---------------------------------------
```

### Install ⬇️

`https://github.com/nakshatrasinghh/OneShot.git`

### Uninstall 👋

`pip uninstall OneShot`

### How to use it? 🤔

*Use this function to clean your dataset*
```
----------------------------------------------------------
def get_clean(x):
    x = str(x).lower().replace('\\', '').replace('_', ' ')
    x = osx.cont_exp(x)
    x = osx.remove_emails(x)
    x = osx.remove_urls(x)
    x = osx.remove_html_tags(x)
    x = osx.remove_rt(x)
    x = osx.remove_mentions(x)
    x = osx.remove_accented_chars(x)
    x = osx.remove_special_chars(x)
    x = osx.remove_stopwords(x)
    x = osx.remove_dups_char(x)
    x = re.sub("(.)\\1{2,}", "\\1", x)
    return x
----------------------------------------------------------
```

*Use this function to get numeric features, but wait is'nt this cumbersome? We have a surprise for you.*
```
----------------------------------------------------------
def numeric_feats(x):
    x = osx.get_wordcounts(x)
    x = osx.get_charcounts(x)
    x = osx.get_avg_wordlength(x)
    x = osx.get_stopwords_counts(x)
    x = osx.get_hashtag_counts(x)
    x = osx.get_mentions_counts(x)
    x = osx.get_uppercase_counts(x)
    x = osx.get_digit_counts(x)
    x = re.sub("(.)\\1{2,}", "\\1", x)
    return x
----------------------------------------------------------
```

### Surprise 🤗

*Use this ONE function to get all the numeric features mentioned above.*
```
def numeric_feats(x):
    x = osx.get_basic_features(x)
    return x
```

### Use it indivitually 🧨
```
---------------------------------------
import pandas as pd
import OneShot as osx

df = pd.read_csv('imdb_reviews.txt', sep = '\t', header = None)
df.columns = ['reviews', 'sentiment']

#@ you're -> you are; i'm -> i am
df['reviews'] = df['reviews'].apply(lambda x: osx.cont_exp(x))
#@ removes emails
df['reviews'] = df['reviews'].apply(lambda x: osx.remove_emails(x))
#@ removes html tags
df['reviews'] = df['reviews'].apply(lambda x: osx.remove_html_tags(x))
#@ removes urls
df['reviews'] = df['reviews'].apply(lambda x: osx.remove_urls(x))
#@ removes special characters
df['reviews'] = df['reviews'].apply(lambda x: osx.remove_special_chars(x))
#@ removes accented characters
df['reviews'] = df['reviews'].apply(lambda x: osx.remove_accented_chars(x))
#@ converts root word to its base word
df['reviews'] = df['reviews'].apply(lambda x: osx.make_base(x))
#@ corrects the spelling using textblob
df['reviews'] = df['reviews'].apply(lambda x: osx.spelling_correction(x).raw_sentences[0]) 
---------------------------------------
```

Note: Avoid to use `make_base` and `spelling_correction` for very large dataset otherwise it might take hours to process.


### Extras 😎

```
----------------------------------
import re
x = 'lllooooovvveeee youuuu'
x = re.sub("(.)\\1{2,}", "\\1", x)
print(x)
---
love you
----------------------------------
```
