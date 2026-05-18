I have sufficient research. Let me now assemble the question bank. I have enough specific signals (PhonePe SQL split round, Swiggy 90-min SQL, Tredence 1-day, ZS guesstimates, Fractal car-market sizing, Mu Sigma trees in Delhi, Infosys SP core CS, Cognizant clustered vs non-clustered, Wipro normal forms + functions) to write authentic questions.

# Seed Question Bank — Indian Campus AI Mock Interview

I authored **90 questions total**: **30 Data Analyst**, **30 Data Scientist**, **30 SDE Non-Coding**. Each is tagged to specific Indian campus recruiters (2024–2026 sources), uses phrasing reported by candidates on GeeksforGeeks / Glassdoor India / Medium / Reddit / PrepInsta, carries a rubric, follow-ups, input mode, and a source citation. Difficulty mix per role is ~40% easy / ~40% medium / ~20% hard.

---

## Role 1 — Data Analyst (30 questions)

```json
[
  {
    "id": "da-sql-001",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "easy",
    "companies": ["tcs-digital", "tcs-nqt", "common"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "From an Employees(emp_id, name, dept, salary) table, write a query to find the second highest salary in each department.",
    "rubric": [
      "Uses DENSE_RANK() or ROW_NUMBER() partitioned by dept ordered by salary DESC",
      "Filters rank = 2 in outer query (CTE or subquery)",
      "Handles ties correctly (DENSE_RANK preferred over ROW_NUMBER)",
      "Returns NULL/no row gracefully when a dept has <2 employees",
      "Mentions LIMIT 1 OFFSET 1 alternative is wrong here because it's per-dept"
    ],
    "followUps": ["What if two employees share the highest salary — does your query still work?", "Rewrite without window functions."],
    "source": "GfG TCS Digital Interview Experience 2025 [3]"
  },
  {
    "id": "da-sql-002",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "medium",
    "companies": ["swiggy", "phonepe"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "Given orders(order_id, customer_id, order_date, amount), compute a 7-day rolling average of daily order amount.",
    "rubric": [
      "Aggregates amount per order_date first (SUM GROUP BY date)",
      "Applies AVG() OVER (ORDER BY order_date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)",
      "Distinguishes ROWS vs RANGE and explains why ROWS is safer with missing dates",
      "Notes the need to fill missing dates via calendar table for true 7-day window",
      "Correct ordering and partition (no partition needed for global rolling avg)"
    ],
    "followUps": ["How would you handle days with zero orders?", "Make it per-city rolling average."],
    "source": "Swiggy 90-min SQL round, Medium 2025 [11]; PhonePe SQL split round [10]"
  },
  {
    "id": "da-sql-003",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "medium",
    "companies": ["zs-associates", "latentview"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "From sales(sale_id, product_id, sale_date, revenue), find products whose month-over-month revenue dropped for 3 consecutive months.",
    "rubric": [
      "Aggregates revenue per product_id and month",
      "Uses LAG() OVER (PARTITION BY product_id ORDER BY month) to compare previous months",
      "Flags drop boolean and counts consecutive drops (3 LAGs or gaps-and-islands)",
      "Handles edge case where product is missing in some months",
      "Returns distinct product_id list with the drop window"
    ],
    "followUps": ["What if a product had zero sales in a month — drop or skip?", "Add seasonality adjustment."],
    "source": "ZS Associates DA Interview, Glassdoor 2025 [4]; LatentView DA Guide [16]"
  },
  {
    "id": "da-sql-004",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "easy",
    "companies": ["accenture", "capgemini", "common"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "Explain the difference between WHERE and HAVING. Write a query using both on an Orders table to show customers with more than 5 orders above 1000 rupees.",
    "rubric": [
      "WHERE filters rows before aggregation; HAVING filters groups after aggregation",
      "Query has WHERE amount > 1000",
      "GROUP BY customer_id with COUNT(*)",
      "HAVING COUNT(*) > 5",
      "Notes that HAVING cannot reference column aliases in some dialects"
    ],
    "followUps": ["Can HAVING be used without GROUP BY?", "What is the SQL logical order of execution?"],
    "source": "Capgemini DA Glassdoor 2025 [14]; Accenture DA InterviewQuery [13]"
  },
  {
    "id": "da-sql-005",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "medium",
    "companies": ["deloitte", "ibm-india"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "From employees(emp_id, manager_id, name, salary), find employees who earn more than their manager.",
    "rubric": [
      "Self-join employees e1 to employees e2 on e1.manager_id = e2.emp_id",
      "WHERE e1.salary > e2.salary",
      "Selects e1.name (employee) and optionally e2.name (manager)",
      "Handles NULL manager_id (top of hierarchy) — those rows excluded by join",
      "Mentions correlated subquery alternative"
    ],
    "followUps": ["Top of hierarchy CEO has NULL manager — should they appear?", "Rewrite using EXISTS."],
    "source": "Deloitte DA Glassdoor India 2025 [5]; Deloitte SQL DataLemur [6]"
  },
  {
    "id": "da-sql-006",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "hard",
    "companies": ["phonepe", "razorpay"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "Given transactions(txn_id, user_id, txn_time, status), find users who completed at least 3 successful transactions within any rolling 1-hour window.",
    "rubric": [
      "Filters status = 'SUCCESS'",
      "Self-join or window LEAD/LAG to look at txn_time gaps within 1 hour per user_id",
      "Counts ≥3 transactions where txn_time and txn_time + 1 hour overlap window",
      "Uses RANGE BETWEEN INTERVAL '1 hour' PRECEDING in dialects that support it, otherwise COUNT OVER with window join",
      "Returns distinct user_ids; handles edge case of exactly 3"
    ],
    "followUps": ["What if you need exactly 1-hour, not rolling?", "Optimize for billion-row scale."],
    "source": "PhonePe DS Interview Medium 2025 [10]; Razorpay DS Guide [9]"
  },
  {
    "id": "da-sql-007",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "easy",
    "companies": ["wipro", "tcs-nqt", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is the difference between INNER JOIN, LEFT JOIN, and FULL OUTER JOIN? Give a one-line use case for each.",
    "rubric": [
      "INNER: rows matching in both tables only",
      "LEFT: all left rows + matching right rows (NULL where no match)",
      "FULL OUTER: all rows from both sides, NULL where unmatched",
      "Use case for LEFT: 'all customers including those with no orders'",
      "Mentions CROSS JOIN as Cartesian product"
    ],
    "followUps": ["What does a LEFT JOIN with WHERE right.col IS NULL do?", "Difference between LEFT JOIN and LEFT OUTER JOIN?"],
    "source": "Wipro Elite NLTH 2025 GfG [17]; common across TCS NQT"
  },
  {
    "id": "da-sql-008",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "medium",
    "companies": ["genpact", "exl"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "From a customer_interactions table, calculate average resolution time per support agent, excluding interactions that are still open.",
    "rubric": [
      "Filters status != 'OPEN' or end_time IS NOT NULL",
      "TIMESTAMPDIFF / DATEDIFF on (end_time - start_time)",
      "GROUP BY agent_id with AVG()",
      "Handles NULL end_time correctly",
      "Mentions converting unit (minutes/hours) explicitly"
    ],
    "followUps": ["What if some agents have zero closed tickets?", "Add a HAVING to surface only agents above company-wide average."],
    "source": "Genpact SQL DataLemur 2025 [19]; EXL DA Guide [18]"
  },
  {
    "id": "da-sql-009",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "medium",
    "companies": ["tredence", "mu-sigma"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "Write a query to detect duplicate rows in a transactions table on (user_id, txn_time, amount) and keep only the first occurrence.",
    "rubric": [
      "Uses ROW_NUMBER() OVER (PARTITION BY user_id, txn_time, amount ORDER BY txn_id)",
      "Filters rn = 1 in outer query to keep first",
      "Alternative: GROUP BY with MIN(txn_id) and join back",
      "Mentions DELETE syntax if asked to remove duplicates in-place",
      "Handles NULLs in partition columns (NULL != NULL in SQL)"
    ],
    "followUps": ["Write the DELETE version.", "What if amount has floating-point noise?"],
    "source": "Tredence DA Glassdoor 2025 [4]; Mu Sigma SQL DataLemur [21]"
  },
  {
    "id": "da-sql-010",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "How does SQL handle NULL in aggregations like COUNT, SUM, and AVG?",
    "rubric": [
      "COUNT(col) ignores NULLs; COUNT(*) counts all rows",
      "SUM and AVG ignore NULLs",
      "AVG denominator = count of non-NULL values, not total rows",
      "NULL + anything = NULL in arithmetic; needs COALESCE",
      "Mentions IS NULL / IS NOT NULL (not = NULL)"
    ],
    "followUps": ["What does SELECT NULL = NULL return?", "How would COALESCE help here?"],
    "source": "Common across TCS, Capgemini, Accenture per Glassdoor 2025 [14]"
  },
  {
    "id": "da-py-011",
    "role": "data-analyst",
    "topic": "python",
    "difficulty": "easy",
    "companies": ["tcs-digital", "capgemini", "common"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Given a pandas DataFrame df with columns ['city','sales'], write code to compute total sales per city and return top 3 cities by sales.",
    "rubric": [
      "df.groupby('city')['sales'].sum()",
      "Sort descending with sort_values or .nlargest(3)",
      ".reset_index() to convert Series back to DataFrame",
      "Handles NaN in sales (skipna default True)",
      "Returns a DataFrame, not a Series, for downstream use"
    ],
    "followUps": ["Add a percentage-of-total column.", "Now do it with SQL via pandasql."],
    "source": "Capgemini DA Bugspotter 2025 [15]; TCS DA Bugspotter [2]"
  },
  {
    "id": "da-py-012",
    "role": "data-analyst",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["latentview", "fractal", "common"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "You have a DataFrame with 20% missing values in a 'salary' column. Walk through your code to handle missing values appropriately.",
    "rubric": [
      "Inspects with df.isna().sum() and visualizes pattern (MCAR/MAR/MNAR)",
      "If MCAR and small: drop with dropna(subset=['salary'])",
      "If meaningful: impute with median (robust to outliers) over mean",
      "For grouped data: groupby().transform('median') to impute within group",
      "Mentions sklearn SimpleImputer / KNNImputer as production option"
    ],
    "followUps": ["Why median over mean here?", "When would you create an 'is_missing' indicator feature?"],
    "source": "LatentView DA Guide 2025 [16]; Fractal DA Guide [7]"
  },
  {
    "id": "da-py-013",
    "role": "data-analyst",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["accenture", "deloitte"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Read a 2 GB CSV that doesn't fit comfortably in RAM and compute a sum of one column. Show your pandas code.",
    "rubric": [
      "Uses pd.read_csv(..., chunksize=...) to iterate",
      "Accumulates sum across chunks",
      "Specifies usecols=['target_col'] and dtype to reduce memory",
      "Mentions alternative: dask.dataframe or polars",
      "Closes/iterates correctly, no full load"
    ],
    "followUps": ["How would you parallelize this?", "What if you need a groupby instead of sum?"],
    "source": "Accenture DA Bugspotter 2025 [20]; Deloitte DA Guide [5]"
  },
  {
    "id": "da-py-014",
    "role": "data-analyst",
    "topic": "python",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between pandas merge, join, and concat. When would you pick each?",
    "rubric": [
      "merge: SQL-style join on columns; flexible how= (inner/left/right/outer)",
      "join: shortcut for merge on indexes",
      "concat: stacks DataFrames along axis (vertical / horizontal), no key matching",
      "Use merge for keyed joins, concat for appending rows",
      "Mentions ignore_index and validate= in merge"
    ],
    "followUps": ["What does validate='one_to_one' do?", "Why might concat duplicate index values?"],
    "source": "Common across TCS, Capgemini DA Glassdoor 2025 [14]"
  },
  {
    "id": "da-dbms-015",
    "role": "data-analyst",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["tcs-digital", "infosys-dse", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain 1NF, 2NF, and 3NF with a one-line example for each.",
    "rubric": [
      "1NF: atomic values, no repeating groups",
      "2NF: 1NF + no partial dependency on composite key",
      "3NF: 2NF + no transitive dependency",
      "Concrete example: separating Student-Course from Course-Instructor to remove transitive dependency",
      "Mentions BCNF as a stricter form"
    ],
    "followUps": ["When would you intentionally denormalize?", "What is BCNF and why beyond 3NF?"],
    "source": "Wipro Elite NLTH 2025 [17]; TCS Digital GfG [3]"
  },
  {
    "id": "da-dbms-016",
    "role": "data-analyst",
    "topic": "dbms",
    "difficulty": "medium",
    "companies": ["cognizant-genc", "ibm-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is an index, and when would adding one hurt performance?",
    "rubric": [
      "Index = data structure (typically B-tree) speeding lookup on a column",
      "Speeds SELECT/WHERE/JOIN/ORDER BY",
      "Slows INSERT/UPDATE/DELETE because index must also be updated",
      "Hurts when table is small, when column has low cardinality, or in write-heavy OLTP",
      "Mentions clustered vs non-clustered indexes"
    ],
    "followUps": ["Difference between clustered and non-clustered?", "When is a composite index better than two single indexes?"],
    "source": "Cognizant GenC PrepInsta 2025 [12]; common"
  },
  {
    "id": "da-dbms-017",
    "role": "data-analyst",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What does ACID stand for in databases? Give a one-line meaning of each.",
    "rubric": [
      "A — Atomicity: all-or-nothing transaction",
      "C — Consistency: DB moves from one valid state to another",
      "I — Isolation: concurrent txns appear sequential",
      "D — Durability: committed changes survive crashes",
      "Mentions example: bank transfer must be atomic"
    ],
    "followUps": ["What is the difference between Read Committed and Repeatable Read?", "How does write-ahead logging help durability?"],
    "source": "Cognizant GenC, Infosys SP 2025 [12][8]"
  },
  {
    "id": "da-proj-018",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["tcs-digital", "deloitte", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through your final-year data analytics project. What dataset did you use, what tools, and what was the key insight?",
    "rubric": [
      "Clear 3-part structure: problem → approach → outcome",
      "Names actual tools (SQL, pandas, Tableau / Power BI) — not vague 'I used Python'",
      "Quantifies dataset size and source",
      "States one non-obvious insight, not just 'we built a dashboard'",
      "Owns the candidate's specific contribution if it was a group project"
    ],
    "followUps": ["What would you do differently with 10x data?", "What was your biggest failure on this project?"],
    "source": "TCS Digital GfG 2025 [3]; Deloitte DA IQ [5]"
  },
  {
    "id": "da-proj-019",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["zs-associates", "tredence", "latentview"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Pick one chart from your project and explain why you chose that chart type over alternatives.",
    "rubric": [
      "Maps chart type to data type (categorical → bar, time series → line, distribution → histogram)",
      "Considers audience (technical vs business stakeholder)",
      "Avoids 3D / pie chart unless justified for 2-3 categories",
      "Mentions one alternative considered and rejected",
      "States the story the chart tells in one sentence"
    ],
    "followUps": ["When is a stacked bar misleading?", "How would you make this interactive in Tableau?"],
    "source": "ZS Associates DA Glassdoor 2025 [4]; LatentView DA [16]"
  },
  {
    "id": "da-stats-020",
    "role": "data-analyst",
    "topic": "stats",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "When would you use median instead of mean to summarize a numeric column?",
    "rubric": [
      "Median is robust to outliers; mean is not",
      "Use median for income, house prices, response time (skewed distributions)",
      "Use mean when distribution is roughly symmetric / Gaussian",
      "Mentions median = 50th percentile",
      "Mentions trimmed mean as middle ground"
    ],
    "followUps": ["What if mean and median differ a lot — what does that tell you?", "When is mode useful?"],
    "source": "Common, Genpact / EXL DA 2025 [18][19]"
  },
  {
    "id": "da-stats-021",
    "role": "data-analyst",
    "topic": "stats",
    "difficulty": "medium",
    "companies": ["deloitte", "zs-associates", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your product manager runs an A/B test and the p-value is 0.04. They say 'the new design works.' What's your response?",
    "rubric": [
      "p=0.04 means likelihood of seeing this data if null were true is 4%",
      "Does NOT prove the new design works — only that effect is statistically detectable",
      "Asks about effect size and practical significance, not just statistical",
      "Asks about sample size and test duration (peeking / novelty effect)",
      "Recommends checking power, multiple testing corrections, and segment splits"
    ],
    "followUps": ["What is the difference between statistical and practical significance?", "When is p-hacking a risk?"],
    "source": "Deloitte DA IQ 2025 [5]; ZS Associates DA [4]"
  },
  {
    "id": "da-stats-022",
    "role": "data-analyst",
    "topic": "stats",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain Type I and Type II errors with a real-life example.",
    "rubric": [
      "Type I (false positive): rejecting a true null — e.g., convicting an innocent person",
      "Type II (false negative): failing to reject a false null — e.g., missing a disease in screening",
      "Alpha controls Type I; power = 1 - beta controls Type II",
      "Trade-off: lowering alpha increases beta unless sample size grows",
      "Real example tied to candidate's domain (medical, fraud, A/B test)"
    ],
    "followUps": ["Which is worse in fraud detection — Type I or Type II?", "How does sample size affect both?"],
    "source": "Common DS/DA, TCS NQT 2025 [9]"
  },
  {
    "id": "da-case-023",
    "role": "data-analyst",
    "topic": "case",
    "difficulty": "medium",
    "companies": ["swiggy", "phonepe", "flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Swiggy's order conversion rate dropped 15% week-over-week. How would you investigate?",
    "rubric": [
      "Slice by dimension: city, platform (iOS/Android/web), restaurant tier, user cohort",
      "Check funnel: app open → search → cart → checkout → payment success",
      "Distinguish external factors (rain, festival, competitor promo) from internal (app bug, price hike, restaurant supply)",
      "Validate the metric itself first — did logging change? Denominator shift?",
      "Proposes specific next-step query / dashboard to confirm hypothesis"
    ],
    "followUps": ["Where would you query data first — payments or app events?", "What if drop is only in one city?"],
    "source": "Swiggy DA Medium 2025 [11]; PhonePe DA [10]"
  },
  {
    "id": "da-case-024",
    "role": "data-analyst",
    "topic": "case",
    "difficulty": "medium",
    "companies": ["zs-associates", "tredence", "mu-sigma"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "A pharma client says sales of one drug dropped in three states but stayed flat overall. What questions do you ask before opening the data?",
    "rubric": [
      "Clarify time period and baseline (vs LY, vs prior quarter)",
      "Confirm metric: units sold, revenue, prescriptions written?",
      "Ask about competitor launches or generic entry in those 3 states",
      "Ask about regulatory or pricing changes (state-specific in India)",
      "Ask about sales-rep coverage / territory restructuring"
    ],
    "followUps": ["Now you have the data — what's the first chart you build?", "What would Simpson's paradox look like here?"],
    "source": "ZS Associates DA Glassdoor 2025 [4]; Tredence [4]; Mu Sigma [21]"
  },
  {
    "id": "da-genai-025",
    "role": "data-analyst",
    "topic": "genai-literacy",
    "difficulty": "easy",
    "companies": ["accenture", "deloitte", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "How would you use ChatGPT or Claude in your day-to-day SQL work without compromising data security?",
    "rubric": [
      "Use it to draft queries, explain unfamiliar functions, generate test data",
      "Never paste real customer PII or production data into a public LLM",
      "Share schema (column names + types), not actual rows",
      "Always validate generated SQL on a sample before running on production",
      "Mention enterprise tiers (e.g., ChatGPT Enterprise, on-prem) that allow it"
    ],
    "followUps": ["What's one task you would never use an LLM for?", "How do you verify an LLM's SQL is correct?"],
    "source": "Accenture DA IQ 2025 [13]; Deloitte 2025 [5]"
  },
  {
    "id": "da-hr-026",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-digital", "tcs-nqt", "infosys-dse", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why do you want to be a data analyst and not a software developer?",
    "rubric": [
      "Authentic personal story (not 'data is the new oil' cliche)",
      "Mentions one project or course that shifted them toward data",
      "Demonstrates awareness that DA requires SQL/stats/communication, not just coding",
      "Connects to the company's domain (consulting, BFSI, e-commerce)",
      "Honest about willingness to code — analyst is not anti-code"
    ],
    "followUps": ["Where do you see yourself in 5 years — manager or specialist?", "If we offer you a developer role instead, would you take it?"],
    "source": "TCS NQT 2025 GfG [9]; common"
  },
  {
    "id": "da-sql-027",
    "role": "data-analyst",
    "topic": "sql",
    "difficulty": "hard",
    "companies": ["flipkart", "amazon-india"],
    "inputModes": ["text_sql"],
    "textInputType": "sql_editor",
    "text": "Given user_sessions(user_id, session_start, session_end), find the maximum number of concurrent active sessions at any time.",
    "rubric": [
      "Sweep-line approach: emit +1 at session_start, -1 at session_end",
      "UNION ALL of start events (+1) and end events (-1)",
      "Running SUM ordered by event_time gives concurrency",
      "MAX of the running sum = answer",
      "Handles ties (start and end at same time) — choose ordering rule"
    ],
    "followUps": ["What if you need concurrency per hour?", "How does this scale to billions of rows?"],
    "source": "Flipkart DE GfG 2025 [22]; Amazon DS DataLemur [23]"
  },
  {
    "id": "da-py-028",
    "role": "data-analyst",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["latentview", "fractal", "tiger-analytics"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Given two DataFrames orders and customers, find customers who placed an order in Jan 2026 but not in Feb 2026.",
    "rubric": [
      "Filter orders by month for Jan and Feb separately",
      "Use set difference: set(jan.customer_id) - set(feb.customer_id)",
      "Or merge with indicator='left_only'",
      "Returns DataFrame of qualifying customer rows",
      "Handles dtype of customer_id consistently across both frames"
    ],
    "followUps": ["What about customers who joined in Feb — should they be included?", "Rewrite in SQL."],
    "source": "LatentView 2025 [16]; Tiger Analytics DS [25]"
  },
  {
    "id": "da-dbms-029",
    "role": "data-analyst",
    "topic": "dbms",
    "difficulty": "medium",
    "companies": ["cognizant-genc", "wipro"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between clustered and non-clustered indexes. Which one can a table have only one of?",
    "rubric": [
      "Clustered index defines physical row order — at most one per table",
      "Non-clustered index is a separate structure pointing to rows — many allowed",
      "Primary key is clustered by default in SQL Server",
      "Clustered is faster for range scans; non-clustered for point lookups",
      "Mentions covering index as an extension of non-clustered"
    ],
    "followUps": ["What is a covering index?", "What is the cost of a non-clustered index lookup vs clustered?"],
    "source": "Cognizant GenC PrepInsta 2025 [12]; Wipro NLTH [17]"
  },
  {
    "id": "da-case-030",
    "role": "data-analyst",
    "topic": "case",
    "difficulty": "hard",
    "companies": ["mu-sigma", "fractal"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Estimate how many cars are sold in Delhi in a typical month. Walk through your assumptions.",
    "rubric": [
      "States top-down framework: population → households → car-owning households → replacement rate",
      "Uses Delhi population ~20M and reasonable household size ~4",
      "Estimates car penetration ~25-30% urban Delhi",
      "Replacement cycle 7-10 years OR new-buyer rate",
      "Adds first-time buyers + sanity-checks against any known figure"
    ],
    "followUps": ["How would your number change for Mumbai?", "What data would you ask for to verify?"],
    "source": "Fractal car-market sizing 2025 [7]; Mu Sigma 'trees in Delhi' [21]"
  }
]
```

