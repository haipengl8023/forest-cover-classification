# Forest Cover Classification

Predict seven forest cover types from terrain, soil, and wilderness-area characteristics. This collaborative project compares an interpretable logistic baseline, a decision tree, and a random forest, with equal weight given to each class in macro-F1. [UCI Covertype dataset](https://archive.ics.uci.edu/dataset/31/covertype)

## Workflow

- [Prepare the data](01_prepare_data.ipynb). Profile the 581,012-row source, consolidate wilderness and soil indicators, and take a reproducible stratified sample of 30,000 rows.
- [Compare the models](02_compare_models.ipynb). Keep a stratified 20% holdout. Fit imputation, scaling, and encoding inside the training pipeline. Tune the tree models on three training folds, then compare holdout macro-F1 and inspect class-level errors.

## Holdout results

| Model | Accuracy | Macro-F1 |
| --- | ---: | ---: |
| Logistic regression | 0.7285 | 0.5175 |
| Decision tree | 0.7815 | 0.6538 |
| Random forest | **0.8355** | **0.7138** |

The random forest led on both metrics across the 6,000-row holdout. It recalled 27% of Aspen and 43% of Cottonwood/Willow examples, two of the least represented classes.

## Reproduce

Use Python 3.11 and run the two notebooks in order from the repository root.

```bash
python -m pip install -r requirements.txt
jupyter lab
```

The first notebook downloads and caches Covertype through scikit-learn. It writes the prepared CSV under `data/`. Set `SAMPLE_ROWS = None` to use the full dataset. [scikit-learn data loader](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.fetch_covtype.html)

## 中文简介

使用地形、土壤和荒野区域信息预测七种森林覆盖类型。项目通过分层抽样、训练折内预处理和 Macro-F1 对比逻辑回归、决策树与随机森林，并检查少数类别的召回情况。
