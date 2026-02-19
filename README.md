# Capstone-Initial-Report-and-Exploratory-Data-Analysis-EDA-
Capstone: Initial Report and Exploratory Data Analysis (EDA)
Supply Chain SLA Risk Prediction

Author: Roy José Arce

Executive Summary
This project analyzes shipment performance data to understand the drivers of Service Level Agreement (SLA) compliance and to develop a predictive model for identifying shipments at risk of missing SLA.

Using engineered lead-time features and classification modeling, the final tuned model achieved:
ROC-AUC: 0.947
PR-AUC: 0.997
Accuracy: 0.891

The model demonstrates strong ability to rank SLA risk while maintaining robust cross-validation and no data leakage. This framework can support proactive shipment risk management and operational monitoring.

Rationale
SLA misses in supply chain operations lead to:
Customer dissatisfaction
Revenue delays
Increased working capital exposure
Operational escalations
Understanding the drivers of SLA performance allows organizations to:
Identify systemic operational delays
Monitor weekly SLA trends
Proactively flag at-risk shipments
Optimize planning and fulfillment processes

This analysis demonstrates how structured data science methods can transform operational data into actionable insights.


Research Question

What operational factors drive SLA misses?
Can we accurately predict whether a shipment will meet SLA?
Which engineered features contribute most strongly to SLA outcomes?

Data Sources

The dataset consists of open and shipped order records containing:
Order creation dates
Requested delivery dates
Planned shipment dates
Actual shipment dates
Delivery priorities
Quantity ordered
Operational hold indicators
Financial attributes
The target variable was engineered as:

sla_met = 1 → Shipment met requested delivery date  
sla_met = 0 → Shipment missed requested delivery date

Methodology

The project followed a structured data science workflow:

1. Data Cleaning

Standardized column names
Removed duplicate records
Handled missing values
Converted date fields safely
Filtered invalid records

2. Feature Engineering

Created operational timing features:
order_to_pdd_days
planned_ship_to_pdd_days    
pdd_to_actual_ship_days
Performed outlier detection using IQR
Capped extreme delay values
Removed ID-like numeric fields

3. Exploratory Data Analysis (EDA)

Distribution analysis of shipment delays
SLA outcome comparison
Weekly SLA trend visualization
Class imbalance assessment

4. Modeling

Two models were evaluated:
Model 1 (Leaky – Diagnostic Only)
ROC-AUC: 0.931
Accuracy: 0.875
This model unintentionally included leakage and is shown for comparison purposes only.

Model 2 (No Leakage – Valid Model)

ROC-AUC: 0.950
Accuracy: 0.887

After hyperparameter tuning using 3-fold cross-validation:

Final ROC-AUC: 0.947
Final PR-AUC: 0.997
Final Accuracy: 0.891

Because the dataset is highly imbalanced (~95% SLA met), ROC-AUC and PR-AUC were prioritized over accuracy.
Accuracy alone would be misleading in this context.

Results

Key findings:

Engineered shipment delay features are the strongest predictors of SLA outcome.
The final model demonstrates strong ranking ability (ROC-AUC ≈ 0.95).
Recall for SLA misses is high (0.88), meaning the model captures most late shipments.
Precision for SLA misses is lower (0.29), reflecting class imbalance and false positives.

From a business perspective:

The model is effective for early risk detection where missing a late shipment is more costly than generating false alarms.

Next Steps

Potential improvements include:

Implement cost-sensitive learning
Explore ensemble models (Random Forest, Gradient Boosting)

Outline of project

Use SHAP values for deeper interpretability
Develop a real-time SLA risk dashboard
Incorporate operational capacity metrics
