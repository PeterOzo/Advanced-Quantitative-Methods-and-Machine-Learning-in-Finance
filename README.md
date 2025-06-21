# Advanced Portfolio Risk Analysis & Optimization
*FIN 666 - Advanced Quantitative Methods and Machine Learning in Finance*

## **Problem Statement**

The financial industry confronts substantial challenges in accurately measuring and managing portfolio risk, particularly when dealing with non-normal return distributions that characterize real market conditions. Traditional risk measures such as standard deviation and parametric Value-at-Risk (VaR) often inadequately capture tail risks and extreme market events, leading to systematic underestimation of downside exposure. This research addresses the critical need to develop comprehensive risk assessment frameworks that incorporate higher-order moments (skewness and kurtosis) while simultaneously optimizing portfolio allocation strategies to maximize risk-adjusted returns across diverse industry sectors.

## **Abstract**

This study implements advanced quantitative finance methodologies to conduct comprehensive portfolio risk analysis and asset allocation optimization using the Fama-French 48 Industry Portfolios dataset. The research employs sophisticated techniques including the Cornish-Fisher expansion for enhanced Value-at-Risk calculations, comprehensive Sharpe ratio analysis, Conditional Value-at-Risk (CVaR) modeling, and efficient frontier construction. The empirical analysis spans 312 monthly observations from January 1990 through December 2016, providing robust insights into industry-specific risk characteristics and optimal portfolio construction strategies for institutional investment management.

## **Dataset Description**

The dataset comprises monthly value-weighted returns for 48 industry portfolios classified according to the Fama-French research methodology. Each portfolio represents a distinct sector of the U.S. equity market, encompassing the full spectrum of economic activities including Agriculture, Consumer Products, Technology, Healthcare, Financial Services, and Energy sectors.

**Dataset Specifications:**
- **Temporal Coverage**: January 1990 to December 2016 (312 monthly observations)
- **Cross-sectional Dimension**: 48 industry classifications
- **Return Measurement**: Monthly value-weighted portfolio returns
- **Data Format**: Decimal returns (converted from percentage format)
- **Primary Source**: Kenneth R. French Data Library, Dartmouth College

**Industry Classification Framework:**
The comprehensive industry categories include Agriculture, Food Products, Beverages, Tobacco, Toys & Recreation, Entertainment, Healthcare Services, Medical Equipment, Pharmaceuticals, Chemicals, Textiles, Construction Materials, Steel Works, Machinery, Electronic Equipment, Automotive, Aerospace & Defense, Mining, Petroleum & Natural Gas, Utilities, Telecommunications, Personal Services, Business Services, Computer Technology, Banking, Insurance, Real Estate, Diversified Financials, and Other Industries.

## **Methodology & Data Analysis**

### **Data Preprocessing Protocol**

The research employs rigorous data preprocessing procedures to ensure analytical integrity:
- Systematic loading and validation of the Fama-French 48 Industry Portfolios dataset
- Conversion of percentage returns to decimal format for computational consistency
- Temporal indexing with monthly period frequency starting January 1990
- Column name standardization through whitespace removal
- Comprehensive missing value assessment and data quality verification

### **Statistical Analysis Framework**

The study implements comprehensive statistical analysis encompassing:
- **Distributional Analysis**: Computation of first through fourth moments (mean, variance, skewness, kurtosis)
- **Rolling Window Estimation**: 120-month (10-year) rolling calculations for dynamic moment estimation
- **Higher-Order Moment Analysis**: Third and fourth moment calculations for non-normality assessment
- **Cross-sectional Correlation Structure**: Pairwise correlation matrices for diversification analysis

### **Risk Measurement Results**

![Modified Cornish-Fisher VaR Analysis](image-placeholder)

**Figure 1: Modified Cornish-Fisher VaR Analysis Across 48 Industry Portfolios**

The Modified Cornish-Fisher VaR analysis reveals substantial heterogeneity in tail risk exposure across industry portfolios. The energy and commodity sectors demonstrate the highest risk profiles, with Coal exhibiting extreme tail risk at 22.99% VaR, reflecting the pronounced volatility and cyclical sensitivity inherent in commodity markets. Energy-related industries (Coal, Oil, Mining) consistently rank among the highest-risk categories, indicating systematic exposure to economic cycles and commodity price volatility.

