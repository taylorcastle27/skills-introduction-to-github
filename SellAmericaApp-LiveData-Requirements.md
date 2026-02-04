# SellAmericaApp Live Data Requirements

This document outlines the detailed plan to make the SellAmericaApp work with live data using specified sources, including identifying data brokers and potential costs.

---

## Step 1: Assess Available APIs and Data Integrations

### 1. Federal Reserve Economic Data (FRED)
- **API**: Investigate the FRED API provided by the Federal Reserve Bank of St. Louis.
  - Authentication: Requires free API key registration.
  - Endpoints of interest: Currency signals, interest rate data, and economic indicators.
  - **Costs**: Free.
  - **Next Step**: Read the developer documentation to identify required endpoints (e.g., DXY proxies, yield curve dynamics).

### 2. Treasury International Capital (TIC) System
- **Access**: TIC data is entirely free and published monthly.
- **Format**: Review available information and formats (CSV/Excel) on the U.S. Treasury website.
- **Challenges**: Slight data lag as TIC is updated on a delayed basis (~1 month).
- **Next Step**: Analyze historical data for integration and set up workflows for monthly updates.

### 3. Bloomberg/Reuters Market Data
- **Access**: Both platforms provide comprehensive market data including DXY movements, Treasury yields, ETF flows, and more.
- **Costs**: Requires professional subscription.
  - Bloomberg Terminal: ~$24,000/year.
  - Reuters Eikon: Similar pricing.
  - **Next Step**: Evaluate if costs are justified or look for lower-cost proxies from platforms like Alpha Vantage, Quandl, or Yahoo Finance APIs (some free, others with tiered pricing).

### 4. CFTC Commitments of Traders Reports
- **Access**: Free, available online.
- **Challenges**: Provided weekly in CSV format with no direct API.
- **Next Step**: Automate parsing and processing of CSV files into the system.

### 5. World Gold Council Data
- **Access**: Check the availability of live gold prices and historical trends.
- **Costs**: World Gold Council may require membership or purchase for comprehensive data. Other alternatives include free APIs like GoldAPI or paid platforms such as Xignite for better reliability.
- **Next Step**: Compare free versus premium gold price sources based on requirements.

### 6. News APIs for Sentiment Analysis
- **Access**: Use sentiment analysis APIs from providers like:
  - Google News API or ContextualWebNews API (free/low-cost tiers for searching headlines).
  - Advanced sentiment solutions like Aylien, AWS Comprehend, or Microsoft Azure (paid).
- **Costs**: 
  - Aylien: ~$99/month for baseline features.
  - Azure/AWS: Pay-per-request (~$1 to $3 per 1,000 API calls).
- **Next Step**: Trial multiple APIs for sentiment accuracy and integration flexibility.

---

## Step 2: Mock Data Analysis and Transition Plan

### 1. Create Mock Data
- Populate `/data` directory with realistic timestamps and values.
- Include proxies and explain missing data with a "Limitations" section.

### 2. Develop an API Wrapper
- Centralized fetch module to interface with live APIs.
  - Example: `fetchFREDData`, `fetchGoldPrice`.

### 3. Test and Validate with Static Data
- Test mock datasets for algorithm accuracy.
- Validate scoring logic (e.g., Signal Strength: 0-100).

---

## Step 3: Broker and Subscription Evaluation

### 1. Compare Alternatives
- For Bloomberg/Reuters costs, consider partial substitutes like:
  - Alpha Vantage: Free/basic, $75/month for premium.
  - Quandl: Free/basic, $50-$300/month for premium datasets.
  - Yahoo Finance API: Free tier available.
- World Gold Council's premium data can be replaced with GoldAPI (~$10/month as a start).

### 2. Contact Major Brokers
- Reach out to Bloomberg/Reuters teams for custom packages.
- Establish partnerships, potentially lowering subscription tiers for smaller data pulls.

### 3. Use Open Data Sources for Core Needs
- Consolidate free avenues (FRED, TIC, CFTC).

---

## Step 4: Build the System for Live Data

### 1. Implement Caching
- Use FastAPI routes to cache fetched data for frequently updated APIs.
- Setup refresh intervals based on:
  - High-frequency: Currency movements (every few minutes via free APIs).
  - Low-frequency: TIC reports (~monthly).

### 2. Design Limitations Messaging
- Provide disclaimers where proxies are used instead of actual data.

### 3. UI Integrations
- Update charts and dashboard components with live data layers.
- Add "Data Freshness" and "Data Limitations" badges where required.

---

## Step 5: Budget and Timeline

### 1. Initial Costs
- Free sources (FRED/TIC/CFTC) setup: $0.
- Additional sources:
  - GoldAPI or similar: ~$10-$30/month.
  - Sentiment analysis APIs: Trial->Premium (~$99+).

### 2. Timeline
- Week 1: Research APIs and subscriptions.
- Weeks 2-3: Mock data setup; facilitate fetching scripts.
- Week 4: Test systems; detect gaps for refinements.
- Week 5+: Fully implement, integrate feedback.

---

By following these steps, it is feasible to achieve full live data integration for the "SellAmericaApp" while keeping budget considerations in check.
