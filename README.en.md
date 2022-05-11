# LECTAUREP Base Model

This model, "lectaurep_base", was produced using all the ground truth data published at the end of the LECTAUREP project.


| Script | Language | Period    | Score sur Dev | Score du Test (in-domain) |
| :----: | :------: | :-------: | :-----------: | :-----------------------: |
| Lat    | Fra      | 1742-1928 | 90.90 %       | 92.58%                    |

List of characters known by the model: 
```
" % & ' ( ) + , - . / 0 1 2 3 4 5 6 7 8 9 : ; = ? A B C D E F G H I J K L M N O P Q R S T U V W X Y Z [ ] ^ _ ` a b c d e f g h i j k l m n o p q r s t u v w x y z | ~ ¥ ¨ ° ½ æ œ ȼ ̀ ́ ̂ ̃ ̈ ̧ € ↑ ∟
```

## Kraken version

```
kraken --version
>>> kraken, version 4.1.0
```

## Dataset

Training was performed using the data in:
- [lectaurep-bronod v0.0.1](https://github.com/HTR-United/lectaurep-bronod/releases/tag/v0.0.1)
- [lectaurep-mariages-et-divorces v.1.0](https://github.com/HTR-United/lectaurep-mariages-et-divorces/releases/tag/v1.0)
- [lectaurep-repertoires v2.0](https://github.com/HTR-United/lectaurep-repertoires/releases/tag/v2.0)

### Test
12 pages were randomly selected from the datasets to create a test set. 

```
- 0036.xml
- FRAN_0025_0183_L-0.xml
- FRAN_0056_00607_L.xml
- 0088.xml
- FRAN_0025_1443_L-1.xml
- FRAN_0056_06068_L.xml
- DAFANCH96_048MIC06481_L-1.xml
- FRAN_0056_00015_L.xml
- FRAN_0187_16402_L-0.xml
- DAFANCH96_048MIC06489_L-1.xml
- FRAN_0056_00436_L.xml
- FRAN_0187_16411_L-0.xml
```

## Hyper paramètres

The model was trained with the following command: 

```
ketos train -o lectaurep_base -f binary train.arrow --device cuda:1 --augment -u NFD -s '[1,120,0,1 Cr3,13,32 Do0.1,2 Mp2,2 Cr3,13,32 Do0.1,2 Mp2,2 Cr3,9,64 Do0.1,2 Mp2,2 Cr3,9,64 Do0.1,2 S1(1x0)1,3 Lbx200 Do0.1,2 Lbx200 Do.1,2 Lbx200 Do]' -r 0.0001
```

## Training report

```
WARNING:root:scikit-learn version 1.0.2 is not supported. Minimum required version: 0.17. Maximum required version: 0.19.2. Disabling scikit-learn conversion API.
WARNING:root:Torch version 1.11.0+cu102 has not been tested with coremltools. You may run into unexpected errors. Torch 1.10.2 is the most recent version that has been tested.
Trainer already configured with model summary callbacks: [<class 'pytorch_lightning.callbacks.rich_model_summary.RichModelSummary'>]. Skipping setting a default `ModelSummary` callback.
GPU available: True, used: True
TPU available: False, using: 0 TPU cores
IPU available: False, using: 0 IPUs
HPU available: False, using: 0 HPUs
`Trainer(val_check_interval=1.0)` was configured so validation will run at the end of the training epoch..
LOCAL_RANK: 0 - CUDA_VISIBLE_DEVICES: [0,1]
┏━━━━┳━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━┓
┃    ┃ Name      ┃ Type                     ┃ Params ┃
┡━━━━╇━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━┩
│ 0  │ net       │ MultiParamSequential     │  4.0 M │
│ 1  │ net.C_0   │ ActConv2D                │  1.3 K │
│ 2  │ net.Do_1  │ Dropout                  │      0 │
│ 3  │ net.Mp_2  │ MaxPool                  │      0 │
│ 4  │ net.C_3   │ ActConv2D                │ 40.0 K │
│ 5  │ net.Do_4  │ Dropout                  │      0 │
│ 6  │ net.Mp_5  │ MaxPool                  │      0 │
│ 7  │ net.C_6   │ ActConv2D                │ 55.4 K │
│ 8  │ net.Do_7  │ Dropout                  │      0 │
│ 9  │ net.Mp_8  │ MaxPool                  │      0 │
│ 10 │ net.C_9   │ ActConv2D                │  110 K │
│ 11 │ net.Do_10 │ Dropout                  │      0 │
│ 12 │ net.S_11  │ Reshape                  │      0 │
│ 13 │ net.L_12  │ TransposedSummarizingRNN │  1.9 M │
│ 14 │ net.Do_13 │ Dropout                  │      0 │
│ 15 │ net.L_14  │ TransposedSummarizingRNN │  963 K │
│ 16 │ net.Do_15 │ Dropout                  │      0 │
│ 17 │ net.L_16  │ TransposedSummarizingRNN │  963 K │
│ 18 │ net.Do_17 │ Dropout                  │      0 │
│ 19 │ net.O_18  │ LinSoftmax               │ 40.9 K │
└────┴───────────┴──────────────────────────┴────────┘
Trainable params: 4.0 M                                                                                                            
Non-trainable params: 0                                                                                                            
Total params: 4.0 M                                                                                                                
Total estimated model params size (MB): 16                                                                                         
stage 0/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:39:16 val_accuracy: 0.23447  early_stopping: 0/5 0.23447
stage 1/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:36:53 val_accuracy: 0.54866  early_stopping: 0/5 0.54866
stage 2/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:56 val_accuracy: 0.72389  early_stopping: 0/5 0.72389
stage 3/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:55 val_accuracy: 0.79733  early_stopping: 0/5 0.79733
stage 4/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:32 val_accuracy: 0.82193  early_stopping: 0/5 0.82193
stage 5/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:45 val_accuracy: 0.84075  early_stopping: 0/5 0.84075
stage 6/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:52 val_accuracy: 0.85990  early_stopping: 0/5 0.85990
stage 7/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:57 val_accuracy: 0.86943  early_stopping: 0/5 0.86943
stage 8/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:35 val_accuracy: 0.87453  early_stopping: 0/5 0.87453
stage 9/∞  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:54 val_accuracy: 0.87611  early_stopping: 0/5 0.87611
stage 10/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:58 val_accuracy: 0.89034  early_stopping: 0/5 0.89034
stage 11/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:28 val_accuracy: 0.88987  early_stopping: 1/5 0.89034
stage 12/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:56 val_accuracy: 0.89582  early_stopping: 0/5 0.89582
stage 13/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:50 val_accuracy: 0.90355  early_stopping: 0/5 0.90355
stage 14/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:54 val_accuracy: 0.90402  early_stopping: 0/5 0.90402
stage 15/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:51 val_accuracy: 0.90193  early_stopping: 1/5 0.90402
stage 16/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:46 val_accuracy: 0.90530  early_stopping: 0/5 0.90530
stage 17/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:20:10 val_accuracy: 0.90902  early_stopping: 0/5 0.90902
stage 18/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:20:09 val_accuracy: 0.90375  early_stopping: 1/5 0.90902
stage 19/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:59 val_accuracy: 0.90220  early_stopping: 2/5 0.90902
stage 20/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:50 val_accuracy: 0.90522  early_stopping: 3/5 0.90902
stage 21/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:35 val_accuracy: 0.90774  early_stopping: 4/5 0.90902
stage 22/∞ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42107/42107 0:00:00 0:19:46 val_accuracy: 0.90803  early_stopping: 5/5 0.90902
Moving best model lectaurep_base_17.mlmodel (0.9090173840522766) to lectaurep_base_best.mlmodel
```

## Testing lectaurep_base_best on the test set (in-domain)

```
$ ketos test -m lectaurep_base_best.mlmodel -e test.list -f xml -u NFD -d cuda:1
```

```
WARNING:root:scikit-learn version 1.0.2 is not supported. Minimum required version: 0.17. Maximum required version: 0.19.2. Disabling scikit-learn conversion API.
WARNING:root:Torch version 1.11.0+cu102 has not been tested with coremltools. You may run into unexpected errors. Torch 1.10.2 is the most recent version that has been tested.
Loading model lectaurep_base_best.mlmodel	✓
[05/11/22 13:56:30] WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
                    WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
                    WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
                    WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
                    WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
                    WARNING  Region eSc_dummyblock_ without coordinates                                                  xml.py:242
