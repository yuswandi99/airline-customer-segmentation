# Airline Customer Segmentation — K-Means Clustering (LRFMC)

Segments **61,871 frequent-flyer members** with K-Means and the **LRFMC model** (Length, Recency, Frequency, Monetary, Discount). Each segment gets its own marketing strategy, so the airline does not have to spread discounts evenly across everyone.

## Dataset
- **Airline frequent flyer program data** (public dataset): 62,988 rows × 23 columns
- 61,871 rows remain after cleaning

## Tools
Python · Pandas · NumPy · Scikit-learn (KMeans, PCA, StandardScaler) · Matplotlib · Seaborn

## Workflow
1. **Data cleaning**
   - Dropped high-cardinality location columns (3,000+ unique cities) and demographic columns (age, gender), which do not reflect flight behavior
   - Removed inconsistent records (zero revenue and zero discount but a positive flight distance) following Tao (2020)
   - Dropped the remaining missing values (1.76%)
2. **Feature engineering (LRFMC)**

   | | Feature | Meaning |
   |---|---|---|
   | L | `TIME_MONTH` | Membership length (months) |
   | R | `LAST_TO_END` | Time since last flight |
   | F | `FLIGHT_COUNT` | Number of flights |
   | M | `SEG_KM_SUM` | Total distance flown |
   | C | `avg_discount` | Average discount factor |
3. **Transformation**: log transform for skewed features, square-root transform for recency, then StandardScaler
4. **Choosing k**: Elbow method and Silhouette score (candidates k = 2, 4, 5). Clusters were visualized with PCA.
5. **Final model**: **k = 5**, which gives the most actionable segments (every segment is larger than 12%)

## Customer Segments
| Cluster | Segment | Profile | Share | Strategy |
|---|---|---|---|---|
| 2 | **Core Loyalists** | ~7 years as members, median 25 flights, flew ~20 days ago | 12.6% | Exclusive rewards (lounge, priority boarding, upgrades). Avoid large discounts. |
| 0 | **Rising Flyers** | Newer members (~2.7 years) with high activity | ~25% | Bonus points and faster tier upgrades to grow them into loyalists |
| 3 | **Drifting Veterans** | Long-time members, but activity is only at the median | — | Personal reminders and offers on routes they have flown before |
| 1 | **Discount Hunters** | Almost a year since last flight, ~3 flights, highest discount (0.85) | ~20% | Time-limited win-back discounts with a capped budget |
| 4 | **Passive New Members** | New and not yet active | **27.2%** (largest) | Activation with first- or second-flight promos and onboarding |

## Key Insights
- About **48% of members are passive or at risk** (clusters 1 + 4), so there is a lot of room for reactivation.
- **Recency and activity separate the segments**, not discount (0.60–0.85 across segments).
- **Drifting Veterans are the cheapest segment to save**: they are still recent enough to win back before they become Discount Hunters.

## Repository Structure
```
airline-customer-segmentation/
├── airline_customer_clustering.ipynb   # full analysis (narrative in Bahasa Indonesia)
└── README.md
```

## How to Run
1. Open the notebook in Google Colab or Jupyter
2. Upload `flight.csv`, then run all cells

## Reference
Tao, Y. (2020). *Analysis Method for Customer Value of Aviation Big Data Based on LRFMC Model.*

---
**Author:** Andi Yuswandi · [GitHub](https://github.com/yuswandi99)
