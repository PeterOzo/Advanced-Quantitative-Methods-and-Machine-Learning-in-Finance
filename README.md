# Advanced-Quantitative-Methods-and-Machine-Learning-in-Finance
Portfolio Risk Analysis &amp; Optimization



# Advanced Portfolio Risk Analysis & Optimization
*FIN 666 - Advanced Quantitative Methods and Machine Learning in Finance*

## **Problem Statement**
The financial industry faces significant challenges in accurately measuring and managing portfolio risk, particularly when dealing with non-normal return distributions. Traditional risk measures like standard deviation and normal VaR often fail to capture tail risks and extreme market events. The challenge is to develop comprehensive risk assessment models that account for higher-order moments (skewness and kurtosis) while optimizing portfolio allocation for maximum risk-adjusted returns across multiple industry sectors.

## **Abstract**
This project implements advanced quantitative finance techniques to analyze portfolio risk and optimize asset allocation using the Fama-French 48 Industry Portfolios dataset. The analysis employs the Cornish-Fisher expansion for Value-at-Risk (VaR) calculations, Sharpe ratio optimization, Conditional Value-at-Risk (CVaR) modeling, and efficient frontier construction. The study spans 312 monthly observations from January 1990 onwards, providing insights into industry-specific risk characteristics and optimal portfolio construction strategies.

## **Dataset Description**
The dataset contains monthly value-weighted returns for 48 industry portfolios as classified by the Fama-French research methodology. Each industry represents a distinct sector of the U.S. equity market, including Agriculture, Food, Technology, Healthcare, Finance, and Energy sectors. The data includes:
- **Time Period**: January 1990 to December 2016 (312 monthly observations)
- **Industries**: 48 distinct industry classifications
- **Return Format**: Monthly percentage returns converted to decimal format
- **Data Source**: Kenneth French's Data Library at Dartmouth College

**Industry Categories Include:**
Agriculture, Food, Beverages, Tobacco, Toys, Entertainment, Healthcare, Medical Equipment, Pharmaceuticals, Chemicals, Textiles, Construction, Steel, Machinery, Electronics, Automotive, Aerospace, Mining, Energy, Utilities, Telecommunications, Business Services, Technology, Banking, Insurance, Real Estate, and more.

## **Data Analysis**

### **Data Preprocessing**
The project involves comprehensive data preprocessing steps including:
- Loading and formatting the Fama-French 48 Industry Portfolios CSV file
- Converting percentage returns to decimal format (dividing by 100)
- Parsing date indices and filtering data from January 1990 onwards
- Cleaning column names by removing trailing spaces
- Handling missing values and ensuring data consistency

### **Statistical Analysis**
Comprehensive statistical analysis is performed including:
- **Descriptive Statistics**: Mean, standard deviation, skewness, and kurtosis calculations
- **Rolling Window Analysis**: 120-month (10-year) rolling calculations for moment estimation
- **Higher-Order Moments**: Third and fourth moment calculations for distribution analysis
- **Correlation Analysis**: Cross-sectional correlation matrices for portfolio construction