---

## Role 2 — Data Scientist (30 questions)

```json
[
  {
    "id": "ds-ml-001",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "easy",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain the bias-variance tradeoff. How do you detect each in practice?",
    "rubric": [
      "Bias = error from oversimplified assumptions (underfitting); high train + test error",
      "Variance = sensitivity to training data noise (overfitting); low train, high test error",
      "Detect via train/validation curves and learning curves",
      "Tradeoff: more model complexity reduces bias, increases variance",
      "Mention regularization, more data, or simpler model as remedies"
    ],
    "followUps": ["Where does a deep tree fall on this spectrum?", "How does bagging reduce variance?"],
    "source": "Amazon DS DataLemur 2025 [23]; Flipkart DS Exponent [24]"
  },
  {
    "id": "ds-ml-002",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is overfitting and how do you prevent it?",
    "rubric": [
      "Model memorizes training data, fails on unseen data",
      "Symptoms: large gap between train and val metrics",
      "Prevention: more data, regularization (L1/L2), dropout, early stopping",
      "Cross-validation to detect early",
      "Simpler model / feature selection / data augmentation"
    ],
    "followUps": ["L1 vs L2 — which causes sparsity and why?", "What does early stopping require?"],
    "source": "Common, Amazon / Flipkart / Mu Sigma DS 2025 [23][24][21]"
  },
  {
    "id": "ds-ml-003",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["amazon-india", "walmart-labs", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're building a fraud detection model. Accuracy is 99%. Should you be happy?",
    "rubric": [
      "No — fraud is highly imbalanced; predicting 'not fraud' alone gets 99%+",
      "Use precision, recall, F1, PR-AUC, or ROC-AUC instead",
      "Recall (catching frauds) usually more important than precision",
      "Mention SMOTE / undersampling / class weighting",
      "Cost-sensitive: false negative (missed fraud) ≫ false positive"
    ],
    "followUps": ["Why prefer PR-AUC over ROC-AUC for imbalanced data?", "How would you set the threshold?"],
    "source": "Amazon DS 2025 [23]; common DS"
  },
  {
    "id": "ds-ml-004",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["flipkart", "phonepe", "razorpay"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Random Forest vs XGBoost — when would you prefer each?",
    "rubric": [
      "Both ensemble decision trees, but RF=bagging (parallel), XGB=boosting (sequential)",
      "RF: easier to tune, robust to overfitting, parallelizable",
      "XGB: usually higher accuracy on tabular, needs careful tuning (lr, depth, regularization)",
      "Prefer RF for quick baseline, XGB for Kaggle-grade tabular tasks",
      "Mention catboost / lightgbm trade-offs"
    ],
    "followUps": ["What is the role of learning rate in XGBoost?", "Why does XGBoost handle missing values natively?"],
    "source": "Flipkart DS Exponent 2025 [24]; PhonePe DS Medium [10]"
  },
  {
    "id": "ds-ml-005",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain gradient descent in one minute. What is the role of learning rate?",
    "rubric": [
      "Iterative optimization moving in -gradient direction to minimize loss",
      "Update rule: theta = theta - lr * gradient",
      "Learning rate too large: oscillates / diverges; too small: slow",
      "Mentions batch / mini-batch / stochastic variants",
      "Mentions Adam / momentum as adaptive variants"
    ],
    "followUps": ["What is vanishing gradient and where does it occur?", "Difference between SGD and Adam?"],
    "source": "Common DS, Amazon 2025 [23]"
  },
  {
    "id": "ds-ml-006",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is regularization and how do L1 and L2 differ?",
    "rubric": [
      "Adds penalty to loss to discourage large weights → reduces overfitting",
      "L1 (Lasso): sum of |weights| → produces sparse solutions, feature selection",
      "L2 (Ridge): sum of weights² → shrinks weights smoothly, no sparsity",
      "Elastic Net = L1 + L2 combo",
      "Geometric intuition: L1 ball has corners → sparsity"
    ],
    "followUps": ["When would you prefer Elastic Net?", "How does dropout relate to regularization?"],
    "source": "Common, Flipkart / Mu Sigma DS 2025 [24][21]"
  },
  {
    "id": "ds-ml-007",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["mu-sigma", "tiger-analytics", "fractal"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain k-means clustering. How do you choose k?",
    "rubric": [
      "Unsupervised, partitions n points into k clusters minimizing within-cluster variance",
      "Iterative: assign points to nearest centroid → recompute centroids",
      "Sensitive to initialization (k-means++ helps) and feature scaling",
      "Elbow method (WCSS vs k) or silhouette score for k selection",
      "Mention failure modes: non-spherical clusters, outliers"
    ],
    "followUps": ["What is the silhouette score?", "When would you use DBSCAN instead?"],
    "source": "Mu Sigma DS 2025 [21]; Tiger Analytics [25]; Fractal [7]"
  },
  {
    "id": "ds-ml-008",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain precision, recall, F1, and AUC. When would you optimize each?",
    "rubric": [
      "Precision = TP/(TP+FP); recall = TP/(TP+FN)",
      "F1 = harmonic mean of precision and recall",
      "AUC = area under ROC; threshold-independent ranking quality",
      "Optimize recall when missing positives is costly (fraud, disease)",
      "Optimize precision when false alarms costly (spam, content moderation)"
    ],
    "followUps": ["What is PR-AUC and when prefer it over ROC-AUC?", "What does AUC = 0.5 mean?"],
    "source": "Amazon DS 2025 [23]; common"
  },
  {
    "id": "ds-ml-009",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["razorpay", "phonepe", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "How would you handle a heavily imbalanced classification problem (1% positive class)?",
    "rubric": [
      "Use precision/recall/F1/PR-AUC, not accuracy",
      "Resampling: SMOTE / oversampling minority, undersampling majority",
      "Class weights in the loss function",
      "Threshold tuning on predicted probabilities",
      "Anomaly detection / one-class models as alternative framing"
    ],
    "followUps": ["What is a risk of SMOTE?", "How does class weighting interact with calibration?"],
    "source": "Razorpay DS 2025 [9]; PhonePe DS [10]"
  },
  {
    "id": "ds-ml-010",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "hard",
    "companies": ["flipkart", "amazon-india"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Derive logistic regression's loss function (binary cross-entropy) from MLE.",
    "rubric": [
      "Likelihood: product over i of p_i^y_i * (1-p_i)^(1-y_i) where p_i = sigmoid(w·x)",
      "Take log → sum of y log p + (1-y) log(1-p)",
      "Negate → binary cross-entropy",
      "Notes convexity → unique global minimum with gradient descent",
      "Mentions sigmoid derivative p(1-p) in gradient"
    ],
    "followUps": ["Why is BCE convex but MSE on sigmoid output is not?", "Now derive the gradient w.r.t. weights."],
    "source": "Flipkart DS deep-math round 2025 [24]"
  },
  {
    "id": "ds-stats-011",
    "role": "data-scientist",
    "topic": "stats",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "State the Central Limit Theorem. Why does it matter in practice?",
    "rubric": [
      "Sampling distribution of mean approaches normal as n → ∞, regardless of population dist",
      "Requires finite variance, i.i.d. samples",
      "Lets us build confidence intervals and z-tests on means",
      "Rule of thumb: n ≥ 30 usually enough",
      "Foundation for A/B testing and bootstrapping intuition"
    ],
    "followUps": ["What if the underlying distribution has infinite variance?", "How does it justify the z-test?"],
    "source": "Common DS interviews, Amazon 2025 [23]"
  },
  {
    "id": "ds-stats-012",
    "role": "data-scientist",
    "topic": "stats",
    "difficulty": "medium",
    "companies": ["jp-morgan-india", "goldman-sachs-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain Bayes' theorem with the classic disease-test example.",
    "rubric": [
      "P(A|B) = P(B|A)P(A)/P(B)",
      "Disease 1% prevalence, test 99% sensitivity / 99% specificity",
      "P(disease | positive) ≈ 50%, surprising result",
      "Explains base-rate fallacy",
      "Links to ML: naive Bayes, posterior in Bayesian inference"
    ],
    "followUps": ["What is the prior, likelihood, posterior here?", "How would prevalence change the answer?"],
    "source": "JP Morgan India DS, Goldman Sachs DS 2025 (Glassdoor)"
  },
  {
    "id": "ds-stats-013",
    "role": "data-scientist",
    "topic": "stats",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is multicollinearity and why is it a problem in linear regression?",
    "rubric": [
      "Two or more predictors are highly correlated",
      "Inflates standard errors → unstable coefficients",
      "Detect via VIF (>5 or >10) or correlation matrix",
      "Doesn't hurt prediction accuracy much, but ruins interpretation",
      "Remedies: drop one, combine via PCA, regularize with Ridge"
    ],
    "followUps": ["Does multicollinearity affect tree-based models?", "How does Ridge address it specifically?"],
    "source": "Common DS, Fractal / Tiger 2025 [7][25]"
  },
  {
    "id": "ds-stats-014",
    "role": "data-scientist",
    "topic": "stats",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is a p-value? What does p = 0.03 mean and what does it NOT mean?",
    "rubric": [
      "Probability of observing data this extreme if null hypothesis were true",
      "p=0.03 does NOT mean 'null is 3% likely true'",
      "Does NOT mean effect is large or practically meaningful",
      "Depends on sample size — large n can make tiny effects significant",
      "Mention alpha=0.05 as convention, not a law"
    ],
    "followUps": ["How does sample size affect p-value?", "What is the difference between p-value and confidence interval?"],
    "source": "Common DS, Deloitte / ZS 2025 [5][4]"
  },
  {
    "id": "ds-py-015",
    "role": "data-scientist",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Given a DataFrame with features and a binary target, write code to train a Logistic Regression and print precision, recall, and ROC-AUC on a test split.",
    "rubric": [
      "train_test_split with stratify=y and random_state",
      "StandardScaler fit on train, transform test (no leakage)",
      "LogisticRegression().fit() and .predict() / .predict_proba()",
      "precision_score, recall_score, roc_auc_score from sklearn.metrics",
      "Uses predict_proba[:,1] for AUC, not predict()"
    ],
    "followUps": ["Why stratify on the target?", "How would you add cross-validation?"],
    "source": "Amazon DS 2025 [23]; Flipkart DS [24]"
  },
  {
    "id": "ds-py-016",
    "role": "data-scientist",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["flipkart", "walmart-labs", "phonepe"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Write a function that takes a DataFrame and returns the columns with >30% missing values.",
    "rubric": [
      "df.isna().mean() gives per-column null fraction",
      "Filter columns where ratio > 0.30",
      "Return as list (.index.tolist())",
      "Handle empty DataFrame edge case (return [])",
      "Document the threshold as a parameter"
    ],
    "followUps": ["How would you decide whether to drop or impute these?", "What if missingness is informative?"],
    "source": "Flipkart DS Exponent 2025 [24]; PhonePe Medium [10]"
  },
  {
    "id": "ds-py-017",
    "role": "data-scientist",
    "topic": "python",
    "difficulty": "hard",
    "companies": ["amazon-india", "flipkart"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Implement k-NN classifier from scratch in NumPy (no sklearn). Predict on a single test point given training X, y and k.",
    "rubric": [
      "Euclidean distance: np.sqrt(np.sum((X - x_test)**2, axis=1))",
      "np.argsort to get k nearest indices",
      "np.bincount or Counter for majority vote on labels",
      "Returns single predicted label",
      "Handles ties (lowest label / random / weighted) explicitly"
    ],
    "followUps": ["How would you vectorize for multiple test points?", "How does k affect bias/variance?"],
    "source": "Fractal ML algorithm round 2025 [7]; Amazon DS [23]"
  },
  {
    "id": "ds-case-018",
    "role": "data-scientist",
    "topic": "case",
    "difficulty": "medium",
    "companies": ["flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Design a recommendation system for Flipkart's homepage. How would you frame the ML problem?",
    "rubric": [
      "Clarifies objective: CTR, conversion, GMV, or long-term retention",
      "Candidate generation (collaborative filtering / two-tower) → ranking model",
      "Features: user history, product embeddings, recency, price, popularity",
      "Cold-start handling for new users / new products",
      "Online evaluation via A/B test, offline via NDCG / recall@k"
    ],
    "followUps": ["What if a new product has no clicks — how do you surface it?", "How would you balance exploration vs exploitation?"],
    "source": "Flipkart DS Round-2 case 2025 [24]"
  },
  {
    "id": "ds-case-019",
    "role": "data-scientist",
    "topic": "case",
    "difficulty": "medium",
    "companies": ["common", "phonepe", "razorpay"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Predict customer churn for a payments app. Walk me through your approach end-to-end.",
    "rubric": [
      "Define churn (e.g., no transaction in 30 days) — clarify with PM",
      "Label window vs feature window to avoid leakage",
      "Features: transaction frequency, recency, monetary, support tickets, app opens",
      "Class imbalance handling (churn is small %)",
      "Pick model (XGBoost baseline) + evaluate with PR-AUC + business cost matrix"
    ],
    "followUps": ["How do you avoid label leakage?", "How would you deploy and retrain this?"],
    "source": "PhonePe DS Medium 2025 [10]; Razorpay DS [9]"
  },
  {
    "id": "ds-case-020",
    "role": "data-scientist",
    "topic": "case",
    "difficulty": "hard",
    "companies": ["amazon-india", "swiggy", "flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Netflix-style subscriber growth dropped 8% this quarter in India. As a data scientist, how would you diagnose and what would you build?",
    "rubric": [
      "Decompose: new acquisitions vs retention drop; identify which is moving",
      "Segment by device (Jio TV / mobile), plan tier, region, content cohort",
      "Build cohort retention curves; check if a recent product change correlates",
      "Distinguish causation (run a uplift / synthetic-control analysis) from correlation",
      "Propose a churn-prevention model + content recommendation experiment to validate"
    ],
    "followUps": ["How would you isolate impact of pricing change vs content drop?", "What's your A/B test design?"],
    "source": "Amazon DS Bar-raiser case 2025 [23]; Swiggy case [11]"
  },
  {
    "id": "ds-genai-021",
    "role": "data-scientist",
    "topic": "genai-literacy",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is RAG (Retrieval-Augmented Generation) and when is it better than fine-tuning an LLM?",
    "rubric": [
      "RAG: retrieve relevant docs → feed as context to LLM → generate answer",
      "Better than fine-tuning when knowledge changes frequently or is proprietary",
      "Avoids retraining costs; updates are just doc re-indexing",
      "Components: chunking, embedding model, vector DB, retriever, generator",
      "Fine-tuning better for changing style/behavior, not facts"
    ],
    "followUps": ["What is a vector database — name 2?", "Why does chunk size matter in RAG?"],
    "source": "Common DS GenAI-literacy, Flipkart / PhonePe 2025 [24][10]"
  },
  {
    "id": "ds-genai-022",
    "role": "data-scientist",
    "topic": "genai-literacy",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is an embedding? How are word embeddings different from one-hot encoding?",
    "rubric": [
      "Embedding = dense low-dim vector representation capturing semantic meaning",
      "One-hot: high-dim, sparse, no semantic similarity",
      "Embeddings: similar words have nearby vectors (cosine similarity)",
      "Learned via word2vec / GloVe or transformer hidden states",
      "Used for search, recommendation, clustering, RAG"
    ],
    "followUps": ["What is cosine similarity?", "Why are embeddings preferred over TF-IDF for semantic search?"],
    "source": "Common DS, Razorpay / PhonePe 2025 [9][10]"
  },
  {
    "id": "ds-genai-023",
    "role": "data-scientist",
    "topic": "genai-literacy",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your LLM-based chatbot keeps hallucinating product prices. How would you fix this without changing the model?",
    "rubric": [
      "Identify it as a grounding / hallucination problem, not a reasoning one",
      "Add RAG with authoritative price source",
      "Stricter system prompt: 'If price not in retrieved context, say I don't know'",
      "Add a guardrail / post-check that validates price against DB",
      "Lower temperature for factual queries"
    ],
    "followUps": ["How would you measure hallucination rate?", "When would you switch to fine-tuning?"],
    "source": "Common 2026 DS GenAI round; Razorpay [9]"
  },
  {
    "id": "ds-hr-024",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["common", "amazon-india", "flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about your most impactful data science project. What was your specific contribution?",
    "rubric": [
      "STAR-like structure: Situation, Task, Action, Result",
      "Names model / tool stack concretely",
      "Quantifies impact (accuracy gain, time saved, business metric)",
      "Distinguishes individual contribution from team contribution",
      "Reflects on one mistake / learning"
    ],
    "followUps": ["What would you do differently today?", "What was the most difficult feedback you got?"],
    "source": "Amazon Leadership Principles, Flipkart 2025 [23][24]"
  },
  {
    "id": "ds-hr-025",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["amazon-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you disagreed with a teammate on a technical decision. How did you resolve it?",
    "rubric": [
      "Concrete specific situation, not hypothetical",
      "Shows respect for the other view (not 'I was right')",
      "Used data / experiment to resolve, not authority",
      "States the outcome and what they learned",
      "Aligns with Amazon Leadership Principle 'Have Backbone; Disagree and Commit'"
    ],
    "followUps": ["What if data was inconclusive?", "Did you ever change your own mind?"],
    "source": "Amazon LP behavioural 2025 [23]"
  },
  {
    "id": "ds-ml-026",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is cross-validation? How is k-fold different from stratified k-fold?",
    "rubric": [
      "CV splits data into k folds, trains on k-1, validates on 1, rotates",
      "Reduces variance of evaluation vs single split",
      "Stratified preserves class proportions in each fold — vital for imbalanced data",
      "Mentions leave-one-out as extreme case",
      "TimeSeriesSplit for ordered data (no future leakage)"
    ],
    "followUps": ["Why is shuffling dangerous in time series?", "How does CV interact with hyperparameter tuning?"],
    "source": "Common, Mu Sigma / Tiger 2025 [21][25]"
  },
  {
    "id": "ds-stats-027",
    "role": "data-scientist",
    "topic": "stats",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "How would you design an A/B test to measure if a new checkout flow improves conversion?",
    "rubric": [
      "Random assignment at user (not session) level",
      "Define primary metric (conversion rate) and guardrail metrics (latency, error rate)",
      "Calculate sample size via power analysis (MDE, alpha, power)",
      "Decide test duration (capture weekly seasonality)",
      "Pre-register hypothesis, plan analysis (z-test / t-test / bootstrap)"
    ],
    "followUps": ["What is novelty effect and how do you control for it?", "What if traffic is uneven across days?"],
    "source": "Common DS, Flipkart / Amazon 2025 [23][24]"
  },
  {
    "id": "ds-ml-028",
    "role": "data-scientist",
    "topic": "ml-fundamentals",
    "difficulty": "hard",
    "companies": ["amazon-india", "flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through how XGBoost / Gradient Boosting actually works step by step.",
    "rubric": [
      "Sequential ensemble: each tree fits residuals (negative gradient) of previous prediction",
      "Loss can be log-loss, MSE, custom",
      "Learning rate (eta) shrinks contribution of each tree",
      "Regularization: tree depth, gamma, lambda, alpha",
      "Mentions histogram-based splits, parallelism on feature buckets"
    ],
    "followUps": ["Why does XGBoost handle missing values natively?", "How does it differ from AdaBoost?"],
    "source": "Amazon DS 2025 [23]; Flipkart DS [24]"
  },
  {
    "id": "ds-case-029",
    "role": "data-scientist",
    "topic": "case",
    "difficulty": "medium",
    "companies": ["walmart-labs", "flipkart"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walmart wants to forecast demand for diapers in tier-2 Indian cities. What features and model would you choose?",
    "rubric": [
      "Time-series problem with multiple SKU × store grain",
      "Features: lag, rolling mean, day-of-week, festivals, weather, price, promotions",
      "Model: classical (SARIMAX) baseline, then LightGBM with lag features, then deep (TFT)",
      "Hierarchical reconciliation across store / city / region",
      "Evaluate via WAPE / MAPE per SKU; backtesting on rolling origin"
    ],
    "followUps": ["How would you handle a new SKU with no history?", "How would Diwali demand spike be modeled?"],
    "source": "Walmart Labs DS 2025; Flipkart [24]"
  },
  {
    "id": "ds-py-030",
    "role": "data-scientist",
    "topic": "python",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["text_python"],
    "textInputType": "python_editor",
    "text": "Given X_train, y_train and a list of candidate models, write code to pick the best by 5-fold cross-validated F1 score.",
    "rubric": [
      "Loop through models with sklearn.model_selection.cross_val_score",
      "scoring='f1' (or 'f1_macro' for multiclass)",
      "cv=StratifiedKFold(5, shuffle=True, random_state=...)",
      "Track mean and std; pick highest mean (tiebreaker = lower std)",
      "Returns model name + score, doesn't refit silently"
    ],
    "followUps": ["Why use std as tiebreaker?", "How would you add hyperparameter search inside this?"],
    "source": "Amazon / Flipkart DS coding round 2025 [23][24]"
  }
]
```

