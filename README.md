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

![image](https://github.com/user-attachments/assets/eba1aed4-32ad-44bf-9c3a-490f7e150be0)

**Figure 1: Modified Cornish-Fisher VaR Analysis Across 48 Industry Portfolios**

The Modified Cornish-Fisher VaR analysis reveals substantial heterogeneity in tail risk exposure across industry portfolios. The energy and commodity sectors demonstrate the highest risk profiles, with Coal exhibiting extreme tail risk at 22.99% VaR, reflecting the pronounced volatility and cyclical sensitivity inherent in commodity markets. Energy-related industries (Coal, Oil, Mining) consistently rank among the highest-risk categories, indicating systematic exposure to economic cycles and commodity price volatility.

Conversely, defensive sectors exhibit superior risk characteristics: Food (6.26%), Beer (6.27%), and Utilities (7.06%) demonstrate the lowest VaR values, validating their classification as defensive investments during periods of market stress. Consumer staples and regulated utilities provide natural portfolio diversification benefits through their stable demand characteristics and reduced correlation with economic cycles.

Technology and manufacturing sectors display moderate risk levels with significant intra-sector variation. While Computer Technology (8.6%) and Semiconductors (9.7%) exhibit manageable risk profiles, traditional manufacturing industries including Steel, Fabricated Products, and Textiles demonstrate elevated tail risk exceeding 15%. This pattern indicates that knowledge-intensive sectors benefit from reduced physical asset requirements and enhanced operational flexibility compared to capital-intensive traditional industries.

### **Risk-Adjusted Performance Analysis**

![image](https://github.com/user-attachments/assets/928082f2-5719-4300-9df8-8a04b4142500)

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

![image](https://github.com/user-attachments/assets/e39c1c1a-83e5-45ca-aba7-c383be55bf37)
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

