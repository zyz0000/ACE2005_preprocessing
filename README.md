# ACE2005_preprocessing

## Prerequisites

1. Prepare **ACE 2005 dataset**. 

   (Download: https://catalog.ldc.upenn.edu/LDC2006T06. Note that ACE 2005 dataset is not free.)

2. Install the packages.
   ```
   pip install stanfordcorenlp beautifulsoup4 nltk tqdm
   ```
    
3. Download stanford-corenlp model.
    ```bash
    wget http://nlp.stanford.edu/software/stanford-corenlp-full-2018-10-05.zip
    unzip stanford-corenlp-full-2018-10-05.zip
    ```
   Note that to run stanford-corenlp tool, Java should be installed in advance.
   
## A small modification to the original data to avoid bug when running preprocessing code
Find the following two files
```
ace_2005_td_v7/data/English/un/timex2norm/alt.vacation.las-vegas_20050109.0133.afp.xml
```
```
ace_2005_td_v7/data/English/un/timex2norm/alt.vacation.las-vegas_20050109.0133.sgm
```
In each file, file the context around `Doctors Without Borders`. Then you can see the content `Doctors Without Borders/Médecins Sans Frontières`. You should replace `é` with `e` and `è` with e to avoid the bug. Note that this modification should be applied to both two files. The attached `JMEE_train_filter_no_timevalue.json` contains the processed format of alt.vacation.las-vegas_20050109.0133.afp.xml and alt.vacation.las-vegas_20050109.0133.sgm.

## Usage

For Linux system, run:
```bash
sudo python main.py --data=./data/ace_2005_td_v7/data/English --nlp=./stanford-corenlp-full-2018-10-05
``` 

For Windows system, run
```bash
python main.py --data=./data/ace_2005_td_v7/data/English --nlp=./stanford-corenlp-full-2018-10-05
```

- Then you can get the parsed data in `output directory`. 

- If it is not executed with the `sudo`, an error can occur when using `stanford-corenlp`.

- It takes about 30 minutes to complete the pre-processing.

## papers
This preprocessing code is appropriate for the following two papers:
```
[1] Li M, Zareian A, Zeng Q, et al. Cross-media Structured Common Space for Multimedia Event Extraction[C]//Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics. 2020: 2557-2568.
[2] Liu X, Luo Z, Huang H Y. Jointly Multiple Events Extraction via Attention-based Graph Information Aggregation[C]//Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing. 2018: 1247-1256.
```