Conversely, defensive sectors exhibit superior risk characteristics: Food (6.26%), Beer (6.27%), and Utilities (7.06%) demonstrate the lowest VaR values, validating their classification as defensive investments during periods of market stress. Consumer staples and regulated utilities provide natural portfolio diversification benefits through their stable demand characteristics and reduced correlation with economic cycles.

Technology and manufacturing sectors display moderate risk levels with significant intra-sector variation. While Computer Technology (8.6%) and Semiconductors (9.7%) exhibit manageable risk profiles, traditional manufacturing industries including Steel, Fabricated Products, and Textiles demonstrate elevated tail risk exceeding 15%. This pattern indicates that knowledge-intensive sectors benefit from reduced physical asset requirements and enhanced operational flexibility compared to capital-intensive traditional industries.

### **Risk-Adjusted Performance Analysis**

![Sharpe Ratio Comparison](image-placeholder)

**Figure 2: Sharpe Ratio Analysis Across Industry Portfolios**

The Sharpe ratio analysis identifies Meals & Restaurants (0.656) and Medical Equipment (0.600) as superior performers on a risk-adjusted basis, demonstrating exceptional ability to generate excess returns relative to volatility. These sectors benefit from consistent demand patterns and defensive business models that generate stable cash flows across varying economic conditions.

Consumer staples sectors exhibit strong risk-adjusted performance: Food Products, Beer & Liquor, and Retail Trade achieve Sharpe ratios exceeding 0.40, confirming that necessity-based industries provide optimal risk-return profiles for long-term institutional investors. The healthcare sector cluster (Medical Equipment, Pharmaceuticals, Healthcare Services) consistently ranks in the upper performance quartile, reflecting the sector's growth dynamics combined with earnings stability.

Commodity-dependent sectors demonstrate poor risk-adjusted performance: Toys & Recreation (-0.018), Gold (0.002), and Coal (0.062) exhibit inadequate compensation for their elevated volatility. The negative Sharpe ratio for Toys indicates that investors would have achieved superior outcomes holding risk-free Treasury securities.

Technology sectors present mixed performance outcomes: Computer Hardware (0.177) and Semiconductors (0.292) achieve moderate risk-adjusted returns but underperform defensive sectors, suggesting that technology premiums may not fully compensate for sector-specific volatility during the study period.

### **Key Empirical Findings**

**Risk Distribution Characteristics:**
- **Extreme Risk Sectors**: Coal (22.99% VaR), Textiles (16.21% VaR), Fabricated Products (17.29% VaR)
- **Conservative Risk Profiles**: Food (6.26% VaR), Beer (6.27% VaR), Utilities (7.06% VaR)
- **Distributional Asymmetry**: Prevalent negative skewness indicating left-tail risk concentration
- **Tail Risk Concentration**: Real Estate exhibits extreme kurtosis (17.20), signaling fat-tail distributions

**Performance Attribution Analysis:**
- **Superior Risk-Adjusted Returns**: Meals (0.656), Defense (0.628), Medical Equipment (0.600)
- **Suboptimal Performance**: Toys (-0.018), Precious Metals (0.002), Other Industries (0.050)
- **Sector Performance Patterns**: Consumer staples and healthcare outperform cyclical industries

## **Quantitative Models & Implementation**

### **Enhanced Value-at-Risk Methodology**

The study implements the Cornish-Fisher expansion to adjust standard normal quantiles for non-normal return distributions:

```python
# Cornish-Fisher VaR Calculation
z_cf = z + (z**2 - 1)*s/6 + (z**3 - 3*z)*(k-3)/24 - (2*z**3 - 5*z)*(s**2)/36
var_cf = -1 * (ret[-120:].mean() + z_cf * ret[-120:].std())
```

This methodology provides superior tail risk estimation by incorporating skewness and kurtosis adjustments to the standard normal distribution assumption.

### **Portfolio Optimization Framework**