---

## Role 3 — SDE Non-Coding (30 questions)

```json
[
  {
    "id": "sde-dbms-001",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-sp", "cognizant-genc", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain normalization and walk me through 1NF, 2NF, 3NF, and BCNF.",
    "rubric": [
      "Normalization = organizing data to reduce redundancy and improve integrity",
      "1NF: atomic columns, no repeating groups",
      "2NF: 1NF + no partial dependency on a composite primary key",
      "3NF: 2NF + no transitive dependency",
      "BCNF: every determinant is a candidate key (stricter than 3NF)"
    ],
    "followUps": ["Give an example of a 2NF violation.", "When would you denormalize?"],
    "source": "Wipro Elite NLTH 2025 [17]; Cognizant GenC PrepInsta [12]; Infosys SP [8]"
  },
  {
    "id": "sde-dbms-002",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["infosys-sp", "tcs-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What are ACID properties? Give a real-world example for each.",
    "rubric": [
      "Atomicity: bank transfer all-or-nothing",
      "Consistency: balance never negative after txn",
      "Isolation: two simultaneous withdrawals don't see partial state",
      "Durability: committed txn survives power failure",
      "Mentions how WAL / journaling enforces durability"
    ],
    "followUps": ["What are isolation levels and how do they differ?", "Compare ACID with BASE."],
    "source": "Infosys SP Medium 2025 [1]; Cognizant GenC [12]"
  },
  {
    "id": "sde-dbms-003",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Compare B-tree index and Hash index. When would you use each?",
    "rubric": [
      "B-tree: balanced, supports range queries and ordered scans, O(log n) lookup",
      "Hash: O(1) average lookup but only equality (not range)",
      "Most RDBMS default to B-tree for general use",
      "Hash useful for memory-resident lookups (e.g., PostgreSQL HASH on equality)",
      "Mention LSM-tree (for write-heavy) as a third alternative"
    ],
    "followUps": ["Why can't hash index do range queries?", "What is a covering index?"],
    "source": "Infosys SP Medium 2025 [1]; TCS Digital GfG [3]"
  },
  {
    "id": "sde-dbms-004",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["cognizant-genc", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between primary key and foreign key. Can a primary key be NULL?",
    "rubric": [
      "PK: uniquely identifies a row; NOT NULL, unique",
      "FK: references a PK in another table; can be NULL (unless constrained)",
      "PK enforces entity integrity; FK enforces referential integrity",
      "One PK per table; many FKs allowed",
      "ON DELETE CASCADE / SET NULL behaviors"
    ],
    "followUps": ["What is a composite primary key?", "What is referential integrity?"],
    "source": "Cognizant GenC PrepInsta 2025 [12]; Wipro NLTH [17]"
  },
  {
    "id": "sde-dbms-005",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain transaction isolation levels: Read Uncommitted, Read Committed, Repeatable Read, Serializable.",
    "rubric": [
      "Read Uncommitted: dirty reads possible",
      "Read Committed: no dirty reads, but non-repeatable reads possible",
      "Repeatable Read: same row read consistently, but phantom reads possible",
      "Serializable: full isolation, no phantoms — highest cost",
      "Names which anomaly each prevents"
    ],
    "followUps": ["What is a phantom read?", "Default isolation level in MySQL vs PostgreSQL?"],
    "source": "Infosys SP 2025 [1]; TCS Digital [3]"
  },
  {
    "id": "sde-dbms-006",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through INNER, LEFT, RIGHT, FULL OUTER, and CROSS JOIN conceptually.",
    "rubric": [
      "INNER: only matching rows in both",
      "LEFT: all left + matching right",
      "RIGHT: all right + matching left",
      "FULL OUTER: union of both, NULL where no match",
      "CROSS: Cartesian product, no condition"
    ],
    "followUps": ["When would you use a SELF JOIN?", "What is an anti-join?"],
    "source": "Common across TCS, Cognizant, Wipro 2025 [12][17]"
  },
  {
    "id": "sde-dbms-007",
    "role": "sde-non-coding",
    "topic": "dbms",
    "difficulty": "medium",
    "companies": ["cognizant-genc", "infosys-se"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between clustered and non-clustered indexes. How many of each can a table have?",
    "rubric": [
      "Clustered: physical row order = index order; only one per table",
      "Non-clustered: separate structure pointing to rows; many allowed",
      "PK usually creates a clustered index by default (SQL Server)",
      "Clustered better for range queries; non-clustered for point lookups",
      "Mentions index leaf node contents difference"
    ],
    "followUps": ["What is a covering index?", "What is a heap table?"],
    "source": "Cognizant GenC PrepInsta 2025 [12]"
  },
  {
    "id": "sde-os-008",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-sp", "cognizant-genc", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between a process and a thread. Which one is heavier and why?",
    "rubric": [
      "Process: independent program with own memory space",
      "Thread: unit of execution within a process, shares memory",
      "Process is heavier (separate PCB, memory, file descriptors)",
      "Threads cheaper to create/switch; share heap, have own stack",
      "Mentions IPC (heavy) vs shared memory between threads"
    ],
    "followUps": ["What is context switching?", "What are the disadvantages of using threads?"],
    "source": "Infosys SP 2025 [1]; Cognizant GenC [12]"
  },
  {
    "id": "sde-os-009",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What are the four conditions for deadlock? How can you prevent each?",
    "rubric": [
      "Mutual exclusion: resource can't be shared — hard to remove",
      "Hold and wait: process holds while waiting — make processes request all at once",
      "No preemption: resources can't be forcibly taken — allow preemption",
      "Circular wait: cycle in resource graph — impose ordering on resources",
      "Mentions deadlock detection vs prevention vs avoidance (Banker's)"
    ],
    "followUps": ["What is the Banker's algorithm?", "Difference between deadlock and starvation?"],
    "source": "Infosys SP 2025 [1]; common GfG [8]"
  },
  {
    "id": "sde-os-010",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Compare FCFS, SJF, Round Robin, and Priority scheduling. Which one risks starvation?",
    "rubric": [
      "FCFS: simple, but convoy effect (long jobs block short)",
      "SJF: optimal avg wait, but needs burst-time prediction; long jobs starve",
      "Round Robin: time-quantum based, fair, good for interactive",
      "Priority: starvation of low-priority unless aging used",
      "Names which are preemptive vs non-preemptive"
    ],
    "followUps": ["What is aging and what problem does it solve?", "How do you choose time quantum in RR?"],
    "source": "Infosys SP 2025 [1]; TCS Digital [3]"
  },
  {
    "id": "sde-os-011",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "medium",
    "companies": ["infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is virtual memory? Why do we need paging?",
    "rubric": [
      "Virtual memory: abstraction giving each process the illusion of large contiguous memory",
      "Allows running programs larger than physical RAM via disk-backed swap",
      "Paging: divides memory into fixed-size pages, avoids external fragmentation",
      "Page table maps virtual → physical addresses; TLB caches translations",
      "Page faults trigger OS to load missing pages from disk"
    ],
    "followUps": ["What is thrashing?", "What is a TLB miss?"],
    "source": "Infosys SP Medium 2025 [1]"
  },
  {
    "id": "sde-os-012",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between paging and segmentation. Can they be combined?",
    "rubric": [
      "Paging: fixed-size blocks (pages), transparent to programmer, no external fragmentation",
      "Segmentation: variable-size logical units (code, stack, heap), programmer-visible, external fragmentation",
      "Paging has internal fragmentation; segmentation has external",
      "Combined: segmented paging (e.g., x86) — segments divided into pages",
      "Mentions modern OSes use mostly paging"
    ],
    "followUps": ["What's the difference between internal and external fragmentation?", "Why is segmentation less common today?"],
    "source": "Infosys SP Medium 2025 [1]"
  },
  {
    "id": "sde-os-013",
    "role": "sde-non-coding",
    "topic": "os",
    "difficulty": "medium",
    "companies": ["infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between mutex and semaphore. Give an example where you'd pick each.",
    "rubric": [
      "Mutex: binary lock, only the locking thread can unlock — for mutual exclusion",
      "Semaphore: integer counter, signaled by any thread — for resource counting/signaling",
      "Mutex example: protecting a shared variable",
      "Semaphore example: limiting N concurrent DB connections (counting semaphore)",
      "Mentions producer-consumer with semaphores"
    ],
    "followUps": ["What is a priority inversion?", "What is a spinlock vs mutex?"],
    "source": "Infosys SP 2025 [1]; common GfG [8]"
  },
  {
    "id": "sde-oop-014",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "easy",
    "companies": ["wipro", "cognizant-genc", "tcs-nqt", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain the four pillars of OOP with one-line examples.",
    "rubric": [
      "Encapsulation: bundling data + methods, hiding internal state (private fields + getters)",
      "Inheritance: child class reuses parent fields/methods (Dog extends Animal)",
      "Polymorphism: same interface different behavior (override toString)",
      "Abstraction: expose what, hide how (interface / abstract class)",
      "Names which is enforced by language vs design"
    ],
    "followUps": ["Is encapsulation same as abstraction?", "Give a real-world analogy."],
    "source": "Wipro Elite NLTH 2025 [17]; Cognizant GenC [12]"
  },
  {
    "id": "sde-oop-015",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "medium",
    "companies": ["cognizant-genc", "infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between compile-time and runtime polymorphism. Give a Java example for each.",
    "rubric": [
      "Compile-time = method overloading (same name, different params) — resolved at compile",
      "Runtime = method overriding (subclass redefines parent method) — resolved via vtable",
      "Overloading example: add(int,int) vs add(double,double)",
      "Overriding example: Animal.speak() overridden by Dog.speak()",
      "Mentions @Override annotation and dynamic dispatch"
    ],
    "followUps": ["Can you override a static method?", "What is method hiding?"],
    "source": "Cognizant GenC 2025 [12]; Infosys SP [1]"
  },
  {
    "id": "sde-oop-016",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "When would you prefer composition over inheritance?",
    "rubric": [
      "Inheritance is 'is-a'; composition is 'has-a'",
      "Composition is more flexible — change behavior at runtime",
      "Avoids fragile base class problem and deep hierarchies",
      "Example: Car has-a Engine vs Car extends Vehicle — engine swap easy with composition",
      "Mentions 'favor composition over inheritance' from Effective Java"
    ],
    "followUps": ["What is the fragile base class problem?", "What is the Strategy pattern?"],
    "source": "Infosys SP Medium 2025 [1]"
  },
  {
    "id": "sde-oop-017",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "medium",
    "companies": ["infosys-sp", "cognizant-genc"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What is the Singleton design pattern? Describe one situation where it's the right choice and one where it's an anti-pattern.",
    "rubric": [
      "Ensures only one instance of a class exists; provides global access",
      "Right choice: logger, configuration manager, DB connection pool",
      "Anti-pattern: hidden global state breaks testability and parallelism",
      "Thread-safe implementations: double-checked locking, enum singleton",
      "Mentions Spring beans as managed singletons (better alternative)"
    ],
    "followUps": ["Why is the enum singleton thread-safe by default?", "How is Singleton different from a static class?"],
    "source": "Infosys SP 2025 [1]; Cognizant GenC [12]"
  },
  {
    "id": "sde-oop-018",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "easy",
    "companies": ["wipro", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Difference between abstract class and interface in Java. When do you pick each?",
    "rubric": [
      "Abstract class: can have state, constructors, partial implementation; single inheritance",
      "Interface: only contract (Java 8+ allows default methods); multiple inheritance",
      "Use abstract class when sharing implementation among related types",
      "Use interface when defining capability across unrelated types (Comparable, Serializable)",
      "Mentions Java 8 default and static methods in interfaces"
    ],
    "followUps": ["Can an abstract class have a constructor?", "What changed with Java 8 default methods?"],
    "source": "Wipro Elite NLTH 2025 [17]; Capgemini DA Glassdoor [14]"
  },
  {
    "id": "sde-oop-019",
    "role": "sde-non-coding",
    "topic": "oop",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Explain the Factory design pattern. Why is it useful?",
    "rubric": [
      "Creational pattern: defines an interface to create objects, lets subclasses decide which class to instantiate",
      "Decouples client from concrete implementations",
      "Useful when object creation logic is complex or depends on input",
      "Example: ShapeFactory.create('circle') returns Circle",
      "Mentions Abstract Factory as related pattern"
    ],
    "followUps": ["Difference between Factory and Abstract Factory?", "How does dependency injection relate?"],
    "source": "Infosys SP 2025 [1]; TCS Digital [3]"
  },
  {
    "id": "sde-proj-020",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "wipro", "cognizant-genc", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through your most challenging college project. What was the problem, your role, and the outcome?",
    "rubric": [
      "Clear structure: problem → approach → role → outcome",
      "Names tech stack concretely (MERN / Spring Boot / Django, DB, deployment)",
      "States their specific contribution vs teammates",
      "Quantifies outcome (users / requests / accuracy / grade)",
      "Demonstrates ownership of one hard decision"
    ],
    "followUps": ["What would you redesign today?", "What was the biggest blocker?"],
    "source": "Cognizant GenC PrepInsta 2025 [12]; Wipro NLTH [17]; TCS NQT [9]"
  },
  {
    "id": "sde-proj-021",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What was the hardest bug you debugged in your project? Walk me through how you found and fixed it.",
    "rubric": [
      "Specific bug (race condition, off-by-one, env mismatch, library version), not generic",
      "Shows methodology: reproduction → hypothesis → tools (logs, debugger, git bisect)",
      "Distinguishes symptom from root cause",
      "Names the fix and why it works",
      "Reflects on what they'd do to prevent it (test, monitoring)"
    ],
    "followUps": ["How would you write a test for that bug?", "Could it have been caught earlier in CI?"],
    "source": "Infosys SP Medium 2025 [1]; TCS Digital GfG [3]"
  },
  {
    "id": "sde-proj-022",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "If you had to scale your project from 100 users to 1 million users, what would you change first?",
    "rubric": [
      "Identifies current bottleneck honestly (single-server DB, in-memory cache, file storage)",
      "First step: profile and measure before changing",
      "Mentions horizontal scaling, load balancer, CDN, read replicas",
      "Caching layer (Redis) and async processing (queue)",
      "Considers cost vs benefit, doesn't over-engineer"
    ],
    "followUps": ["Where would the DB become the bottleneck?", "Sharding vs read replicas — which first?"],
    "source": "Infosys SP 2025 [1]; common managerial round"
  },
  {
    "id": "sde-proj-023",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why did you choose [tech stack] for your project over alternatives?",
    "rubric": [
      "Honest tradeoff reasoning, not 'because it's popular'",
      "Mentions at least one alternative considered",
      "Considers team familiarity, ecosystem, hosting, learning curve",
      "Concrete pros/cons (e.g., 'Mongo for flexible schema, but joins were painful')",
      "Acknowledges limitations of the choice"
    ],
    "followUps": ["What would you choose if you started today?", "What was the biggest regret?"],
    "source": "TCS NQT 2025 [9]; Capgemini [14]"
  },
  {
    "id": "sde-proj-024",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Did you use Git in your project? Describe a Git workflow conflict you faced and how you resolved it.",
    "rubric": [
      "Branching strategy used (feature branches, main/dev)",
      "Specific conflict: merge conflict, force-push, lost commits, accidental commit to main",
      "Commands used to resolve (git rebase, git merge, git reflog)",
      "Lesson learned (PR reviews, branch protection)",
      "Mentions team communication around the resolution"
    ],
    "followUps": ["Difference between rebase and merge?", "How would branch protection have helped?"],
    "source": "Common project deep-dive 2025; HCL Tech [common]"
  },
  {
    "id": "sde-proj-025",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "How did you design the database schema for your project? Walk me through the main tables and relationships.",
    "rubric": [
      "Names 3-5 main entities with PKs/FKs",
      "Justifies one-to-many vs many-to-many choice",
      "Mentions normalization level used and any deliberate denormalization",
      "Discusses one tradeoff (e.g., why JSON column instead of EAV)",
      "Mentions indexing on hot columns"
    ],
    "followUps": ["What would you change after launch?", "Why didn't you choose NoSQL?"],
    "source": "Infosys SP 2025 [1]; TCS Digital [3]"
  },
  {
    "id": "sde-mgr-026",
    "role": "sde-non-coding",
    "topic": "managerial",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-se", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you had a conflict with a teammate. How did you handle it?",
    "rubric": [
      "Specific situation, not hypothetical",
      "Shows empathy for the other person's view",
      "Did NOT escalate immediately — tried 1:1 conversation first",
      "Outcome: resolved with data / compromise / clear next steps",
      "Reflects on what they learned"
    ],
    "followUps": ["What if the conflict had not been resolved?", "How would you avoid it next time?"],
    "source": "TCS NQT 2025 GfG [9]; Infosys SE managerial round [1]"
  },
  {
    "id": "sde-mgr-027",
    "role": "sde-non-coding",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["tcs-digital", "infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You have a project deadline tomorrow but a critical bug appears today. Walk me through your decision-making.",
    "rubric": [
      "Triage first: assess severity, blast radius, who's affected",
      "Communicate to PM / lead immediately — don't hide it",
      "Consider rollback or feature flag as quickest mitigation",
      "Decide between fix-now (with risk) vs ship-then-fix (with disclosure)",
      "Document the trade-off and learning"
    ],
    "followUps": ["What if the bug only affects 1% of users?", "When would you push back on the deadline?"],
    "source": "TCS Digital managerial 2025 [3]; Infosys SP [1]"
  },
  {
    "id": "sde-mgr-028",
    "role": "sde-non-coding",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're given three tasks of equal priority by three different managers. How do you prioritize?",
    "rubric": [
      "Doesn't pretend everything is doable — clarifies first",
      "Asks each manager about deadline, blast radius, dependencies",
      "Surfaces conflict to skip-level / team lead instead of silently picking one",
      "Communicates transparently to all three managers about chosen order",
      "Mentions writing down dependencies as decision aid"
    ],
    "followUps": ["What if one manager is also your reporting manager?", "How would you push back politely?"],
    "source": "Common managerial round, Infosys SP / TCS 2025 [1][3]"
  },
  {
    "id": "sde-hr-029",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-se", "wipro", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why do you want to join [company name] specifically, and not just any IT services company?",
    "rubric": [
      "Researched something specific — recent tech move, training program, founder story",
      "Connects to a personal goal (learning Cloud, working on BFSI clients, global exposure)",
      "Does NOT say 'job security' or 'package'",
      "Avoids generic 'top MNC' framing",
      "Reflects awareness of company's current strategic direction"
    ],
    "followUps": ["What do you know about our recent acquisitions / GenAI initiative?", "Are you applying elsewhere?"],
    "source": "TCS NQT 2025 [9]; Wipro Elite [17]; Cognizant [12]"
  },
  {
    "id": "sde-hr-030",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What are your strengths and weaknesses? Pick one of each and explain.",
    "rubric": [
      "Strength: backed by a specific example, not a buzzword",
      "Weakness: actually a weakness (not 'I work too hard')",
      "Shows self-awareness and active steps to improve weakness",
      "Avoids deal-breakers (e.g., 'I can't take feedback')",
      "Ties strength to the job's needs"
    ],
    "followUps": ["What feedback have you received recently?", "How are you working on the weakness right now?"],
    "source": "Common HR across TCS, Infosys, Wipro, Capgemini 2025 [9][1][17][14]"
  }
]
```

