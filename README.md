# HSK 3.0 vocabulary

Cleaned up HSK 3.0 vocabulary list with pinyin, POS, traditional terms, variants and other useful data. Cross-referenced/validated against several data sources.

Files:
  * `hsk30.csv`: main file - vocabulary list in .csv format. One row for each of 11092 terms on HSK 3.0 list.
  * `hsk30-expanded.csv`: version with variants (both simplified and traditional) expanded onto separate lines. Thus leaving just clean hanzi and requiring no extra logic to handle variants.
  * `hsk30-grammar.csv`: grammar points list.
  * `hsk30-chars.csv`: characters list, 3000 characters total (incl. 29 chars outside of wordlist).
  * `hsk30.ipynb`: parsing/data cleaning code.

Columns:
  * `ID`: unique key of the form `Ln-nnnn`, level + index from the original .pdf. Levels 7-9 have `L7` prefix.
  * `Simplified`: term in simplified characters as listed on HSK website. Mostly clean hanzi with just a few exceptions:
    * Some variant terms are listed with `（）|` characters, e.g. `爸爸|爸`, `零|〇`, `有（一）点儿`, etc.
    * Prefix/suffix terms have an example full word, e.g. `第（第二）`, `子（桌子）`, etc.
    * Couple multisense words and two-char affixes: `称1`, `称2`, `面1`, `面2`, `…极了`, `…分之…`.
    * All these cases have a `Variants` field set with a list of cleaned up variants. In `hsk30-expanded.csv` everything is expanded/cleaned up.
  * `Traditional`: term converted to traditional characters, variants separated by `|`.
    * Not exhaustive variants list: uncommon variants filtered out (a bit heuristically, so possible errors esp. at higher levels), as well variants not matching pinyin/POS.
    * Main/more common/taiwanese variant first.
  * `Pinyin`: cleaned up pinyin with diacritics. Tone changes are not indicated for ease of joining with other data sources.
  * `POS`: part of speech, `/`-separated with english codes:
    * `N` (名): noun
    * `V` (动): verb
    * `Adj` (形): adjective; usually `Vs` (state verb, 狀態動詞) in taiwanese linguistical tradition and TOCFL
    * `Adv` (副): adverb
    * `Pron` (代): pronoun; usually `Det` in TOCFL
    * `Num` (数): numeral
    * `M` (量): measure word/classifier
    * `Prep` (介): preposition
    * `Conj` (连): conjunction
    * `Aux` (助): auxiliary word/particle; usually `Ptc` in TOCFL
    * `Int` (叹): interjection/exclamation/particle, e.g. 喂, 啊, 哎呀
    * `Prefix` (前缀), `Suffix` (后缀): prefix/suffix bound forms
    * `Phonetic` (拟声): e.g. 哈哈 \[hāhā\]
  * `Level`: HSK 3.0 level - 1, 2, 3, 4, 5, 6 or "7-9" for advanced level. Note: HSK does not split 7-9 terms by level. If you need some kind of split for them, consider sorting by frequency and splitting evenly.
  * `WebNo`: index of the term on HSK website: https://www.chinesetest.cn/standardsAction.do?means=getStandardWordsList&leves=&words=&pinyin=&words_type=&pager.offset=0
  * `WebPinyin`: original pinyin from HSK website. Tone changes for 不 and 一 are indicated. Separable (mostly) verbs indicated with `∥`.
  * `OCR`: OCR'ed term from the original .pdf. Normally matches `Simplified` except sometimes would also contain POS.
  * `Variants`: for terms with multiple variants and a few other oddities, a cleaned up list of variants as a JSON list of objects with alternatives column values.
    * Additionally has `Example` key to mark terms which are merely examples for suffix/prefix terms rather than proper part of wordlist.
  * `CEDICT`: matching [CC-CEDICT](https://www.mdbg.net/chinese/dictionary?page=cc-cedict) (MDBG) entries. Just the entry key in its usual format: `traditional|simplified[numbered pinyin]`, multiple keys separated by `/`.

Character list:
  * `Level`: reading level = level of the first appearance in the wordlist.
  * `WritingLevel`: one of three writing levels indicated for a subset of 1200 characters.
  * `Traditional`: traditional variants, `/`-separated.
  * `Freq`: number of words with this character.
  * `Examples`: first few example words.

Sources:
  * Primary source is a document by PRC's Ministry of Education:
    * http://www.moe.gov.cn/jyb_xwfb/gzdt_gzdt/s5987/202103/t20210329_523304.html
    * http://www.moe.gov.cn/jyb_xwfb/gzdt_gzdt/s5987/202103/W020210329527301787356.pdf
    * However, it's just a scanned .pdf document without a text layer.
    * Good quality and proof-read OCR data taken from [elkmovie/hsk30](https://github.com/elkmovie/hsk30) - but only contains characters.
  * HSK website has an online database with pinyin and part of speech for most terms:
    * https://www.chinesetest.cn/standardsAction.do?means=standardInfo
    * Has parseable pinyin and part of speech for most terms.
    * Copy of the data available at [shawkynasr/HSK-official-Query-System](https://github.com/shawkynasr/HSK-official-Query-System/).

License:
  * Code (`*.ipynb`) is MIT licensed.
  * Data (`hsk30*.csv`) is largely derived from [elkmovie/hsk30](https://github.com/elkmovie/hsk30) and [shawkynasr/HSK-official-Query-System](https://github.com/shawkynasr/HSK-official-Query-System/) repos, both also under MIT license and claiming copyright -- of course, somewhat questionably, as the [original work](http://www.moe.gov.cn/jyb_xwfb/gzdt_gzdt/s5987/202103/t20210329_523304.html) they *copy* is PRC's government work (notice on website: `版权所有：中华人民共和国教育部`). Depending on PRC law specifics might be public domain.
