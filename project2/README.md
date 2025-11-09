# Hotel Customer Segmentation and Revenue Analysis

## Goal

This project segments hotel customers based on their booking behaviour and revenue contribution. The aim is to:

- Identify distinct customer groups,
- Understand how they differ in age, stay characteristics and spending, and
- Provide data-driven recommendations on which segments to target and how.

The analytical logic (segmenting users and linking segments to value) is directly relevant to player segmentation in games.

## Data

- **Source:** Hotel customer dataset.
- **Unit of analysis:** Individual hotel customers.
- **Key variables (examples):**
  - Demographics: `Age`
  - Booking behaviour: `AverageLeadTime`, `DaysSinceCreation`, `DaysSinceFirstStay`, `DaysSinceLastStay`
  - Stay characteristics: `PersonsNights`, `RoomNights`
  - Revenue: `LodgingRevenue` (room-related), `OtherRevenue` (ancillary services: F&B, spa, etc.)

Records with invalid or missing values (e.g. non-numeric ages) were filtered out, and all numeric variables were scaled prior to clustering.

## Methods & Tools

- **Language:** R
- **Key packages:** `tidyverse`, `cluster`, `factoextra`, `ggplot2`, `gt`
- **Steps:**
  1. **Data cleaning & preparation**
     - Converted fields to numeric where appropriate.
     - Removed unrealistic or missing ages.
     - Selected a subset of behaviour and revenue variables for clustering.
     - Standardised (scaled) the features so all variables contribute comparably.
  2. **Choosing the number of clusters**
     - Applied **k-means clustering** for k = 1–10.
     - Used:
       - **Elbow method** (total within-cluster sum of squares) and
       - **Average silhouette width**
       to evaluate solutions.
     - Both diagnostics suggested **k = 4** as a good balance between fit and parsimony.
  3. **4-cluster k-means solution**
     - Fitted a k-means model with 4 clusters on the scaled data.
     - Inspected cluster sizes and within-cluster cohesion.
     - Visualised clusters in a **PCA projection** for interpretability.
  4. **Cluster profiling**
     - Computed per-cluster means for age, lead time, stay length and revenues.
     - Created bar charts and tables summarising each cluster’s profile.
  5. **Revenue analysis & recommendations**
     - Compared **average lodging** and **ancillary revenue** by cluster.
     - Identified high-value and under-monetised segments.
     - Developed targeted positioning and loyalty recommendations based on the profiles.

## Key Insights

- A **4-cluster solution** provides a clear and interpretable segmentation of hotel customers.
- One cluster consists of **middle-aged guests with long stays and very high lodging and ancillary revenue**, making them the most valuable segment for premium loyalty programs and upselling.
- Another cluster includes **older guests who book far in advance but generate relatively low revenue**, representing an opportunity to increase ancillary spending through tailored packages and personalised communication.
- The remaining clusters differ in booking horizon, stay length and revenue, illustrating diverse customer needs and behaviours.
- The segmentation supports **concrete marketing and retention strategies**, such as:
  - Loyalty programs and pre-arrival offers for high-value guests.
  - Senior-friendly, themed packages to unlock more value from early-booking seniors.

## Files

- `analysis.Rmd` – full R code for:
  - data cleaning and scaling  
  - k-means clustering for multiple k  
  - elbow and silhouette diagnostics  
  - 4-cluster k-means solution and PCA visualisation  
  - cluster profiling and revenue analysis
- Optional figures:
  - Elbow and silhouette plots 
  - Bar charts of cluster sizes and revenue per cluster  
  - Tables with cluster statistics (means, medians, 95% CIs).
