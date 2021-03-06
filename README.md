# Nonsense Poetry Generator
Poetry generation using the Natural Language Toolkit and CMU Pronouncing Dictionary

"Given an infinite number of monkeys at an infinite number of typewriters working for an infinite amount of time, one will eventually produce a work worthy of Shakespeare"

Currently generating nonsense poetry on Twitter under Infinite Typewriters [(@infinite_poetry)](https://twitter.com/infinite_poetry) and on Facebook at [Infinite Typewriters](https://facebook.com/infinitetypewriters) messenger bot. 

## Usage
The poetry script provides an extensible class that allows generation of haikus, love poems, limericks, sonnets, and villanelles, with more forms of poetry planned. 

```
p = Poet()

p.print_haiku()
```

will print out a random haiku, such as 

```
A Nonsense Haiku
By Poetry Bot

Quantum dimension
Offense guardian save bring
Thank validation

Composed in 0.01 seconds
```

### Pre-compiled Dictionaries
To utilize rhymes between words in the work, a rhyming dictionary must be compiled before running the `poetry.py` script. To compile the dictionary of rhymes, run

```
python3 rhyme_dict.py [filename]
```

A `.pkl` file will be created in the same directory that contains the dictionary of rhyme sets for the input corpus.

To eliminate the overhead from finding the word cadences, a dictionary of word stress and complexity metric (see below) needs to be created beforehand and named `cmudict.pkl`. Note that this file is already included, but if the stress dictionary is updated or the complexity metric is changed, this dictionary needs to be created again. This can be done by running

```
python3 stress_dict.py
```

The `cmudict.pkl` file will be created in the root directory. 

## Word Complexity Metric
To optimize the flow of the poetry, words that were too complex were filtered out. To measure the complexity of a word, Stoel-Gammon's Word Complexity Measure was employed (C. Stoel-Gammon. 2010. The Word Complexity Measure: Description and application to developmental phonology and disorders. Clinical Linguistics and Phonetics 24(4-5): 271-282).

Complicated phonemes and long syllable clusters increase a word's complexity score. See `stress_dict.py` for the implementation as well as metric rules and details. 

## Benchmarks
<b>NOTE:</b> The script has now been optimized to call from a pre-compiled dictionary of rhymes and stresses. The runtimes listed below, while obsolete, are a good indication of the complexity of the poetry format. The runtimes are not nearly as long though; most poems are now created almost instantly on the given specifications.

Different poetry formats have varying runtimes, depending on the complexity of the poem. For instance, haikus are simple to generate, as they only depend on syllable counts, whereas limericks are much harder, as they require rhyming, cadence, and syllable counts. 

Tests were run on a dual-core Intel i5-5200U @ 2.2 GHz.

Poem | Average | Maximum | Minimum |
|:---:|---:|---:|---:|
Love Poem | 0.83s | 0.84s | 0.83s |
Haiku | 0.00s | 0.00s | 0.00s |
Doublet | 4.33s | 7.56s | 1.69s |
Limerick | 5.08s | 8.16s | 4.17s |
Sonnet | 20.51s | 26.87s | 12.54s | 
Quatrain | 5.75s | 10.36s | 4.08s |
Villanelle | 30.15s | 59.61s | 13.33s |
Ballade | 40.28s | 64.28s | 22.05s |

## General Methods
A separate script, `lang_utils.py` provides functionality for rhyming, streses, syllable splitting, and complexity without any of the poetry generation. The methods provided are `rhyme_set()`, `rhyme()`, `stress()`, `syllables()`, and `complexity()`. Either import `lang_utils` or run

```
python3 -i lang_utils.py
```

to utilize these methods. 

## Social Network Integration

## Tweeting
The file `tweet.py` contains methods that allow for the generation of short 140-character poems by randomly selecting a poetry format and brute-forcing until the poem is below 140 characters. Note that this limitation necessarily disqualifies long-format poems such as the villanelle, ballade, and sonnet.

## Messenger
For the Facebook Messenger script and its changes, see the Github repository [messsenger-bot](www.github.com/zhangxingshuo/messsenger-bot). The bot is deployed on a Heroku cloud app. Since this cloud server runs Python 2.7, the dictionaries need to be dumped into Python2 pickle files, and NLTK needs to be installed on Python 2.7 if modifications wish to be made. 
