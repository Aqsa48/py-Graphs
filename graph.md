import networkx as nx
import matplotlib.pyplot as plt

# Provided data
data = {
    'Research articles': [45, 43, 62, 76, 459],
    'Review articles': [338, 388, 402, 416, 80],
    'Encyclopedia': [18, 5, 13, 34, 13],
    'Book chapters': [102, 82, 89, 110, 100],
    'Conference abstracts': [21, 7, 6, 3, 2],
    'Data articles': [1, 1, 2, 0, 0],
}

years = [2019, 2020, 2021, 2022, 2023]

# Create a directed graph
G = nx.DiGraph()

# Add nodes for platforms and years
for platform in data.keys():
    G.add_node(platform)
for year in years:
    G.add_node(year)

# Add edges based on the provided data
for platform, counts in data.items():
    for i, count in enumerate(counts):
        G.add_edge(platform, years[i], weight=count)

# Draw the network graph
plt.figure(figsize=(10, 8))
pos = nx.spring_layout(G, seed=42)
nx.draw(G, pos, with_labels=True, node_size=800, node_color='skyblue', font_weight='bold', font_size=10)
plt.title("Network Graph of Press Mud Data Across Platforms and Years")
plt.show()
