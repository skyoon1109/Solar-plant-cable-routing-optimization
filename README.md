# 🏆Cable routing optimization for large scale solar plant
- 1st place, AI/OR Business Challenge, Korean Operations Research and Management Science Society (KORMS)
- Research used Capacitated K-means algorithm and MILP to optimize solar power plant cable routing
- Implemented Capacitated K-means for clustering solar panels with capacity constraints
- Applied Mixed Integer Linear Programming with no-crossing constraints to minimize costs
- Achieved 13.2% cost reduction ($87,825 USD savings across 17 instances)
- Significantly reduced execution time compared to manual methods
- Methodology applicable to other renewable energy infrastructure including wind farms

### 💡The detailed description is all described in the pdf file.

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

- The objective function minimizes the total cost of cable connections in the solar power plant.
- The first term represents the cost of connecting PVA panels to junction boxes, and second term represents the cost of connecting selected junction boxes to inverters.
- Below is a description of the constraints.  
(2): Variable definition constraint ensuring only one cable type is selected for each connection  
(3): Flow conservation constraint ensuring the difference between incoming and outgoing flow equals 1 for each PVA node (Ph = 1, ∀h ∈ VT)  
(4): Capacity constraint ensuring flow doesn't exceed the capacity of installed cables  
(5): Constraint limiting each PVA to have exactly one outgoing cable  
(6): Constraint ensuring no outgoing cables from junction boxes  
(7): Constraint allowing only one junction box to be selected  
(8): Constraint linking variables for PVA-to-Inverter connections; ensures cables can only connect to selected junction boxes  


# 3️⃣CCW Algorithm and Lazy Constraints(To prevent crossings)
- CCW (Counter-Clock-Wise) algorithm prevents cable crossing by determining the orientation of three points
- Function calculates whether points are arranged clockwise, counter-clockwise, or collinear
- CrossingCheck function uses CCW to determine if two line segments intersect
- GetCrossingPair function identifies all crossing cable segments in the solution
- NoCrossingCallback function dynamically adds constraints during optimization to prevent crossings
- Uses "lazy constraints" to ensure selected cable segments don't cross each other
- Algorithm terminates when no more crossing segments are detected during optimization

