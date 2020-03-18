# Technqiue and Algorithms Problem
## Bit Manipulation 
`I use it to find the middle element of an array given left and right most index`
```Java
middle = left + right >> 1;

Test kth bit is set: num & (1 << k) != 0.
Set kth bit: num |= (1 << k).
Turn off kth bit: num &= ~(1 << k).
Toggle the kth bit: num ^= (1 << k).
To check if a number is a power of 2, num & num - 1 == 0

```
when to use it, how to know it will help ?
``` Java
2 >> 1 = 1
5 >> 1 = 2
```
* Cannot sort in subsequence subarray problems
```Java
for(int i = arr.length-1; i > -1; --i){
	some temp var init
	for(int j = i + 1; j < arr.length ; j++){
		do something with prev seen elements
		cache the result
	}
	store the result in a cache
}
```

// above is o(n2) way of solving subsequence problem, substring problems

* Making adjency list quickly.
```Java
public List<Integer>[] getAdjacencyList(int n, int[][] prereqs) {
        List<Integer>[] list = new ArrayList[n];
        for (int[] prereq : prereqs){
            if(list[prereq[0]] == null){
                list[prereq[0]]  = new ArrayList<>();
            }
            list[prereq[0]].add(prereq[1]);
        }
       return list;
    }
```
## Handling time strings
```Java
private int convert(String str){
	// convert everything to minutes, was the trick 23:59 is how many minutes ?
        String[] split = str.split(":", 2);
        int hour = Integer.parseInt(split[0]) * 60;
        int min =  Integer.parseInt(split[1]);
        return hour + min;
    }
```
## Intervals: 
sort them based on the __start time__. 
* Meeting rooms
* Meeting rooms which uses Priority Queue

```[[1, 2], [4, 7]]```
```Java
public boolean overlap(int[] a, int[]b){
	return a[0]<b[1] &&  b[0]8i<a[1];
}

public int[] mergeInterval(int[] a , int[] b){
	return new int[]{Math.min(a[0], b[0]), Math.max(a[1], b[1])};
}
```

## Strings and arrays:
* [0, ... n-1] indexing 
* memorize the code for deletion of element in an array
* memorize the code for shift elements in an array
```Java
placesToShift = 0
int index = 0 
while(index < n){
	if(arr[index].isIn(removeList){
		placesToShift++;
	}
	else{
		arr[index - placesToShift] = arr[index];
	}
}
n = n - placesToShift;
```
* if the solution takes n^2, try to sort the array (not possible in case of subsequence and subarray problems)
* 256 length array to calculate the frequency
* if need is to deal with individual digit in an number use this.
```Java
int n = 123456789
narray = (n + "").toCharArray() \\ ['1','2','3','4','5','6','7','8','9]
````

### sliding window is a very important problem - it applies to many substrings and subarray problems.
* Hashset as the window 
* Running pre/suffix sum and product 
TODO: 
```code template for Sliding window```
* Dutch flag problem:
	implace moving of elements, elements values needs to be known
+ generate array from arraylist
```Java
new ArrayList().toArray(new Integer[0]);
note: cannot convert to primitive types
so cannot do this new ArrayList().toArray(new int[0]); ERROR
```
* To initialize an array ``` Arrays.fill(arr, -1);```
### String patterns & string calculations

to get the asci value for using 26 int frequency array 
```Java
'b' - 'a' = 1 returns int value
'b' - 1 = 97 still returns the int value
(char)('b' - 1) = 'a' need to explicitly type cast into character
```

best time to buy and sell stocks:
```Java
for(currentPrice : prices){
	if(minPrice > currentPrice){
		minPrice = currentPrice;
	}
	else{
		if(maxProfit < currentPrice - minPrice){
			maxProfit = currentPrice - minPrice;
		}
	}
}
return maxProfit;
```
* Things about traversing from right to left.

Kadane's algorithm:
```TODO```


## Graphs:
### Depth First Search: Depth wise
Time complexity: for adjacency List O(V+E)
Space complexity: ??

* Many problems using DFS 
* Maze search, connected Islands, 
`few problems which seems DFS but arent be aware of that trick, if order of print matters then its not DFS, its most probably Topological sort`

```Java
int [][] Directions = new int[][]{
	{0, -1}, \\ Left 
	{0, 1}, \\ Right 
	{-1, 0}, \\ Up 
	{1, 0}, \\ Down
}
```

```Java
DFS(Node node, HashSet<Node> visited){
	if(visited.contains(node))
		return // you have detected cycle
	visited(node);
	// do something with DFS, print it (?? ) search it
	for(Node neighnors : node){
		DFS(neignors, visited);
	}
	// if ans not found, the mark the node un-visited also, so it can be reached via another path 
	unvisit(node);
}
```

### Topological sort: 
```Java
private boolean topologicalSort(int course, List<Integer> result) {
        if (done[course])
            return true;
        if (visited[course])
            return false; // cycle found
        visited[course] = true;
        if (adjacency_list[course] != null) {
            for (int prereqCourse : adjacency_list[course]) {
                if (!topologicalSort((prereqCourse, result))){
                    return false; 
                }
            }
        }
        visited[course] = false;
        done[course] = true;
        result.add(course);
        return true;
    }
```

### Breadth First Search: Level wise
Time complexity: for adjacency List O(V+E)
Space complexity: ??
* common problems and uses // TODO
1. Zig Zag traversal, level wise sum, traversal.
2. RightSideView
not very interesting problems on BFS
```Java
Queue<something> queue = new LinkedList();
queue.add(rootNote);
// BFS can be done using queue without recursion
while(!queue.isEmpty()){
	currentNode = queue.poll();
	// do something with currentNode, print search 
	// add the next nodes in the queue
	for(node neighbor: currentNode){
		queue.add(neighbor);
	}
}
```

## Backtracking 

## Dynamic programming 

## Permutation & combinations

# Datastructure 
### Linked List
* Dummy head 
* Runner techniques are two main techniques when solving problems involving linked list 
Limitations of linked List, cannot index into the element, cannot traverse back in singly linked list

Find the middle element using runner technique
```Java
Node fast = head; Node slow = fast;
whie(fast != null || fast.next != null){
	fast = fast.next.next;
	slow = slow.next;
}
```

### Trees: 

```Java
//This is the poor man's sorted insertion / Binary Search Tree 
    ArrayList<Integer> list = new ArrayList<Integer>() {
        public boolean add(Integer mt) {
            int index = Collections.binarySearch(this, mt);
            if (index < 0) index = ~index;
            super.add(index, mt);
            return true;
        }
    };
```

Tree problems are designed tot think recursively.
```Java
public Node insert(Node root, int value){
	if(root == null )
		return new Node(value);
	if(value <= root.value)
		root.left = insert(root.left, value);	
	else
		root.right = insert(root.right, value );
	return root;
}
```

### PriorityQueue:
* to find max element use min-heap (want to preserve max element at the bottom)
* to find min element use max-heap (want to preserve min element at the bottom)
### Trie

# Java Specific

#### comparable and Comparable
