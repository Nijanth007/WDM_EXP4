### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 21/11/2026
### NAME: NIJANTH K
### REG: 212224230186
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```python
import pandas as pd
import matplotlib.pyplot as plt

# Read CSV file
df = pd.read_csv("clustervisitor.csv")

# Select Age feature
X = df["Age"].tolist()

# Number of clusters
k = 3

# Step 1: Choose initial centroids (first k values)
centroids = X[:k]

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    # Step 2: Assign each data point to the nearest centroid
    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    # Step 3: Calculate new centroids
    new_centroids = []
    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    # Step 4: Stop if centroids do not change
    if new_centroids == centroids:
        break

    centroids = new_centroids

# Add cluster labels to DataFrame
df["Cluster"] = labels

# Display complete dataset
print("Complete Dataset")
print(df)

print("\nVisitor Segmentation (Cluster-wise)\n")

# Display cluster-wise output
for i in range(k):
    print(f"Cluster {i}")
    print(df[df["Cluster"] == i])
    print("-" * 50)

# Visualize clusters
plt.figure(figsize=(8,6))	

colors = ["red", "blue", "green"]

for i in range(k):
    cluster_data = df[df["Cluster"] == i]
    plt.scatter(cluster_data["Age"],
                cluster_data["Cluster"],
                color=colors[i],
                s=80,
                label=f"Cluster {i}")

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()

```
### Output:
<img width="716" height="370" alt="image" src="https://github.com/user-attachments/assets/b29d8228-ed9d-419f-b46d-8d0c006ac706" />
<img width="592" height="298" alt="image" src="https://github.com/user-attachments/assets/f2f6b9a0-8c24-4f94-9ebd-c228b2e514b8" />
<img width="511" height="277" alt="image" src="https://github.com/user-attachments/assets/c240051c-a867-4ba2-a36a-1235c3c75ae0" />
<img width="536" height="237" alt="image" src="https://github.com/user-attachments/assets/be8cbb3b-0b78-4c79-8beb-230ff40e921d" />

### Visualization:

### Output:
<img width="1007" height="785" alt="image" src="https://github.com/user-attachments/assets/834feda0-3248-4ea9-a473-f9bb20d85fc2" />


### Result:
