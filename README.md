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

![image](https://github.com/user-attachments/assets/85c100d5-08e7-4dc0-bd4b-fedc0abaf421)

# 2️⃣MIP Model
$$\text{Min} \qquad \sum_{(i, j) \in A} \sum_{t \in T} c_{i,\, j}^{t} \, x_{i,\, j}^t + \sum_{k \in V_{0}} a_{k} u_{k}$$ **(1)**

$$\text{s.t.} \qquad \sum_{t \in T} x_{i,\, j}^{t} = y_{i,\, j}, \quad \forall (i, j) \in A $$ **(2)**

$$\sum_{i \in V : i \ne h} \left( f_{h,\, i} - f_{i,\, h} \right) = P_{h}, \quad \forall h \in V_{T}  $$ **(3)**

$$\sum_{t \in T} k_t \ x_{i,\, j}^{t} \ge f_{i,\, j}, \quad \forall (i, j) \in A $$ **(4)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 1, \quad \forall h \in V_{T} $$ **(5)**

$$\sum_{j \in V : j \ne h} y_{h,\, j} = 0, \quad \forall h \in V_{0}$$ **(6)**

$$\sum_{k \in V_{0}} u_{k} = 1$$ **(7)**

$$y_{i, j} \le u_j, \quad i \in V_T, \; j \in V_{0} $$ **(8)**


$$x_{i, j}^t \in \{0, 1 \}, \quad (i, j) \in A, \; t \in T$$ **(9)**

$$y_{i,\, j} \in \{0, 1 \}, \quad (i, j) \in A $$ **(10)**

$$f_{i,\, j} \ge 0, \quad (i, j) \in A  $$ **(11)**

$$u_{k} \in \{0, 1 \}, \quad k \in V_{0}  $$ **(12)**
