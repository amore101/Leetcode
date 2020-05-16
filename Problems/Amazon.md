## 200. Number of Islands
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Key ideas
- Use what data structure to store an whole island.
   - Use 2-dimension array to represent island with many nodes.
- How to find all connected nodes from one node.
   - Nodes next to the land node (up, down, left, right).
- How to avoid repeat counting.
   - Change land nodes to water nodes after this island is counted.

### Solutions
- DFS
   - Solve the whole layer(4 nodes) at one time.
- BFS
   - Solve every node separately in each layer.
   - Because of using queue, consider what to store in the queue to tranfer the node.