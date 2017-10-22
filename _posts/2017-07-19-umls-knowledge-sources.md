---
layout: post
title: UMLS Knowledge Sources
categories: []
tags: [setup, UMLS]
description: The Unified Medical Language System (UMLS), created in 1986, is a compendium of many controlled vocabularies in the biomedical sciences.
cover: "/assets/images/dictionary.jpg"
cover_source: "http://lewisallen.org/wp-content/uploads/2015/05/image20.jpg"
comments: true
---

### [UMLS](https://en.wikipedia.org/wiki/Unified_Medical_Language_System){:target="_blank"}
The Unified Medical Language System (UMLS) is a compendium of many controlled vocabularies in the biomedical sciences (created 1986). It provides a mapping structure among these vocabularies and thus allows one to translate among the various terminology systems. It may also be viewed as a comprehensive thesaurus and ontology of biomedical concepts. UMLS further provides facilities for natural language processing. It is intended to be used mainly by developers of systems in medical informatics. 

> UMLS consists of Knowledge Sources (databases) and a set of software tools.

### UMLS Knowledge Sources

* **Metathesaurus**: The Metathesaurus forms the base of the UMLS and comprises **over 1 million biomedical concepts** and **5 million concept names**, all of which stem from the **over 100 incorporated controlled vocabularies and classification systems**. Some examples of the incorporated controlled vocabularies are ICD-10, MeSH, SNOMED CT, DSM-IV, LOINC, WHO Adverse Drug Reaction Terminology, UK Clinical Terms, RxNorm, Gene Ontology, and OMIM etc.

* **Semantic Network**: Each concept in the Metathesaurus is assigned one or more **semantic types** (categories), which are linked with one another through semantic relationships. The semantic network is a catalog of these semantic types and relationships. This is a rather broad classification; there are **127 semantic types and 54 relationships** in total.

* **Specialist Lexicon**: The SPECIALIST Lexicon contains information about common English vocabulary, biomedical terms, terms found in MEDLINE and terms found in the UMLS Metathesaurus. Each entry contains **syntactic** (how words are put together to create meaning), **morphological** (form and structure) and **orthographic** (spelling) information. A set of Java programs use the lexicon to work through the variations in biomedical texts by relating words by their parts of speech, which can be helpful in web searches or searches through an electronic medical record.

### UMLS Metathesaurus to MySQL

The setup procedure can be broken down into two steps mainly:

1. Creating the MySQL Script
2. Loading the MySQL Script to SQL Server.


* **Creating MySQL Script** (Current Version - 2017AA):
  * Download the **Full Release** from [**UMLS Knowledge Sources**](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html){:target="_blank"} which would be over **4.5GB** in size and requires licence to login and download.
  * Extract **umls-2017AA-full.zip** which requires over **30GB** free space
  * cd **2017AA-full**
  * Extract **mmsys.zip**
  * Copy contents of folder **mmsys** to parent folder **2017AA-full**
  * Go to Terminal and run **.\\run\_linux.sh** or **.\\run\_mac.command** based on platform
  * After **MetaMorphosys** starts click **Install UMLS**
  * Select **Source : \<path_to_folder\>/2017AA-full**, **Destination**, and **Metathesaurus** only from Knowledge Source List.
  * Click **New Configuration** and **Accept Licence Agreement Notice**
  * Select **Level 0** among options in **Default Subset Configuration**
  * Input Data Format should be **NLM Data File Format** in **Input Options** tab
  * Select Database to **MySQL** in **Write Database Load Script** section of **Output Options** tab
  * Select all **ENG** souces from **Source List** after selecting **INCLUDE in subset** option
  * Click **Done** in the **Action Bar** and let the process finish.

* **Shortcut**: Can skip the above step by downloading the [2017AA.tar.gz](https://drive.google.com/open?id=0ByBfN7yJVa9qM3ZzeFNIWHhsVnc){:target="_blank"} directly

* **Loading From MySQL Script**:
  * Go to **Destination** folder provided in previous section
  * cd **2017AA/META**
  * Edit **populate\_mysql\_db.sh** to provide details of **MYSQL_HOME**, **user**, **password** and **db\_name**
  * Save and run **.\\populate\_mysql\_db.sh**
  * Run **tail -f mysql.log** to follow the logs.



## REFERENCES:

<small>[Unified Medical Language System](https://en.wikipedia.org/wiki/Unified_Medical_Language_System){:target="_blank"}</small><br>
<small>[Unified Medical Language System - Knowledge Sources Downloads](https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html){:target="_blank"}</small>