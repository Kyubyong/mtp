# Multi-Language Text Processing


## Basic Text Processing 
(Main source: [Lecture slides from the Stanford Coursera course](http://spark-public.s3.amazonaws.com/nlp/slides/textprocessingboth.pdf))

### Regular Expressions
* Syntax for processing strings
* ****`LIBRARY`**** re (built-in)
* ****`LIBRARY`**** [regex](https://pypi.org/project/regex/) (third-party): You can use unicode category expressions such as '\p{Han}' for all Chinese characters and '\p{Latin}' for the Latin script.
* ****`ONLINE`**** https://regexr.com/
* ****`SOFTWARE`**** [PowerGrep](https://www.powergrep.com/)

### Tokenization

### Normalization
#### Lemmatization
* Lemma: the canonical or dictionary form of a set of words
  * E.g., produce, produced, production -> produce
* ****`WHY?`**** Word frequency, dictionary lookup
* ****`HOW?`**** Language knowledge
* ****`LIBRARY`**** [nltk stemmers](http://www.nltk.org/howto/stem.html)

#### Stemming
* Stem: the part of the word that never changes even when morphologically inflected
  * E.g., produce, produced, production -> produc-
* ****`WHY?`**** Query-document match
* ****`HOW?`**** Rule
* ****`LIBRARY`**** [nltk wordnet lemmatizer](https://www.nltk.org/api/nltk.stem.html)

#### Unicode Normalization 
(Main source: [unicode.org](http://unicode.org/reports/tr15/))

 * Canonical
 * Compatibility
* NFD
* NFC
* NFKC
* NFKD
* Strip diacritics
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
  * Advantageous for computer processing.

### Abjads (= Consonant alphabets)
  * Each letter stands for a consonant, leaving the reader to supply the vowel.
  * Arabic script, Hebrew script
  * Hard to learn
  * Challenging for processing.

### Abugidas
  * Consonants (Primary) + Vowels (Secondary)
  * Devanagari

### Syllabaries
  * Corresponds to a syllable that is not further decomposed.
  * Hiragana, Katakana
  * For computer processing you may need to convert each syllable into a consonant and a vowel.
    * E.g., か -> ka

### Logographs
  * Not phonetic
  * Each letter represents an abstract concept.
  * Chinese characters
  * Tons of letters
  * Challenging for processing

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

### Braille
### Emoticons

## Languages
### Arabic
  * ****`SCRIPT`**** Arabic abjad
  * ****`CHAR SET`**** [\p{Arabic}.؟!،]
  * Written from right to left
  * Cursive
  * no distinct upper and lower case letter forms
Both printed and written Arabic are cursive, with most of the letters within a word directly connected to the adjacent letters. 
 it should be noted that some punctuation marks in Arabic look different from the English counterparts, e.g. the English comma is (,) while the Arabic comma (الفاصلة) points the opposite way (،) and it is written on top of the line. The English question mark is (?) while the Arabic question mark (علامة الاستفهام) looks like this (؟).

### Bengali

### Czech
  * ****`SCRIPT`**** Latin script 
  * ****`CHAR SET`**** [ AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZzÁáÉéÍíÓóÚúÝýČčĎďĚěŇňŘřŠšŤťŮůŽž.!?\-0-9]

The full stop is placed after a number if it stands for ordinal numerals (as in German), e.g. 1. den (= první den) – the 1st day. 

### Dutch
  * ****`SCRIPT`**** Latin script 
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
* To identify multi word expressions is not always easy. (See [Multiword Expression Project](http://mwe.stanford.edu/))
   * Idioms e.g., ‘kick the bucket’
   * Compounds e.g., ‘San Francisco’
   * Phrasal verbs e.g. ‘get … across’

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
### Polish
### Portuguese
### Punjabi

### Russian
* ****`SCRIPT`**** Cyrillic script
* ****`CHAR SET`**** [ \p{Cyrillic}.!?'\-0-9]


### Spanish

### Swedish

### Tagalog
### Tamil
### Telugu

### Thai

### Turkish
### Urdu

### Vietnamese

### Zulu
