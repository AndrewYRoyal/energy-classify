# energy-classify
Classification of Energy End-Use: Modeling AMI with Random Convolutional Kernels

This repository automates training and classification of meter loadpaths of any interval (e.g. hourly, daily, monthly). The classification algorithm uses a ridge regression with features generated by random convlutional kernels (see https://github.com/angus924/rocket). All modeling options are specified in `cfg.yaml`. The model is trained from the command line with:

```$ python train.py```

The model and kernels are then stored in `output/model_bundle.pkl`. Predictions are generated using:

```$ python predict.py```

Output:
```
predictions.head(10)
Out[10]: 
      tenant   laundry  lighting      pool  pred
id                                              
0   0.002780  0.435816  0.558282  0.003122     2
1   0.004709  0.067743  0.912986  0.014562     2
2   0.005381  0.084194  0.848237  0.062188     2
3   0.005587  0.032438  0.935994  0.025982     2
4   0.004071  0.116428  0.840876  0.038625     2
5   0.918275  0.049711  0.029384  0.002630     0
6   0.319146  0.548611  0.127307  0.004936     1
7   0.163174  0.783827  0.044362  0.008638     1
8   0.037627  0.702198  0.249432  0.010743     1
9   0.112792  0.754352  0.126365  0.006491     1
```

Each column in the resulting `prediction.csv` above indicates indicates the probability that the service point (`id`) corresponds to one of the end use classes specified in the ground truth dataset. The `pred` column indicates the class index with the greatest probability.


In addition to a configuration file, training and prediction require three tables stored in an '~/input/' directory: `classes.csv` (columns: `id`, `class`), `splits.csv` (columns: `id`, `group`) and `interval.csv` (columns: `id`, `time`, `use`). The first table stores ground truth class labels for training observations, the second splits observations into groups ('train', 'holdout', 'unknown') and the third includes interval consumption data in long format. 

The `cfg.yaml` allows configuration for automated downloading and syncing from AWS s3 buckets.
