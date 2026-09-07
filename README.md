# 📊 Snapdeal Customer Insights & Segmentation Analysis

An analysis of customer purchasing behavior survey data (800 respondents, 24 fields) to clean the dataset, understand purchasing patterns, segment customers, and generate actionable recommendations on retention, recommendations, and reviews.

**Note on the dataset:** some source column descriptions in the raw survey retain "Amazon" references from the original template. All analysis in this project is framed and interpreted under the Snapdeal context per the assignment brief.

## 📋 Problem Statement

- What data quality issues exist in the raw survey, and how were they resolved?
- What do customer demographics and purchase behavior reveal about the platform?
- Can customers be meaningfully segmented to identify retention risk?
- What drives recommendation and review satisfaction, and how should the business act on it?

## 🔄 Pipeline

| Task | File | Description |
|---|---|---|
| **Task 1 — Data Cleaning & Preparation** | `Task_1.ipynb` | Resolved duplicate columns, standardized casing, handled 149 missing values and junk placeholder entries (`.` → `Not Specified`), verified 0 duplicate rows |
| **Task 2 — Descriptive Behavior Analysis** | `Task_2.ipynb` | Demographics, purchase frequency, product category popularity, and cart abandonment analysis |
| **Task 3 — Customer Segmentation & Profiling** | `Task_3.ipynb` | Rule-based segmentation + K-Means clustering (unsupervised) on behavioral features |
| **Task 4 — Recommendation & Review Insights** | `Task_4.ipynb` | Analysis of recommendation frequency vs. helpfulness, and review/rating trust dynamics |
| **Task 5 — Visualization** | `Task_5.ipynb` | Supporting charts for product categories, browsing frequency, satisfaction, and recommendation-usefulness trends |
| **Cleaned Dataset** | `Snapdeal_Cleaned.xlsx` | Final cleaned dataset used across all analysis |
| **Full Report** | `Snapdeal_Project_Summary_VideoLink.pdf` | Complete write-up with visualizations and a video walkthrough link |

## 🧹 Key Data Quality Fixes (Task 1)

| Issue Found | Fix Applied |
|---|---|
| Duplicate column name (`Personalized_Recommendation_Frequency`) | Renamed numeric version to `*_Numeric` |
| `Product_Search_Method` — 149 missing + inconsistent casing | Standardized casing, filled missing as "Unknown" |
| Hidden trailing whitespace across text columns | Regex word-boundary replace |
| `.` used as junk/placeholder answers (89+38 rows) | Replaced with NaN, then "Not Specified" |
| 0 duplicate rows | Verified via `.duplicated().sum()` |

## 🔍 Key Findings

**Demographics:** No dominant gender group found (Male 26.6%, Female 25.1%, Prefer not to say 24.2%, Others 24.0%). Age distribution was found to be artificially uniform (3–67, no natural clustering) — treated as an unreliable variable throughout the analysis rather than used for segmentation.

**Purchase Behavior:** Clothing & Fashion is the top product category (476 mentions), followed by Beauty & Personal Care (414). **The leading cause of cart abandonment is price competitiveness (27.4%)** — a platform-wide, actionable insight ahead of shipping cost and changed intent.

**Customer Segmentation (Rule-Based):**

| Segment | Count | % of Customers |
|---|---|---|
| Occasional Shopper | 352 | 44.0% |
| At-Risk Customers | 320 | 40.0% |
| Frequent Buyer | 128 | 16.0% |

More customers are At-Risk (40%) than Frequent Buyers (16%) — Snapdeal's retention problem outweighs its current loyalty base.

**K-Means Clustering (Unsupervised):** Applied to Purchase Frequency, Shopping Satisfaction, Customer Review Importance, and Rating Accuracy. Optimal K=4 selected via the Elbow Method. **Key insight the manual rules missed:** frequency and satisfaction don't always move together — At-Risk customers buy fairly often yet report the lowest satisfaction of any group, despite trusting ratings highly.

**Recommendations & Reviews:** No meaningful trend between recommendation frequency and perceived helpfulness (scores narrowly ranged 1.86–2.06 on a 1–3 scale) — showing recommendations more often doesn't make them feel more useful. Recommendations, reviews, and ratings behave as largely independent systems.

## 💡 Business Recommendations

1. **Fix pricing competitiveness first** — the single largest lever for reducing cart abandonment, benefiting all segments roughly equally
2. **Prioritize retention over loyalty growth** — the At-Risk segment (40%) is a bigger opportunity than growing Frequent Buyers (16%)
3. **Improve recommendation relevance, not frequency** — starting with the At-Risk segment specifically, since they report the lowest recommendation satisfaction
4. **Exclude age from targeting/segmentation** — the field shows signs of being randomly generated rather than reflective of real customers
5. **Use the K-Means "At-Risk Regulars" signal** (high purchase frequency + low satisfaction) as the starting point for future targeted retention campaigns

## 🎥 Full Report & Video Walkthrough

Full write-up with all visualizations: [`Snapdeal_Project_Summary_VideoLink.pdf`](./Snapdeal_Project_Summary_VideoLink.pdf)
Video walkthrough: linked inside the report

## 🛠️ Tools & Technologies

Python (Pandas, NumPy, scikit-learn, Matplotlib) · Jupyter Notebook · K-Means Clustering · Rule-Based Segmentation