Evaluating lectaurep_base_best.mlmodel
Evaluating ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 1821/1821 0:00:00 0:10:57
=== report  ===

36332	Characters
2696	Errors
92.58%	Accuracy

1006	Insertions
360	Deletions
1330	Substitutions

Count	Missed	%Right
10869	638	94.13%	Common
24674	1564	93.66%	Latin
789	134	83.02%	Inherited

Errors	Correct-Generated
175	{ SPACE } - {  }
88	{ e } - {  }
79	{  } - { SPACE }
62	{ s } - {  }
62	{ . } - {  }
57	{ u } - { n }
56	{ r } - {  }
44	{ COMBINING ACUTE ACCENT } - {  }
43	{ ^ } - {  }
42	{  } - { e }
41	{ i } - {  }
40	{ t } - {  }
40	{ COMBINING GRAVE ACCENT } - {  }
33	{ n } - {  }
30	{  } - { r }
26	{ n } - { u }
26	{ e } - { o }
24	{ o } - {  }
23	{ a } - {  }
23	{ l } - {  }
23	{ a } - { o }
23	{ COMBINING GRAVE ACCENT } - { COMBINING ACUTE ACCENT }
21	{  } - { s }
20	{ c } - { e }
20	{ u } - {  }
19	{ d } - {  }
19	{  } - { i }
19	{ , } - {  }
18	{ r } - { n }
18	{ 1 } - {  }
17	{  } - { COMBINING ACUTE ACCENT }
17	{ n } - { r }
16	{ l } - { t }
16	{ - } - {  }
15	{ i } - { e }
14	{  } - { COMBINING GRAVE ACCENT }
13	{ t } - { l }
13	{ a } - { A }
13	{  } - { n }
12	{ c } - {  }
12	{ m } - { n }
12	{ r } - { s }
11	{  } - { t }
11	{  } - { - }
11	{  } - { ^ }
11	{ a } - { e }
10	{ c } - { C }
10	{ s } - { r }
10	{ &#34; } - {  }
9	{  } - { o }
9	{ u } - { a }
9	{ q } - { g }
9	{ 5 } - {  }
9	{ 7 } - {  }
9	{ r } - { u }
9	{ u } - { r }
9	{ i } - { r }
9	{  } - { , }
8	{  } - { l }
8	{ 0 } - {  }
8	{ s } - { S }
8	{ n } - { m }
8	{  } - { c }
8	{ p } - {  }
8	{ e } - { a }
8	{ . } - { , }
8	{ s } - { e }
8	{ s } - { n }
8	{ o } - { s }
7	{ v } - {  }
7	{ e } - { i }
7	{ t } - { s }
7	{ u } - { i }
7	{ m } - {  }
6	{  } - { . }
6	{ s } - { f }
6	{ &#39; } - {  }
6	{ a } - { u }
6	{ l } - { h }
6	{ f } - {  }
6	{ ) } - {  }
6	{ m } - { M }
6	{ d } - { D }
6	{ s } - { t }
6	{ v } - { r }
5	{ u } - { e }
5	{ b } - { l }
5	{ ^ } - { . }
5	{ i } - { u }
5	{ S } - { F }
5	{ COMBINING DIAERESIS } - {  }
5	{ 5 } - { 6 }
5	{ e } - { s }
5	{ x } - { s }
5	{ v } - { s }
5	{ t } - { e }
5	{ r } - { t }
5	{ o } - { e }
5	{ d } - { s }
5	{ n } - { s }
5	{ r } - { e }
5	{ c } - { d }
5	{  } - { u }
4	{ r } - { l }
4	{ i } - { l }
4	{ s } - { o }
4	{ L } - { l }
4	{ i } - { t }
4	{ 9 } - { 5 }
4	{ 3 } - { 8 }
4	{ i } - { n }
4	{ n } - { i }
4	{ a } - { n }
4	{ s } - { d }
4	{ v } - { o }
4	{ SPACE } - { s }
4	{ G } - {  }
4	{ p } - { f }
4	{  } - { p }
4	{ i } - { s }
4	{ COMBINING CIRCUMFLEX ACCENT } - {  }
4	{ t } - { r }
4	{ m } - { i }
4	{ e } - { c }
4	{ m } - { u }
4	{ M } - { m }
4	{ S } - { s }
4	{ h } - { b }
4	{ L } - { P }
4	{ | } - {  }
3	{ COMBINING TILDE } - {  }
3	{ C } - {  }
3	{ ^ } - { r }
3	{ 1 } - { 4 }
3	{ 2 } - { 3 }
3	{ 8 } - {  }
3	{ 2 } - { 1 }
3	{ c } - { t }
3	{ y } - { g }
3	{ 2 } - {  }
3	{ i } - { o }
3	{ f } - { p }
3	{ o } - { a }
3	{ a } - { d }
3	{ o } - { d }
3	{ d } - { t }
3	{ g } - { y }
3	{ r } - { c }
3	{ F } - { P }
3	{ e } - { . }
3	{ n } - { t }
3	{ c } - { u }
3	{ ^ } - { e }
3	{ e } - { t }
3	{ c } - { i }
3	{ 5 } - { 0 }
3	{ SPACE } - { l }
3	{  } - { a }
3	{ H } - { h }
3	{ ( } - {  }
3	{ C } - { c }
3	{ - } - { SPACE }
3	{ M } - {  }
3	{ 1 } - { 2 }
3	{ g } - { e }
3	{  } - { ) }
3	{ L } - {  }
3	{ 9 } - { 8 }
3	{  } - { M }
3	{ - } - { . }
3	{ C } - { ( }
3	{ ° } - { o }
3	{ 9 } - { 3 }
2	{ &amp; } - {  }
2	{ F } - { S }
2	{ t } - { T }
2	{ A } - {  }
2	{ e } - { u }
2	{ l } - { b }
2	{ SPACE } - { f }
2	{ d } - { b }
2	{ S } - { J }
2	{ . } - { ^ }
2	{ e } - { l }
2	{ o } - { O }
2	{ e } - { g }
2	{ j } - { i }
2	{ S } - {  }
2	{ d } - { S }
2	{ l } - { L }
2	{ N } - { M }
2	{ 6 } - { 5 }
2	{ 7 } - { 3 }
2	{ 8 } - { 3 }
2	{ 2 } - { 4 }
2	{ 9 } - { 1 }
2	{ 5 } - { 1 }
2	{ r } - { i }
2	{ e } - { r }
2	{ b } - { S }
2	{ a } - { h }
2	{  } - { P }
2	{ s } - { a }
2	{ x } - { a }
2	{ c } - { a }
2	{ 1 } - { 5 }
2	{  } - { g }
2	{ e } - { n }
2	{ U } - { A }
2	{ C } - { G }
2	{ b } - {  }
2	{ Z } - { G }
2	{ P } - { S }
2	{ d } - { A }
2	{ D } - { C }
2	{ E } - { C }
2	{  } - { 1 }
2	{  } - { 9 }
2	{  } - { 0 }
2	{  } - { 7 }
2	{ V } - { P }
2	{ b } - { i }
2	{ x } - { e }
2	{ m } - { s }
2	{ 8 } - { 1 }
2	{ n } - { e }
2	{ t } - { i }
2	{ . } - { e }
2	{ L } - { R }
2	{ b } - { P }
2	{ P } - {  }
2	{ D } - { S }
2	{ o } - { i }
2	{ s } - { c }
2	{ c } - { COMBINING ACUTE ACCENT }
2	{ 8 } - { 0 }
2	{ % } - { 5 }
2	{ B } - { P }
2	{ v } - { d }
2	{ 9 } - {  }
2	{ r } - { ^ }
2	{ l } - { s }
2	{ o } - { n }
2	{ 6 } - { 8 }
2	{ 3 } - { 2 }
2	{ a } - { r }
2	{ 1 } - { e }
2	{ X } - {  }
2	{ N } - { ¥ }
2	{ z } - {  }
2	{ T } - { C }
2	{ ; } - {  }
2	{ H } - { B }
2	{ 0 } - { 9 }
2	{ , } - { . }
2	{ 7 } - { 5 }
2	{ t } - { f }
2	{ e } - { d }
2	{ J } - { F }
2	{ Q } - { q }
2	{ h } - { l }
2	{ E } - { T }
2	{ c } - { r }
2	{ x } - { n }
2	{ l } - { f }
2	{ f } - { l }
2	{ SPACE } - { a }
2	{ x } - { r }
2	{ t } - { d }
2	{ D } - { d }
2	{ y } - {  }
2	{ z } - { r }
2	{ f } - { F }
2	{ / } - {  }
2	{  } - { d }
2	{ M } - { N }
2	{ COMBINING ACUTE ACCENT } - { i }
2	{ d } - { P }
2	{ J } - { G }
2	{ I } - { S }
2	{ r } - { d }
2	{ r } - { a }
2	{ g } - { z }
2	{ d } - { i }
2	{ R } - { P }
2	{ | } - { - }
2	{ | } - { SPACE }
2	{ &#34; } - { - }
2	{  } - { S }
2	{ &#39; } - { e }
2	{ , } - { d }
2	{ D } - { B }
2	{ i } - { COMBINING GRAVE ACCENT }
2	{  } - { m }
2	{ t } - { n }
2	{ C } - { A }
2	{ g } - { d }
2	{ k } - { l }
2	{ J } - { S }
2	{ r } - { v }
2	{ i } - { m }
2	{  } - { COMBINING CIRCUMFLEX ACCENT }
2	{ ° } - {  }
2	{ c } - { v }
2	{ 4 } - { 6 }
1	{ SPACE } - { 8 }
1	{ V } - { R }
1	{ SPACE } - { d }
1	{ &amp; } - { ^ }
1	{ &#39; } - { SPACE }
1	{ d } - { u }
1	{ SPACE } - { &#39; }
1	{ c } - { l }
1	{ T } - { R }
1	{ G } - { g }
1	{ K } - { H }
1	{ g } - { q }
1	{ s } - { v }
1	{ i } - { y }
1	{ u } - { f }
1	{ V } - { l }
1	{ f } - { t }
1	{ 2 } - { 0 }
1	{ U } - { V }
1	{ S } - { f }
1	{ q } - { y }
1	{ u } - { p }
1	{ r } - { b }
1	{  } - { 4 }
1	{ 1 } - { 7 }
1	{ 4 } - { 7 }
1	{ 0 } - { 6 }
1	{  } - { 3 }
1	{ 6 } - { 0 }
1	{ b } - { R }
1	{ p } - { y }
1	{ L } - { E }
1	{ S } - { L }
1	{ , } - { c }
1	{ SPACE } - { o }
1	{ SPACE } - { y }
1	{ 5 } - { ( }
1	{ &amp; } - { p }
1	{ SPACE } - { e }
1	{ G } - { Q }
1	{ T } - { E }
1	{ 3 } - { d }
1	{ - } - { e }
1	{ 6 } - { SPACE }
1	{ - } - { b }
1	{ 9 } - { i }
1	{ 1 } - { V }
1	{ h } - {  }
1	{ COMBINING GRAVE ACCENT } - { i }
1	{ d } - { l }
1	{ l } - { C }
1	{  } - { D }
1	{  } - { ( }
1	{ l } - { i }
1	{ s } - { b }
1	{ 5 } - { f }
1	{ F } - { D }
1	{ A } - { E }
1	{ s } - { 1 }
1	{ M } - { R }
1	{ u } - { s }
1	{ y } - { p }
1	{ b } - { A }
1	{ b } - { t }
1	{ i } - { d }
1	{ a } - { f }
1	{ z } - { o }
1	{ e } - { &amp; }
1	{ G } - { F }
1	{ z } - { a }
1	{ % } - { 0 }
1	{ Y } - { I }
1	{ l } - { a }
1	{ SPACE } - { M }
1	{ d } - { o }
1	{ 2 } - { 5 }
1	{  } - { A }
1	{ , } - { s }
1	{ p } - { r }
1	{ R } - { L }
1	{ P } - { V }
1	{ H } - { V }
1	{ e } - { f }
1	{ H } - { R }
1	{ f } - { + }
1	{ R } - { J }
1	{ J } - { B }
1	{ n } - { o }
1	{ l } - { 4 }
1	{ SPACE } - { J }
1	{ t } - { p }
1	{ SPACE } - { t }
1	{ v } - { u }
1	{ a } - { 7 }
1	{ a } - { i }
1	{ c } - { n }
1	{ I } - { F }
1	{ Q } - { E }
1	{ L } - { T }
1	{ , } - { G }
1	{ SPACE } - { r }
1	{  } - { 6 }
1	{ l } - { B }
1	{ . } - { i }
1	{ j } - {  }
1	{ o } - { r }
1	{ , } - { t }
1	{ g } - { G }
1	{ g } - { o }
1	{ b } - { s }
1	{ h } - { r }
1	{ &#39; } - { t }
1	{ d } - { n }
1	{ SPACE } - { S }
1	{ L } - { C }
1	{ COMBINING ACUTE ACCENT } - { COMBINING GRAVE ACCENT }
1	{ p } - { COMBINING ACUTE ACCENT }
1	{ SPACE } - { b }
1	{ c } - { s }
1	{ COMBINING GRAVE ACCENT } - { o }
1	{ f } - { J }
1	{ 8 } - { 5 }
1	{ p } - { e }
1	{ i } - { a }
1	{ R } - { C }
1	{ P } - { b }
1	{ P } - { C }
1	{ COMBINING CIRCUMFLEX ACCENT } - { i }
1	{ J } - { p }
1	{ a } - { s }
1	{ n } - { a }
1	{ t } - { v }
1	{ 2 } - { 9 }
1	{ . } - { 8 }
1	{ i } - { COMBINING CIRCUMFLEX ACCENT }
1	{ j } - { J }
1	{ ^ } - { i }
1	{ r } - { o }
1	{ A } - { C }
1	{ v } - { n }
1	{ 7 } - { SPACE }
1	{ S } - { ( }
1	{ t } - { ^ }
1	{ 9 } - { u }
1	{ 0 } - { e }
1	{ 4 } - {  }
1	{ s } - { g }
1	{ O } - { B }
1	{ f } - { S }
1	{ u } - { G }
1	{ COMBINING GRAVE ACCENT } - { t }
1	{ s } - { SPACE }
1	{ C } - { S }
1	{ s } - { F }
1	{ m } - { &#39; }
1	{ M } - { p }
1	{ T } - { b }
1	{ : } - {  }
1	{  } - { COMBINING CEDILLA }
1	{ F } - { p }
1	{ c } - { g }
1	{ COMBINING CEDILLA } - { u }
1	{ B } - { b }
1	{ F } - { f }
1	{ d } - { T }
1	{ 1 } - { 3 }
1	{ 1 } - { 0 }
1	{ E } - { a }
1	{ 5 } - { 8 }
1	{ 5 } - { 3 }
1	{ ( } - { 1 }
1	{ ^ } - { b }
1	{ t } - { &#39; }
1	{ &amp; } - { e }
1	{ n } - { N }
1	{ 3 } - { P }
1	{ &amp; } - { 5 }
1	{ n } - { COMBINING GRAVE ACCENT }
1	{ COMBINING CEDILLA } - { e }
1	{ b } - { c }
1	{  } - { h }
1	{ d } - { E }
1	{ &#39; } - { i }
1	{ 1 } - { S }
1	{ R } - {  }
1	{ COMBINING DIAERESIS } - { t }
1	{ k } - { t }
1	{ i } - { COMBINING ACUTE ACCENT }
1	{ 1 } - { t }
1	{ f } - { s }
1	{ d } - { C }
1	{ P } - { L }
1	{ o } - { m }
1	{ e } - { y }
1	{ v } - { a }
1	{ P } - { f }
1	{ s } - { p }
1	{ r } - { x }
1	{ q } - { o }
1	{ . } - { 1 }
1	{ . } - { 3 }
1	{ . } - { 2 }
1	{ t } - { u }
1	{ 1 } - { 9 }
1	{ . } - { SPACE }
1	{ a } - { ^ }
1	{ e } - { SPACE }
1	{ B } - { D }
1	{ N } - { h }
1	{ 1 } - { 8 }
1	{ 8 } - { 2 }
1	{ 7 } - { 2 }
1	{ 7 } - { 9 }
1	{ &gt; } - {  }
1	{ ~ } - { a }
1	{ J } - { Y }
1	{ 5 } - { I }
1	{ 0 } - { v }
1	{ 0 } - { o }
1	{ 0 } - { r }
1	{ 0 } - { s }
1	{ v } - { V }
1	{ o } - { H }
1	{ S } - { M }
1	{ 7 } - { P }
1	{ ^ } - { y }
1	{ P } - { D }
1	{ a } - { c }
1	{ F } - { V }
1	{ ^ } - { SPACE }
1	{ o } - { A }
1	{ h } - { H }
1	{ A } - { H }
1	{ d } - { B }
1	{ H } - { M }
1	{ J } - { H }
1	{ t } - { M }
1	{ ( } - { p }
1	{ t } - { S }
1	{ COMBINING GRAVE ACCENT } - { a }
1	{ p } - { . }
1	{ p } - { G }
1	{ V } - { v }
1	{ / } - { ( }
1	{ o } - { y }
1	{ l } - { e }
1	{ J } - { g }
1	{ X } - { l }
1	{ X } - { e }
1	{ SPACE } - { C }
1	{ R } - { l }
1	{  } - { y }
1	{ r } - { p }
1	{ COMBINING GRAVE ACCENT } - { s }
1	{ d } - { a }
1	{ 7 } - { 4 }
1	{ 7 } - { 1 }
1	{ 3 } - { 5 }
1	{ o } - { ° }
1	{ 2 } - { 7 }
1	{ 3 } - { 4 }
1	{ 0 } - { 8 }
1	{ 5 } - { 2 }
1	{ 0 } - { 4 }
1	{ p } - { a }
1	{ o } - { SPACE }
1	{ r } - { B }
1	{ T } - { D }
1	{ J } - { j }
1	{ n } - { p }
1	{ p } - { n }
1	{ A } - { D }
1	{ ( } - { t }
1	{ I } - { A }
1	{ + } - {  }
1	{ 7 } - { ( }
1	{ + } - { f }
1	{ % } - {  }
1	{ d } - { f }
1	{ a } - { SPACE }
1	{ Y } - { A }
1	{ m } - { v }
1	{ v } - { b }
1	{ I } - {  }
1	{ 6 } - { b }
1	{ r } - { m }
1	{ SPACE } - { x }
1	{ - } - { s }
1	{ S } - { SPACE }
1	{  } - { Q }
1	{ &#34; } - { a }
1	{ ) } - { f }
1	{ N } - { H }
1	{ . } - { l }
1	{ C } - { O }
1	{ V } - { S }
1	{ 2 } - { A }
1	{ C } - { V }
1	{ s } - { x }
1	{ a } - { L }
1	{ X } - { C }
1	{ t } - { b }
1	{ 3 } - { V }
1	{ % } - { r }
1	{ &#39; } - { . }
1	{ I } - { V }
1	{ V } - { B }
1	{ J } - { ( }
1	{ SPACE } - { | }
1	{ 3 } - { 9 }
1	{ V } - { F }
1	{ I } - { 1 }
1	{ P } - { F }
1	{ SPACE } - { i }
1	{ G } - { 5 }
1	{ ^ } - { t }
1	{ R } - { F }
1	{ 4 } - { 5 }
1	{ M } - { O }
1	{ &#39; } - { E }
1	{ I } - { b }
1	{  } - { b }
1	{ r } - { N }
1	{ P } - { a }
1	{ y } - { i }
1	{ COMBINING DIAERESIS } - { z }
1	{ H } - {  }
1	{ H } - { F }
1	{ E } - { P }
1	{ k } - { b }
1	{ 4 } - { 1 }
1	{ ¥ } - { 2 }
1	{ z } - { s }
1	{ b } - { r }
1	{ M } - { V }
1	{ V } - { a }
1	{ D } - { P }
1	{ m } - { e }
1	{ L } - { S }
1	{ 2 } - { 8 }
1	{ p } - { g }
1	{  } - { ° }
1	{ h } - { u }
1	{ f } - { r }
1	{ d } - { M }
1	{ G } - { J }
1	{ a } - { E }
1	{ d } - { 2 }
1	{ e } - { 0 }
1	{ R } - { N }
1	{ p } - { s }
1	{ A } - { N }
1	{ t } - { I }
1	{ e } - { T }
1	{ T } - { P }
1	{ f } - { P }
1	{ 4 } - { 8 }
1	{  } - { &#34; }
1	{ M } - { P }
1	{ C } - { f }
1	{ K } - { R }
1	{ y } - { 1 }
1	{ COMBINING GRAVE ACCENT } - { g }
1	{ E } - { i }
1	{ t } - { c }
1	{ y } - { e }
1	{ p } - { 8 }
1	{ p } - { 7 }
1	{ % } - { , }
1	{  } - { 5 }
1	{ h } - { s }
1	{ A } - { d }
1	{ COMBINING ACUTE ACCENT } - { u }
1	{ v } - { e }
1	{ B } - { d }
1	{ u } - { m }
1	{ b } - { e }

Average accuracy: 92.58%, (stddev: 0.00)
```