The research implements Modern Portfolio Theory extensions including:
- **Minimum Variance Portfolio**: Analytical optimization for risk minimization
- **Efficient Frontier Construction**: Systematic risk-return optimization
- **Sharpe Ratio Maximization**: Risk-adjusted return optimization

### **Conditional Value-at-Risk Implementation**

Advanced tail risk measurement capturing expected losses beyond VaR thresholds:

```python
# CVaR Calculation
isbeyond = ret < (ones * var_cf * -1)
cvar = ret[isbeyond].mean()
```

## **Portfolio Optimization Results**

### **Efficient Frontier Analysis**

![Efficient Frontier Construction](image-placeholder)

**Figure 3: Efficient Frontier for Food & Beer Portfolio**

The efficient frontier analysis for the Food and Beer industry portfolio demonstrates fundamental Modern Portfolio Theory principles through well-defined risk-return relationships. The minimum variance portfolio (highlighted in red) achieves optimal risk reduction at 12.84% annualized volatility with 7.59% expected return, corresponding to the analytically derived 60% Food / 40% Beer allocation that minimizes portfolio risk through diversification.

The characteristic hyperbolic frontier shape illustrates diminishing marginal returns to risk-taking: progression from the minimum variance point toward higher expected returns necessitates disproportionately larger volatility increases. This relationship validates the fundamental risk-return trade-off confronting portfolio managers.

Diversification effectiveness is quantified through the minimum variance portfolio's 15.2% volatility reduction compared to the weighted average of constituent assets. The moderate correlation structure between Food and Beer industries (ρ = 0.25) enables substantial risk reduction while preserving reasonable expected returns.

**Optimal Portfolio Characteristics:**
- **Asset Allocation**: 60% Food Industries, 40% Beer & Liquor
- **Expected Annual Return**: 7.59%
- **Portfolio Volatility**: 12.84%
- **Sharpe Ratio**: 0.584
- **Diversification Benefit**: 15.2% volatility reduction

### **Comprehensive Risk Metrics**

| **Performance Metric** | **Best Performer** | **Value** | **Worst Performer** | **Value** |
|------------------------|-------------------|-----------|---------------------|-----------|
| **95% VaR** | Other Industries | 6.26% | Coal | 22.99% |
| **Sharpe Ratio** | Meals & Restaurants | 0.656 | Toys & Recreation | -0.018 |
| **CVaR (Expected Shortfall)** | Food Products | -8.70% | Coal | -29.16% |
| **Annualized Return** | Shipping Containers | 14.00% | Toys & Recreation | 2.55% |
| **Annualized Volatility** | Food Products | 13.52% | Coal | 47.48% |

## **Implementation Guide**

### **Technical Requirements**

```bash
# Required Dependencies
pip install pandas numpy scipy matplotlib seaborn scikit-learn
```

### **Analytical Workflow**

**Phase 1: Data Preparation**
1. Import Fama-French 48 Industry Portfolios dataset
2. Execute return format conversion and temporal filtering
3. Implement datetime indexing for time series analysis
4. Conduct data quality assessment and validation

**Phase 2: Risk Analysis**
1. Calculate Cornish-Fisher VaR with 120-month rolling windows
2. Compute comprehensive Sharpe ratio analysis across all industries
3. Implement CVaR calculations for tail risk assessment
4. Generate cross-sectional risk metric comparisons

**Phase 3: Portfolio Optimization**
1. Construct efficient frontiers for selected industry pairs
2. Derive minimum variance portfolio solutions analytically
3. Evaluate portfolio performance metrics and risk characteristics
4. Conduct sensitivity analysis for alternative correlation assumptions

**Phase 4: Results Documentation**
1. Generate comprehensive visualization suite for risk metrics
2. Create detailed performance attribution analysis
3. Export quantitative results for further analysis
4. Prepare executive summary with investment implications

## **Research Contributions & Investment Implications**

This research provides several significant contributions to portfolio risk management:

**Methodological Advances**: Implementation of the Cornish-Fisher expansion for VaR calculations provides more accurate tail risk assessment compared to traditional parametric methods, particularly for non-normal return distributions prevalent in financial markets.

**Sector-Specific Insights**: Comprehensive analysis across 48 industry portfolios reveals distinct risk-return characteristics, enabling more informed sector allocation decisions for institutional portfolio managers.