![image](https://github.com/user-attachments/assets/d90467c0-7da8-4d12-8735-bff7070e5cf8)

The Modified Cornish-Fisher VaR analysis above reveals significant heterogeneity in tail risk exposure across the 48 industry portfolios. Coal emerges as the highest-risk sector with a VaR of approximately 23%, reflecting the extreme volatility and cyclical nature of commodity markets. Energy-related industries (Coal, Oil, Mines) consistently rank among the highest-risk categories, indicating sector-specific vulnerability to economic cycles and commodity price shocks.
In contrast, defensive sectors demonstrate superior risk profiles: Food (6.3%), Beer (6.3%), and Utilities (7.1%) exhibit the lowest VaR values, confirming their reputation as safe-haven investments during market stress. The consumer staples and utilities sectors provide natural portfolio diversification benefits due to their stable demand characteristics and lower correlation with economic cycles.
Technology and manufacturing sectors show moderate risk levels, with notable variations: while Computers and Chips display manageable risk (8.6% and 9.7% respectively), traditional manufacturing industries like Steel, Fabricated Products, and Textiles exhibit elevated tail risk exceeding 15%. This pattern suggests that new economy sectors benefit from lower physical asset intensity and higher adaptability compared to capital-intensive traditional industries.
The wide dispersion of VaR values (ranging from 6.3% to 23%) validates the importance of sector diversification in portfolio construction and highlights the critical need for industry-specific risk management approaches in institutional investment strategies.

### **Key Observations:**

**Risk Distribution Patterns:**
- **High-Risk Industries**: Coal (22.99% VaR), Textiles (16.21% VaR), and Fabricated Products (17.29% VaR) show the highest tail risk exposure
- **Low-Risk Industries**: Food (6.26% VaR), Beer (6.27% VaR), and Utilities (7.06% VaR) demonstrate conservative risk profiles
- **Skewness Patterns**: Most industries exhibit negative skewness, indicating left-tail risk, with notable exceptions in Agriculture (0.51) and Textiles (0.49)
- **Kurtosis Analysis**: Real Estate shows extreme kurtosis (17.20), indicating fat-tail distributions and higher probability of extreme events

![image](https://github.com/user-attachments/assets/928082f2-5719-4300-9df8-8a04b4142500)


**Risk-Adjusted Performance Insights:**
- **Top Performers**: Meals (0.656), Guns (0.628), and Medical Equipment (0.600) achieve the highest risk-adjusted returns
- **Underperformers**: Toys (-0.018), Gold (0.002), and Other (0.050) show poor risk-adjusted performance
- **Sector Patterns**: Consumer staples and healthcare sectors generally outperform cyclical industries on a risk-adjusted basis

### **Interpretation:**
The analysis reveals distinct risk-return characteristics across industry sectors:

**Market Segmentation**: Clear differentiation between defensive sectors (utilities, food, healthcare) and cyclical sectors (mining, steel, automotive) in terms of risk exposure and return patterns.

**Tail Risk Concentration**: Certain industries (Coal, Real Estate, Textiles) exhibit extreme tail risk characteristics, requiring specialized risk management approaches.

**Diversification Benefits**: The varying correlation structures across industries provide significant opportunities for portfolio diversification and risk reduction.

## **Machine Learning & Optimization Models**

### **Cornish-Fisher VaR Model**
A sophisticated VaR calculation method that adjusts for non-normal return distributions:
```python
z_cf = z + (z**2 - 1)*s/6 + (z**3 - 3*z)*(k-3)/24 - (2*z**3 - 5*z)*(s**2)/36
var_cf = -1 * (ret[-120:].mean() + z_cf * ret[-120:].std())
```

### **Portfolio Optimization Framework**
Implementation of Modern Portfolio Theory with:
- **Minimum Variance Portfolio**: Analytical solution for optimal weights
- **Efficient Frontier Construction**: Risk-return optimization across portfolio combinations
- **Sharpe Ratio Maximization**: Risk-adjusted return optimization

### **Conditional Value-at-Risk (CVaR)**
Advanced tail risk measurement calculating expected shortfall beyond VaR thresholds:
```python
isbeyond = ret < (ones * var_cf * -1)
cvar = ret[isbeyond].mean()
```

## **Results and Interpretation**

### **Portfolio Optimization Results**
**Minimum Variance Portfolio (Food & Beer)**:
- **Optimal Allocation**: 60% Food, 40% Beer
- **Expected Return**: 7.59% annually
- **Portfolio Volatility**: 12.84% annually
- **Sharpe Ratio**: 0.584

![image](https://github.com/user-attachments/assets/e39c1c1a-83e5-45ca-aba7-c383be55bf37)

The attached plot illustrates the Efficient Frontier Analysis for two selected industries, Food and Beer, using annualized returns and volatilities. The blue curve represents the efficient frontier, which consists of various portfolios created by adjusting the weight combinations of the two assets in increments of 0.10, ranging from fully investing in one asset to the other. The x-axis denotes portfolio volatility (risk), while the y-axis represents the expected return. Each point on the curve corresponds to a different portfolio composition of Food and Beer.
The red star marks the minimum-variance portfolio (MVP), which is the portfolio with the lowest volatility, offering the most efficient balance between return and risk. This MVP is characterized by specific weights assigned to Food and Beer, along with its portfolio return and volatility. Investors seeking to minimize risk exposure while maintaining reasonable returns would prefer the minimum-variance portfolio, as it provides the optimal risk-return tradeoff for a two-asset portfolio.


### **Risk Metrics Summary**
| **Metric** | **Best Performer** | **Value** | **Worst Performer** | **Value** |
|------------|-------------------|-----------|---------------------|-----------|
| **95% VaR** | Other | 6.26% | Coal | 22.99% |
| **Sharpe Ratio** | Meals | 0.656 | Toys | -0.018 |
| **CVaR** | Food | -8.70% | Coal | -29.16% |
| **Annualized Return** | Ships | 14.00% | Toys | 2.55% |
| **Volatility** | Food | 13.52% | Coal | 47.48% |

### **Model Performance Evaluation**
- **VaR Model Accuracy**: Cornish-Fisher adjustment provides superior tail risk estimation compared to normal VaR
- **Portfolio Efficiency**: Minimum variance portfolio achieves optimal risk-return balance with 58.4% excess return per unit of risk
- **Diversification Impact**: Two-asset portfolio reduces volatility by 15.2% compared to weighted average of individual assets

## **Setup and Run**

### **Dependencies Installation**
```bash
pip install pandas numpy scipy matplotlib seaborn scikit-learn
```

### **Data Preprocessing**
1. **Load Dataset**: Import Fama-French 48 Industry Portfolios data
2. **Format Returns**: Convert percentage returns to decimal format
3. **Date Parsing**: Set up proper datetime indexing for time series analysis
4. **Data Cleaning**: Remove trailing spaces and handle missing values

### **Risk Analysis Execution**
1. **VaR Calculation**: Run Cornish-Fisher VaR analysis with rolling 120-month windows
2. **Sharpe Ratio Computation**: Calculate annualized risk-adjusted returns for all industries
3. **CVaR Analysis**: Compute conditional value-at-risk for tail risk assessment

### **Portfolio Optimization**
1. **Efficient Frontier**: Generate risk-return combinations for two-asset portfolios
2. **Minimum Variance Portfolio**: Calculate optimal weights using analytical solutions
3. **Performance Evaluation**: Assess portfolio metrics and risk-adjusted returns

### **Results Visualization**
- Generate comprehensive bar charts for VaR comparisons across industries
- Create Sharpe ratio performance rankings with sector analysis
- Plot efficient frontier curves with minimum variance portfolio highlighting
- Export results to CSV files for further analysis and reporting

**Clone the repository and follow the structured analysis pipeline for comprehensive portfolio risk assessment and optimization.**
