# Multi-Language Text Processing


## Basic Text Processing 
(Main source: [Lecture Slides from the Stanford Coursera course](http://spark-public.s3.amazonaws.com/nlp/slides/textprocessingboth.pdf)))

### Regular Expressions
* Syntax for processing strings
* ****`LIBRARY`**** re (built-in)
* ****`LIBRARY`**** regex (third-party): You can use unicode category expressions such as '\p{Han}' for all Chinese characters.
* ****`ONLINE`**** https://regexr.com/
* ****`SOFTWARE`**** [PowerGrep](https://www.powergrep.com/)

### Tokenization

### Normalization
#### Lemmatization
* Lemma: 
* Why?
* E.g., am, are, is -> be
* E.g., car, cars, car's -> car


#### Stemming
* Stem:
* E.g., automate(s),    automaGc,    automaGon
* Why?
* How?

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
  * Used in the CMU Pronouncing Dictionary and the TIMIT dataset.
  * [Symbols](https://en.wikipedia.org/wiki/ARPABET)

### Braille
### Emoticons

## Languages
### Arabic

### Bengali

### Czech

### Dutch

### English
  * ****`SCRIPT`**** Latin script 
  * ****`CHAR SET`**** [ A-Za-z.!?'\-0-9]
  * Diacrtics can be treated as optional.
     * E.g., naïve = naive, façade = facade, résumé = resume
  * Normalization function example:
```
	import unicodedata
	def strip_diacritics(str):
		return ''.join(char for char in unicodedata.normalize('NFD', str)
                   if unicodedata.category(char) != 'Mn')
```
  * Periods (.) are used at the end of a sentence or for abbreviations.
    * E.g., etc., i.e., e.g.
  * The closing quotation mark (’) and apostrophe (') are often mixed up. (Read [this](https://webdesignledger.com/common-typography-mistakes-apostrophes-versus-quotation-marks/#5d9cd1131b))
  * ****`ORTHOGRAPHY`**** Many words have more than one spelling. (E.g., gray or grey)
  * Graphemes and phonemes are not directly linked. In other words, it's not always possible to infer the pronunciation of a word from its spelling. Therefore in speech synthesis a preprocessor that converts graphemes to phonemes is often used.
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
  * A morph analyzer functions as a tokenizer and a grapheme to phoneme converter. (Check [MeCab])

### Javanese

### Khmer
* ****`SCRIPT`**** Khmer abugida
   * No space between words.

### Korean

### Malay
* ****`SCRIPT`**** Latin script
* ****`CHAR SET`**** [ A-Za-z.!?'\-0-9]


### Mandarin


### Persian
### Polish
### Portuguese
### Punjabi

### Russian

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