**Practical Applications**: The efficient frontier analysis provides actionable insights for portfolio construction, demonstrating quantifiable diversification benefits and optimal allocation strategies for risk-conscious investors.

**Risk Management Framework**: The integration of VaR, CVaR, and Sharpe ratio analysis provides a comprehensive risk assessment framework suitable for institutional investment management and regulatory capital requirements.

## **Conclusion**

This study demonstrates the critical importance of employing sophisticated risk measurement techniques that account for the non-normal characteristics of financial return distributions. The Cornish-Fisher VaR methodology provides superior tail risk assessment, while the comprehensive Sharpe ratio analysis reveals significant performance disparities across industry sectors. The portfolio optimization results confirm substantial benefits from diversification, particularly for defensive sector combinations that offer attractive risk-adjusted returns for institutional investors.

---

*This research represents advanced application of quantitative finance methodologies to real-world investment management challenges, providing practical insights for institutional portfolio construction and risk management strategies.*
























## Portfolio Risk Analysis &amp; Optimization

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

![image](https://github.com/user-attachments/assets/eba1aed4-32ad-44bf-9c3a-490f7e150be0)


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

The Sharpe ratio analysis above reveals Meals (0.656) and Medical Equipment (0.600) as the top-performing sectors on a risk-adjusted basis, demonstrating their ability to generate superior excess returns relative to volatility. These sectors benefit from consistent demand patterns and defensive characteristics that provide stable cash flows across economic cycles.
Consumer staples sectors dominate the upper performance tiers: Food, Beer, and Retail all achieve Sharpe ratios above 0.40, confirming that necessity-based industries offer optimal risk-return profiles for long-term investors. The healthcare cluster (Medical Equipment, Drugs, Healthcare) consistently ranks in the top quartile, reflecting the sector's growth potential combined with relatively stable earnings.
Notable underperformers include commodity-dependent sectors: Toys (-0.018), Gold (0.002), and Coal (0.062) exhibit poor risk-adjusted returns, indicating that high volatility in these industries is not adequately compensated by excess returns. The negative Sharpe ratio for Toys suggests investors would have been better served holding risk-free assets.
Technology sectors show mixed performance: while Computers (0.177) and Chips (0.292) demonstrate moderate risk-adjusted returns, they lag behind defensive sectors, suggesting that innovation premiums may not fully offset technology sector volatility during the study period.
The inverse relationship between VaR and Sharpe ratios is evident, where industries with moderate risk exposure (10-15% VaR) tend to achieve the highest risk-adjusted returns, validating the importance of balanced risk-taking in portfolio optimization.

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

The efficient frontier for the Food and Beer portfolio demonstrates classic Modern Portfolio Theory principles with a well-defined risk-return trade-off. The minimum variance portfolio (red star) achieves optimal risk reduction at 12.84% volatility with a 7.59% expected return, representing the 60% Food / 40% Beer allocation that minimizes portfolio risk through diversification benefits.
The hyperbolic shape of the efficient frontier illustrates diminishing marginal returns to risk-taking: moving from the minimum variance point toward higher expected returns requires disproportionately larger increases in volatility. This characteristic curve validates that investors face an increasingly steep risk-return trade-off as they pursue higher portfolio returns.
Diversification effectiveness is clearly demonstrated as the minimum variance portfolio achieves 15.2% volatility reduction compared to a simple weighted average of the individual assets. The correlation structure between Food and Beer industries (ρ = 0.25 based on the covariance analysis) enables substantial risk reduction while maintaining reasonable expected returns.
Portfolio implications: Risk-averse investors should target allocations near the minimum variance point, while those seeking higher returns must accept exponentially increasing volatility. The Sharpe ratio of 0.584 for the minimum variance portfolio suggests this conservative allocation provides attractive risk-adjusted returns, making it suitable for defensive portfolio strategies and risk-conscious institutional investors.
The smooth, continuous frontier confirms that intermediate portfolio combinations offer superior risk-return profiles compared to corner solutions of 100% allocation to either asset.RetryClaude can make mistakes. Please double-check responses.


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
