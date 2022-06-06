
## MCSCSet: A Specialist-annotated Dataset for Medical-domain Chinese Spelling Correction


### Introduction

We introduce MCSCSet, a large-scale specialist-annotated dataset dedicated for the task of Medical-domain Chinese Spelling Correction (MCSC). In contrast to existing open-domain CSC datasets, MCSCSet involves: i) extensive real-world medical queries collected from  [Tencent Yidian](https://baike.qq.com/), ii) corresponding misspelled sentences manually annotated by medical specialists. Our resource further offers a medical-domain confusion set consisting of the common errorprone characters in medicine and their corresponding misspellings.



The dataset paper is submitted to CIKM 2022 (Short and Resource Track). See paper for more details.


### Data

The data is stored in `./data`.
- `./data/original_query_log.txt`: 901,766 queries collected from real-world query logs.
- `./data/annotated_data.txt`: 199,763 samples with specialist annotation.
- `./data/med_confusionset.txt` : Medical-domain confusion set consisting of 2623 error-prone characters and their corresponding misspellings.
- `./data/mcsc_benchmark_dataset/` : Benchmark dataset for MCSC task.
  - `./data/mcsc_benchmark_dataset/filtered_data.txt`: 196,496 filtered samples focusing on spelling errors.
  - `./data/mcsc_benchmark_dataset/(train, valid, test).txt`: Benchmark dataset consisting of train set (157,194 samples), valid set (19,652 samples) and test set (19,650 samples).

#### Statistics
Several aspects of statistics of the dataset are shown as follows:

|    Aspect  | Value  |
|:------|:----|
| Number of samples |196,496 |
| Number of train/ valid/ test sets |157,194 / 19,652 / 19,650 |
| Avg. query length |10.90 |
| Avg. number of misspelled characters per query |1.86 |
| Avg. number of medical entities per query |1.46 |
| Number of unique medical entities |81,020 |


#### Data Format
This section explains the key files data format (`annotated_data.txt`, `filtered_data.txt` and `med_confusionset.txt`).
<!-- Each element in (`annotated_data.txt`) is a line of string as follows: -->

The format of each piece of data in `annotated_data.txt` is：

`Wrong query \t Correct query \t Error type(s) \n`


The format of each piece of data in `filtered_data.txt` is：

`Wrong query \t Correct query \n`

The format of each piece of data in `med_confusionset.txt` is：

`Key character \t Value characters \n`



- `Wrong query`: Query that contains misspelled characters. 
- `Correct query`: Corresponding query that are definitely correct.
- `Error type(s)`: Corresponding error type(s) of misspelled character(s) in the wrong query.
- `Key character`: An error-prone character in the medical domain.
- `Value characters`: Corresponding misspelled characters of a given key character, split with single space.




#### Data Loading
The data can be loaded with simple python scripts like:
```py
train_wrong_queries = []
train_correct_queries = []
with open('.\data\mcsc_benchmark_dataset\train.txt', 'r', encoding='utf-8) as f:
    train_samples = f.readlines()
    for sample in train_samples:
        pair = sample.strip().split('\t')
        train_wrong_queries.append(pair[0])
        train_correct_queries.append(pair[1])
```



### Benchmark Experiments

The source code of several representative baseline methods is in `./src/`.

The benchmark experimental results are shown as follows:


<table class="tg">
<thead>
  <tr>
    <th class="tg-9wq8" rowspan="2">Method</th>
    <th class="tg-c3ow" colspan="3">Detection</th>
    <th class="tg-c3ow" colspan="3">Correction</th>
  </tr>
  <tr>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;P (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;R (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;F1 (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;P (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;R (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
    <th class="tg-c3ow">&nbsp;&nbsp;&nbsp;&nbsp;F1 (%)&nbsp;&nbsp;&nbsp;&nbsp;</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-8bgf">N-gram LM</td>
    <td class="tg-c3ow">38.43</td>
    <td class="tg-c3ow">20.38</td>
    <td class="tg-c3ow">26.64</td>
    <td class="tg-c3ow">30.32</td>
    <td class="tg-c3ow">16.08</td>
    <td class="tg-c3ow">21.02</td>
  </tr>
  <tr>
    <td class="tg-8bgf">BERT-Corrector</td>
    <td class="tg-7btt">87.05</td>
    <td class="tg-c3ow">86.08</td>
    <td class="tg-c3ow">86.55</td>
    <td class="tg-c3ow">80.93</td>
    <td class="tg-c3ow">80.05</td>
    <td class="tg-c3ow">80.49</td>
  </tr>
  <tr>
    <td class="tg-8bgf">MedBERT-Corrector</td>
    <td class="tg-c3ow">87.01</td>
    <td class="tg-c3ow">86.25</td>
    <td class="tg-c3ow">86.63</td>
    <td class="tg-c3ow">80.98</td>
    <td class="tg-c3ow">80.24</td>
    <td class="tg-c3ow">80.61</td>
  </tr>
  <tr>
    <td class="tg-8bgf">Soft-Masked BERT</td>
    <td class="tg-c3ow">80.03</td>
    <td class="tg-7btt">86.29</td>
    <td class="tg-7btt">86.66</td>
    <td class="tg-7btt">81.22</td>
    <td class="tg-7btt">80.54</td>
    <td class="tg-7btt">80.88</td>
  </tr>
</tbody>
</table>



### License

This repository is liciensed under Apache-2.0 License.

The MCSCSet dataset is licensed under [CC BY-NC 2.0](https://creativecommons.org/licenses/by-nc/2.0/).



### FAQ
