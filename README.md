# Predicting Perfect Rating Scores for Airbnb Listings

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## Overview

This data mining project predicts whether Airbnb listings will achieve a perfect (100%) rating score, developed as a group project for **BUDT 758T: Data Mining and Predictive Analytics** (Spring 2023, taught by Professor Jessica Clark) at the **Robert H. Smith School of Business, University of Maryland, College Park**. Using R, we applied advanced data mining techniques, feature engineering, and machine learning to analyze a comprehensive Airbnb dataset. Our goal was to generate accurate binary predictions with a high True Positive Rate (TPR) while keeping the False Positive Rate (FPR) below 10%, helping hosts optimize listings for better ratings.

**Primary Objectives**:
- Predict perfect rating scores for Airbnb listings using machine learning.
- Identify key factors influencing perfect ratings through exploratory data analysis (EDA) and feature engineering.
- Achieve high prediction accuracy with minimal false positives.
- Provide actionable insights for Airbnb hosts to enhance guest experiences.

## Features

- **Predictive Modeling**: Implements multiple machine learning models (Ranger Random Forest, Logistic Regression, Decision Trees, Lasso, Ridge) to predict perfect ratings.
- **Feature Engineering**: Creates 36 features (e.g., price per person, host response rate, availability ratios) to enhance model performance.
- **Data Exploration**: Visualizes key variables (e.g., price, square footage, cancellation policy) to uncover insights.
- **Model Evaluation**: Uses accuracy, TPR, FPR, and ROC curves to compare model performance.

## Dataset

The dataset, sourced from Airbnb, includes attributes such as:
- **Property Details**: Square footage, property type, room type, bathrooms, beds.
- **Pricing**: Price, cleaning fees, security deposits, price per person.
- **Host Information**: Host response rate, acceptance rate, superhost status, years as host.
- **Booking Metrics**: Availability, cancellation policy, booking flexibility, instant bookability.
- **Location**: Market, exact location indicator.
- **Reviews**: First review date, number of reviews.

