# Salary Prediction Using CART & ENSEMBLE METHODS 💼📊

![Repository](https://img.shields.io/badge/View-Repository-blue?style=for-the-badge&logo=github) ![Download](https://img.shields.io/badge/Download-Dataset-green?style=for-the-badge&logo=databricks)

---

[![Jump to Overview](https://img.shields.io/badge/Jump%20to-Overview-orange)](#project-overview-) 
[![Jump to Insights](https://img.shields.io/badge/Jump%20to-Insights%20&%20Recommendations-yellow)](#results--recommendations-) 
[![Jump to Conclusion](https://img.shields.io/badge/Jump%20to-Conclusion-lightblue)](#conclusion-)

---

## Project Overview 📚
This project, inspired by the **Hitters dataset** from the `ISLR2` package, aims to predict salary using a variety of machine learning techniques, including **CART**, **Bagging**, **Random Forests**, and **Boosting**.

### Table of Contents 🗂️
- [Business Impact & Insights](#business-impact--insights-)
- [Data Set & Preparation](#data-set--preparation-)
- [Modeling Techniques & Comparisons](#modeling-techniques--comparisons-)
- [Results & Recommendations](#results--recommendations-)
- [Key Takeaways](#key-takeaways-)
- [Conclusion](#conclusion-)

---

## Business Impact & Insights 💼💡

### Why This Matters
Understanding salary prediction is crucial for organizations to maintain competitive compensation strategies. Accurate models can:

| Benefit | Description |
|---------|-------------|
| **Optimize Salary Structures** | Align employee compensation with market trends. |
| **Identify Key Predictors** | Focus on the factors that most influence salary, leading to informed HR decisions. |
| **Reduce Turnover** | Predict under-compensated roles to proactively address potential dissatisfaction. |


---

## Data Set & Preparation 🗂️🔧

### Data Source
The dataset used in this analysis is the **Hitters dataset** from the `ISLR2` package.

### Data Cleaning:
- Removed categorical variables: `League`, `Division`, `NewLeague`.
- Excluded incomplete records with missing salary data.
- Applied a logarithmic transformation to the `Salary` variable to normalize the distribution.

```r
# Log transformation of Salary
new_Hitters$log_of_Salary <- log(new_Hitters$Salary)
```

## Modeling Techniques & Comparisons 🧠⚖️

### A) CART: Full Tree vs. Pruned Tree
- **Full Tree**: Low MSE but prone to overfitting.
- **Pruned Tree**: Higher MSE, but better generalization.

### B) Bagging 🌳🌳🌳
- **Misclassification Rate**: 0.2115
- **Improves Overfitting**: Bagging averages predictions to reduce variance.

### C) Random Forests 🌲
- **Explored Different mtry Values**:
  - `m = p`, `m = p/2`, and `m = √p`
- **Findings**:
  - Random forests with `m = p/2` and `m = √p` showed slight improvements over Bagging.

### D) Boosting 🚀
- **Shrinkage Parameters Tested**: 0.1, 0.4, 0.6, 0.8
- **Test Errors**: Found optimal performance with a slower learning rate.

```r
# Example code for Boosting
library(gbm)
fit <- gbm(High ~ ., data = train, n.trees = 1000, shrinkage = 0.1, interaction.depth = 3, distribution = "adaboost")
```

## Results & Recommendations 🎯💬

### Results:
| Technique          | Outcome                                               |
|--------------------|-------------------------------------------------------|
| **CART Pruned Tree** | Balance between interpretability and accuracy.        |
| **Bagging**         | Reduced variance but some misclassifications remain. |
| **Random Forests**  | Marginal improvements with specific mtry values.      |
| **Boosting**        | Importance of selecting the right shrinkage parameter for better generalization. |

### Recommendations for Business:
- **Use Pruned CART**: For simpler, interpretable models with a balance of accuracy.
- **Consider Random Forests**: When you need robustness and can afford computational intensity.
- **Boosting**: Optimal when you require the best possible accuracy and are dealing with large datasets.

## Key Takeaways 📝
- **CART Models**: Pruning is essential to avoid overfitting.
- **Ensemble Methods**: Bagging and Random Forests reduce variance and prevent overfitting, while Boosting focuses on sequential improvement.
- **Predictor Subsets**: In Random Forests, using a subset of predictors can sometimes outperform using all predictors.

## Conclusion 🎓
The analysis provides a comprehensive comparison of various predictive modeling techniques applied to salary prediction. From CART to Boosting, each method has its strengths and is suited to different business needs. For data scientists, understanding the nuances of model selection is crucial, as it directly impacts the accuracy and generalization of predictive models.

### Importance as a Data Scientist:
- **Model Selection**: Always consider the trade-off between complexity and accuracy.
- **Statistical Implications**: Proper model tuning, like pruning or selecting appropriate mtry values, is critical for robust predictions.
- **Real-World Impact**: Accurate salary predictions can significantly affect business decisions and employee satisfaction.

