
from https://ssb22.user.srcf.net/gradint/wenlin3.html (also [mirrored on GitLab Pages](https://ssb22.gitlab.io/gradint/wenlin3.html) just in case)

# Wenlin improvements

In mid-2009 [Wenlin Institute](http://www.wenlin.com/) kindly allowed me access to their C source code and I was able to add features such as:
1. Pinyin transcription: Wenlin 4 can resolve segmentation and pinyin ambiguities automatically (based on its frequency data and some rules I added), and there are improvements in spacing and capitalisation, as well as the handling of full-width ASCII etc.

   Also, pinyin can be **placed over hanzi** (like Ruby markup) in:
   * TeX code (copes with narrow columns, Simplified/Traditional switching, Greek and various symbols, hyperlinks, and has a function to quickly add highlighting to selected words in the TeX output)
   * Lilypond lyrics
   * HTML (with popup definitions)
   * .odt document (in Wenlin 4.0.2+) that OpenOffice/LibreOffice can convert to Word 97
   * ![wenlin41.png](https://ssb22.user.srcf.net/gradint/wenlin41.png)Wenlin’s own window (4.1+)
   * LyX 2/XeTeX document (Wenlin 4.1+)

or beside hanzi in a text-only “column” format for PDAs etc. Pinyin can be omitted when the word is made up of hanzi you know. “Make transformed copy” and “Find Fix:” now have shortcut keys too, and transcription runs faster. 4.1+ can also transcribe into Chinese Braille, and can automatically make sandhi changes for ‘yi’ and ‘bu’ pinyin.
2. Improvements that help if you’re using Wenlin on a laptop while interpreting a talk:
   * Lookup dialogue can go directly to the list of adjacent words (from a hotkey or the command line);
   * page down with the space bar when not editing; swap between two places with hotkeys like Emacs “mark”;
   * underline text or turn it blue with a single keypress (4.1 adds bold and other formatting);
   * add a quick pinyin gloss of a selected hanzi phrase with a single keypress (useful for preparing mixed-language notes);
   * markup for adding clocks and countdown timers to your document (Wenlin 4.0.2+, also in 4.2’s Free Edition)
3. “Break paragraphs into lines” (for email) copes better with punctuation, and can change indented lines into indented blocks (with hanging indent if you use tab); 4.1+ (and 4.2-free) also copes with hidden codes. (TeX and HTML transforms also recognise tab-indented lines)
4. Improved recognition of words that contain variant forms of hanzi and/or mix Traditional and Simplified hanzi in the same word
5. Try to convert pinyin spelling mistakes like *shaban* for *xiaban* (Wenlin 4.0.2+)
6. Fixed the display of some symbols (bullets etc) that Wenlin 3 wouldn’t display, and added some extra useful symbols to the Convert key (pp=paragraph sign; full-width ? and ! characters; etc); in 4.1+ they’re user-customizable
7. “Transform 1-4 to tone marks” now copes with digit 0 (or 5) for neutral tone, and with missing apostrophes; in 4.1+ “tone marks to 1-4” optionally leaves Latin1 characters as-is
8. “Import list of entries” Test button can now warn of any serial-number collisions between your user entries and someone else’s list; in 4.1 you can also set a custom prefix, and there is better support for user-modified entries in general (they’re marked with a `+` and you can search them)
9. Quicker access to sample texts and ABC references (4.1+ also has CUV lookup); Web links to various Chinese reference sites for checking out words that aren’t in the ABC (also in 4.2-free); 4.2+ “words ending with” search
10. WINE and low-vision compatibility improvements, e.g.
    * instant lookup from keyboard cursor as well as mouse
    * the conversion bar now appears where the Wenlin window is, instead of always at the top of the desktop which can drag a magnified viewport around too much and cause window-selection problems in flwm
    * Wenlin now supports smaller windows, and makes it more obvious how many lines the instant lookup area has when you’re resizing it; 4.1+ can omit the title row and 4.2+ has a customisable toolbar
    * the maximum phrase length is automatically adjusted according to available space in instant lookup
11. Windows Mobile version (runs on [WM](https://ssb22.user.srcf.net/wm/) 6.0 or earlier, with or without touchscreen; can also be built for 6.1/6.5 if you have a MSVS9 license). The WM version installs a shortcut to “open Wenlin and paste the clipboard contents”, optionally as a hanzi+pinyin column, and adds a built-in quota counter for writing Chinese SMS messages.
12. Option to compile for pre-Win2K systems (like the original Libretto), and to compile command-line transformations (for “add pinyin” CGIs etc) and command-line dictionary maintenance
13. Autosave and recovery
14. 4.1+ also has a clipboard watcher (can be used to script an integration with Pidgin IM etc), and can read Rich Text from the clipboard

Most of the above features can now be found in the “Advanced Options” screen. I was also able to try some other things that weren’t published.

My old Python helper scripts for Wenlin 3 are still here (below), but they don’t do as good a job as the above Wenlin 4 features.

# Old Python helper scripts for Wenlin 3

You will need Python 2 and Wenlin 3.

Contents:
* Pinyin with characters underneath
* Pinyin colouriser
* Automatic “fix”
* Importing cidian entries from a CEDICT/Adso-like format, with corrections
* Extracting a word list from a document
* Adding apostrophes to pinyin with tone numbers
* Checking an entry list for specific phrases
* Checking a cidian entry list for words not already recognised by Wenlin
* Extracting new yinghan entries from a cidian entry list
* Capitalising the first pinyin letter in certain cidian entries
* Exporting to CEDICT format
* Exporting to Pleco format
* Exporting to WM-Dict
* Exporting to LaTeX
* Batch-printing hanzi entries

## Pinyin with characters underneath

Sometimes it’s useful to keep the characters in a Pinyin transcription. If you segment the hanzi first, fix any problems and save as `segmented.u8`, then do a pinyin transcription, fix any problems and save as `pinyin.u8`, then this script will read those two files and produce HTML markup that has pinyin with characters, written to `pinyin.html`.

It is advisable to replace `|` with `/` in the segmented version before taking the pinyin transcription (and say “no” if it asks “segment first?” again). Then the `/` characters will still be present in the pinyin. This is desirable because, if you happen to hit a dictionary entry with a space in it (such as zai4wo3), it will show up as one word in the segmentation but two words in the pinyin; having the `/`s in gives the script something other than spaces to synchronize on (but it will try to synchronize on spaces as well).

You can save it as a `.py` file or paste it into a Python interpreter.

Code:
```
o=open("pinyin.html","w")
o.write("<html><head><meta http-equiv=Content-type content=\"text/html; charset=utf-8\"></head><body><style>ruby { display: inline-table; } ruby * { display: inline; line-height:1.0; text-indent:0; text-align:center; } rb { display: table-row-group; font-size: 100%; } rt { display: table-header-group; font-family: FreeSerif, Lucida Sans Unicode, Times New Roman, DejaVu Sans, serif; }</style>")
for pPara,hPara in zip(open('pinyin.u8').read().replace("\r\n","\n").split("\n"),open('segmented.u8').read().decode('utf-8').replace(u'\u3002',u'\u3002 ').replace('|','').encode('utf-8').replace("\r\n","\n").split("\n")):
 if pPara.replace(" ","")==hPara.replace(" ",""): # probably a paragraph with no pinyin (wenlin transcription may have changed some spacing)
   o.write(hPara.replace("/","").replace("|","")+"<p>") ; continue # (still pick up stray / or | at start)
 for pinyin,hanzi in zip(pPara.split("/"),hPara.split("/")):
  p2,h2 = pinyin.strip().split(),hanzi.strip().split()
  if not len(p2)==len(h2) and len(p2)<10: p2,h2=[pinyin],[hanzi]
  while len(p2)>len(h2): h2.append("") # in case stray word(s) at end
  while len(h2)>len(p2): p2.append("") # ditto
  for pinyin,hanzi in zip(p2,h2):
    if hanzi==pinyin: pinyin="-" 
    o.write("<ruby><rb>"+hanzi+"</rb><rt>"+pinyin+"</rt></ruby>\n")
 if pPara or hPara: o.write("<p>")

o.write("</body></html>")
```
If you are programming a GUI then instead of writing to HTML you might prefer to use a Tkinter text widget. Below is a version of the above script that inserts the result into Tkinter instead of producing an HTML file. (You need to set up the Tkinter text widget and call the function.)

Code:
```

def insert_into_text_widget (text_widget, pinyin_u8str, segmented_u8str):
  pinyin = pinyin_u8str.decode('utf-8').replace("\r\n","\n")
  segmented = segmented_u8str.decode('utf-8').replace(u'\u3002',u'\u3002 ').replace('|','').replace("\r\n","\n")
  widgets = []
  import Tkinter
  for pPara,hPara in zip(pinyin.split("\n"),segmented.split("\n")):
    if pPara.replace(" ","")==hPara.replace(" ",""):
      if hPara.strip(): text_widget.insert(Tkinter.INSERT,hPara.replace("/","").replace("|","")+"\n\n")
      continue
    firstWord = 1
    for pinyin,hanzi in zip(pPara.split("/"),hPara.split("/")):
      p2,h2 = pinyin.strip().split(),hanzi.strip().split()
      if not len(p2)==len(h2) and len(p2)<10: p2,h2=[pinyin],[hanzi]
      while len(p2)>len(h2): h2.append("")
      while len(h2)>len(p2): p2.append("")
      for pinyin,hanzi in zip(p2,h2):
        if hanzi==pinyin: pinyin="-"
        if not firstWord: text_widget.insert(Tkinter.INSERT," ") # (you can increase that space's width if you want)
        firstWord = 0
        widgets.append(Tkinter.Label(text_widget.master, text=pinyin+"\n"+hanzi, font=text_widget['font'], foreground=text_widget['foreground'], background=text_widget['background']))
        text_widget.window_create(Tkinter.INSERT,window=widgets[-1])
    if pPara or hPara: text_widget.insert(Tkinter.INSERT,"\n\n")
  return widgets # a list of the created widgets (in case it's useful for changing the font later, etc)
```
## Pinyin colouriser

If you make some notes using a mixture of English, pinyin and hanzi, this script will turn them into an HTML file with colours to help differentiate the Chinese and English parts. Input is `notes.u8`, output `notes.html`. Simple HTML tags are allowed in the input, so you can also colourize text that includes pinyin over characters from the above script (just rename `pinyin.html` to `notes.u8` first). Otherwise you may have to add `<head><meta http-equiv=Content-type content="text/html; charset=utf-8"></head> <body>` to the beginning of `notes.html`.

Code:
```

curWord=[] ; isChinese = 0 ; inTag = 0 ; out=[]
for x in open("notes.u8").read().decode("utf-8")+"\n": # add \n to ensure last word is output
  if inTag:
    out.append(x)
    if x==">": inTag=0
    continue
  if ord('A')<=ord(x)<=ord('Z') or ord('a')<=ord(x)<=ord('z') or 0xC0<=ord(x)<=0x1DC:
    curWord.append(x)
    if ord(x)>=0xC0: isChinese = 1
  else:
    if curWord:
      curWord=u"".join(curWord)
      if curWord.lower() in "de le ne ma zhe shang guo ge".split(): isChinese=1
      if isChinese: out.append("<py>")
      out.append(curWord)
      if isChinese: out.append("</py>")
    isChinese=(0x3000<=ord(x)<0xa700 or ord(x)>=0x10000)
    if isChinese: out.append("<hanzi>")
    if x.strip(): out.append(x) # not whitespace
    elif out and not out[-1]=="\n": out.append("\n")
    if isChinese: out.append("</hanzi>")
    curWord=[] ; isChinese = 0
    inTag=(x=="<")

open("notes.html","w").write("<style>.py { color: blue; } .hanzi { color: purple; }</style>"+"".join(out).replace("</hanzi><hanzi>","").replace("</hanzi>\n<hanzi>","\n").replace("</py><py>","").replace("</py>\n<py>","\n").replace("<hanzi>","<SPAN CLASS=hanzi>").replace("</hanzi>","</SPAN>").replace("<py>","<SPAN CLASS=py>").replace("</py>","</SPAN>").encode("utf-8"))
```
## Automatic “fix”

This is a rather bad Python one-liner that “fixes” ambiguities by choosing the first available option. I’m putting “fix” in quotes because it will be wrong a *lot* of the time. Use it only if you’re in a real hurry to get a document finished no matter how poorly done, e.g. you’ve been asked to read Chinese at a few minutes’ notice and need pinyin immediately. This script reads `pinfix.u8` and writes to `pinyin.u8` (you can change these filenames, or you can use it as-is to automatically “fix” pinyin for the above pinyin-over-characters scripts if you’ve saved the pinyin transcription as `pinfix.u8` instead of `pinyin.u8`).

Code:
```
import re;open("pinyin.u8","w").write(re.sub(u"\u3010\u25ce *Fix:[^\u25ce]*\u25ce","",re.sub(u";\u25ce[^\u3011]*\u3011","",open("pinfix.u8").read().decode("utf-8"))).encode("utf-8"))
```
If the ambiguities you are fixing are in segmentation, then you could also try the alternative script below, which, instead of choosing the first option, merely adds together all the possible split points. This should avoid any incorrect grouping of syllables, although some syllables will not be grouped when they should be. May be useful in conjuction with the above pinyin-over-characters scripts. Input is `segfix.u8`, output is `segmented.u8`. If replacing `|` with `/`, do not do it until *after* this script.

Code:
```

data=open("segfix.u8").read().decode('utf-8')
out=open("segmented.u8","w") ; i=0
while i<len(data):
  i2=data.find(u"\u3010\u25ceFix:\u25ce",i)
  if i2==-1: i2=len(data)
  out.write(data[i:i2].encode('utf-8'))
  if i2==len(data): break
  i = i2+7 ; i2 = data.find(u"\u3011",i)
  alternatives = data[i:i2].split(u";\u25ce")
  result = alternatives[0].replace(" | ","")
  splitAfter = [0]*len(result)
  for alt in alternatives:
    tot = 0
    for word in alt.split(" | "):
      tot += len(word)
      if tot<len(result): splitAfter[tot-1]=1
  for i in range(len(result)-1,-1,-1):
    if splitAfter[i]: result=result[:i+1]+" | "+result[i+1:]
  out.write(result.encode('utf-8'))
  i=i2+1
```
## Importing cidian entries from a CEDICT/Adso-like format, with corrections

If you have data in a CEDICT-like format i.e.

`characters [pin1 yin1] /meaning/`

or

`traditional simplified [pin1 yin1] /meaning/`

then you can convert to Wenlin cidian entry-list format, optionally using Wenlin’s existing dictionary to make corrections to the pinyin and/or the traditional/simplified conversion. (You can then re-export if you need a corrected CEDICT for personal use of some other application, or if the dictionary’s scope is such that the Wenlin corrections are fair use.)

If you don’t need to make corrections, you can skip to the main script below.

Otherwise, with the CEDICT file saved in `cedict.u8`, first run this small script to save the first two words of every line to word1.u8 and word2.u8:

Code:
```
o1,o2=open("word1.u8","w"),open("word2.u8","w")
for l in open("cedict.u8"):
  l=l.split()
  if len(l):
    o1.write(l[0]+"\n")
    if len(l)>1: o2.write(l[1]+"\n")
    else: o2.write("\n")

o1.close() ; o2.close()
```
Then, if you want Wenlin to correct the traditional-to-simplified conversion, make a “Simple form characters” transcription of word1.u8 and save it as `simple.u8`, otherwise, make sure `simple.u8` does not exist. You do not have to create `simple.u8` if the resulting cidian list is to be imported into Wenlin’s dictionary, since the import process will do it anyway. But you may want to do this step manually if the cidian is to be re-exported with corrections without actually adding to Wenlin, since otherwise only one version of the characters will be retained. (You don’t have to fix ambiguities; the script will not attempt to correct entries that are still ambiguous.)

Similarly, if you want to correct the simplified-to-traditional conversion (in cases where this is not ambiguous), make a “Full form characters” transcription of word2.u8 and save it as `full.u8`, otherwise, make sure `full.u8` does not exist.

If you want Wenlin to correct the pinyin, you can then open `word1.u8`, segment it, do a pinyin transcription, **replace tone marks with 1-4**, and save that as `word1.u8` (replacing it). You don’t have to fix the ambiguities; the script below will attempt to correct an entry only if there are no ambiguities to fix in the correction. If you leave `word1.u8` un-transcribed (or not created), then pinyin correction will not be attempted at all.

If you have both traditional and simplified versions in the list, it may be better to source the pinyin corrections from the *simplified* i.e. `word2.u8` (but save the result as `word1.u8`) as this is less susceptible to causing Wenlin to fail to recognise a word due to a wrong choice of traditional character. Another option is to run the whole process twice, the first time taking pinyin from full form and the second time taking pinyin from the `full.u8` corrections (you need to re-export to cedict in between the two runs if you are doing this). In all cases, save Wenlin’s pinyin as `word1.u8`.

The script below will take `cedict.u8`, and possibly `word1.u8`, `full.u8` and/or `simple.u8`, and produce `entries.u8`. If the CEDICT-like file does *not* have spaces between each pinyin syllable, but only between words, then set `collapseSpaces` to `False` (this might be useful for adso.dat files).

Code:
```
collapseSpaces = True
o=open("entries.u8","w") ; o.write("cidian\n")
count=0
def genNull():
  while True: yield ""

def tryOpen(fname):
  try: f=open(fname)
  except IOError: f=genNull()
  return f

fw,simp,full = tryOpen("word1.u8"),tryOpen("simple.u8"),tryOpen("full.u8")
import re
for l,corPinyin,corSimp,corFull in zip(open("cedict.u8"),fw,simp,full):
  if not "[" in l or not "/" in l: continue # a comment
  l        =l        .decode("utf-8").replace(u"\uff0c",",").strip()
  corPinyin=corPinyin.decode("utf-8").replace(u"\uff0c",",").strip()
  corSimp  =corSimp  .decode("utf-8").replace(u"\uff0c",",").strip()
  corFull  =corFull  .decode("utf-8").replace(u"\uff0c",",").strip()
  chars = l[:l.index(" ")]
  chars2 = l[l.index(" ")+1:l.index("[")].strip()
  if not chars2: chars2=chars
  make_2_entries = False
  if corFull and not "Fix:" in corFull: chars=corFull # unambiguous conversion to trad - definite override
  if "Fix:" in corSimp: corSimp=chars2
  elif chars2 and not corSimp==chars2 and corSimp==chars:
    # ouch, traditional maps to itself and cedict's simplified is different: cedict may be specifying 2 alternative readings instead of trad+simp
    make_2_entries = True
  if not len(corSimp)==len(chars2): corSimp=chars2 # either there wasn't one or there's some corruption
  chars=list(chars)
  for i in range(len(chars)):
    if corSimp[i]==chars[i]: chars[i]="-"
  chars=u"".join(chars)
  if chars==("-"*len(corSimp)): chars=corSimp
  else: chars = corSimp+u"["+chars+u"]"
  pinyin = l[l.index("[")+1:l.index("]")].replace("5","").replace("u:","v").replace("U:","V")
  if "Fix:" in corPinyin or not corPinyin: corPinyin=pinyin
  else:
    corPinyin=corPinyin.replace(u"\u201c","").replace(u"\u201d","")
    for c in corPinyin:
      if ord(c)>=0x3000:
        corPinyin=pinyin ; break
  if collapseSpaces: corPinyin=re.sub(" ([aAeEoO])",r"'\1",corPinyin).replace(" ","").replace(",",", ")
  o.write(("*** \npinyin "+corPinyin+"\ncharacters "+chars+"\nserial-number CEDict"+str(count)+"\ndefinition "+l[l.index("/")+1:l.rindex("/")]+"\nh\nimported from CEDICT; not manually checked\n").encode("utf-8"))
  if make_2_entries: o.write(("*** \npinyin "+corPinyin+"\ncharacters "+chars2+"\nserial-number CEDict-B"+str(count)+"b\ndefinition "+l[l.index("/")+1:l.rindex("/")]+"\nh\nimported from CEDICT; not manually checked\n").encode("utf-8"))
  count += 1

o.close()
```
If running this more than once, be sure to change the `CEDict` after the `serial-number` unless you want to replace previous entries. You may also want to change the “imported from CEDICT; not manually checked” message.

You will then need to use Wenlin to convert tone numbers to tone marks.

Note: these scripts assume they are working with plain UTF-8 files without BOMs. If your CEDICT files have BOMs (which is possible if they’ve been edited by Windows programs other than Wenlin) then you’ll need to first remove the BOM from each file:

Code:
```

d = open("input.u8").read()
if d.startswith('\xef\xbb\xbf'): d=d[3:]
open("output.u8","w").write(d)
```
## Extracting a word list from a document

To get a list of all the words in a certain document, segment the document, save as `segmented.u8` and run this. Outputs to `words.u8`, one per line. (You don’t have to fix ambiguities in the segmentation, but if you don’t then the script will also list the words from the incorrect segmentation choices.)

Code:
```

words={}
curW=[]
for c in open('segmented.u8').read().decode('utf-8'):
  if 0x4e00<=ord(c)<0xa700 or ord(c)>=0x10000: curW.append(c)
  elif curW and c.strip():
    words[u''.join(curW)]=1 ; curW=[]

words=words.keys() ; words.sort()
open('words.u8','w').write('\n'.join(words).encode('utf-8'))
```
To add pinyin to these words, make a pinyin transcription of `words.u8` (don’t segment first) and save it as `pinyin.u8`, then run:

Code:
```

o=open("output.u8","w")
for w,p in zip(open("words.u8"),open("pinyin.u8")): o.write(w.strip()+"\t"+p.strip()+"\n")

o.close()
```
result is in `output.u8` (tab-delimited). Or if you prefer working with an incomplete cidian format, run this instead:

Code:
```

o=open("output.u8","w") ; o.write("cidian\n") ; count=0
for w,p in zip(open("words.u8"),open("pinyin.u8")):
  o.write("*** \npinyin "+p.strip()+"\ncharacters "+w.strip()+"\nserial-number temporary"+str(count)+"\ndefinition ?\n")
  count += 1

o.close()
```
This can then be exported to CEDICT format if you want, but note the export script will discard any non-Fixed ambiguities in the pinyin, and will not make up for the lack of full-form equivalents (or simple-form equivalents if you’re working in full form).

## Adding apostrophes to pinyin with tone numbers

Some pinyin with tone numbers lacks apostrophes because they aren’t really necessary if the position of the number shows where the syllable ends. Wenlin is very particular about apostrophes being present in the pinyin, but does not add them when converting tone numbers to tone marks. This Python one-liner adds apostrophes to pinyin with tone numbers (input is `entries.txt`, output is `entries2.txt`) :

Code:
```
import re; open("entries2.txt","w").write(re.sub(r"([A-Za-z][1-5])([aAeEoO])",r"\1'\2",open("entries.txt").read()))
```
This can be used as a preprocessor to Wenlin’s conversion to tone marks. (However, it is not needed for the above cedict import.)

## Checking an entry list for specific phrases

If you need to extract all entries that do (or do not) contain a specific phrase, try this Python one-liner. Change `"my phrase"` to put your phrase in quotes (you can also say `not "my phrase"`). Reads from `entries.u8` and writes to `entries2.u8`. You’ll need to re-add the `cidian.db` or whatever at the top.

Code:
```
open("entries2.u8","w").write("".join(filter(lambda x: "my phrase" in x, ["*** "+e+"\n" for e in open("entries.u8").read().replace("\r\n","\n").split("\n*** ")[1:]])))
```
## Checking a cidian entry list for words not already recognised by Wenlin

Suppose you have a large list of cidian entries (converted from CEDICT or whatever), and you want to import them into your Wenlin dictionary, but you don’t want to add entries for words that Wenlin already knows about. You can’t get at Wenlin’s word list due to protection, but you *can* use Wenlin’s “Segment Hanzi” function as a test to see which words Wenlin already recognises. If Wenlin leaves a word unsegmented, then it recognised it.

The following Python script takes two files: `entries.u8` is the entry list, and `segmented.u8` is the Wenlin-segmented version of it (you don’t have to fix anything that needs fixing). It outputs to `entries2.u8` any entries for words that Wenlin didn’t recognise. You can save it as a `.py` file or paste it into a Python interpreter.

Code:
```
known = {}
for w in open("segmented.u8").read().split():
  if "[" in w: w=w[:w.index("[")]
  known[w]=1

o=open("entries2.u8","w")
o.write("cidian.db\n")
count=total=0
for entry in ["*** "+e+"\n" for e in open("entries.u8").read().replace("\r\n","\n").split("\n*** ")]:
  if not "\ncharacters" in entry: continue
  total+=1
  l=entry[entry.index("\ncharacters")+1:] ; l=l[:l.index("\n")]
  if "[" in l: l=l[:l.index("[")]
  if not l.split()[1] in known:
    o.write(entry) ; count+=1

print "Written %d entries (out of %d)" % (count,total)
```
## Extracting new yinghan entries from a cidian entry list

This script checks through a cidian entry list for entries whose definitions are only one English word, and creates a yinghan list for adding them to the English-to-Chinese dictionary. So if you have added lots of Chinese-to-English entries, you can use this to update the English-to-Chinese version. Input is `centries.u8`, output is `yentries.u8`. **Warning:** When Wenlin imports entries into yinghan, they **replace** (not add to) any default yinghan entries for the same English words. It is possible to see which words Wenlin already has in its yinghan by running the Unix `strings` utility on Wenlin’s `yinghan.tre` file; please do `strings -1 yinghan.tre > omit.txt` to tell this script which words to omit because they’re already there (or create an empty `omit.txt` if you don’t want to do this).

Code:
```
import re
omit={}
for o in open("omit.txt").read().lower().split(): omit[o]=1

o=open("yentries.u8","w") ; o.write("yinghan\n")
defs={}
for e in open("centries.u8").read().replace("\r\n","\n").split("\n*** ")[1:]:
  chars=en=None
  for l in e.split("\n"):
    l=re.sub(r"\([^)]*\)","",l)
    if not l.strip().split(): continue
    if l.startswith("characters"): chars=" ".join(l.split()[1:])
    elif "definition" in l.split()[0] and len(l.strip().split())==2: en=l.strip().split()[1]
    elif l=="h": break # (and ignore pinyin - it may be inaccurate anyway if the data originally came from an en-to-zh wordlist)
  if chars and en and re.match(r"^[A-Za-z]*$",en) and not en.lower() in omit:
    if chars not in defs.setdefault(en,[]): defs[en].append(chars)

for en,dList in defs.items():
  o.write("*** \n"+en+"\nautomatic\n")
  for d in dList: o.write("definition "+d+"\n")

o.close()
```
## Capitalising the first pinyin letter in certain cidian entries

If you have a list of cidian entries and many of them are proper names but you forgot to capitalise the first letter of the pinyin, this script can help. Reads from and writes to `entries.u8` (which can then be re-imported to Wenlin, overwriting the first set). Any entries whose definitions start with a capital will be changed so that the pinyin starts with a capital as well.

Code:
```
import re
entries=open("entries.u8").read().replace("\r\n","\n").split("\n*** ")
for i in range(1,len(entries)):
  if re.search(r"\n[0-9]*definition[ \t][^A-Za-z]*[A-Z]",entries[i]):
    lines=entries[i].split("\n")
    for li in range(len(lines)):
      words=lines[li].decode('utf-8').split()
      if len(words)>=2 and words[0]=="pinyin":
        words[1]=words[1][0].upper()+words[1][1:]
        lines[li]=" ".join(words).encode('utf-8')
        break
    entries[i]="\n".join(lines)

open("entries.u8","w").write("\n*** ".join(entries))
```
## Exporting to CEDICT format

Sometimes you might want to do this to share word lists with others who need them in that format, but beware that this will exclude the extra annotations of the Wenlin entries.

Before running this, set Wenlin to use simplified characters (so the full form are in `[]`s), extract the changed cidian entries, and **use Wenlin’s “Replace tone marks with 1-4” function**. Input is `entries.u8`, output is `cedict.u8`.

Code:
```
def add_5(pinyin):
  pinyin += "@@@" # termination
  i=0
  while i<len(pinyin):
    pl=pinyin.lower()
    if pl[i] in "aeiouvr" and pl[i+1] not in "aeiouv12345":
      if pl[i+1:i+3]=="ng" and not pl[i+3] in "aeiouv":
        if pl[i+3] not in "12345": pinyin=pinyin[:i+3]+"5"+pinyin[i+3:]
      elif (pl[i+1]=="n" or pl[i:i+2]=="er") and not pl[i+2] in "aeiouv" and not pl[i]=="r":
        if pl[i+2] not in "12345": pinyin=pinyin[:i+2]+"5"+pinyin[i+2:]
      else: pinyin=pinyin[:i+1]+"5"+pinyin[i+1:]
    i+=1
  return pinyin[:-3] # remove the @@'s

import string
o=open("cedict.u8","w")
for e in open("entries.u8").read().replace("\r\n","\n").split("\n*** ")[1:]:
    en = []; py=ch=None
    for l in e.split("\n"):
        if l.startswith("pinyin"):
            py=add_5(''.join(l.split()[1:])).replace("1","1 ").replace("2","2 ").replace("3","3 ").replace("4","4 ").replace("5","5 ").replace("v","u:").replace("V","U:").replace(",",", ").decode('utf-8').replace(unichr(0xb7),unichr(0xb7)+" ")
            for c in u"*\u00b9\u00b2\u00b3'-": py=py.replace(c,"")
            py=py.encode('utf-8').strip()
        elif l.startswith("characters"):
            ch=' '.join(l.split()[1:]).decode('utf-8').replace(",",u"\uff0c")
            if '[' in ch:
                trad=list(ch[ch.index("[")+1:ch.index("]")])
                ch=ch[:ch.index("[")] ; chLen=len(ch)
                for i in range(len(trad)):
                    if trad[i]=="-": trad[i]=ch[i]
                ch=u"".join(trad)+" "+ch
            else:
                chLen=len(ch)
                ch=ch+" "+ch
        elif l.strip() and "definition" in l.split()[0]: en.append(' '.join(l.split()[1:]))
        elif l=="h": break
    if py and ch and en:
        py_alt = py
        for tone in ["1","2","3","4","5"]: py_alt=py_alt.replace("e"+tone+" r5","er"+tone)
        if chLen==len(py_alt.split()): py=py_alt # spurious mising out 'r' when adding tone marks
        if chLen==len(py.split()):
            o.write(ch.encode("utf-8") + " ["+py+"] /"+"/".join(en)+"/\n")
            # or if you want quoted comma-separated format:
            # o.write('"'+ch.encode("utf-8").replace(' ','","')+'","'+py+'","'+"/".join(en)+'"\n')
        else: print "Warning: Omitting ["+py+"] because "+str(len(py.split()))+" syllables against "+str(chLen)+" characters (conversion problem?)"

o.close()
```
## Exporting to Pleco format

Input is entries.u8 (tone numbers, wenlin in CHS mode), output is pleco-CE.txt and pleco-EC.txt

Code:
```

import string,commands,os,sys
oCE=open("pleco-CE.txt","w")
oEC=open("pleco-EC.txt","w")

def decodeSlash(headword):
    # parses headword into a list, each item being either a
    # single character, or character+slash+character
    assert not "//" in headword, "// not supported here"
    headword = list(headword) ; i=0
    while i<len(headword)-1:
        if headword[i+1]=='/':
            headword[i] = headword[i]+headword[i+1]+headword[i+2]
            del headword[i+1] ; del headword[i+1]
        i += 1
    return headword

pyList,chList,enList,notesList = [],[],[],[]
for e in open("entries.u8").read().replace("\r\n","\n").split("\n*** ")[1:]:
    en = [] ; notes=[] ; py=ch=appendMode=None ; nextEnv=""
    for l in e.split("\n"):
        if appendMode: notes.append(l)
        elif l.startswith("pinyin"): py=' '.join(l.split()[1:])
        elif l.startswith("characters"):
            ch=' '.join(l.split()[1:]).decode('utf-8').replace(",",u"\uff0c")
            if '[' in ch:
                trad=decodeSlash(ch[ch.index("[")+1:ch.index("]")])
                simp=decodeSlash(ch[:ch.index("[")])
                assert len(simp)==len(trad)
                for i in range(len(trad)):
                    if trad[i].endswith("-") and (trad[i]=="-" or len(simp[i])==1): trad[i]=trad[i][:-1]+ch[i] # either a - by itself, or char/- (but we don't touch it if the simp is also complex)
                ch=ch[:ch.index("[")]+"["+u"".join(trad)+"]"
        elif l.strip() and "environment" in l.split()[0]: nextEnv="<"+' '.join(l.split()[1:])+"> "
        elif l.strip() and "definition" in l.split()[0]:
            en.append(nextEnv+' '.join(l.split()[1:]))
            nextEnv = ""
        elif l=="h": appendMode = 1
    if py and ch and en:
        pyList.append(py)
        chList.append(ch)
        enList.append(en)
        notesList.append(notes)

# now write out
for py,ch,en,notes in zip(pyList,chList,enList,notesList):
    # C->E entry:
    oCE.write(ch.encode("utf-8")+"\t"+py+"\t"+"; ".join(en+filter(lambda x:x,notes)).replace("\t","    ")+"\n")
    # E->C entries:
    if len(en)>1: notes=en+notes # ensure the en entries have all the definitions in them
    for head in en: oEC.write(head+"\t"+ch.encode("utf-8")+" "+py+". "+"; ".join(filter(lambda x:x,notes)).replace("\t","    ")+"\n")

oCE.close() ; oEC.close()
```
## Exporting to WM-Dict

Extract the changed cidian entries and save as `entries.u8`, and put WM-Dict 2’s `ce1.sqlite`, `ce2.sqlite` and `ce3.sqlite` files in the same directory. Then run the script below to add your extra entries into those databases (with basic formatting).

Code:
```

import unicodedata,sqlite3,sys
e2hp, p2he, h2pe = sqlite3.connect("ce1.sqlite"),sqlite3.connect("ce2.sqlite"),sqlite3.connect("ce3.sqlite")
removed=added=processed=0
def addToDict(connection,uTerm,uDefinition,uSerial,uSortKey=None):
  # we put our serial number in E1 (or E10 for short entries) so we can recognise and update our own entries later
  searchString=''.join((c for c in unicodedata.normalize('NFD',uTerm) if unicodedata.category(c)!='Mn' and unicodedata.category(c)[0]!='Z')).upper()
  e1e10=map(lambda x:searchString[:x],range(1,min(len(searchString),10)+1))+[u'']*max(10-len(searchString),0)
  if not e1e10[-1]: e1e10[-1]=u"_"+uSerial
  else: e1e10[0]=u"_"+uSerial
  if not uSortKey: uSortKey=searchString[:15]
  connection.execute("insert into Dictionary(Term,Definition,E1,E2,E3,E4,E5,E6,E7,E8,E9,E10,SortControl) values (?,?,?,?,?,?,?,?,?,?,?,?,?)",
    (uTerm,uDefinition)+tuple(e1e10)+(uSortKey,))
  global added ; added += 1

print "Reading cidian"
entries=open("entries.u8").read().replace("\r\n","\n").decode('utf-8').split("\n*** ")[1:]

print "Checking for old entries that are to be replaced"
serialNumbers = {}
for e in entries:
  for l in e.split("\n"):
    if l.startswith("serial"): serialNumbers[l.split()[1]]=1
    elif l=="h": break

for con in [e2hp,p2he,h2pe]:
  for row in con.execute("select e1,e10 from Dictionary"):
    # (usually faster than sending speculative deletes)
    for i in [0,1]:
      if row[i][1:] in serialNumbers:
        if i: what="E10"
        else: what="E1"
        removed += con.execute("delete from Dictionary where "+what+"=?",(row[i],)).rowcount
        if removed%100==0:
          print removed,"\r", ; sys.stdout.flush()

print "Adding new entries"
for e in entries:
    enKeys = []; enDef=[]; chKeys=[]; py=ch=inComments=""
    for l in e.split("\n")[1:]:
        if inComments:
          enDef.append(l) ; continue
        lFirst,lRest = (l.split()+[''])[0],' '.join(l.split()[1:]).strip()
        if l.startswith("serial"): sn=lRest
        elif l.startswith("pinyin"): py=lRest
        elif l.startswith("characters"):
            ch=lRest
            if '[' in ch:
                trad=list(ch[ch.index("[")+1:ch.index("]")])
                for i in range(len(trad)):
                    if trad[i]=="-": trad[i]=ch[i]
                chKeys=[ch[:ch.index("[")],u"".join(trad)]
            else: chKeys=[ch]
        elif l=="h": inComments=1
        elif lRest and not l.startswith("re") and not l.startswith("class") and not l.startswith("span") and not l.startswith("gr") and not l.startswith("freq"):
          if "definition" in lFirst: enKeys.append(lRest)
          elif "measure" in lFirst: lRest="MW "+lRest
          if "example" in lFirst: lRest += ":"
          elif not lRest[-1]==".": lRest += ";"
          enDef.append(lRest)
    if not py: continue # probably at the end
    if enDef and enDef[-1][-1]==';': enDef[-1]=enDef[-1][:-1]
    for k in enKeys: addToDict(e2hp,k,ch+" "+py,sn)
    addToDict(p2he,py,ch+" "+" ".join(enDef),sn,chKeys[0])
    for k in chKeys: addToDict(h2pe,k,py+" "+" ".join(enDef),sn,k)
    processed += 1
    if processed%100==0:
      print processed,"\r", ; sys.stdout.flush()

e2hp.commit() ; p2he.commit() ; h2pe.commit()
print "Processed",processed,"cidian entries; added",added-removed,"new WM-Dict entries and updated",removed,"others"
```
## Exporting to LaTeX

See also my more-recent [ohi_latex script](https://ssb22.user.srcf.net/gradint/ohi.html#tex), which supports more symbols than the method below but may require soft hyphens (U+AD) to be placed between pinyin syllables.

Old method follows:

Add an appropriate CJK command, e.g. on a recent Ubuntu system with `latex-cjk-chinese` and `latex-cjk-chinese-arphic-*` packages, use `\begin{CJK}{GB}{gbsn}` for Simplified in GB, `\begin{CJK}{Bg5}{bsmi}` for Traditional in Big5, `\begin{CJK}{UTF8}{bsmi}` for Traditional in UTF-8, etc. (Some older systems need `\begin{CJK}{GB}{song}` for Simplified in GB and `\begin{CJK*}{Bg5}{song}` for Traditional in Big5.)

Also add `\end{CJK}`. Do not add other TeX markup yet (some of it might be confused for pinyin later). **Use Wenlin’s “Replace tone marks with 1-4” function** and **save the file in the appropriate encoding**, and in a Unix environment do

Code:
```
sed -e 's/[BCDFGHJ-NP-TV-Zbcdfghj-np-tv-z]\?h\?[AEIOUVaeiouv]\+[ngr]*[1-5]/\\&/g' -e 's/\Long/\LONG/g' -e 's/\long/\Long/g' < infile > outfile
```
replacing infile and outfile with the appropriate filenames. Then edit the LaTeX in any text editor as normal (adding `documentclass` etc). Remember to include `\usepackage{CJK}` and `\usepackage{pinyin}` in the preamble.

If you have trouble, please try a different TeX distribution. Some TeX distributions from around 2005 were particularly quirky with CJK (conflicts between `usepackage`s, trouble with hanzi in PDF headings, unreliable UTF-8, ...) and if you have one of these then it’s probably easier to upgrade it than to work around its flaws. However, if you’re stuck (e.g. because some IT department forces you to use an inferior version of Linux with unusable package management) then you *could* try some workarounds:
* If pinyin.sty doesn’t typeset `ding`, add

  Code:
```
\catcode`@=11 \def\ding#1{\py@hy d\py@i dn#1ng\py@sp{}} \catcode`@=12
```
   after the `\usepackage{pinyin}`
* If you’re using the `microtype` package, make sure to `\usepackage{microtype}` *after* the above, and then add this:

  Code:
```

\catcode`@=11
\let\MT@orig@py@macron\py@macron
\@ifpackagelater{pinyin}{2005/08/11}{
 \def\py@macron#1#2{\let\pickup@font\MT@orig@pickupfont
  \MT@orig@py@macron{#1}{#2}\let\pickup@font\MT@pickupfont}%
 }{%
  \def\py@macron#1{\let\pickup@font\MT@orig@pickupfont
  \MT@orig@py@macron{#1}\let\pickup@font\MT@pickupfont}%
}\catcode`@=12
```
   This should solve the problem of some tone marks being printed over spaces instead of letters.
* `pdflatex` may drop some hanzi from `section` headings that are not on the first page; use ordinary `latex` instead, or pdflatex with DVI output.

Again, upgrading your TeX distribution should avoid the need for such workarounds.

## Batch-printing hanzi entries

Wenlin can print its entry for a single hanzi, including the pictorial parts. If you want to do this for large numbers of hanzi at a time, **for personal use only** (for example to load them onto a PDA for viewing on a journey), then the following script may be useful. It is currently Windows only, and the setup is slightly complex as it relies on sending keystrokes to Wenlin.
1. Install CutePDF and set it as the default printer. Make sure its output files go to your home directory (this should happen by default if you haven’t changed it).
2. Set Wenlin to print your desired number of characters per line. If the “printout” is to be on a PDA then you might want to make this quite small, by increasing the font size and reducing Wenlin’s window size, and you can also set 0 margins and no page numbers in Page Setup.
3. Create a Wenlin buffer containing all the characters you want information on, without line breaks or spaces, in editable mode and with the cursor placed at the beginning. For example if you want the characters from [charlearn](https://ssb22.user.srcf.net/gradint/charlearn.html)’s `characters.txt` you can do

   Code:
```
open("hanzi.gb","w").write("".join(map(lambda l:l.split()[0],open("characters.txt").readlines()[1:])))
```
    and open hanzi.gb in edit mode.
4. Run the script below (or paste it into an interpreter), changing the value of `numHanzi` to the actual number of hanzi you have in the buffer. The resulting pdf files will be created in the script’s working directory, named 0.pdf, 1.pdf etc.

   Code:
```
numHanzi = 492

import os, time
# CutePDF's default destination file for Wenlin
# (depends on if we're on Cygwin or just Windows)
if "HOME" in os.environ: f=os.environ["HOME"]+os.sep+"Wenlin.pdf"
else: f=os.environ["HOMEDRIVE"]+os.environ["HOMEPATH"]+"\\Wenlin.pdf"

try: os.remove(f) # in case you did a test print
except: pass

for h in range(numHanzi):
    open("_wenlin_hanzi_vbs.vbs","w").write("\n".join([
        'set WshShell = WScript.CreateObject("WScript.Shell")',
        'WshShell.AppActivate "Wenlin"',
        'WScript.Sleep 100',
        'WshShell.SendKeys "+{RIGHT}^x^l^v~^e^p"', # Shift-Right Cut Lookup Paste Enter Edit Print, i.e. look up the 1st character and print it
        'WScript.Sleep 100',
        'WshShell.SendKeys "~"', # Enter (confirm print dialogue)
        'WScript.Sleep 4000', # allow CutePDF enough time
        'WshShell.AppActivate "Save As"', # ensure got CutePDF's dialogue
        'WshShell.SendKeys "~"', # accept default Wenlin.pdf
        'WScript.Sleep 100',
        'WshShell.AppActivate "Wenlin"',
        'WshShell.SendKeys "^w"', # close hanzi entry
        ]))
    os.system("Cscript.exe _wenlin_hanzi_vbs.vbs")
    os.remove("_wenlin_hanzi_vbs.vbs")
    time.sleep(2)
    p=None
    while not p:
        try: p=open(f,"rb")
        except: time.sleep(1) # allow .pdf to be written
    open(str(h)+".pdf","wb").write(p.read())
    p.close()
    os.remove(f)

pass # (so get the above blank line if pasting into interpreter)
```

5. If your device cannot view PDFs, you can convert them to another format. For example to convert to “extra” PNG’s for the mobile version of charlearn, do this (in a Unix shell with GS and netpbm, such as Cygwin with those packages installed):

   Code:
```
for P in 0.pdf [1-9]*.pdf; do
  gs -sDEVICE=pnggray -sOutputFile=myfile%02d.png -r28 -q -dNOPAUSE - < $P;
  for M in myfile*.png; do
    pngtopnm < $M | pnmcrop -white -top -bottom > $M.pnm;
  done;
  pnmcat -tb myfile*.png.pnm | pnmtopng -compression 9 > x$(echo $P|sed -e s/pdf/png/);
  rm myfile*;
done
```
    and remember to set got_extra to 1 in flashcards.html so that they will display.

Copyright and Trademarks:
All material © Silas S. Brown unless otherwise stated.
CJK was a registered trademark of The Research Libraries Group, Inc. and subsequently OCLC, but I believe the trademark has expired.
Linux is the registered trademark of Linus Torvalds in the U.S. and other countries.
Python is a trademark of the Python Software Foundation.
TeX is a trademark of the American Mathematical Society.
Unicode is a registered trademark of Unicode, Inc. in the United States and other countries.
Unix is a trademark of The Open Group.
Wenlin is a trademark of Wenlin Institute, Inc. SPC.
Windows is a registered trademark of Microsoft Corp.
Any other [trademarks](https://ssb22.user.srcf.net/trademarks.html) I mentioned without realising are trademarks of their respective holders.
