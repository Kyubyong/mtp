# Multi-lingual Text Processing

## Basic Text Processing 
(Main source: [Lecture slides from the Stanford Coursera course](http://spark-public.s3.amazonaws.com/nlp/slides/textprocessingboth.pdf))

### Regular Expressions
* Syntax for processing strings
* ****`LIBRARY`**** [regex](https://pypi.org/project/regex/) (third-party): You can use unicode category expressions such as '\p{Han}' for all Chinese characters and '\p{Latin}' for the Latin script.
* ****`ONLINE`**** https://regexr.com/
* ****`SOFTWARE`**** [PowerGrep](https://www.powergrep.com/)

### Tokenization
* Token: a unit like character, subword ([bpe](https://en.wikipedia.org/wiki/Byte_pair_encoding)), word, [mwe](https://en.wikipedia.org/wiki/Idiom#Multiword_Expression), sentence, etc.
* Character
   * Simple (😄)
   * Small vocabulary (< 100) (😄)
   * Robust to rare words (😄)
   * Long sequence (😭)
* Subword
   * Best performance in machine translation (😄)
   * Robust to rare words (😄)
   * Not intuitive (😭)
   * Data-dependent (😭)
* Word
   * Usually simple (😄)
   * Short sequence (😄)
   * Transfer learning (😄)
   * Large vocabulary (> 10000) (😭)
   * Weak in rare words (😭)
* MWE (Multi-word expression)
   * Idioms e.g., ‘kick the bucket’
   * Compounds e.g., ‘San Francisco’
   * Phrasal verbs e.g. ‘get … across’
   * ****`PROJECT`***** [Multiword Expression Project](http://mwe.stanford.edu/))
* Sentence
   * Usually identified by a sentenc ending symbol (.!?)
   * Period (.) is sometimes ambiguous.
     * Abbreviations like Inc. or Dr.
     * Numbers like .02% or 4.3    

### Normalization
#### Lemmatization
* Lemma: the canonical or dictionary form of a set of words
  * E.g., produce, produced, production -> produce
* ****`WHY?`**** Dictionary lookup
* ****`HOW?`**** Linguistic knowledge
* ****`LIBRARY`**** [nltk wordnet lemmatizer](https://www.nltk.org/_modules/nltk/stem/wordnet.html)

#### Stemming
* Stem: the part of the word that never changes even when morphologically inflected
  * E.g., produce, produced, production -> produc-
* ****`WHY?`**** Query-document match
* ****`HOW?`**** Sequence of rules
* ****`LIBRARY`**** [nltk stemmers](https://www.nltk.org/api/nltk.stem.html)

#### Unicode Normalization 
(Main source: [unicode.org](http://unicode.org/reports/tr15/))

 * Canonical equivalence: a fundamental equivalency between characters which represent the same abstract character
    * E.g., combining sequence: Ç ↔  C+◌̧
    * E.g., ordering of combining marks: q+◌̇+◌̣ ↔ q+◌̣+◌̇
 * Compatibility equivalence: a weaker type of equivalence between characters which represent the same abstract character, but which may have distinct visual appearances or behaviors
   * E.g., circled variants: ① → 1
   * E.g., width variants: ｶ → カ
* NFD: Canonical Decomposition
* NF****K****D: Compatibility Decomposition
* NFC: NFD + Canonical Composition
* NF****K****C: NFKD + Canonical Composition
* Examples

<img src="img/composites.png" />
* Typically NFC is desirable for string matching.
* NFKC is useful if you don't want to distinguish compatibility-equivalent characters like full- and half-width characters. 
* See [this example](https://unicode.org/reports/tr15/images/UAX15-NormFig6.jpg)
* Strip diacritics: to ASCII characters
```
	import unicodedata
	def strip_diacritics(str):
		return ''.join(char for char in unicodedata.normalize('NFD', str)
                   if unicodedata.category(char) != 'Mn')
```

## Writing Systems 
(Main source: [omniglot](https://www.omniglot.com/))

### Alphabets
  * Corresponds to one or more phonemes.
  * Latin alphabet (AaBbCc), Cyrillic alphabet (АБВ)
  * There is a fixed order.
  * Consonants and vowels stand alone.
  * Desirable for computer processing.

### Abjads (= Consonant alphabets)
  * Each letter stands for a consonant, leaving the reader to supply the vowel.
  * Figuratively, "Cn y rcgnz ths?"
  * Arabic script, Hebrew script
  * Hard to learn (See [this discussion](https://www.quora.com/How-can-I-learn-Arabic-by-myself-if-there-is-no-vowel-sounds-haraka-on-words))
  * Challenging for processing.

### Abugidas
  * Consonants (Primary) + Vowels (Secondary)
  * Devanagari, Tamil
  * See [Devanagari compounds](https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Devanagari_matras.png/1500px-Devanagari_matras.png)

### Syllabaries
  * Corresponds to a syllable that is not further decomposed.
  * Hiragana, Katakana
  * Phonemic transcription is often needed.
    * E.g., かわいい -> kawaii

### Logographs
  * Each letter represents an abstract concept.
  * Chinese characters
  * Many letters
  * Challenging for processing
  * Phonemic transcription is often needed.
    * E.g., 我爱你 -> wǒ ài nǐ

### IPA (International Phonetic Alphabet)
* Universal alphabet
* [IPA Chart](https://upload.wikimedia.org/wikipedia/commons/8/8e/IPA_chart_2018.pdf)
* Each distinctive sound is represented as a single letter. (/sh/ -> /ʃ/, /th/ -> /θ/, /ng/ -> /ŋ/)
* Slashes (/ /) for phonemic transcription (e.g., 'pin' /****p****ɪn/ vs. 'spin' /s****p****ɪn/)
* Square brackets ([ ]) for phonetic transcription. (e.g., 'pin' [****pʰ****ɪn] vs. 'spin' [s****p****ɪn])

### ARPABET
  * Represents phonemes of  American English with ASCII characters.
  * Has been used in speech synthesis.
  * Used in the [CMU Pronouncing Dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict) and the [TIMIT](https://catalog.ldc.upenn.edu/ldc93s1) dataset.
  * [ARPABET Symbols](https://en.wikipedia.org/wiki/ARPABET)

## Languages
### Arabic
  * ****`CHAR SET`**** [\p{Arabic}.؟!،]
  * Written from right to left
  * Cursive
  * No distinct upper and lower case letter forms
  * Comma (،), question mark (؟)
  * Many dialects with varying orthographies exist.
  * Clitics are attached to a stem any orthographic marks like an apostrophe. (See [Fahad Alotaiby et al.](http://www.aclweb.org/anthology/Y10-1068))
* ****`TOOL`**** [Stanford Arabic Segmenter](https://nlp.stanford.edu/software/segmenter.shtml)

### Bengali

### Czech
  * ****`CHAR SET`**** [ A-Za-zÁáÉéÍíÓóÚúÝýČčĎďĚěŇňŘřŠšŤťŮůŽž.!?\-0-9]

The full stop is placed after a number if it stands for ordinal numerals (as in German), e.g. 1. den (= první den) – the 1st day. 

### Dutch
    * ****`CHAR SET`**** [ A-Za-z.!?'\-0-9]
  http://www.dutchgrammar.com/en/?n=SpellingAndPronunciation.03


### English
  * ****`SCRIPT`**** Latin script 
  * ****`CHAR SET`**** [ A-Za-z.!?'\-0-9]
  * Diacrtics can be treated as optional.
     * E.g., naïve = naive, façade = facade, résumé = resume
  * Normalization function example:
  * Periods (.) are used at the end of a sentence or for abbreviations.
    * E.g., etc., i.e., e.g.
  * The closing quotation mark (’) and apostrophe (') are often mixed up. (Read [this](https://webdesignledger.com/common-typography-mistakes-apostrophes-versus-quotation-marks/#5d9cd1131b))
  * ****`ORTHOGRAPHY`**** Many words have more than one spelling. (E.g., gray or grey)
  * Graphemes and phonemes are not directly linked. In other words, it's not always possible to infer the pronunciation of a word from its spelling. Therefore in speech synthesis a preprocessor that converts graphemes to phonemes is often used. (Check [English g2p](https://github.com/Kyubyong/g2p))
  * Compared to such languages as Chinese, Japanese, or Thai, tokenization is not so important. You can simply divide text into sentences by [.!?] and words by a white space, respectively at the sacrifice of accuray. (Check [nltk tokenize](https://www.nltk.org/_modules/nltk/tokenize.html)) 
* To identify multi word expressions is not always easy. 

### French
  * ****`SCRIPT`**** Latin script
  * ****`CHAR SET`**** [ A-Za-zçÉéÀàÈèÙùÂâÊêÎîÔôÛûœæ.!?'\-0-9]
  * ****`ORTHOGRAPHY`**** Diacritics on captial letters are often ignored.
  * Mostly two ligatures 'œ' and 'æ' are the same as 'oe' and 'ae', respectively. 
  * hyphen

### German
  * ****`SCRIPT`**** Latin script
  * ****`CHAR SET`**** [ A-Za-zÄäÖöÜüẞß.!?'\-0-9]
  * ****`ORTHOGRAPHY`**** Nouns are written in capital letters.
  * ****`ORTHOGRAPHY`**** No space for compound nouns.
    * E.g., Rinderwahnsinn ("mad cow syndrome").
  * ****`ORTHOGRAPHY`**** 'ß' and 'ss' are interchangeable.

### Greek

### Hindi

### Hungarian

### Italian
### Japanese
  * ****`SCRIPT`**** Hiragana, Katakana, Chinese characters
  * ****`CHAR SET`**** [\p{Hiragana}\p{Katakana}\p{Han}A-Za-z0-9０-９。、？！]
  * No space between words.
  * Both full- and half-width arabic numbers are used.
  * Note that period, comma, question mark, and exclamation mark are different from English ones.
  * A morph analyzer functions as a tokenizer and a grapheme to phoneme converter. (Check [MeCab](http://taku910.github.io/mecab/))

### Javanese

### Khmer
* ****`SCRIPT`**** Khmer abugida
   * No space between words.

### Korean

### Malay
* ****`SCRIPT`**** Latin script
* ****`CHAR SET`**** [ A-Za-z.!?'\-0-9]
* ****`MORPHOLOGY`**** 

### Mandarin


### Persian

### Portuguese
### Punjabi

### Russian
* ****`SCRIPT`**** Cyrillic script
* ****`CHAR SET`**** [ \p{Cyrillic}.!?'\-0-9]


### Spanish

### Tamil
### Telugu

### Thai

### Turkish
### Urdu

### Vietnamese

### Zulu
