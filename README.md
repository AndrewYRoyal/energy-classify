# cnn-ami
Classification of Energy End-Use: Modeling AMI with Random Kernels

This repository automates training and classification of AMI loadpaths of any interval (e.g. hourly, daily, monthly). The classification algorithm uses a ridge regression wieth features from random convlutional kernels (see https://github.com/angus924/rocket). All modeling options are specified in `cfg.yaml`. The model is trained from the CLI with:

```$ python train.py```

The model and kernels are then stored in `output/model_bundle.pkl`. Predictions are generated using:

```$ python predict.py```

In addition to a configuration file, training and prediction require three tables stored in an '~/input/' directory: `classes.csv` (columns: `id`, `class`), `splits.csv` (columns: `id`, `group`) and `interval.csv` (columns: `id`, `time`, `use`). The first table stores ground truth class labels for training observations, the second splits observations into groups ('train', 'holdout', 'unknown') and the third includes interval consumption data in long format. 

The `cfg.yaml` allows configuration for automated downloading and syncing from AWS s3 buckets.
