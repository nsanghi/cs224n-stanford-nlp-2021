## Select answers to the assignment

### 2(a) Complete the sequence of transitions needed for parsing the sentence `Today I parsed a sentence`

| Stack | Buffer | New Dependency | Transition |
|:-----:|:------:|:---------------:|:---------:|
| `[ROOT]` | `[Today, I, parsed, a, sentence]` |  | `Initial COnfiguration` |
| `[ROOT, Today]` | `[I, parsed, a, sentence]` |  | `SHIFT` |
| `[ROOT, Today, I]` | `[parsed, a, sentence]` |  | `SHIFT` |
| `[ROOT, Today, I, parsed]` | `[a, sentence]` |  | `SHIFT` |
| `[ROOT, Today, parsed]` | `[a, sentence]` | `parsed -> I` | `LEFT-ARC` |
| `[ROOT, parsed]` | `[a, sentence]` | `parsed -> Today` | `LEFT-ARC` |
| `[ROOT, parsed, a]` | `[sentence]` |  | `SHIFT` |
| `[ROOT, parsed, a, sentence]` | `[]` |  | `SHIFT` |
| `[ROOT, parsed, sentence]` | `[]` |  | `LEFT-ARC` |
| `[ROOT, parsed]` | `[]` |  | `RIGHT-ARC` |
| `[ROOT]` | `[]` |  | `RIGHT-ARC` | 

### 2(b) A sentence containing n words will be parsed in how many steps (in terms of n)? Briefly explain in 1-2 sentences why

A sentence with `n` words will need `n` shifts and `n` dependecies, one for each word. Therefore, in total we will need `2n` transitions consisting of `n` `SHIFT` and `n` `LEFT-ARC` \ or `RIGHT-ARC` transitions.

### Results
```
$ python run.py
================================================================================
INITIALIZING
================================================================================
Loading data...
took 1.09 seconds
Building parser...
took 0.76 seconds
Loading pretrained embeddings...
took 1.42 seconds
Vectorizing data...
took 1.09 seconds
Preprocessing training data...
took 25.01 seconds
took 0.00 seconds

================================================================================
TRAINING
================================================================================
Epoch 1 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:57<00:00, 32.38it/s]
Average Train Loss: 0.18377389395972352
Evaluating on dev set
1445850it [00:00, 76960512.18it/s]                                                                                                            
- dev UAS: 83.57
New best dev UAS! Saving model.

Epoch 2 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.70it/s]
Average Train Loss: 0.11377566545653395
Evaluating on dev set
1445850it [00:00, 77319645.53it/s]                                                                                                            
- dev UAS: 86.25
New best dev UAS! Saving model.

Epoch 3 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.86it/s]
Average Train Loss: 0.09955062138045699
Evaluating on dev set
1445850it [00:00, 76982982.40it/s]                                                                                                            
- dev UAS: 87.18
New best dev UAS! Saving model.

Epoch 4 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.84it/s]
Average Train Loss: 0.09094518216254262
Evaluating on dev set
1445850it [00:00, 77379827.21it/s]                                                                                                            
- dev UAS: 87.87
New best dev UAS! Saving model.

Epoch 5 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.85it/s]
Average Train Loss: 0.08446321019991523
Evaluating on dev set
1445850it [00:00, 77225122.74it/s]                                                                                                            
- dev UAS: 87.85

Epoch 6 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.86it/s]
Average Train Loss: 0.07975053802955073
Evaluating on dev set
1445850it [00:00, 78124477.46it/s]                                                                                                            
- dev UAS: 88.25
New best dev UAS! Saving model.

Epoch 7 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:57<00:00, 32.39it/s]
Average Train Loss: 0.0755631838304301
Evaluating on dev set
1445850it [00:00, 75764404.17it/s]                                                                                                            
- dev UAS: 88.75
New best dev UAS! Saving model.

Epoch 8 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.85it/s]
Average Train Loss: 0.07199204924367207
Evaluating on dev set
1445850it [00:00, 77186788.84it/s]                                                                                                            
- dev UAS: 88.34

Epoch 9 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.87it/s]
Average Train Loss: 0.0686643494946229
Evaluating on dev set
1445850it [00:00, 77014267.15it/s]                                                                                                            
- dev UAS: 88.81
New best dev UAS! Saving model.

Epoch 10 out of 10
100%|█████████████████████████████████████████████████████████████████████████████████████████████████████| 1848/1848 [00:56<00:00, 32.84it/s]
Average Train Loss: 0.0661010595524353
Evaluating on dev set
1445850it [00:00, 77935722.49it/s]                                                                                                            
- dev UAS: 88.66

================================================================================
TESTING
================================================================================
Restoring the best model weights found on the dev set
Final evaluation on test set
2919736it [00:00, 109332824.90it/s]                                                                                                           
- test UAS: 89.03
Done!
```