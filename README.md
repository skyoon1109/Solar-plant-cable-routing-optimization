# 🏆Cable routing optimization for large scale solar plant
- 1st place, AI/OR Business Challenge, Korean Operations Research and Management Science Society (KORMS)
- Research used Capacitated K-means algorithm and MILP to optimize solar power plant cable routing
- Implemented Capacitated K-means for clustering solar panels with capacity constraints
- Applied Mixed Integer Linear Programming with no-crossing constraints to minimize costs
- Achieved 13.2% cost reduction ($87,825 USD savings across 17 instances)
- Significantly reduced execution time compared to manual methods
- Methodology applicable to other renewable energy infrastructure including wind farms

# 🖥️Code files


# 1️⃣Capacitated K-means for grouping solar panels
- Capacitated K-means is an extension of traditional K-means clustering algorithm with capacity constraints
- Solves the Capacitated Clustering Problem (CCP) by limiting the number of data points per cluster
- Designed to create balanced clusters where each junction box can connect maximum 8 solar panels
- Process includes initialization, cluster assignment respecting capacity limits, centroid recalculation
- Uses Euclidean distance to assign points to nearest clusters without exceeding capacity
- Critical for solar panel grouping to optimize cable connections while maintaining balanced load distribution

![Image](https://github.com/user-attachments/assets/e4f78b36-304b-414f-b692-d6c339743f7c)
<img src="https://github.com/user-attachments/assets/e4f78b36-304b-414f-b692-d6c339743f7c"  width="200" height="400"/>