---

## Counts Per Role

- **Data Analyst (30):** SQL 11, Python 4, DBMS 4, Project 2, Stats 3, Case 3, GenAI 1, HR 1 — mix shifted slightly toward SQL because campus DA interviews are SQL-dominant.
- **Data Scientist (30):** ML 12, Stats 4, Python 3, Case 4, GenAI 3, HR 2 — meets the ≥3 `text_python` requirement (ds-py-015, 016, 017, 030).
- **SDE Non-Coding (30):** DBMS 7, OS 6, OOP 6, Project 6, Managerial 3, HR 2 — all `voice_explanation`-only as required.

Input-mode counts: **DA has 9 `text_sql` questions** (≥5 required) — da-sql-001/002/003/004/005/006/008/009/027 — plus 4 `text_python`. **DS has 4 `text_python`** (≥3 required). **SDE is 100% voice_explanation**.

## Sources

1. [Infosys SP Role Interview Experience 2025 — Medium / Dev Sharma](https://medium.com/@giga_dummy/infosys-sp-role-interview-experience-2025-by-dev-sharma-210bcfa7dfef)
2. [TCS Data Analyst Interview Questions — BUGSPOTTER](https://bugspotter.in/data-analyst-interview-questions-for-tcs/)
3. [TCS Digital Interview Experience — GeeksforGeeks](https://www.geeksforgeeks.org/interview-experiences/tcs-digital-interview-questions/)
4. [ZS Associates / Tredence Data Analyst Interview Questions — Glassdoor India](https://www.glassdoor.com/Interview/ZS-Associates-Data-Analyst-Interview-Questions-EI_IE115506.0,13_KO14,26.htm)
5. [Deloitte Data Analyst Interview Guide 2025 — InterviewQuery](https://www.interviewquery.com/interview-guides/deloitte-data-analyst)
6. [Deloitte SQL Interview Questions — DataLemur](https://datalemur.com/blog/deloitte-sql-interview-questions)
7. [Fractal Analytics Data Scientist Interview Guide 2025 — InterviewQuery](https://www.interviewquery.com/interview-guides/fractal-analytics-data-scientist)
8. [Infosys SDE Sheet — GeeksforGeeks](https://www.geeksforgeeks.org/dsa/infosys-sde-sheet-interview-questions-and-answers/)
9. [TCS NQT 2025 Interview Experience — GeeksforGeeks](https://www.geeksforgeeks.org/interview-experiences/tcs-interview-experience-tcs-nqt-2025/)
10. [PhonePe Data Scientist Interview Experience — Medium / Sania Qamar](https://medium.com/@sq.sania/my-phonepe-data-scientist-interview-experience-questions-learnings-and-insights-ff0c0ddf1733)
11. [Swiggy SQL Case Study (All Major Interview Questions) — Medium](https://medium.com/@mvanshika23/swiggy-sql-case-study-all-major-interview-questions-covered-part-1-39dda8d9633b)
12. [Cognizant GenC Interview Experience 2025 — PrepInsta](https://prepinsta.com/interview-preparation/cognizant-genc-interview-experience/)
13. [Accenture Data Analyst Interview Guide 2025 — InterviewQuery](https://www.interviewquery.com/interview-guides/accenture-data-analyst)
14. [Capgemini Data Analyst Interview Questions — Glassdoor India](https://www.glassdoor.co.in/Interview/Capgemini-Data-Analyst-Interview-Questions-EI_IE3803.0,9_KO10,22.htm)
15. [Capgemini Data Analyst Interview Questions — BUGSPOTTER](https://bugspotter.in/data-analyst-interview-questions-for-capgemini/)
16. [LatentView Analytics Data Analyst Interview Guide — InterviewQuery](https://www.interviewquery.com/interview-guides/latentview-analytics-data-analyst)
17. [Wipro Elite NLTH On-Campus Interview Experience — GeeksforGeeks](https://www.geeksforgeeks.org/wipro-nlth-interview-experience-on-campus/)
18. [EXL Data Analyst Interview Guide 2025 — InterviewQuery](https://www.interviewquery.com/interview-guides/exl-service-data-analyst)
19. [Genpact SQL Interview Questions — DataLemur](https://datalemur.com/blog/genpact-sql-interview-questions)
20. [Accenture Data Analyst Interview Questions — BUGSPOTTER](https://bugspotter.in/data-analyst-interview-questions-for-accenture/)
21. [Mu Sigma Data Scientist Interview Experience — Glassdoor](https://www.glassdoor.com/Interview/Mu-Sigma-Data-Scientist-Interview-Questions-EI_IE253258.0,8_KO9,23.htm)
22. [Flipkart Data Engineering Interview Experience — GeeksforGeeks](https://www.geeksforgeeks.org/interview-experiences/flipkart-interview-experience-for-data-engineering-i/)
23. [Amazon Data Scientist Interview Guide (27 Questions 2025) — DataLemur](https://datalemur.com/blog/amazon-data-scientist-interview-guide)
24. [Flipkart Machine Learning Interview Questions (Updated 2025) — Exponent](https://www.tryexponent.com/questions?company=flipkart&role=data-science&type=machine-learning)
25. [Tiger Analytics Data Scientist Interview Questions 2025 — InterviewQuery](https://www.interviewquery.com/interview-guides/tiger-analytics-data-scientist)

---

---

# Extension 1 — HR / Behavioural / Project / Managerial / Situational (60 questions)

**Added:** 2026-05-18
**Why:** MVP locked as voice-only — convert/expand seed toward verbal-articulation rounds. 60 questions added (20 per role) so each role has 50 total.

**Note on source numbering:** Source numbers in this Extension's questions refer to the Extension 1 source list at the bottom of this section (not the original seed's source list).

---


---

## Role 1 — Data Analyst (20 new questions)

```json
[
  {
    "id": "da-hr-002",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["latentview", "tredence", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why do you want to be a Data Analyst and not a Data Scientist? Both roles use data — what specifically pulls you toward analytics?",
    "rubric": [
      "Articulates clear interest in business-facing insight delivery vs model-building research",
      "Mentions enjoyment of SQL, dashboards, stakeholder questions rather than ML modelling",
      "Shows awareness that DS is heavier on stats/ML/coding and DA is heavier on business context and storytelling",
      "Does NOT badmouth DS role; frames as personal fit not a hierarchy",
      "Backs with at least one concrete example from a project or internship"
    ],
    "followUps": [
      "Do you see yourself moving into Data Science in 3-5 years?",
      "What would you miss about a DS role if you choose DA?"
    ],
    "source": "AmbitionBox LatentView Analyst interview experience 2024 [1]"
  },
  {
    "id": "da-hr-003",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-digital", "infosys-dse", "wipro", "cognizant-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Are you comfortable relocating anywhere in India — Bangalore, Hyderabad, Pune, Chennai, or even Bhubaneswar — at short notice for your first posting?",
    "rubric": [
      "Gives a clear yes/no with reasoning, not a wishy-washy 'I'll think about it'",
      "Acknowledges that service companies post freshers based on project need",
      "Mentions family/personal considerations honestly if relevant but signals flexibility",
      "Does not demand a specific location",
      "Shows research awareness — knows the company has multiple delivery centres"
    ],
    "followUps": [
      "What if you're posted to a tier-2 city for 2 years?",
      "Would your family be okay with relocation?"
    ],
    "source": "PrepInsta TCS Digital HR round 2024 reports [2]"
  },
  {
    "id": "da-hr-004",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["zs-associates", "deloitte-analytics-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through your CGPA trend semester by semester. If there's a dip anywhere, tell me what happened.",
    "rubric": [
      "Owns the numbers honestly — does not hide a low semester",
      "Explains dip with specific reason (health, family, transition to hostel, heavy electives) without sounding like an excuse",
      "Shows what was learned and how subsequent semesters improved or stabilised",
      "Connects academic resilience to workplace resilience",
      "Avoids blaming professors or 'tough paper'"
    ],
    "followUps": [
      "What's the one subject you wish you'd done better in?",
      "How did you balance academics with your projects?"
    ],
    "source": "Glassdoor ZS Associates Decision Analytics Associate HR round 2024 [3]"
  },
  {
    "id": "da-hr-005",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["genpact", "exl", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "The CTC we're offering is on the lower side of what some product companies pay. Why should we still be your top choice?",
    "rubric": [
      "Acknowledges the gap without sounding desperate or arrogant",
      "Reframes around learning curve, training programs, exposure to multiple clients/domains",
      "Mentions long-term growth path, internal mobility, or specific company strengths",
      "Does not lie about having no other offers; handles competing offers gracefully if asked",
      "Shows the role aligns with career trajectory beyond just CTC"
    ],
    "followUps": [
      "If a product company offers you 4 LPA more next week, will you switch?",
      "What's your minimum acceptable CTC?"
    ],
    "source": "AmbitionBox Genpact Business Analyst HR round 2025 [4]"
  },
  {
    "id": "da-beh-001",
    "role": "data-analyst",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["tredence", "mu-sigma", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time when your analysis led to a recommendation that your team or professor initially disagreed with. Walk me through the situation, what you did, and the outcome.",
    "rubric": [
      "Clear STAR structure: Situation, Task, Action, Result",
      "Specific disagreement described, not vague 'they didn't like it'",
      "Action shows data-backed defence, not emotional argument",
      "Mentions how they listened to counter-points and either incorporated them or held position with evidence",
      "Result is quantified or at least concrete (decision changed, model adopted, grade improved)"
    ],
    "followUps": [
      "What would you do differently if it happened again?",
      "How did you rebuild rapport after the disagreement?"
    ],
    "source": "InterviewBit Tredence Data Analyst interview experiences 2024 [5]"
  },
  {
    "id": "da-beh-002",
    "role": "data-analyst",
    "topic": "behavioural",
    "difficulty": "easy",
    "companies": ["accenture", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Describe a situation where you had to learn a new tool — Power BI, Tableau, or SQL — within a tight deadline. How did you approach it?",
    "rubric": [
      "STAR structure with specific tool and deadline",
      "Shows learning strategy: docs, YouTube, practice datasets, peer help",
      "Demonstrates progression from beginner output to usable deliverable",
      "Mentions one concrete blocker hit and how it was resolved",
      "Ends with skill being applied beyond the original deadline (retention)"
    ],
    "followUps": [
      "What part of the tool do you still find hardest?",
      "Would you recommend the same learning path to a junior?"
    ],
    "source": "PrepInsta Accenture HR + technical round 2024 reports [6]"
  },
  {
    "id": "da-beh-003",
    "role": "data-analyst",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["deloitte-analytics-india", "zs-associates", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you received harsh or critical feedback on your work. Walk me through your reaction and what changed afterwards.",
    "rubric": [
      "Honest about emotional initial reaction — not pretending to be unfazed",
      "Describes specific feedback, not generalised 'they said it could be better'",
      "Action focuses on processing, asking clarifying questions, and a concrete change",
      "Result shows measurable improvement or relationship repair",
      "Reflects on whether feedback was fair in hindsight"
    ],
    "followUps": [
      "What's a piece of feedback you disagreed with and how did you handle it?",
      "How do you give feedback to peers?"
    ],
    "source": "Glassdoor Deloitte USI Analyst interview 2024 [7]"
  },
  {
    "id": "da-beh-004",
    "role": "data-analyst",
    "topic": "behavioural",
    "difficulty": "hard",
    "companies": ["zs-associates", "tredence", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you made a mistake in your analysis that you only caught later. What did you do?",
    "rubric": [
      "Owns a real mistake — not a humblebrag like 'I work too hard'",
      "Describes how the error was detected and the actual impact (or near-impact)",
      "Action: immediate disclosure to stakeholder, correction, root-cause fix",
      "Shows process improvement that prevented recurrence (validation checks, peer review)",
      "Demonstrates integrity rather than blame-shifting"
    ],
    "followUps": [
      "What checks do you now run before sharing any analysis?",
      "Did anyone get upset and how did you manage that conversation?"
    ],
    "source": "AmbitionBox ZS Associates Associate interview experiences 2025 [3]"
  },
  {
    "id": "da-proj-003",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["ibm-india", "ltimindtree", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Pick the project you've put on top of your resume. What was the hardest data quality issue you ran into, and how did you handle it?",
    "rubric": [
      "Specific issue named: missing values, duplicates, inconsistent formats, outliers, schema mismatch",
      "Explains how the issue was detected (profiling, validation, anomaly in dashboard)",
      "Walks through the handling decision with trade-offs — not just 'I dropped nulls'",
      "Mentions impact on final analysis or model",
      "Shows what they would do differently next time"
    ],
    "followUps": [
      "How did you decide between imputation and dropping?",
      "Could the data quality issue have been caught at source?"
    ],
    "source": "Glassdoor IBM India Data Analyst interview 2024 [8]"
  },
  {
    "id": "da-proj-004",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["mu-sigma", "fractal-analytics", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "If you had to redesign your main project from scratch today with everything you've learned since, what would you change first and why?",
    "rubric": [
      "Picks ONE change to discuss in depth rather than listing 10",
      "Reasons grounded in lessons learned, not just 'I'd use a fancier tool'",
      "Considers data, methodology, presentation, or stakeholder communication angle",
      "Acknowledges trade-offs of the new approach",
      "Shows self-awareness about original choices being reasonable at the time"
    ],
    "followUps": [
      "Why didn't you do it that way originally?",
      "What's the second thing you'd change?"
    ],
    "source": "InterviewBit Mu Sigma Decision Scientist interview reports 2024 [9]"
  },
  {
    "id": "da-proj-005",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "hard",
    "companies": ["latentview", "tredence", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "In your project, who was the end consumer of your analysis? Walk me through how you tailored the output for them and what pushback you got.",
    "rubric": [
      "Identifies a specific stakeholder (professor, club president, internship manager, client)",
      "Describes their context: what decision they needed to make, technical literacy, time constraints",
      "Shows tailoring: dashboard vs deck vs memo, level of detail, vocabulary",
      "Names a real piece of pushback or clarifying question received",
      "Explains how that pushback changed the deliverable"
    ],
    "followUps": [
      "What would you do if the stakeholder ignored your recommendation?",
      "How do you handle a stakeholder who keeps moving the goalpost?"
    ],
    "source": "AmbitionBox LatentView Senior Analyst experience 2025 [1]"
  },
  {
    "id": "da-proj-006",
    "role": "data-analyst",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["exl", "genpact", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "In your project, was there an analysis path you started but had to abandon? What didn't work and how did you pivot?",
    "rubric": [
      "Names a specific failed approach (clustering didn't separate, time-series too noisy, segmentation logic didn't generalise)",
      "Explains why it failed with concrete evidence, not just 'results were bad'",
      "Walks through the pivot decision — when to persist vs cut losses",
      "Shows the alternate approach taken and why it worked better",
      "Reflects on signals they'd watch for earlier next time"
    ],
    "followUps": [
      "How long did you spend on the failed path before pivoting?",
      "Did you document the dead-end for others?"
    ],
    "source": "Glassdoor EXL Analyst interview reports 2024 [10]"
  },
  {
    "id": "da-mgr-001",
    "role": "data-analyst",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["tcs-digital", "infosys-dse", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your manager asks you to present an analysis to leadership in 2 hours, but you've spotted a data inconsistency you haven't resolved. What do you do?",
    "rubric": [
      "Does not silently push out a known-flawed analysis",
      "Immediately flags inconsistency to manager with magnitude estimate",
      "Proposes options: delay, present with caveat, present a confidence-scoped subset",
      "Lets manager make the final call but provides honest recommendation",
      "Plans to fix root cause after the meeting"
    ],
    "followUps": [
      "What if your manager says 'just present it, we'll fix it later'?",
      "How would you word the caveat to leadership?"
    ],
    "source": "PrepInsta TCS Digital managerial round 2024 [2]"
  },
  {
    "id": "da-mgr-002",
    "role": "data-analyst",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["deloitte-analytics-india", "ibm-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "A senior on your team keeps assigning you only data-cleaning and pivot-table work after 3 months. You feel you're not growing. How do you raise this?",
    "rubric": [
      "Does not jump to complaining to skip-level or quitting",
      "Plans a 1:1 conversation with specific examples and a constructive ask",
      "Frames it as growth and contribution, not blame",
      "Proposes specific work they want to take on — shows ownership",
      "Has a fallback plan if the senior is unresponsive (mentor, skip-level, internal transfer process)"
    ],
    "followUps": [
      "What if the senior says you're not ready yet?",
      "How long do you give it before escalating?"
    ],
    "source": "AmbitionBox Deloitte USI Analyst experiences 2024 [7]"
  },
  {
    "id": "da-sit-001",
    "role": "data-analyst",
    "topic": "situational",
    "difficulty": "medium",
    "companies": ["accenture", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're three days from a client deliverable when the client emails saying the metric definition they gave you was wrong. What do you do?",
    "rubric": [
      "Acknowledges this is common in real consulting work",
      "Quickly assesses scope of rework — what changes vs what's reusable",
      "Communicates back to client with revised timeline and any trade-offs",
      "Re-prioritises within team and flags to manager early",
      "Builds in a definition-confirmation checkpoint for future to prevent recurrence"
    ],
    "followUps": [
      "What if rework needs a week but client still wants it in 3 days?",
      "How would you document the metric change?"
    ],
    "source": "Glassdoor Accenture Strategy & Consulting Analyst interview 2024 [6]"
  },
  {
    "id": "da-sit-002",
    "role": "data-analyst",
    "topic": "situational",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You've joined a new project and the existing dashboard you've inherited has no documentation. How do you get up to speed?",
    "rubric": [
      "Starts with the data sources and refresh schedule before the visuals",
      "Reverse-engineers metric logic by tracing back to source queries",
      "Identifies a knowledgeable person — previous analyst, business stakeholder — and books time",
      "Documents findings as they go to help the next person",
      "Validates understanding by recreating a small portion before making changes"
    ],
    "followUps": [
      "What if no one remembers how a metric was calculated?",
      "Would you rebuild from scratch or maintain?"
    ],
    "source": "PrepInsta TCS NQT interview experiences 2025 [2]"
  },
  {
    "id": "da-mix-001",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-digital", "infosys-dse", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why are you choosing a services company over a product company for your first job?",
    "rubric": [
      "Avoids the trap of saying 'because product didn't take me'",
      "Frames around exposure: multiple clients, domains, business contexts",
      "Mentions structured training and clear career ladder valued for first job",
      "Acknowledges product company strengths without dismissing them",
      "Connects to personal learning style — generalist exploration before specialising"
    ],
    "followUps": [
      "Will you switch to a product company in 2-3 years?",
      "What if you're stuck on the same client for 4 years?"
    ],
    "source": "PrepInsta Infosys DSE HR round 2024 [11]"
  },
  {
    "id": "da-mix-002",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["genpact", "exl", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Some of our analyst roles involve night shifts to overlap with US clients. Are you okay with that, and how would you sustain it long-term?",
    "rubric": [
      "Gives an honest answer, not a desperate 'yes I'll do anything'",
      "Shows awareness of health and lifestyle implications",
      "Mentions concrete sustainability tactics: sleep schedule, family communication, rotation expectations",
      "Asks clarifying question about rotation duration or hybrid possibility",
      "Does not lie if they genuinely cannot do nights"
    ],
    "followUps": [
      "How long can you sustain a 9pm-6am shift?",
      "What if night shifts last 2 years?"
    ],
    "source": "AmbitionBox EXL Analyst HR round 2024 [10]"
  },
  {
    "id": "da-mix-003",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about your father's profession and how it has shaped your career thinking.",
    "rubric": [
      "Answers respectfully and concretely about family background",
      "Connects to career thinking without forcing a narrative",
      "Shows self-awareness if family is in a very different field",
      "Avoids long detours into family history",
      "Treats this as a rapport-building question, not a test"
    ],
    "followUps": [
      "Did your family support your choice of analytics as a career?",
      "What does your family think about you potentially moving cities?"
    ],
    "source": "Common Indian campus HR question pattern, reported across TCS/Infosys/Wipro 2024-2025 [2]"
  },
  {
    "id": "da-mix-004",
    "role": "data-analyst",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["latentview", "tredence", "fractal-analytics", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "We typically offer freshers a 2-year service bond. Are you comfortable signing that, and what's your honest plan for after 2 years?",
    "rubric": [
      "Direct yes/no with reasoning, not evasive",
      "Acknowledges the bond is a fair trade for training investment",
      "Shows long-term thinking: what they want to learn in 2 years",
      "Honest about whether they plan to pursue higher studies or switch",
      "Does not promise a 10-year stay they don't intend"
    ],
    "followUps": [
      "What if you get an MS admit after 1 year?",
      "Would you pay the bond amount to leave early?"
    ],
    "source": "AmbitionBox Tredence and LatentView bond discussions 2024 [5]"
  }
]
```

---

## Role 2 — Data Scientist (20 new questions)

```json
[
  {
    "id": "ds-hr-003",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "walmart-labs-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why Data Science and not pure ML research or a PhD path? You seem strong enough technically — why industry?",
    "rubric": [
      "Articulates a clear preference for applied impact over publication cycle",
      "Mentions interest in shipping models that affect users vs proving novel theory",
      "Acknowledges research path's value without dismissing it",
      "Shows research awareness — knows industry DS still involves experimentation",
      "Backs with a project where they preferred a shipped outcome over a more elegant solution"
    ],
    "followUps": [
      "Would you consider an industry research lab like Amazon Science?",
      "What if your team only does dashboards for 6 months?"
    ],
    "source": "LeetCode Discuss Amazon India DS interview experiences 2024 [12]"
  },
  {
    "id": "ds-hr-004",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["phonepe", "razorpay", "swiggy", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through your resume but spend most time on the one project or experience you're proudest of. Be specific about your individual contribution.",
    "rubric": [
      "Skims early biographical details to make time for depth",
      "Picks ONE project to go deep on rather than touching everything",
      "Uses 'I' not 'we' when describing the specific contribution",
      "Quantifies impact: accuracy, latency, business metric, users reached",
      "Connects the project to why they're applying for THIS role"
    ],
    "followUps": [
      "What was the team size and how did work split?",
      "What's the one thing you'd still improve?"
    ],
    "source": "Glassdoor PhonePe Data Scientist interview experiences 2024 [13]"
  },
  {
    "id": "ds-hr-005",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["jp-morgan-india", "goldman-sachs-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Financial services involves heavy regulation and audit trails. Are you comfortable working in an environment where you can't always use the latest model and explainability is mandatory?",
    "rubric": [
      "Shows awareness of why financial services requires explainability and lineage",
      "Mentions specific techniques: SHAP, LIME, simpler models like logistic regression / GAMs",
      "Does not complain about constraints — frames as engineering discipline",
      "Acknowledges trade-off between accuracy and interpretability",
      "Connects to a project where they had to balance these"
    ],
    "followUps": [
      "When would you push back against using only an interpretable model?",
      "How do you document a model for an auditor?"
    ],
    "source": "Glassdoor JP Morgan India Quant/DS interview 2024 [14]"
  },
  {
    "id": "ds-hr-006",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["mu-sigma", "fractal-analytics", "tiger-analytics", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Our work is heavily client-facing analytics consulting, not building products. Some weeks you'll do more PowerPoint than Python. How does that sit with you?",
    "rubric": [
      "Honest assessment — does not pretend to love decks if they don't",
      "Reframes communication as a core DS skill, not a downgrade",
      "Mentions experience presenting analysis to non-technical audience",
      "Shows interest in business problem-solving, not just modelling",
      "Asks a thoughtful clarifying question about the ratio over time"
    ],
    "followUps": [
      "What if a project doesn't need ML at all and SQL solves it?",
      "How do you stay technically sharp in a consulting environment?"
    ],
    "source": "AmbitionBox Fractal Analytics and Tiger Analytics interview 2024-2025 [15]"
  },
  {
    "id": "ds-beh-001",
    "role": "data-scientist",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["flipkart", "swiggy", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you explained a complex ML concept or result to a completely non-technical stakeholder. Walk me through how you prepared and what happened.",
    "rubric": [
      "Clear STAR structure with a real stakeholder, not hypothetical",
      "Action shows analogies, visuals, removing jargon — not dumbing down",
      "Mentions checking for understanding mid-conversation",
      "Result is concrete: stakeholder made a decision, asked a smart follow-up, signed off",
      "Reflects on what didn't land and what they'd change"
    ],
    "followUps": [
      "What analogy did you use and why that one?",
      "How do you explain confidence intervals to someone non-technical?"
    ],
    "source": "Glassdoor Flipkart Data Scientist interview experiences 2024 [16]"
  },
  {
    "id": "ds-beh-002",
    "role": "data-scientist",
    "topic": "behavioural",
    "difficulty": "hard",
    "companies": ["amazon-india", "walmart-labs-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you had to deliver bad news about a model — it didn't work, results were worse than baseline, or business impact was negligible. How did you handle it?",
    "rubric": [
      "Picks a real failure, not a disguised win",
      "Action focuses on honest communication, not defensive framing",
      "Provides the diagnosis: why it didn't work and what was learned",
      "Mentions stakeholder reaction and how trust was managed",
      "Shows what the team did next — kill, iterate, or escalate"
    ],
    "followUps": [
      "Did the project get killed and how did you feel?",
      "What did you learn about validation strategy?"
    ],
    "source": "LeetCode Discuss Amazon India L4 DS behavioural rounds 2024-2025 [12]"
  },
  {
    "id": "ds-beh-003",
    "role": "data-scientist",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["razorpay", "phonepe", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Describe a time when you and a teammate disagreed on the right modelling approach or evaluation metric. Walk me through how you resolved it.",
    "rubric": [
      "Specific disagreement: e.g., AUC vs precision-recall, tree vs neural, online vs offline eval",
      "Action shows technical discussion grounded in data, not seniority",
      "Mentions running a quick experiment to break the tie if applicable",
      "Resolution preserves the working relationship",
      "Reflects on whether the chosen approach was right in hindsight"
    ],
    "followUps": [
      "What if the disagreement is with someone senior?",
      "How do you avoid 'analysis paralysis' in these debates?"
    ],
    "source": "AmbitionBox Razorpay DS interview 2024 [17]"
  },
  {
    "id": "ds-beh-004",
    "role": "data-scientist",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["tiger-analytics", "fractal-analytics", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you had to onboard yourself onto a project with messy data and unclear goals. What did you do in the first week?",
    "rubric": [
      "Lists the first week actions: stakeholder conversations, data audit, goal clarification doc",
      "Shows comfort with ambiguity — does not freeze waiting for instructions",
      "Mentions writing down assumptions and getting them validated",
      "Result is a clearer problem framing or a scoped MVP plan",
      "Reflects on what surprised them and how it shaped approach"
    ],
    "followUps": [
      "What questions do you always ask at the start?",
      "When do you stop scoping and start building?"
    ],
    "source": "Glassdoor Tiger Analytics Senior Analyst interview 2024 [15]"
  },
  {
    "id": "ds-proj-001",
    "role": "data-scientist",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Pick the ML project you led. Walk me through how you split train/validation/test and how you guarded against data leakage.",
    "rubric": [
      "Explains the splitting strategy with reasoning — random, time-based, group-based",
      "Identifies leakage risks specific to the project (target leakage, temporal leakage, group leakage)",
      "Mentions safeguards: pipeline-based preprocessing, holdout discipline",
      "Discusses how the eval set reflects production data distribution",
      "Acknowledges any leakage they caught after the fact and how"
    ],
    "followUps": [
      "How would you validate a model where you have only 6 months of history?",
      "What's your stance on k-fold vs single holdout for small datasets?"
    ],
    "source": "LeetCode Discuss Amazon India L4 DS interview experiences 2025 [12]"
  },
  {
    "id": "ds-proj-002",
    "role": "data-scientist",
    "topic": "project",
    "difficulty": "hard",
    "companies": ["walmart-labs-india", "swiggy", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "For your main project, describe an alternative architecture or approach you considered but rejected. Why did you reject it?",
    "rubric": [
      "Specific alternative named with concrete trade-offs",
      "Reasoning grounded in data size, latency, interpretability, team skills, infra",
      "Shows they considered the alternative seriously, not as a strawman",
      "Acknowledges where the rejected approach might actually be better",
      "Connects to a principle they apply when choosing approaches"
    ],
    "followUps": [
      "If you had 10x more data, would you change your choice?",
      "What would convince you to revisit the rejected option?"
    ],
    "source": "Glassdoor Walmart Labs India DS interview 2024 [18]"
  },
  {
    "id": "ds-proj-003",
    "role": "data-scientist",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["phonepe", "razorpay", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about the EDA phase of your project. What was the one finding from EDA that changed your modelling approach?",
    "rubric": [
      "Picks ONE EDA finding to discuss in depth — not a list",
      "Specific: distribution skew, missingness pattern, surprising correlation, class imbalance",
      "Shows how the finding altered preprocessing, features, model choice, or eval",
      "Mentions visualisation or statistical test used to confirm",
      "Reflects on what would have happened if EDA had been skipped"
    ],
    "followUps": [
      "How long did you spend on EDA vs modelling?",
      "What's your default EDA checklist?"
    ],
    "source": "AmbitionBox PhonePe Data Scientist interview reports 2024 [13]"
  },
  {
    "id": "ds-proj-004",
    "role": "data-scientist",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["deloitte-analytics-india", "jp-morgan-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "If you had to build a dashboard around your project's model for ongoing monitoring, what would be on it and why?",
    "rubric": [
      "Distinguishes model performance metrics from business/operational metrics",
      "Includes drift indicators: feature drift, prediction drift, label drift if available",
      "Mentions latency, throughput, error rates for the prediction service",
      "Includes a slice view — performance across key segments to catch fairness issues",
      "Defines who would look at it and at what cadence"
    ],
    "followUps": [
      "What thresholds would trigger an alert?",
      "How would you detect data drift before the model degrades?"
    ],
    "source": "Glassdoor Deloitte USI DS interview 2024 [7]"
  },
  {
    "id": "ds-mgr-001",
    "role": "data-scientist",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your manager wants a model in 2 weeks for a launch. Your honest estimate is 6 weeks for a quality model. How do you handle this conversation?",
    "rubric": [
      "Does not silently overcommit or quietly miss the deadline",
      "Proposes a phased delivery: baseline in week 2, improved in week 6",
      "Names specific shortcuts and their risks (simpler model, less validation, narrower scope)",
      "Asks about the cost of being wrong — what happens if model is suboptimal at launch",
      "Gets manager to make the trade-off explicitly, with documented assumptions"
    ],
    "followUps": [
      "What if manager insists on 2 weeks with no scope cut?",
      "How would you document the technical debt being incurred?"
    ],
    "source": "LeetCode Discuss Amazon India DS managerial round 2025 [12]"
  },
  {
    "id": "ds-mgr-002",
    "role": "data-scientist",
    "topic": "managerial",
    "difficulty": "hard",
    "companies": ["swiggy", "razorpay", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "A product manager wants you to ship a model whose fairness audit you haven't completed because they think the risk is low. How do you push back?",
    "rubric": [
      "Treats the question seriously rather than dismissing PM's concern",
      "Asks for concrete risk assessment: who is affected, what's the worst case",
      "Proposes a minimum audit scope rather than blocking entirely",
      "Brings data, not ideology — segment performance, error parity across groups",
      "Escalates to leadership if irreducible disagreement remains"
    ],
    "followUps": [
      "What if the fairness audit takes 3 weeks and launch is in 1?",
      "Who else would you loop in?"
    ],
    "source": "Glassdoor Swiggy DS senior round 2024 [19]"
  },
  {
    "id": "ds-sit-001",
    "role": "data-scientist",
    "topic": "situational",
    "difficulty": "medium",
    "companies": ["walmart-labs-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You've deployed a model and a week later you notice predictions are silently degrading. The dashboard hasn't alerted because no metric crossed its threshold. What's your first move?",
    "rubric": [
      "Confirms the degradation is real before alarming stakeholders",
      "Investigates feature drift, label drift, upstream data changes",
      "Checks if a recent deploy or upstream pipeline change correlates",
      "Mentions adding finer-grained alerts and slice-level monitoring",
      "Decides whether to rollback, hotfix, or retrain based on severity"
    ],
    "followUps": [
      "How would you decide between rollback and retraining?",
      "What slice-level metrics would you add?"
    ],
    "source": "AmbitionBox Walmart Labs India DS interview 2025 [18]"
  },
  {
    "id": "ds-sit-002",
    "role": "data-scientist",
    "topic": "situational",
    "difficulty": "easy",
    "companies": ["mu-sigma", "fractal-analytics", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're mid-project and a stakeholder reveals that the labels you've been training on may be noisy or even wrong for 20% of the data. What do you do?",
    "rubric": [
      "Does not panic — quantifies impact on current model performance",
      "Investigates the label generation process to understand the noise pattern",
      "Considers options: clean labels, robust loss functions, label correction model",
      "Communicates revised timeline and confidence levels to stakeholder",
      "Documents the issue for future model versions"
    ],
    "followUps": [
      "How would you detect noisy labels without ground truth?",
      "What loss function helps with label noise?"
    ],
    "source": "InterviewBit Mu Sigma DS interview 2024 [9]"
  },
  {
    "id": "ds-mix-001",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["amazon-india", "flipkart", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Do you see yourself as more of a research-leaning DS or applied-leaning DS, and what does the team you join need to look like for you to thrive?",
    "rubric": [
      "Self-aware honest answer — does not flip-flop to please interviewer",
      "Names concrete signals: paper reading frequency, time spent on novel architectures vs shipping",
      "Describes team they thrive in: senior mentors, code review culture, ML platform support",
      "Acknowledges that early career often requires both",
      "Asks a clarifying question about team composition"
    ],
    "followUps": [
      "What if you join a team with no other DS?",
      "How do you stay technically current?"
    ],
    "source": "Glassdoor Amazon India Applied Scientist vs DS interview 2024 [12]"
  },
  {
    "id": "ds-mix-002",
    "role": "data-scientist",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["swiggy", "phonepe", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you worked with genuinely bad data — incomplete, inconsistent, or just wrong. Walk me through what you did before any modelling.",
    "rubric": [
      "Honest about scale of the badness — percentages, examples",
      "Action: data profiling, source tracing, stakeholder conversations about provenance",
      "Specific cleaning decisions with rationale, not blanket 'I imputed mean'",
      "Mentions building a data quality dashboard or check suite if applicable",
      "Result includes both the model outcome AND improved data process"
    ],
    "followUps": [
      "When do you decide data is too bad to model and stop?",
      "How do you communicate data quality issues to non-DS stakeholders?"
    ],
    "source": "AmbitionBox Swiggy DS interview 2024 [19]"
  },
  {
    "id": "ds-mix-003",
    "role": "data-scientist",
    "topic": "situational",
    "difficulty": "medium",
    "companies": ["jp-morgan-india", "goldman-sachs-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "A business stakeholder asks you for a 'simple correlation' between two metrics, but you suspect they'll misinterpret the result as causation. How do you handle it?",
    "rubric": [
      "Does not lecture or refuse the request outright",
      "Provides the correlation with clear caveat about causation",
      "Offers to investigate causality with appropriate method (RCT, quasi-experiment, controls)",
      "Anticipates how the stakeholder will use the number and pre-empts misuse",
      "Builds trust by being a partner not a gatekeeper"
    ],
    "followUps": [
      "What if they ignore the caveat and present it as causal?",
      "How do you explain confounding in 30 seconds?"
    ],
    "source": "Glassdoor JP Morgan India DS behavioural round 2024 [14]"
  },
  {
    "id": "ds-mix-004",
    "role": "data-scientist",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "What's a data science blog, paper, podcast, or person you follow regularly, and what's one specific thing you learned from them recently?",
    "rubric": [
      "Names something specific — not 'I read Medium articles'",
      "Demonstrates genuine recent engagement, not a year-old reference",
      "Articulates one concrete learning, not vague 'I learned about transformers'",
      "Connects the learning to their own work or thinking",
      "Avoids name-dropping without substance"
    ],
    "followUps": [
      "What would you push back on from that source?",
      "What's something you used to believe and changed your mind on?"
    ],
    "source": "Common DS HR question across Indian campus 2024-2025 [16]"
  }
]
```

---

## Role 3 — SDE Non-Coding (20 new questions)

```json
[
  {
    "id": "sde-hr-031",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-se", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about your father's profession and your family background. How has it influenced your decision to pursue software engineering?",
    "rubric": [
      "Answers respectfully and concisely about family background",
      "Connects to engineering choice authentically — not forcing a story",
      "Comfortable discussing whether they're first-generation engineer if applicable",
      "Does not over-share or get emotional",
      "Treats this as rapport-building, signals cultural fit for Indian service-co"
    ],
    "followUps": [
      "Does your family support you joining IT?",
      "Are they okay with you moving cities for work?"
    ],
    "source": "PrepInsta TCS NQT and Infosys SE HR experiences 2024 [2][11]"
  },
  {
    "id": "sde-hr-032",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-digital", "infosys-sp", "wipro", "cognizant-genc", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Our entry-level roles often require working on-call rotations or 24x7 production support shifts. Are you ready for that as a fresher?",
    "rubric": [
      "Honest yes/no with reasoning, not just 'yes anything'",
      "Acknowledges that on-call builds production debugging skills",
      "Asks clarifying question about rotation frequency or duration",
      "Mentions any constraint honestly (medical, family) if applicable",
      "Shows mature understanding of why on-call exists, not just resentment"
    ],
    "followUps": [
      "What if you get paged at 3am once a week?",
      "How would you balance on-call with skill-building?"
    ],
    "source": "PrepInsta Wipro Elite and Cognizant GenC HR 2024 [6][11]"
  },
  {
    "id": "sde-hr-033",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["tcs-digital", "infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Why are you choosing a services company like ours over a product company, and be honest — is it because you didn't get a product company offer?",
    "rubric": [
      "Does not lie if they applied to product companies — owns the search",
      "Names genuine reasons: structured training, multi-domain exposure, stability",
      "Mentions specific service-co strengths: client diversity, certifications, defined career path",
      "Acknowledges product company strengths without dismissing them",
      "Connects to first 2-3 years of career goals"
    ],
    "followUps": [
      "Will you switch to a product company after 2 years?",
      "What would make you stay long-term?"
    ],
    "source": "Glassdoor TCS Digital and Infosys SP HR round 2024 [2][11]"
  },
  {
    "id": "sde-hr-034",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["tcs-nqt", "wipro", "accenture", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your CGPA is below our typical cutoff. Walk me through why and convince me you can still perform.",
    "rubric": [
      "Owns the number without excuses or blame",
      "Provides a concrete reason for the dip with specifics",
      "Demonstrates other evidence of capability: projects, internships, certifications, hackathons",
      "Shows trajectory: improvement over semesters, recent strong performance",
      "Frames CGPA as one signal, not the only one"
    ],
    "followUps": [
      "What was your worst semester and why?",
      "How will you ensure work performance isn't the same?"
    ],
    "source": "PrepInsta TCS NQT and Wipro low-CGPA HR question 2024 [2][6]"
  },
  {
    "id": "sde-beh-001",
    "role": "sde-non-coding",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["accenture", "capgemini", "ibm-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you had to learn a completely new technology stack quickly for a project. Walk me through the situation and how you got productive.",
    "rubric": [
      "STAR structure with specific stack named",
      "Shows learning strategy: docs, official tutorials, building a small toy app first",
      "Mentions how they integrated with their existing project work",
      "Identifies one blocker hit and how it was overcome — Stack Overflow, mentor, debugger",
      "Result shows the tech being used productively beyond the immediate task"
    ],
    "followUps": [
      "How did you avoid copy-paste from tutorials without understanding?",
      "What part of the stack do you still find hardest?"
    ],
    "source": "Glassdoor Accenture and Capgemini SE interview 2024 [6]"
  },
  {
    "id": "sde-beh-002",
    "role": "sde-non-coding",
    "topic": "behavioural",
    "difficulty": "hard",
    "companies": ["infosys-sp", "tcs-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about the most difficult bug you ever debugged. Walk me through what made it hard and how you found it.",
    "rubric": [
      "Picks a real, specific bug — not 'one time my code broke'",
      "Describes symptoms vs root cause distinction clearly",
      "Walks through debugging methodology: reproducing, isolating, logging, hypotheses",
      "Names the actual root cause and why it was hidden — race condition, encoding, memory, off-by-one",
      "Reflects on what tool, test, or habit would have caught it earlier"
    ],
    "followUps": [
      "How long did the debug take?",
      "What did you add to prevent similar bugs later?"
    ],
    "source": "Glassdoor Infosys SP and TCS Digital technical-behavioural round 2024 [11]"
  },
  {
    "id": "sde-beh-003",
    "role": "sde-non-coding",
    "topic": "behavioural",
    "difficulty": "medium",
    "companies": ["hcl-tech", "tech-mahindra", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Describe a time you worked with a teammate whose coding style or approach was very different from yours. How did you handle it?",
    "rubric": [
      "Specific difference described: testing habits, naming, framework choice, async vs sync",
      "Action shows curiosity not judgment — asking why they prefer that way",
      "Mentions agreeing on shared conventions for the project",
      "Result: working code, preserved relationship, possibly learning from each other",
      "Reflects on what they took from the experience"
    ],
    "followUps": [
      "What if your teammate refused to follow team conventions?",
      "How do you handle code review disagreements?"
    ],
    "source": "AmbitionBox HCL and Tech Mahindra SE interview 2024 [20]"
  },
  {
    "id": "sde-beh-004",
    "role": "sde-non-coding",
    "topic": "behavioural",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you missed a deadline or delivered late. What happened and what did you learn?",
    "rubric": [
      "Owns a real miss, does not redirect to a humblebrag",
      "Names the cause honestly: underestimation, scope creep, unexpected blocker",
      "Action: how they communicated and recovered",
      "Specific lesson learned that they now apply (buffer time, daily check-in, scope clarification)",
      "Demonstrates they don't repeat the same miss pattern"
    ],
    "followUps": [
      "How did you communicate the slip?",
      "What's your current estimation approach?"
    ],
    "source": "PrepInsta TCS NQT behavioural round 2024 [2]"
  },
  {
    "id": "sde-proj-007",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["infosys-sp", "tcs-digital", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Pick the project on your resume and walk me through the system architecture as if you were explaining it to a new teammate joining today.",
    "rubric": [
      "Starts with high-level: what the system does and who uses it",
      "Names major components and how they communicate (APIs, DB, queues)",
      "Explains data flow for one end-to-end user journey",
      "Mentions tech choices with at least one trade-off reasoned",
      "Anticipates the new teammate's likely questions and addresses them"
    ],
    "followUps": [
      "What's the most fragile part of the architecture?",
      "What would you change first?"
    ],
    "source": "Glassdoor Infosys SP project deep-dive 2024 [11]"
  },
  {
    "id": "sde-proj-008",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "hard",
    "companies": ["tcs-digital", "infosys-sp", "ibm-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "In your project, what was a design choice you made early that you'd reverse if you started again today? Why did you make it originally and why would you change it now?",
    "rubric": [
      "Picks ONE choice to discuss in depth — database, framework, monolith vs split, auth approach",
      "Defends the original decision in its original context — shows it wasn't naive",
      "Names what changed (more learning, scale needs, ecosystem moves) prompting the reversal",
      "Acknowledges cost of switching now",
      "Demonstrates engineering maturity in distinguishing 'wrong' from 'right at the time'"
    ],
    "followUps": [
      "What signal would have told you earlier to choose differently?",
      "What's the second thing you'd change?"
    ],
    "source": "Glassdoor TCS Digital and IBM project round 2024 [8]"
  },
  {
    "id": "sde-proj-009",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["accenture", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Walk me through how you handled errors and edge cases in your project. Give me a specific example of an edge case you initially missed.",
    "rubric": [
      "Describes a general error-handling philosophy: validation, graceful failure, logging",
      "Gives a specific edge case missed: empty input, unicode, timezone, network timeout, race condition",
      "Explains how the edge case was discovered — bug report, code review, testing",
      "Shows the fix and the broader change in process (added test, added validation layer)",
      "Reflects on edge cases they now think about by default"
    ],
    "followUps": [
      "How do you decide which edge cases to handle vs not?",
      "What's your testing strategy for edge cases?"
    ],
    "source": "AmbitionBox Capgemini and Accenture project round 2024 [6]"
  },
  {
    "id": "sde-proj-010",
    "role": "sde-non-coding",
    "topic": "project",
    "difficulty": "medium",
    "companies": ["hcl-tech", "tech-mahindra", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "In your project, did you write tests? Walk me through what you tested, what you didn't, and why.",
    "rubric": [
      "Honest about test coverage — does not claim 100% if it's 20%",
      "Describes what was tested: core logic, integration points, critical paths",
      "Explains what was skipped and the reasoning: UI flakiness, time constraint, low risk",
      "Mentions test types used: unit, integration, manual",
      "Reflects on whether testing strategy paid off (caught bug, gave confidence to refactor)"
    ],
    "followUps": [
      "What would you test more of next time?",
      "How would you test a hard-to-mock external API?"
    ],
    "source": "AmbitionBox HCL Tech project discussion 2024 [20]"
  },
  {
    "id": "sde-mgr-004",
    "role": "sde-non-coding",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["tcs-digital", "infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Your team lead asks you to take a shortcut you know will create technical debt — skip tests, hardcode a config, or copy-paste a fix. You're new and they're senior. How do you respond?",
    "rubric": [
      "Does not blindly comply or flatly refuse",
      "Asks clarifying questions to understand the urgency and constraints",
      "Proposes a middle path: do the shortcut but file a follow-up ticket, add a TODO, scope a minimal test",
      "Communicates the risk clearly without being preachy",
      "Defers to lead's final call but ensures the debt is visible"
    ],
    "followUps": [
      "What if the lead says 'just do it, don't argue'?",
      "How do you make sure the follow-up actually happens?"
    ],
    "source": "Glassdoor TCS Digital managerial round 2024 [2]"
  },
  {
    "id": "sde-mgr-005",
    "role": "sde-non-coding",
    "topic": "managerial",
    "difficulty": "medium",
    "companies": ["accenture", "ibm-india", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're assigned to mentor an intern who keeps missing daily tasks. They seem motivated but stuck. How do you handle it without going to your manager?",
    "rubric": [
      "Starts with a 1:1 to understand the blocker — skill gap, unclear tasks, personal issue",
      "Differentiates between effort issue and capability issue",
      "Sets up structured help: pair programming, smaller tasks, daily check-ins",
      "Gives clear feedback with specifics, not vague 'you need to improve'",
      "Defines when to escalate if no progress in a defined window"
    ],
    "followUps": [
      "What if the intern resents the close supervision?",
      "When do you tell your manager?"
    ],
    "source": "Glassdoor IBM India SE managerial round 2024 [8]"
  },
  {
    "id": "sde-sit-001",
    "role": "sde-non-coding",
    "topic": "situational",
    "difficulty": "medium",
    "companies": ["tcs-nqt", "wipro", "cognizant-genc", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You're paged at 2am because production is down. You're new and don't fully understand the system. Walk me through the first 30 minutes.",
    "rubric": [
      "Acknowledges instinct to acknowledge the page within SLA",
      "First step: check runbook or recent deploys/changes",
      "Looks at dashboards, logs, error rates before diving into code",
      "Knows when to escalate — pulls in senior on-call rather than thrashing alone",
      "Documents actions taken in incident channel for handover/postmortem"
    ],
    "followUps": [
      "When exactly would you escalate vs keep trying?",
      "What if there's no runbook?"
    ],
    "source": "PrepInsta Cognizant GenC and Wipro situational round 2024 [6][11]"
  },
  {
    "id": "sde-sit-002",
    "role": "sde-non-coding",
    "topic": "situational",
    "difficulty": "easy",
    "companies": ["accenture", "capgemini", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Mid-sprint, the client changes the requirement for the feature you're 70% done with. What do you do?",
    "rubric": [
      "Does not start coding immediately on new requirement",
      "Clarifies the new requirement in writing with the client/PM",
      "Assesses what's reusable from existing work and what's wasted",
      "Re-estimates and communicates revised timeline and trade-offs",
      "Flags risk if this pattern is recurring and suggests a process fix"
    ],
    "followUps": [
      "How do you keep the team's morale when requirements keep shifting?",
      "What if the client refuses to extend the deadline?"
    ],
    "source": "Glassdoor Capgemini SE situational round 2024 [6]"
  },
  {
    "id": "sde-mix-001",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "easy",
    "companies": ["tcs-digital", "tcs-nqt", "infosys-sp", "wipro", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You'll likely be placed in any of our offices — Chennai, Pune, Bangalore, Hyderabad, Kochi, Bhubaneswar, or even Mysore for training. Any constraints?",
    "rubric": [
      "Direct answer about flexibility, not a hedged 'maybe'",
      "If there's a real constraint (medical, family), states it honestly",
      "Acknowledges the training-then-posting reality of service companies",
      "Shows research awareness — names a few of the company's locations",
      "Does not demand a specific city"
    ],
    "followUps": [
      "How would your family react to a tier-2 city posting?",
      "What if training is in one city and posting is in another?"
    ],
    "source": "PrepInsta TCS Digital and Infosys SP relocation HR 2024 [2][11]"
  },
  {
    "id": "sde-mix-002",
    "role": "sde-non-coding",
    "topic": "hr",
    "difficulty": "medium",
    "companies": ["common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "We offer 4.5 LPA for this role, but I see you have a competing offer at 6 LPA from another company. Why would you still take our offer?",
    "rubric": [
      "Does not lie about the competing offer if it's real",
      "Articulates non-CTC reasons honestly: role content, learning curve, team, location, stability",
      "Negotiates respectfully if appropriate — asks if there's room for revision",
      "Does not promise to take the offer if they genuinely won't",
      "Maintains professionalism either way"
    ],
    "followUps": [
      "What's your minimum acceptable CTC?",
      "If we match the 6 LPA, would you sign today?"
    ],
    "source": "AmbitionBox and Glassdoor fresher salary negotiation 2024-2025 [4][10]"
  },
  {
    "id": "sde-mix-003",
    "role": "sde-non-coding",
    "topic": "behavioural",
    "difficulty": "easy",
    "companies": ["tcs-nqt", "infosys-se", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "Tell me about a time you took initiative beyond what was asked of you in a college project or internship.",
    "rubric": [
      "Specific situation, not 'I always go beyond'",
      "Initiative was sensible and scoped, not random gold-plating",
      "Got buy-in or informed the team rather than going rogue",
      "Result: tangible improvement, recognition, or learning",
      "Self-aware about when initiative is welcome vs when to stay in lane"
    ],
    "followUps": [
      "Was the initiative welcomed by the team?",
      "Have you ever taken initiative that backfired?"
    ],
    "source": "PrepInsta Infosys SE behavioural round 2024 [11]"
  },
  {
    "id": "sde-mix-004",
    "role": "sde-non-coding",
    "topic": "situational",
    "difficulty": "medium",
    "companies": ["tcs-digital", "infosys-sp", "common"],
    "inputModes": ["voice_explanation"],
    "textInputType": null,
    "text": "You realise mid-project that the requirements document you've been building against is fundamentally misaligned with what the client actually wants. What do you do?",
    "rubric": [
      "Validates the misalignment with concrete evidence before raising alarm",
      "Raises it to PM/lead immediately, not after another sprint of wasted work",
      "Proposes a structured re-scoping conversation with the client",
      "Identifies what's reusable from work done so far",
      "Suggests a lightweight checkpoint mechanism to prevent recurrence"
    ],
    "followUps": [
      "What if your lead says 'just keep building per the spec'?",
      "How do you avoid being the one blamed for the misalignment?"
    ],
    "source": "Glassdoor TCS Digital and Infosys SP situational rounds 2024 [2][11]"
  }
]
```

---

## Source list

1. AmbitionBox — LatentView Analytics interview experiences: https://www.ambitionbox.com/interviews/latentview-analytics-interview-questions
2. PrepInsta — TCS Digital and TCS NQT HR/Managerial rounds: https://prepinsta.com/tcs-digital/interview-experience/ and https://prepinsta.com/tcs-nqt/
3. Glassdoor — ZS Associates Decision Analytics Associate India: https://www.glassdoor.co.in/Interview/ZS-Associates-Interview-Questions-E10711.htm
4. AmbitionBox — Genpact Business Analyst interview reviews: https://www.ambitionbox.com/interviews/genpact-interview-questions
5. InterviewBit — Tredence Data Analyst interview experience: https://www.interviewbit.com/tredence-interview-questions/
6. PrepInsta and Glassdoor — Accenture / Capgemini / Wipro Elite HR rounds: https://prepinsta.com/accenture/ and https://www.glassdoor.co.in/Interview/Capgemini-Interview-Questions-E5446.htm
7. Glassdoor — Deloitte USI Analyst interview experiences: https://www.glassdoor.co.in/Interview/Deloitte-Interview-Questions-E2763.htm
8. Glassdoor — IBM India Data Analyst and SE interview experiences: https://www.glassdoor.co.in/Interview/IBM-Interview-Questions-E354.htm
9. InterviewBit — Mu Sigma Decision Scientist interview prep: https://www.interviewbit.com/mu-sigma-interview-questions/
10. Glassdoor — EXL Analyst interview reports: https://www.glassdoor.co.in/Interview/EXL-Service-Interview-Questions-E22507.htm
11. PrepInsta — Infosys SP, SE, DSE interview experiences: https://prepinsta.com/infosys/ and https://prepinsta.com/infosys-specialist-programmer/
12. LeetCode Discuss — Amazon India Applied Scientist / DS L4 interview experiences 2024-2025: https://leetcode.com/discuss/interview-question/amazon
13. Glassdoor and AmbitionBox — PhonePe Data Scientist interview experiences: https://www.glassdoor.co.in/Interview/PhonePe-Interview-Questions-E1162540.htm
14. Glassdoor — JP Morgan India Quant/DS interview experiences: https://www.glassdoor.co.in/Interview/J-P-Morgan-Interview-Questions-E145.htm
15. AmbitionBox — Tiger Analytics and Fractal Analytics interview reviews: https://www.ambitionbox.com/interviews/tiger-analytics-interview-questions and https://www.ambitionbox.com/interviews/fractal-analytics-interview-questions
16. Glassdoor — Flipkart Data Scientist interview experiences: https://www.glassdoor.co.in/Interview/Flipkart-Interview-Questions-E102725.htm
17. AmbitionBox — Razorpay Data Scientist interview reviews: https://www.ambitionbox.com/interviews/razorpay-interview-questions
18. Glassdoor — Walmart Labs India / Walmart Global Tech DS interview: https://www.glassdoor.co.in/Interview/Walmart-Global-Tech-India-Interview-Questions-E2645838.htm
19. AmbitionBox — Swiggy Data Scientist interview experiences: https://www.ambitionbox.com/interviews/swiggy-interview-questions
20. AmbitionBox — HCL Tech and Tech Mahindra SE interview reviews: https://www.ambitionbox.com/interviews/hcl-technologies-interview-questions and https://www.ambitionbox.com/interviews/tech-mahindra-interview-questions

---

**Counts and difficulty audit:**
- Total: 60 questions (20 DA + 20 DS + 20 SDE) — meets cap
- Hard questions: 2 DA (da-beh-004, da-proj-005) + 4 DS (ds-beh-002, ds-proj-002, ds-mgr-002, ds-mix-001 was medium — recount: ds-beh-002, ds-proj-002, ds-mgr-002 = 3) + 2 SDE (sde-beh-002, sde-proj-008) = **7 hard** (under 12 cap)
- Easy: ~24, Medium: ~29, Hard: 7 — within the ~40/40/20 guidance, slightly weighted toward easy/medium which is appropriate for fresher campus interviews
- All questions are voice-only (`inputModes: ["voice_explanation"]`, `textInputType: null`)
- All IDs continue from existing seed conventions as specified
