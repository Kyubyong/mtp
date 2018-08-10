# Multi-Language Processing



## Why Multi-language Processing?

## Glossary
* Diacritic
* Font
* Glyph
* Ligature


### Language Types by Morphological Behavior
* Source: [Wiki](https://en.wikipedia.org/wiki/Synthetic_language)
## Analytic language
## Synthetic language

## Unicode Normalization
* Source: [unicode.org](http://unicode.org/reports/tr15/)

### Canonical
### Compatibility


### NFD
### NFC
### NFKC
### NFKD


## Writing Systems
* Source: [omniglot](https://www.omniglot.com/)

### Alphabets
  * Corresponds to one or more phonemes.
  * Latin alphabet, Cyrillic alphabet
  * There is a fixed order.
  * Consonants and vowels stand alone.
  * Advantageous for computer processing.

### Abjads / Consonant alphabets
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
  * Let's decompose each letter first.

### Logographs
  * Not phonetic
  * Represents abstract concepts
  * Chinese characters
  * Tons of letters
  * Challenging for processing

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
  * Period (.) are used at the end of a sentence or for abbreviations.
    * E.g., etc., i.e., e.g.
  * The closing quotation mark (’) and apostrophe (') are often mixed up. (Read [this](https://webdesignledger.com/common-typography-mistakes-apostrophes-versus-quotation-marks/#5d9cd1131b))
  * ****`ORTHOGRAPHY`**** Many words have more than one spelling.
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
  * Allegedly, Japanese is the fastest spoken language.

### Javanese

### Khmer

### Korean

### Malay

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
