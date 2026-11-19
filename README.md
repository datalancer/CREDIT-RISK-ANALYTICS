22.12% of borrowers in a 30,000-customer credit card portfolio defaulted—and 58.5% of those defaults came from a single risk segment. 💳📊

Watch the quick walkthrough above to see how my end-to-end Power BI Credit Risk & Default Analytics Dashboard uncovers delinquency patterns, tracks 6-month risk escalation, and isolates high-risk borrower segments in real time.

4 Key Takeaways from the Portfolio (N = 30,000):
1️⃣ High-Risk Concentration: Out of 6,636 total defaulters, 3,880 (58.5%) fall into the High Risk tier—where default rates cross 45% across both female (45.2%) and male (47.7%) cardholders.
2️⃣ The Repayment Gap: Average monthly statement bills (44.98K) are nearly 8.5x higher than average monthly repayments (5.28K), highlighting growing revolving balance pressure.
3️⃣ Delinquency Escalation: Between April and September 2005, overall monthly delinquency more than doubled from ~10% to >22%, with High Risk delinquency surging past 60% by September.
4️⃣ AI Root-Cause Drilldown: Using Power BI's Decomposition Tree, High Risk → Female → University emerges as the largest single volume cluster of defaults (1,133 accounts).

How It Was Built:
🔹 Star Schema Modeling: Normalized 6 months of wide billing, payment, and status columns in Power Query into a clean Customers (1:*) Monthly_History model (180K longitudinal rows).
🔹 DAX & Conditional Formatting: Built custom risk tiers, longitudinal delinquency rates, a 3-color heatmap Matrix benchmarked against the 22.12% portfolio average, and a bookmark-powered RESET filter rail.

📂 Explore the .pbix file, DAX formulas, screenshots, and full demo video on GitHub: [Insert GitHub Repo Link]

What feature do you think adds the most clarity for executive stakeholders—the conditional heatmap matrix or the interactive AI decomposition tree? 👇

#PowerBI #DataAnalytics #CreditRisk #BusinessIntelligence #DAX #DataVisualization #FinTech #PortfolioProject
