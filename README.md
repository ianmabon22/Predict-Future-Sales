# **Predict-Future-Sales**

## **Basic Information**  
**Group Members and Emails:**  
- Sean Vaghedi: seanvaghedi15@gwu.edu  
- Yejin Han: yhan214h@gwu.edu  
- Tyler Nguyen: tylernguyen@gwu.edu  
- Ian Mabon: ianmabon@gwu.edu  

**Date:** 12/09/2024  

**Model Version:** 1.0  

**License:**  
Apache 2.0 License  

---


# Data Dictionary for train_sales.csv

| **Column Name**     | **Modeling Role** | **Measurement Level** | **Description**                                                                 |
|----------------------|-------------------|------------------------|---------------------------------------------------------------------------------|
| `date`              | Input            | Nominal               | The date of the transaction, formatted as DD.MM.YYYY.                          |
| `date_block_num`    | Input            | Ordinal               | A continuous month identifier, where each number represents a unique month.    |
| `shop_id`           | Input            | Nominal               | The unique identifier for the shop where the transaction occurred.             |
| `item_id`           | Input            | Nominal               | The unique identifier for the item being sold.                                 |
| `item_price`        | Input            | Continuous            | The price of the item at the time of the transaction.                          |
| `item_cnt_day`      | Target           | Continuous            | The number of items sold on that day (can be negative for returns).            |

## **Intended Use**  
Educational Purposes**  

### **Intended Users**  
Students and people who are working with Machine Learning.  

### **Out-of-Scope Uses**  
Everything that’s not educational use.  

---

## **Training Data**

### **Source of Training Data**  
The `sales_train.csv` file is the training dataset. It includes daily sales data from January 2013 to October 2015. This data was downloaded from Kaggle's "Predict Future Sales" competition, created by the user *Inversion*.  

The test data is split at 7% of the training data.  

### **Number of Rows in Training and Validation Data**  
- **Training Rows**: 2,348,679  
- **Test Rows**: 214,200  

---

## **Model Details**

This model was built referencing two notebooks:  
1. [Jagan Gupta](https://www.kaggle.com/code/jagangupta/time-series-basics-exploring-traditional-ts/notebook)  
2. [Ashioya Jotham](https://www.kaggle.com/code/ashioyajotham/predict-future-sales#Time-Series-Analysis)  

### **Features Used in the Final Model**  
- Input columns: `shop_id`, `item_id`, `date`, and `item_cnt_month`.  
- Target column: `item_cnt_month`.  

### **Model Type**  
- ARIMA (Autoregressive Integrated Moving Average) model.  

### **Software Used**  
- Python with libraries: `pandas`, `sklearn`, `statsmodels`, `seaborn`, and `numpy`.  

### **Software Versions**  
- Python: 3.12.4  
- NumPy: 1.26.4  
- Pandas: 2.2.2  
- Seaborn: 0.13.2  

### **Hyperparameters**  
ARIMA model parameters and model periods.  

---

## **Quantitative Analysis**

### **Metrics to Evaluate Model Performance**  
- **Training RMSE**: 3.048607  
- **Validation RMSE**: 2.35458  
- **Test RMSE**: 1.17645  

The training RMSE was calculated using months 0 to 32 while the validation RMSE was calculated using month 33.
The test RMSE is very low because the submission file for the Kaggle competition was a 3 month average of each shop/item pair instead of individual predictions with the ARIMA model we created.

> **Note:**  
> - The code for individual predictions exists on the model, but it is commented out due to the processing load on our computers’ CPU
> - If we had better computers, the submission file would reflect the ARIMA model built.
> - The model predicts total monthly sales up to six months after the last date given in the training data.
> - The training data was explored using descriptive statistical methods and tested for stationarity.
> - Once found to be stationary, the predictive ARIMA model was built using stat models.
> - RMSE was calculated by code created by ChatGPT. 

---

## **Ethical Considerations**

### **Potential Negative Impacts**  
1. **Math or Software Problems:**  
- Errors in the ARIMA model, like incorrect assumptions of stationarity or parameter selection, can lead to misleading results.
- Coding errors in preprocessing, splitting the data, or implementing the ARIMA model may push inaccuracies.
- The computational limitations of hardware may result in suboptimal model performance or inaccurate predictions.

2. **Real-World Risks:**
- If the model is repurposed for real-world business decisions, incorrect predictions can lead to inventory mismanagement, financial losses, or incorrect/flawed decisions.
- One may misunderstand the limitations of the dataset, such as its restricted scope, leading to general or invalid conclusions.
- The exclusion of test data columns (date, item_price, item_cnt_day) limits the model's ability to understand pricing factors, potentially making its general reliability worse.
- Different applications, for example, using the model for policy decisions or long-term forecasts could cause users to face unexpected risks.
- If users do not fully understand the data’s limitations, they may apply the model to markets or industries where it won’t be suitable, showing its predictive weaknesses.

3. **Potential Uncertainties:**
- The model’s use of past data assumes that those sales trends will be consistent, which might not be true in a changing, real-world sales environment.
- Incorrect evaluation of the model’s stationarity or misinterpretation of validation metrics may indirectly deceive users into believing the model is more accurate than it is.
- The potential for bias in the training data might produce unequal predictions that favor certain locations etc.

4. **Describe any unexpected or results:**
- The model produced followed the downward trend of the sales data, leading to static and low sales compared to a few years earlier which is expected.

# Descriptive Statistics and Forecast

Heatmap

<img width="675" alt="Screenshot 2024-12-06 at 4 47 11 PM" src="https://github.com/user-attachments/assets/59680f80-9a15-41bd-a69c-546cbb44d901">

Histogram of Columns

<img width="675" alt="Screenshot 2024-12-06 at 4 47 36 PM" src="https://github.com/user-attachments/assets/f48ed5a7-73fa-41b7-b421-67f265233fe4">

Total Sales

<img width="673" alt="Screenshot 2024-12-06 at 4 48 08 PM" src="https://github.com/user-attachments/assets/5959b9a3-8ca4-48f4-a48a-7dc4f7a5064e">

Items per Category

<img width="359" alt="Screenshot 2024-12-06 at 4 48 28 PM" src="https://github.com/user-attachments/assets/b9573632-931b-4598-9e6b-ce28e70ad059">

Items per Shop

<img width="662" alt="Screenshot 2024-12-06 at 4 48 51 PM" src="https://github.com/user-attachments/assets/e9ac4408-1f60-4e98-b15b-6743028ed601">

Trends and Residuals

<img width="322" alt="Screenshot 2024-12-06 at 4 49 35 PM" src="https://github.com/user-attachments/assets/52c4eeb0-f3a1-4d59-aa13-0b27d91f8ae7">

De-Trend

<img width="677" alt="Screenshot 2024-12-06 at 4 50 09 PM" src="https://github.com/user-attachments/assets/0c7ef970-e884-487d-a3c6-a28f24cae89d">

De-Seasonalization

<img width="677" alt="Screenshot 2024-12-06 at 4 50 22 PM" src="https://github.com/user-attachments/assets/a4362305-3701-473e-aedc-6d7d9d58455a">

Residuals and KDE

<img width="298" alt="Screenshot 2024-12-06 at 4 50 56 PM" src="https://github.com/user-attachments/assets/2e2c0907-b747-4703-8105-edaeef1b96fc">

Sales Forecast

<img width="669" alt="Screenshot 2024-12-06 at 4 51 19 PM" src="https://github.com/user-attachments/assets/6c034e10-b14a-428b-bf01-63991dcd0560">


