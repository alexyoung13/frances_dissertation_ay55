# frances_dissertation_ay55

## Environment

Please create a virtual environment using the requirements.txt file. VSCode makes this quite easy and is reccommended for running this repo.
 
## [Data](https://github.com/alexyoung13/frances_dissertation_ay55/tree/main/data)

The data necessary for running all of these scripts as well as all intermediate data that is saved is stored in this folder. 

#### eb07-v1.2-TXT

This contains all of the txt files corresponding to the 7th edition of the Encyclopedia Britannica from the [Knowledge Project](https://tu-plogan.github.io/source/r_releases.html). This repo only contains the zip file and must be extracted before running any of the scripts.

#### Edition 7 Clean

This repo is also where dataframes and knowledge graphs of the 7th edition will be stored as they are too large (> 100 MB) to be stored on gitbhub.

## [Notebooks](https://github.com/alexyoung13/frances_dissertation_ay55/tree/main/Notebooks)

Please run the notebooks in the following order:

#### [Create_DataFrame_7ed_EB_final.ipynb](https://github.com/alexyoung13/frances_dissertation_ay55/blob/main/Notebooks/Create_DataFrame_7ed_EB_final.ipynb)

Input: txt files from eb07-v1.2-TXT

Output: pandas dataframe in json format "final_eb_7_dataframe_clean"

This notebook creates a dataframe of all the different terms and corresponding metadata from the cleaned txt files

#### [DataFrame2RDF_7thEdition.ipynb](https://github.com/alexyoung13/frances_dissertation_ay55/blob/main/Notebooks/DataFrame2RDF_7thEdition.ipynb)

Input: pandas dataframe in json format "final_eb_7_dataframe_clean"

Output: knowledge graph in ttl format "edition7_clean.ttl"

This notebook takes a dataframe in and converts it into a knowledge graph following the [EB Ontology](https://francesnlp.github.io/EB-ontology/doc/index-en.html) and saves it as a ttl file

#### [Create_documents.ipynb](https://github.com/alexyoung13/frances_dissertation_ay55/blob/main/Notebooks/Create_documents.ipynb)

Input: knowledge graph in ttl format "edition7_clean.ttl"

Output: 
- terms_definitions.txt/topics_defintions.txt -> the definitions of either all terms or just topics
- terms_details.txt/topics_details.txt: the article, edition number, the year, the volume number, the part number (optional), and letter of all terms or just topics 
- terms_uris.txt/topics_uris.txt -> the terms and topics uris fromt he KG

This notebook takes in a Knowledge Graph and converts it into the necessary files for use in summarizing and future NLP tasks. There are 3 files for all terms and 3 files for just topics. This is because topics will need to be summarized but not articles.

#### [Summarizing.ipynb](https://github.com/alexyoung13/frances_dissertation_ay55/blob/main/Notebooks/Summarizing.ipynb)

Input: 
- topics_defintions.txt -> the definitions of either all terms or just topics
- topics_details.txt: the article, edition number, the year, the volume number, the part number (optional), and letter of all terms or just topics 
- topics_uris.txt -> the terms and topics uris fromt he KG

Output: topics_summary_7.txt -> the summarized topics

This notebook will use a XLNet transformer model to summarize all topics definitions for processing later on. This will help when trying to find similar terms and other NLP tasks as the models used for embeddings have max sizes of words for the embeddings.
