## Union Find

### Applications
- Pixels in a picture
- Computers in a network
- Friends in a social network

### Simple situation
Given a set of objects
- 
```
UF(int N) // initialize the data structure with all objects
void union(int p, int q) // connect two objects
boolean connected(int p, int q) // are two objects connected
//Find the whole component from a single object.
int count() // number of components
```

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
    // O(n)
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
    // 
    private int root(int i){
        int root;
        while (id[i] != i){
            i = id[i];
        }
        return i;
    }
    // O(1)
    public boolean connected(int p, intq){
        return id[p] == id[q];
    }
    // O(n) - *2N+2 array acesses*
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