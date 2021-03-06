---
title: "Readme: Digital Manār"
author: Till Grallert
date: 2019-03-29
ORCID: orcid.org/0000-0002-5739-8094
---


This repository is part of [OpenArabicPE](https://openarabicpe.github.io). It is home to the digital (TEI XML) edition of Rashīd Riḍā's journal *al-Manār*. It was originally set up in early 2016, inspired by and following the principles of [Digital Muqtabas](https://github.com/tillgrallert/digital-muqtabas). However, the files lay dormant for almost three years. If you just want to browse the edition in a more human-readable view, start [here](https://openarabicpe.github.io/journal_al-manar/tei/oclc_1588981-v_1-i_1.TEIP5.xml). All bibliographic metadata is available as part of [OpenArabicPE's public Zotero group](https://www.zotero.org/groups/904125/openarabicpe/items/). A simple [Google search](https://cse.google.com/cse?cx=012251040084107011117:jof1v_ejndo) has been set-up to search the full-text of OpenArabicPE's entire corpus.

The digital text was downloaded from shamela.ws. Digital facsimiles are available from

1. [*arshīf al-majallāt al-adabiyya wa-l-thaqafiyya al-ʿarabiyya*](http://archive.alsharekh.org/newmagazineYears.aspx?MID=33)
2. HathiTrust

# **IMPORANT NOTES**:

1. According to Florian Zemmin, the text from shamela.ws is missing all of Riḍā's tafṣīr that made up some 30 per cent of *al-Manār*'s text corpus.
2. The EPub / HTML from shamela.ws looks very different from other works I have seen and which were easly converted to TEI XML (re-)using the same code. I therefore asume that it is of a different origin than the other early twentieth-century texts.
    - I used regex to structure the file into
        + volumes: `<div type="volume" n="\d+"/>`
        + issues: `<div type="issue"/>` as children of the volumes
    - This was then split into one file per issue using the volume and the issue counts
3. Authorship information: a lot of the articles carry generic bylines with the following pattern: "الكاتب: محمد رشيد رضا". These are not found in the originals, if one consults the facsimiles available from <http://archive.alsharekh.org/> (formerly archive.sakhrit.co), but must have been added by later editors to the text.
    + their accuracy is unclear, some articles by Riḍā where either published posthumously after his death in 1935 or the attribution is wrong
4. The facsimiles from <http://archive.alsharekh.org/> confirm that shamela's page numbers correspond to the **second** printed edition (published in 1327 aH.). However, there are only page numbers between articles! This means, they can only be used as an approximation.

# to do
## structure

- there are many articles, which are still marked-up as notes
- paragraphs: the mark-up contains only line breaks but not paragraphs
- poetry:
- sections:
    + titles:
        * new publications/ review section
            + done تقريظ المطبوعات الجديدة
            + done تقريظ المطبوعات الحديثة
            + done تقريظ المطبوعات
        + done الأخبار والآراء
    + dividers of articles in sections
        * a line with 3 asterisks
        * the next line is wrapped in brackets
    + workflow:
        1. Regex: search and replace
            + find: `(<div[^>]+type=)"item" subtype="article"([^>]+>\s+<head[^>]+>تقريظ المطبوعات الجديدة</head>)`
            + replace: `$1"section"$2`
        2. XSLT: wrap the entire content of these `<div>`s in `<div type="item" subtype="article">`
- empty notes