# 📈 Stock Price Predictor using Java

## 📌 Project Overview

The **Stock Price Predictor** is a console-based application developed using Core Java. It analyses historical stock prices, calculates technical indicators and estimates the next stock price using mathematical algorithms.

The application allows users to add multiple stocks, analyse price movements, compare stocks, generate prediction reports and evaluate prediction performance.

This project demonstrates the practical application of Java programming, Object-Oriented Programming (OOP), data structures and mathematical techniques in financial data analysis.

## 🎯 Objectives

- Analyse historical stock price data.
- Calculate technical indicators to understand stock trends.
- Estimate future stock prices using linear regression.
- Compare the performance of different stocks.
- Generate stock analysis and prediction reports.
- Demonstrate Core Java and OOP concepts through a practical application.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Java | Main programming language |
| Core Java | Application development and logic |
| OOP | Organizing stock information using classes and objects |
| ArrayList | Dynamic storage of stock data |
| Scanner | Accepting user input |
| Mathematical Algorithms | Stock analysis and price prediction |
| Linear Regression | Calculating the historical price trend |

**Note:** The current version uses manually entered historical prices. It does not use a live stock market API, external SQL database, separate backend or trained machine learning model.

## ✨ Features

1. **Load Stock Data:** Enter stock names and historical prices.
2. **Technical Indicators:** Calculate SMA, EMA, momentum and trend slope.
3. **Predict Next Price:** Estimate the next stock price using linear regression slope.
4. **Show Price History:** Display previously entered stock prices.
5. **Prediction Score:** Evaluate a prediction against a held-out historical price.
6. **Forecast Report:** Generate prediction reports for available stocks.
7. **Display All Stocks:** View all stored stock records.
8. **Calculate Price Change:** Calculate absolute and percentage price changes.
9. **Compare Two Stocks:** Compare stock prices and trends.
10. **Delete Stock Data:** Remove stored stock records.

## 📊 Algorithms Used

### 1. Simple Moving Average (SMA)

Calculates the average of a specified number of recent stock prices.

Formula:

SMA = Sum of selected prices / Number of prices

### 2. Exponential Moving Average (EMA)

Gives greater importance to recent stock prices.

Formula:

EMA = (Current Price - Previous EMA) × k + Previous EMA

Where:

k = 2 / (Period + 1)

### 3. Momentum

Measures the difference between the current price and an earlier price.

Formula:

Momentum = Current Price - Previous Price

### 4. Linear Regression Slope

Calculates the overall direction of historical stock prices using a best-fit straight line.

The next price is estimated using:

Predicted Price = Latest Price + Calculated Slope

**Note:** This is a basic mathematical forecasting approach and does not guarantee actual future market prices.

## ☕ Java Concepts Implemented

- Classes and Objects
- Constructors
- Encapsulation through class-based data organization
- Static variables and methods
- ArrayList 
- Scanner for user input
- Methods and modular programming
- For loops and do-while loops
- If-else statements
- Switch-case statements
- String handling
- Input validation

## ⚙️ Requirements

- Java Development Kit (JDK 8 or above)
- Any Java IDE or text editor (VS Code, IntelliJ IDEA, Eclipse)
- Command Prompt or Terminal

## 🚀 How to Run the Project

### Step 1: Clone the repository

```bash
git clone https://github.com/surendra-3112/Java-Programs.git
```

### Step 2: Open the project folder

Navigate to the directory containing `stockpricepredictor.java`.

### Step 3: Compile the program

```bash
javac stockpricepredictor.java
```

### Step 4: Run the program

```bash
java stockpricepredictor
```

**Note:** The public class name and Java filename must match exactly. If you rename the public class to `StockPricePredictor`, rename the file and use `java StockPricePredictor` to run it.

## 🖥️ Application Workflow

1. Run the Java application.
2. Select an operation from the menu.
3. Enter the stock name.
4. Provide historical stock prices.
5. Select technical analysis or prediction.
6. View the calculated indicators and predicted price.
7. Generate reports or compare stocks.

## 🔮 Future Enhancements

- Integrate real-time stock market APIs.
- Implement Machine Learning models using Python and Scikit-learn.
- Integrate MySQL for permanent data storage.
- Develop a graphical user interface or web dashboard.
- Implement advanced forecasting algorithms such as Random Forest and LSTM.
- Use historical datasets for more comprehensive model evaluation.

## 📚 Learning Outcomes

Through this project, I gained practical experience in:

- Applying Core Java concepts to a real-world problem.
- Implementing Object-Oriented Programming.
- Working with dynamic data structures.
- Developing mathematical algorithms.
- Understanding basic stock market technical analysis.
- Building a menu-driven Java application.

## 👨‍💻 Author

**Surendra**

GitHub: https://github.com/surendra-3112

---

⭐ If you find this project interesting, consider giving the repository a star!

**Disclaimer:** This project is developed for educational purposes only. Stock price predictions are estimates based on historical data and should not be considered financial or investment advice.