**Access**: The dataset is available via [Google Drive](https://drive.google.com/drive/folders/0B9w6UZ00foOlfkhMNElianZ1bXhTd3RRN2dUNkE0VC13aHl0SUY0eUxTMEFaVzhEV3RObWs?resourcekey=0-TFPomCnJaUus_S_ZpA2zew&usp=sharing). Due to size and privacy constraints, it’s hosted externally.

## Methodology

### Data Preparation
- **Exploratory Data Analysis (EDA)**:
  - Visualized price vs. square footage, identifying outliers (e.g., prices >$5,000 for small properties).
  - Analyzed listing counts by price category, market (e.g., New York, Los Angeles), and host response rates.
  - Examined trends in first reviews (peak in 2015-2016, decline in 2017-2018).
- **Preprocessing**:
  - Handled missing values by imputing ‘None’ for categorical nulls and 0 for numerical nulls.
  - Removed outliers (e.g., properties >10,000 sq ft) to reduce data distortion.
- **Feature Engineering**:
  - Created 36 features, including `years_as_host`, `availability_30_ratio`, `price_per_person`, and `booking_flexibility`.
  - Applied dummy variable encoding for categorical variables to support models like Ranger and Logistic Regression.

### Modeling
We evaluated five models in R, with the **Ranger Random Forest** as the winner:
- **Ranger Random Forest** (Winner):
  - Accuracy: 76.79% (test set).
  - TPR: ~42%, FPR: ~8.6%.
  - Used 800 trees, 20 variables per split, and 32 features.
- **Logistic Regression**: Accuracy: 75.22%, TPR: 40.06%, FPR: 9.94%.
- **Decision Trees**: Accuracy: 73.61%, TPR: 33.19%, FPR: 9.33%.
- **Lasso Regression**: Accuracy: 75.29%, TPR: 39.56%, FPR: 9.63%.
- **Ridge Regression**: Accuracy: 75.23%, TPR: 39.01%, FPR: 9.48%.

**Hyperparameter Tuning**:
- Ranger: Tuned `mtry` (5-22), `num.trees` (100-2000).
- Decision Trees: Tuned `cp` (0.0001-0.001), `maxdepth` (5-10).
- Lasso/Ridge: Grid search for `lambda` (10^-7 to 10^7).

**Evaluation Metrics**:
- Accuracy, TPR, FPR, ROC curves, and learning curves.
- Optimized cutoff values to balance TPR and FPR (<10%).

### Libraries
- R libraries: `tidyverse`, `caret`, `dplyr`, `pROC`, `Metrics`, `mlr`, `ggplot2`, `plotly`, `randomForest`, `glmnet`, `tidytext`, `ranger`.

## Setup Instructions

### Prerequisites
- R (version 4.0 or higher).
- RStudio (recommended).
- Install required libraries:
  ```R
  install.packages(c("tidyverse", "caret", "dplyr", "pROC", "Metrics", "mlr", "ggplot2", "plotly", "randomForest", "glmnet", "tidytext", "ranger"))
  ```

### Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yash-makadia/Predicting-Perfect-Rating-Scores-for-Airbnb-Listings.git
   cd Predicting-Perfect-Rating-Scores-for-Airbnb-Listings
   ```
2. **Download the Dataset**:
   - Access the dataset from [Google Drive](https://drive.google.com/drive/folders/0B9w6UZ00foOlfkhMNElianZ1bXhTd3RRN2dUNkE0VC13aHl0SUY0eUxTMEFaVzhEV3RObWs?resourcekey=0-TFPomCnJaUus_S_ZpA2zew&usp=sharing).
   - Place the dataset in the repository root or update the file path in `airbnb_rating_prediction.R`.
3. **Run the Code**:
   - Open `airbnb_rating_prediction.R` in RStudio.
   - Update the dataset path in the script.
   - Run the script to preprocess data, engineer features, train models, and evaluate results.

## Key Findings

- **Ranger Random Forest** outperformed other models, achieving 76.79% accuracy and a low FPR (8.6%).
- **Influential Features**:
  - **Price and Fees**: Listings with cleaning fees average $163.44 vs. $119.90 without, impacting perceived quality.
  - **Availability**: Unique properties (e.g., treehouses) have higher availability, while apartments have lower due to demand.
  - **Host Responsiveness**: 66.5% of hosts respond to all inquiries, correlating with higher ratings.
  - **Cancellation Policy**: Strict policies (most common) have lower prices ($120) vs. flexible policies ($180).
  - **Location**: 80% of listings have exact locations, preferred by travelers for planning.
- **Market Insights**: New York (35,000 listings) and Los Angeles (22,000) dominate, while niche markets (e.g., North Carolina Mountains) have fewer listings.

## Impact and Recommendations

- **For Hosts**: Adjust pricing, enhance responsiveness, and offer flexible cancellation policies to boost perfect rating chances.
- **For Airbnb**: Use model insights to recommend listing improvements, enhancing guest satisfaction.
- **Actionable Insights**:
  - mikor competitive pricing within property categories.
  - Ensure timely host responses to inquiries.
  - Provide exact location details for better trip planning.

## Project Files

- `airbnb_rating_prediction.R`: R script for data preprocessing, feature engineering, modeling, and evaluation.
- `docs/Airbnb_Listing_Report.pdf`: Comprehensive project report detailing methodology, findings, and conclusions.
- `LICENSE`: GNU General Public License v3.0.

## Course Information

- **Course**: BUDT 758T: Data Mining and Predictive Analytics
- **Professor**: Jessica Clark
- **Semester**: Spring 2023
- **Institution**: Robert H. Smith School of Business, University of Maryland, College Park

## Challenges and Lessons Learned

- **External Data**: Integrating zip code income data didn’t improve accuracy, highlighting the importance of feature relevance.
- **Text Mining**: Amenities text data didn’t enhance TPR/FPR, requiring careful feature selection.
- **Feature Engineering**: Multiple iterations were needed to identify impactful features, emphasizing trial-and-error.
- **Key Takeaways**:
  - Thorough data preprocessing (e.g., handling NAs) is critical for model reliability.
  - Feature selection reduces overfitting and improves interpretability.
  - Comparing multiple models ensures optimal performance.

## Future Scope

- Explore advanced models (e.g., GBMs, SVMs, deep learning).
- Apply time-series analysis for future rating predictions.
- Segment users by demographics for personalized models.
- Deploy the model as a predictive service for real-time use.

## References

- [Airbnb Dataset](https://drive.google.com/drive/folders/0B9w6UZ00foOlfkhMNElianZ1bXhTd3RRN2dUNkE0VC13aHl0SUY0eUxTMEFaVzhEV3RObWs?resourcekey=0-TFPomCnJaUus_S_ZpA2zew&usp=sharing)
- R Documentation: [ranger](https://cran.r-project.org/web/packages/ranger/), [glmnet](https://cran.r-project.org/web/packages/glmnet/), [rpart](https://cran.r-project.org/web/packages/rpart/)

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please fork the repository, create a new branch, and submit a pull request with your changes. Ensure compliance with the GPL-3.0 license.

## Contact

For questions or feedback, please open an issue on GitHub or contact me at [yashmakadia1908@gmail.com](mailto:yashmakadia1908@gmail.com).

## Acknowledgments

Special thanks to my team for their dedication and collaborative spirit. I express gratitude to Professor Jessica Clark for her guidance and support throughout BUDT 758T.
