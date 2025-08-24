# Loan Default Risk Prediction

**Goal:** Predict whether a person is at risk of defaulting on their payment and add explainability using SHAP.

**Dataset link:** github.com/MatteoM95/Default-of-Credit-Card-Clients-Dataset-Analisys

**Dataset columns:** `ID`, `LIMIT_BAL`, `SEX`, `EDUCATION`, `MARRIAGE`, `AGE`, `PAY_0`, `PAY_2`, `PAY_3`, `PAY_4`, `PAY_5`, `PAY_6`, `BILL_AMT1`, `BILL_AMT2`, `BILL_AMT3`, `BILL_AMT4`, `BILL_AMT5`, `BILL_AMT6`, `PAY_AMT1`, `PAY_AMT2`, `PAY_AMT3`, `PAY_AMT4`, `PAY_AMT5`, `PAY_AMT6`, `default payment next month`

**Target definition:** `Default = 1` if the client defaults on the payment the following month, else `0`.


## 🔍 Explainability with SHAP

To ensure the loan default risk model is **transparent and interpretable**, we applied **SHAP (SHapley Additive exPlanations)** to the trained classifiers.

* **Why SHAP?**
  SHAP values explain each prediction as a sum of feature contributions. This helps us understand *why* the model flagged a customer as high or low risk, instead of treating the model as a black box.

* **Global Insights**
  Using SHAP beeswarm and bar plots, we found that the most important risk drivers across the dataset were:

  * **Repayment history (`PAY_0`, `PAY_2`, etc.)** → recent late payments strongly increase default risk.
  * **Utilization ratio** → high credit usage relative to credit limit is a major risk factor.
  * **Repayment trend** → customers paying less over recent months have higher risk.
  * **Demographics (`EDUCATION`, `MARRIAGE`, `AGE`)** → weaker but still relevant signals.

* **Local Explanations**
  For an individual applicant, SHAP waterfall plots show how each feature **pushed the prediction** toward “default” or “no default.”
  Example:

  * High utilization ratio (+0.27) and missed last payment (+0.41) pushed the prediction toward default.
  * A high credit limit (−0.15) reduced the predicted risk.

* **Business Use**
  SHAP explanations can be translated into **plain-English reason codes** to support decisions:

  * “High credit utilization increased risk.”
  * “Recent missed payment raised risk.”
  * “Stable repayment trend lowered risk.”

This enables loan officers (and customers) to understand *why* a risk prediction was made, ensuring both **regulatory compliance** and **trust in the model**.

