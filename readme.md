
### Bit Manipulation 
* I use it to find the middle element of an array, given left and right most index


1. `middle = left + right >> 1;`
1. Test kth bit is set: `num & (1 << k) != 0`
1. Set kth bit: `num |= (1 << k);`
1. Turn off kth bit: `num &= ~(1 << k)`
1. Toggle the kth bit: `num ^= (1 << k)`
1. To check if a number is a power of 2, `num & num - 1 == 0`

* When to use it, how to know it will help ?
``` Java
2 >> 1 = 1
5 >> 1 = 2
```

### Intervals[a,b]: 
* Sort intervals based on the __start time__. 
	* Meeting rooms
	* Meeting rooms which uses Priority Queue
`[[1, 2], [4, 7]]`
```Java
boolean overlap(int[] a, int[]b){
	return a[0]<b[1] &&  b[0]<a[1];
}
int[] mergeInterval(int[] a , int[] b){
	return new int[]{Math.min(a[0], b[0]), Math.max(a[1], b[1])};
}
```

### Strings and arrays:
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

// Above is O(n2) way of solving subsequence problem, substring problems

* Memorize the code for deletion of element in an array
* Memorize the code for shift elements in an array
```Java
placesToShift = 0 ; int index = 0; 
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
* If the solution takes n^2, try to sort the array (not possible in case of subsequence and subarray problems)
* 256 length array to calculate the frequency
* If need is to deal with individual digit in an number use this.
```Java
narray = (1234 + "").toCharArray() \\ ['1','2','3','4']
```
* Looking for dup/unique : try hashing/Bit Manipulation, (also consider that you can use the array itself for hashing)

#### sliding window is a very important problem - it applies to many substrings and subarray problems.
* HashSet as the window 
* Running pre/suffix sum and product 
TODO: 
```code template for Sliding window```
* Dutch flag problem:
	implace moving of elements, elements values needs to be known

>A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

* Generate array from arraylist
```Java
new ArrayList().toArray(new Integer[0]);
note: cannot convert to primitive types
so cannot do this new ArrayList().toArray(new int[0]); ERROR
```
* To initialize an array ` Arrays.fill(arr, -1);`

#### String patterns & string calculations

* To get the asci value for using 26 int frequency array 
```Java
'b' - 'a' = 1 returns int value
'b' - 1 = 97 still returns the int value
(char)('b' - 1) = 'a' need to explicitly type cast into character
```
###### A bit advanced topics in strings:
![alt text](/images/string_matching_algos.png)


* Things about traversing from right to left.

Kadane's algorithm:
```TODO```


### Graphs:
* Making adjency list quickly.
```Java
List<Integer>[] getAdjacencyList(int n, int[][] prereqs) {
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

#### Depth First Search: Depth wise
> DFS has an issue when the Depth of tree is very large, for python 1000 

Time complexity: for adjacency List O(V+E)
Space complexity: ??

* Many problems using DFS  
`Few problems which seems DFS but arent, be aware of that trick, if order of print matters then its not DFS, its most probably Topological sort`

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
	visited.add(node);
	// do something with DFS, print it (?? ) search it
	for(Node neighnors : node){
		DFS(neignors, visited);
	}
	// if ans not found, the mark the node un-visited also, 
	// so it can be reached via another path 
	visited.remove(node);
}
```

#### Topological sort: 
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

#### Breadth First Search: Level wise
> Leads to the shortest path in the graph
Time complexity: for adjacency List O(V+E)
Space complexity: ??
Not very interesting problems on BFS
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
* Multi-source BFS
Add all the sources to the initial queue.

#### Traversal
1. Inorder
2. Preorder
3. PostOrder

* Checking of two trees are similar / two subtrees are similar needs two functions, one which check 
equality and other which traverses the subtree.

### PriorityQueue:
* To find max element use min-heap (want to preserve max element at the bottom)
* To find min element use max-heap (want to preserve min element at the bottom)

#### Trees
* Tree problems are designed tot think recursively.


### MISC
#### Handling time strings
```Java
// convert everything to minutes, was the trick 23:59 is how many minutes ?
String str = "23:59";
String[] split = str.split(":", 2);
int hour = Integer.parseInt(split[0]) * 60;
int min =  Integer.parseInt(split[1]);
return hour + min;
```

### Classic problems
1. Dutch flag problem

``` Java
int p0 = 0; // all elements to the left of this are 0 
int p2 = nums.length - 1; // all elements to the right of this are 2
for(int idx = p0; idx <= p2; idx++){
	if(nums[idx] == 0 ){
		swap(nums, p0, idx);
		p0++;
		continue;
	}
	if(nums[idx] == 2){
		swap(nums, p2, idx);
		p2--;
		idx--;
		continue;
	}   
}
```

2. Best time to buy and sell stocks:
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


##### Communication: 
> Once you get into coding questions, communication is the key. A candidate who needed some help along the way but communicated clearly can be even better than a candidate who breezed through the question.

1. Understand what kind of problem it is. 
2. Think out loud
3. Slow the eff down
4. Get unstuck
    * Draw pictures
    * Solve a simpler version of the problem
    * Write a naive, inefficient solution and optimize it later
5. Wait for a hint
6. Think about the bounds on space and runtime
7. Apply a common algorithmic pattern
8. Get your thoughts down
9. Call a helper function and keep moving

