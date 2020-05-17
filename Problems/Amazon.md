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
       - For 2d grid, ***k = r\*nc + c***

## 130. Surrounded Regions
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.
A region is captured by flipping all 'O's into 'X's in that surrounded region.

### Idea
- my idea: 
   - iterate every node, Wrong!!!!
      - find component and change all 'O's to 'M'
      - change surrounded components 'M' to 'X'  Wrong!!!!!!
   - change 'M' to 'O'
    
-  correct idea:
   - iterate every boundary node
       - find component connected with boundary node, change 'O' to 'M'
   - change 'O' to 'X', change 'M' to 'O'

### Important points
- how to iterate boundary nodes
- change node to avoid repeatedly visiting