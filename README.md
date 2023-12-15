# py-Graphs

import networkx as nx
import matplotlib.pyplot as plt

# Your actual dataset - Replace these with your actual data
years = [2019, 2020, 2021, 2022, 2023]
research_types = [
    'Research articles',
    'Review articles',
    'Encyclopedia',
    'Book chapters',
    'Conference abstracts',
    'Case study'
]

research_counts = {
    'Research articles': [338, 388, 402, 416, 461],
    'Review articles': [45, 43, 62, 76, 80],
    'Encyclopedia': [18, 5, 13, 34, 14],
    'Book chapters': [102, 82, 89, 110, 100],
    'Conference abstracts': [21, 7, 6, 3, 2],
    'Case study': [0, 1, 1, 3, 4]
}

# Calculate total publications for each research category
total_publications = {research_type: sum(counts) for research_type, counts in research_counts.items()}

# Create a directed graph
G = nx.DiGraph()

# Add nodes for years and research types to the graph with adjusted node sizes
for research_type, total_count in total_publications.items():
    G.add_node(research_type, node_type='ResearchType', size=total_count * 10)

# Define the edges (relationships) with the number of publications as weights
for i, year in enumerate(years):
    for research_type, counts in research_counts.items():
        G.add_edge(year, research_type, weight=counts[i])

# Draw the graph with adjusted node sizes
plt.figure(figsize=(12, 8))
pos = nx.spring_layout(G, seed=42)

# Get node sizes from node attributes
node_sizes = [G.nodes[research_type]['size'] for research_type in research_types]

# Draw nodes and edges separately to set different node sizes
nx.draw_networkx_nodes(G, pos, node_size=[size * 100 for size in node_sizes], node_color='skyblue')
nx.draw_networkx_labels(G, pos, font_weight='bold', font_size=10)
nx.draw_networkx_edges(G, pos, edge_color='red')

# Display edge weights
edge_labels = {(u, v): d['weight'] for u, v, d in G.edges(data=True)}
nx.draw_networkx_edge_labels(G, pos, edge_labels=edge_labels, font_color='black')

plt.title('Relationship of Research Studies on Press Mud (2019-2023)')
plt.axis('off')
plt.show()
