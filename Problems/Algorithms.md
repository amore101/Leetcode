## Union Find
The most important thing is how to find an algoritm and improve it.

### Applications
- Pixels in a picture
- Computers in a network
- Friends in a social network

### Simple situation
Given a set of objects:
- UF(int N): initialize the data structure with all objects
- void union(int p, int q): connect two objects
- boolean connected(int p, int q): are two objects connected
- int find(int p): find the whole component from a single object.
- int count(): number of components

### Quick Find
**Use array (index, value) to store the objects and components.**
Union is costly: Takes N<sup>2</sup> array accesses to process sequence of N union commands on N objects.
```
public class QuickFindUF(){
    private int[] id;
    // O(n)
    public QuickFindUF(int N){
        id = new int[N];
        for (int i=0; i<N; i++){
            id[i] = i;
        }
    }
    // O(1)
    public boolean connected(int p, intq){
        return id[p] == id[q];
    }
    // O(n) - 2N+2 array acesses
    public void union(int p, int q){
        int pid = id[p];
        int qid = id[q];
        for (int i=0; i<N; i++){
            if (id[i] == pid){
                id[i] = qid;
            }
        }
    }
}
```

### Quick-union
**Use array (index, value) to store the objects and the parent of the object.**
All operations happen on the root object.
Find is costly.
```
public class QuickFindUF(){
    private int[] id;
    // O(n)
    public QuickFindUF(int N){
        id = new int[N];
        for (int i=0; i<N; i++){id[i] = i;}
    }
    // find the root 
    // Depth of the tree, O(n) in worst case
    private int root(int i){
        int root;
        while (id[i] != i){i = id[i];}
        return i;
    }
    // O(1)
    public boolean connected(int p, intq){
        return id[p] == id[q];
    }
    // change the root O(n) - cost of finding
    public void union(int p, int q){
        int i = root(p);
        int j = root(q);
        id[i] = j;
    }
}
```

### Weighted Quick-union
**Use array (index, value) which is same as Quick-union, an extra array to store the size.**
Make changes to avoid tall trees based on Quick-union.
Keep track of size of each tree (number of objects).
**The depth of tree is at most lgN, Why?**
When the depth increase by one, the size of the tree at least doubles from the smaller one.
```
public class QuickFindUF(){
    private int[] id;
    private int[] size;
    // O(n)
    public QuickFindUF(int N){
        id = new int[N];
        size = new int[N];
        for (int i=0; i<N; i++){id[i] = i; size[i] = 1;}
    }
    // find the root 
    // Depth of the tree, O(lgN) in worst case
    private int root(int i){
        int root;
        while (id[i] != i){i = id[i];}
        return i;
    }
    // O(1)
    public boolean connected(int p, intq){
        return id[p] == id[q];
    }
    // change the root O(lgN) - cost of finding
    public void union(int p, int q){
        int i = root(p);
        int j = root(q);
        if (i == j) return;
        if (size[i] < size[j]){id[i] = j; size[j] += size[i];}
        else {id[j] = i; size[i] += size[j];}
    }
}
```

### Path compression
Simpler one-pass variant: make every other node in this path point to its grandparent.
Only one extra line can half the path length.
```
    private int root(int i){
        int root;
        while (id[i] != i){
            id[i] = id[id[i]];
            i = id[i];
        }
        return i;
    }
```
![Time Cost](Images/Union.png)