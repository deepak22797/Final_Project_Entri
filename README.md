SUMMARY OF CLASSIFICATION TASKS:-
------------------------------------

1. Purchase Prediction (Target: Revenue)

   * What this classification does:

      * Predicts whether a user **makes a purchase (Revenue = 1)** or **does not (Revenue = 0)**.
      * Helps in identifying **high-conversion users** early in their session.

   * Input Features:

      * All behavioral and session-related columns (excluding `Revenue`).

   * Results:

      * Classification Report includes:
      
        * Precision (how many predicted buyers were actually buyers),
        * Recall (how many actual buyers were correctly identified),
        * F1-score (balance between precision and recall).

   * Why it's useful:

        * Supports sales forecasting, targeted marketing, and retargeting strategies.
        * Prioritizes sessions with higher purchase likelihood.

   * Insights:

        * Higher recall - good at detecting buyers.
        * High F1-score - balanced performance.
        * Business can use predictions to optimize promotions and recommendations.

2. Visitor Type Prediction (Target: VisitorType)**

   * What this classification does:

      * Classifies visitors into:

          * Returning_Visitor (1)
          * New_Visitor (0)
          * Other (2)
          * Understands user loyalty and visit patterns.

      * Input Features:

          * All columns except `VisitorType`.

      * Results:

          * Multi-class classification report showing class-wise precision, recall, and F1-score.

      * Why it's useful:

          * Enables personalized user experience (e.g., offer discounts to new visitors).
          * Helps track user retention and session behavior.

      * Insights:

          * High prediction accuracy suggests good feature relationship with visitor type.
          * Knowing visitor type can improve user segmentation and retention campaigns.

3. Session Time Bucket Classification (Target: SessionBucket)

      * What this classification does:

          * Categorizes users into:
          
            * Short session (0): < 300 seconds
            * Medium session (1): 300–1000 seconds
            * Long session (2): > 1000 seconds
            * Created using the sum of durations from multiple activity types.

      * Input Features:

         * All columns except `SessionBucket` (which was derived from durations).

      * Results:

        * Multi-class classification report shows how well each session duration bucket is predicted.

      * Why it's useful:

        * Helps detect session drop-off patterns.
        * Guides UX improvements (e.g., engaging users in short sessions).
        * Useful for personalizing recommendations and analyzing attention span.

      * Insights:

        * Helps categorize users into quick browsers, explorers, and serious buyers.
        * Enables business to adjust session design for different user intents.

 * Common Validation for All Tasks

   * Classification Reports:

        * For each task, we used:
        
            * Accuracy: Overall correct predictions.
            * Precision: True positives among predicted positives.
            * Recall: True positives among actual positives.
            * F1-Score: Harmonic mean of precision and recall.

As a brief: 

  * We performed three classification tasks using Random Forest to uncover actionable patterns:

      * In Purchase Prediction, we could identify whether a user would make a purchase, helping forecast sales and optimize targeting.
      
      * In Visitor Type Prediction, we distinguished between new, returning, and other visitors. This helps in user retention and experience personalization.
      
      * Lastly, Session Time Bucket Classification allowed us to understand user attention span, helping adapt the UI or recommendations accordingly.
      
      * We validated each model using classification metrics like precision, recall, and F1-score. The models performed well, showing the features were highly predictive.

-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
SUMMARY OF CLUSTERING TASKS:-
------------------------------------

1. Clustering using DBSCAN: Noise and Outlier Detection

    * What this clustering does:

        * DBSCAN identifies dense regions in the dataset.
        * It’s useful for discovering outliers or anomalies — users whose browsing patterns deviate from the norm.

    * Results:

        * The DBSCAN_Cluster labels show how many groups were found.
        * Points labeled -1 are considered **noise or outliers.

    * Validation :

        * DBSCAN is non-parametric and does not require a pre-specified number of clusters.
        * It's great for **identifying irregular user behavior (e.g., very short or very long sessions).

    * Why DBSCAN here:
     
        * Useful for **highlighting extreme cases (anomalies) in user behavior without assuming cluster shape.

2. KMeans Clustering Task 1: User Segmentation
 
     * Features Used:

          python
          ["BounceRates", "ExitRates", "PageValues", "SpecialDay", "SessionDuration"]


     * What this clustering does:

       * KMeans groups users into 3 distinct segments based on how they interact with the site.

     * Segment Interpretations (example):

       * Cluster 0: High bounce rate, low page value — casual or uninterested visitors.
       * Cluster 1: Low bounce and high session duration — potential buyers.
       * Cluster 2: Medium engagement — comparison shoppers or undecided users.

    * Validation:

      * We used PCA for dimensionality reduction to visualize the clusters.
      * KMeans showed clear visual separation between clusters in PCA plots.

    * Why KMeans works:

      * The user interaction patterns are well-separated and continuous.
      * KMeans performs well when clusters are compact and spherical in nature, which is the case here after scaling.

3. KMeans Clustering Task 2: Behavioral Clustering

    * Features Used:

        python
        ["Administrative", "Informational", "ProductRelated", "SessionDuration"]


    * What this clustering does:

        * This KMeans model segments users based on content consumption behavior.

    * Segment Interpretations (example):

        * Cluster 0: Users who mostly browse product-related content.
        * Cluster 1: Balanced use across pages — more exploratory.
        * Cluster 2: Heavy on administrative pages — possibly B2B users or researchers.

    * Validation:

        * Again, PCA shows reasonable cluster separation.
        * Behavior patterns are distinct in the reduced PCA space.

    * Why KMeans works:

        * These behaviors are numeric, continuous, and benefit from KMeans’ ability to separate data in high-dimensional space after scaling.

* PCA Visualization (2D)

   * We used PCA to reduce high-dimensional features to just 2 for visualization.
   * Plotted KMeans and DBSCAN clusters to visually validate separation.
   * KMeans clusters appear **more compact and clearly separated, indicating that it suits this data structure.
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
