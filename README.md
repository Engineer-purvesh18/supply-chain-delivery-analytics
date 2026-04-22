# 🚚 Supply Chain Delivery Analytics

An end-to-end data analytics and machine learning project analyzing delivery performance, profitability, and late delivery risk across a global e-commerce supply chain.

---

## 📌 Business Problem

A global e-commerce company operating across multiple regions manages end-to-end order fulfillment for **sporting goods**. The company faces inconsistent delivery performance — actual shipping times frequently deviate from scheduled timelines, leading to:

- High rates of **late deliveries**
- Unpredictable **order profitability**
- Poor customer experience across regions

This project aims to identify the root causes of delivery delays, quantify their business impact, and build a predictive model for late delivery risk.

---

## 📁 Project Structure

```
supply-chain-delivery-analytics/
│
├── DataCoSupplyChainDataset.csv        # Raw dataset (~180k orders)
├── DescriptionDataCoSupplyChain.csv    # Column descriptions and metadata
├── main.ipynb                          # Main analysis notebook
└── README.md
```

---

## 📊 Dataset Overview

The dataset contains **53 features** covering the full order lifecycle — from customer and product info to shipping and delivery outcomes.

| Category | Key Columns |
|---|---|
| **Order Info** | Order ID, Order Status, Order Date, Order Region, Market |
| **Customer Info** | Customer Segment, Customer Country, Customer City |
| **Product Info** | Product Name, Category Name, Department Name, Product Price |
| **Shipping** | Shipping Mode, Days for Shipping (Real), Days for Shipment (Scheduled) |
| **Delivery** | Delivery Status, Late Delivery Risk |
| **Financials** | Sales, Benefit per Order, Order Profit Per Order, Order Item Profit Ratio |

> **Delivery Status values:** Advance Shipping, Late Delivery, Shipping Canceled, Shipping On Time  
> **Shipping Modes:** Standard Class, First Class, Second Class, Same Day  
> **Markets covered:** Africa, Europe, LATAM, Pacific Asia, USCA

---

## 🔍 Analysis Workflow

### 1. Exploratory Data Analysis (EDA)
- Dataset shape, duplicate check, and missing value audit
- Value counts for low-cardinality categorical columns
- Distribution overview of key numeric features

### 2. Feature Engineering
New features derived from raw data:
- **Order Processing Time** — actual days from order to shipment
- **Delay** — difference between actual processing time and scheduled shipment days
- **Is_Delayed** — boolean flag for delayed orders
- **Profitability Flag** — classifies orders as Profit / Loss / Break-even
- **Temporal features** — `order_month`, `order_day`, `order_hour`

### 3. Business KPIs
Key metrics computed:
- Total Orders & Late Deliveries
- On-Time Delivery %
- Late Delivery %
- 90th Percentile Delay (days)
- Total Profit

### 4. Profitability vs Delivery Time
- Mean and total profit broken down by delay days
- Delay distribution (%) across the order base

### 5. Bottleneck Detection
Delay % analyzed across 6 dimensions:
- Order Region
- Customer Segment
- Shipping Mode
- Order Status
- Transaction Type
- Department Name

### 6. Root Cause Analysis
- Top delay drivers identified per region
- Multi-factor breakdown by shipping mode, customer segment, department, and order status

### 7. Time-Based Analysis
- Delay % trend by **Month**
- Delay % trend by **Day of Week**
- Delay % trend by **Hour of Day**

---

## 🤖 Machine Learning Model

**Objective:** Predict whether an order will be a late delivery (`Late_delivery_risk`)

### Features Used
```
Type, Days for shipment (scheduled), Category Name,
Customer Segment, Department Name, Order Region,
Shipping Mode, order_month, order_hour
```

### Pipeline
| Step | Detail |
|---|---|
| Encoding | Frequency encoding for categorical variables |
| Train/Test Split | Stratified split |
| Class Imbalance | SMOTE oversampling on training data |
| Model | Random Forest Classifier |
| Evaluation | Accuracy, Precision, Recall, F1, Classification Report |

---

## 🛠️ Tech Stack

- **Python 3**
- **pandas** — data manipulation
- **numpy** — numerical operations
- **matplotlib / seaborn** — data visualization
- **scikit-learn** — machine learning (Random Forest, train/test split, metrics)
- **imbalanced-learn** — SMOTE for handling class imbalance

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/Engineer-purvesh18/supply-chain-delivery-analytics.git
cd supply-chain-delivery-analytics
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
```

### 3. Run the notebook
```bash
jupyter notebook main.ipynb
```


---

## 📈 Key Insights

- A significant portion of orders are delivered **late**, with Late delivery being the dominant delivery status
- **Standard Class** shipping mode is the biggest contributor to delays
- Delay rates vary considerably across **Order Regions**, revealing geographic bottlenecks
- **Order profitability is negatively correlated** with delivery delay
- The **Random Forest model** achieves strong predictive performance for late delivery risk after SMOTE balancing

---

## 📄 Data Source

The dataset used is the **DataCo Smart Supply Chain Dataset**, which simulates real-world e-commerce supply chain data including order, customer, product, and shipping information.

