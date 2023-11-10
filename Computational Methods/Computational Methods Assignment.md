## task 1
![[Assignment planets diagram]]

```
Let adjacency_matrix = {{0,10,15,12,20}, {10,0,12,25,14}, {15,12,0,16,28}, {12,25,16,0,17}, {20,14,28,17,0}}
Let cargo_pickup_weights = [20,40,70,10,30]

Function get_distance(a, b):
	Return adjacency_matrix[a][b]
End Function

Function calculate_fuel_cost(a, b, c, d, e):
	Let total_fuel = 0
	Let total_weight = 0

	total_weight = total_weight + cargo_pickup_weights[a]
	total_fuel = total_fuel + get_distance(a,b)*total_weight

	total_weight = total_weight + cargo_pickup_weights[b]
	total_fuel = total_fuel + get_distance(b,c)*total_weight

	total_weight = total_weight + cargo_pickup_weights[c]
	total_fuel = total_fuel + get_distance(c,d)*total_weight

	total_weight = total_weight + cargo_pickup_weights[d]
	total_fuel = total_fuel + get_distance(d,e)*total_weight

	total_weight = total_weight + cargo_pickup_weights[e]

	Return total_fuel*25
End Function

Let all_possible_sequences = []

Let a = 0
While a < 5:
	Let sequence = [a]

	Let b = 0
	While b < 5:
		If sequence Contains b:
			Continue
		End If
		Append b to sequence

		Let c = 0
		While c < 5:
			If sequence Contains c:
				Continue
			End If
			Append c to sequence

			Let d = 0
			While d < 5:
				If sequence Contains d:
					Continue
				End If
				Append d to sequence

				Let e = 0
				While e < 5:
					If sequence Contains e:
						Continue
					End If
					Append e to sequence

					Append sequence to all_possible_sequences
					sequence = [a,b,c,d]
					Increment e
				End While
				sequence = [a,b,c]
				Increment d
			End While
			sequence = [a,b]
			Increment c
		End While
		sequence = [a]
		Increment b
	End While

	Increment a
End While

Open "brute_force.csv" as file
Let index = 0
While index < Length of all_possible_sequences:
	Let seq = all_possible_sequences[index]
	Output seq[0] to file
	Output "," to file
	Output seq[1] to file
	Output "," to file
	Output seq[2] to file
	Output "," to file
	Output seq[3] to file
	Output "," to file
	Output seq[4] to file
	Output "," to file
	Output calculate_fuel_cost(seq[0], seq[1], seq[2], seq[3], seq[4]) to file
	Output "\n" to file
End While

Close file
```
brute_force_script.py:
```
alpha = 0
beta = 1
gamma = 2
delta = 3
epsilon = 4

adjacency_matrix = [[0,10,15,12,20], [10,0,12,25,14], [15,12,0,16,28], [12,25,16,0,17], [20,14,28,17,0]]

cargo_pickup_weights = [20,40,70,10,30]

def get_distance(a, b):
    return adjacency_matrix[a][b]

def calculate_fuel_cost(a, b, c, d, e):
    total_fuel = 0
    total_weight = 0
    
    total_weight += cargo_pickup_weights[a]
    total_fuel += get_distance(a,b)*total_weight

    total_weight += cargo_pickup_weights[b]
    total_fuel += get_distance(b,c)*total_weight

    total_weight += cargo_pickup_weights[c]
    total_fuel += get_distance(c,d)*total_weight

    total_weight += cargo_pickup_weights[d]
    total_fuel += get_distance(d,e)*total_weight

    total_weight += cargo_pickup_weights[e]

    return total_fuel*25


all_possible_sequences = []

for a in range(5):
    sequence = [a]
    for b in range(5):
        if (b in sequence): continue
        sequence.append(b)
        for c in range(5):
            if (c in sequence): continue
            sequence.append(c)
            for d in range(5):
                if (d in sequence): continue
                sequence.append(d)
                for e in range(5):
                    if (e in sequence): continue
                    sequence.append(e)
                    all_possible_sequences.append(sequence)
                    sequence = [sequence[0], sequence[1], sequence[2], sequence[3]]
                sequence = [sequence[0], sequence[1], sequence[2]]
            sequence = [sequence[0], sequence[1]]
        sequence = [sequence[0]]
                    
csv_data = ""
for seq in all_possible_sequences:
    csv_data += str(seq[0]) + ","
    csv_data += str(seq[1]) + ","
    csv_data += str(seq[2]) + ","
    csv_data += str(seq[3]) + ","
    csv_data += str(seq[4]) + ","
    csv_data += str(calculate_fuel_cost(seq[0], seql[1], seq[2], seq[3], seq[4])) + "\n"

print("generated " + str(len(all_possible_sequences)) + " sequences")

file = open("brute_force.csv", "w")

file.write(csv_data)
file.close()
```

brute_force.csv:
```
0,1,2,3,4,134500
0,1,2,4,3,182000
0,1,3,2,4,168500
0,1,3,4,2,142250
0,1,4,2,3,153000
0,1,4,3,2,104250
0,2,1,3,4,175250
0,2,1,4,3,148000
0,2,3,1,4,155000
0,2,3,4,1,131500
0,2,4,1,3,212500
0,2,4,3,1,202750
0,3,1,2,4,143750
0,3,1,4,2,119250
0,3,2,1,4,97000
0,3,2,4,1,133500
0,3,4,1,2,69750
0,3,4,2,1,99750
0,4,1,2,3,118500
0,4,1,3,2,123750
0,4,2,1,3,181000
0,4,2,3,1,174250
0,4,3,1,2,98750
0,4,3,2,1,94250
1,0,2,3,4,144000
1,0,2,4,3,191500
1,0,3,2,4,154000
1,0,3,4,2,127750
1,0,4,2,3,167000
1,0,4,3,2,118250
1,2,0,3,4,151750
1,2,0,4,3,186250
1,2,3,0,4,162000
1,2,3,4,0,182000
1,2,4,0,3,207000
1,2,4,3,0,193500
1,3,0,2,4,164250
1,3,0,4,2,145000
1,3,2,0,4,160000
1,3,2,4,0,204000
1,3,4,0,2,123750
1,3,4,2,0,158500
1,4,0,2,3,146750
1,4,0,3,2,116000
1,4,2,0,3,163500
1,4,2,3,0,164000
1,4,3,0,2,105250
1,4,3,2,0,132000
2,0,1,3,4,189500
2,0,1,4,3,162250
2,0,3,1,4,164750
2,0,3,4,1,141250
2,0,4,1,3,213250
2,0,4,3,1,203500
2,1,0,3,4,147000
2,1,0,4,3,181500
2,1,3,0,4,195750
2,1,3,4,0,215750
2,1,4,0,3,177500
2,1,4,3,0,164000
2,3,0,1,4,126000
2,3,0,4,1,147500
2,3,1,0,4,178000
2,3,1,4,0,195000
2,3,4,0,1,149500
2,3,4,1,0,138000
2,4,0,1,3,229000
2,4,0,3,1,216250
2,4,1,0,3,167000
2,4,1,3,0,216500
2,4,3,0,1,157000
2,4,3,1,0,197750
3,0,1,2,4,129500
3,0,1,4,2,105000
3,0,2,1,4,93250
3,0,2,4,1,129750
3,0,4,1,2,69000
3,0,4,2,1,99000
3,1,0,2,4,143000
3,1,0,4,2,123750
3,1,2,0,4,136250
3,1,2,4,0,180250
3,1,4,0,2,101250
3,1,4,2,0,136000
3,2,0,1,4,108000
3,2,0,4,1,129500
3,2,1,0,4,128000
3,2,1,4,0,145000
3,2,4,0,1,147500
3,2,4,1,0,136000
3,4,0,1,2,69250
3,4,0,2,1,85750
3,4,1,0,2,75750
3,4,1,2,0,98500
3,4,2,0,1,106000
3,4,2,1,0,102750
4,0,1,2,3,118500
4,0,1,3,2,123750
4,0,2,1,3,169750
4,0,2,3,1,163000
4,0,3,1,2,97500
4,0,3,2,1,93000
4,1,0,2,3,125750
4,1,0,3,2,95000
4,1,2,0,3,132000
4,1,2,3,0,132500
4,1,3,0,2,115750
4,1,3,2,0,142500
4,2,0,1,3,188500
4,2,0,3,1,175750
4,2,1,0,3,134000
4,2,1,3,0,183500
4,2,3,0,1,126500
4,2,3,1,0,167250
4,3,0,1,2,69750
4,3,0,2,1,86250
4,3,1,0,2,95250
4,3,1,2,0,118000
4,3,2,0,1,102500
4,3,2,1,0,99250
```

cheapest route:
3 0 4 1 2 = Delta -> Alpha -> Epsilon -> Beta -> Gamma
Costs 69000 intergalactic currency

This approach isn't a good way to find the shortest path since it requires checking the cost of an enourmous and rapidly increasing search space. Specifically `n!` possible routes, `n` being the number of planets. Factorial time, $O(n!)$ is a very very bad time complexity and building a route with many destinations would take a very long time.

## task 2

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | start | end | i   | j   | pivot value | notes                                                          |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | ----------- | -------------------------------------------------------------- |
| 10  | 15  | 12  | 12  | 25  | 16  | 20  | 14  | 28  | 17  | 0     | 9   | -1  | 10  | 25          | partition the whole list                                       |
|     |     |     |     |     |     |     |     |     |     |       |     | 0   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 3   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 9   |             |                                                                |
| 10  | 15  | 12  | 12  | 17  | 16  | 20  | 14  | 28  | 25  |       |     |     |     |             | swap 4 and 9                                                   |
|     |     |     |     |     |     |     |     |     |     |       |     | 5   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 7   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 8   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 8   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 8   | 7   |             | partitioning finished                                          |
| 10  | 15  | 12  | 12  | 17  | 16  | 20  | 14  |     |     | 0     | 7   | -1  | 8   | 12          | subsort first half                                             |
|     |     |     |     |     |     |     |     |     |     |       |     | 0   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 7   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 6   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 5   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 4   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 1   | 3   |             |                                                                |
| 10  | 12  | 12  | 15  | 17  | 16  | 20  | 14  |     |     |       |     |     |     |             | swap 1 and 3                                                   |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 3   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 2   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 1   |             | partitioning finished                                          |
| 10  | 12  |     |     |     |     |     |     |     |     | 0     | 1   | -1  | 2   | 10          | subsort first half of first half                               |
|     |     |     |     |     |     |     |     |     |     |       |     | 0   | 2   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 0   | 1   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 0   | 0   |             | subsort done                                                   |
|     |     | 12  | 15  | 17  | 16  | 20  | 14  |     |     | 2     | 7   | 1   | 8   | 17          | subsort second half of first half                              |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 3   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 7   |             |                                                                |
|     |     | 12  | 15  | 14  | 16  | 20  | 17  |     |     |       |     |     |     |             | swap 4 and 7                                                   |
|     |     |     |     |     |     |     |     |     |     |       |     | 5   | 7   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 7   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 6   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 5   |             | partitioning finished                                          |
|     |     | 12  | 15  | 14  | 16  |     |     |     |     | 2     | 5   | 1   | 6   | 15          | subsort first half of second half of first half                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 6   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 3   | 6   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 3   | 5   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 3   | 4   |             |                                                                |
|     |     | 12  | 14  | 15  | 16  |     |     |     |     |       |     |     |     |             | swap 3 and 4                                                   |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 4   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 3   |             | partitioning finished                                          |
|     |     | 12  | 14  |     |     |     |     |     |     | 2     | 3   | 1   | 4   | 12          | subsort first half of first half of second half of first half  |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 4   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 3   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 2   | 2   |             | subsort done                                                   |
|     |     |     |     | 15  | 16  |     |     |     |     | 4     | 5   | 3   | 6   | 15          | subsort second half of first half of second half of first half |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 6   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 5   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 4   | 4   |             | subsort done                                                   |
|     |     |     |     |     |     | 20  | 17  |     |     | 6     | 7   | 5   | 8   | 20          | subsort second half of second half of first half               |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 8   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 6   | 7   |             |                                                                |
|     |     |     |     |     |     | 17  | 20  |     |     |       |     |     |     |             | swap 6 and 7                                                   |
|     |     |     |     |     |     |     |     |     |     |       |     | 7   | 7   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 7   | 6   |             | subsort done                                                   |
|     |     |     |     |     |     |     |     | 28  | 25  | 8     | 9   | 7   | 10  | 28          | subsort second half                                            |
|     |     |     |     |     |     |     |     |     |     |       |     | 8   | 10  |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 8   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     |     |     |             | swap 8 and 9                                                   |
|     |     |     |     |     |     |     |     | 25  | 28  |       |     |     |     |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 9   | 9   |             |                                                                |
|     |     |     |     |     |     |     |     |     |     |       |     | 9   | 8   |             | subsort done                                                   |
| 10  | 12  | 12  | 14  | 15  | 16  | 17  | 20  | 25  | 28  |       |     |     |     |             | sort done                                                      | 

sorted using quick sort

```
Procedure swap(array, first, second) Being:
	Let temp = array[first]
	array[first] = array[second]
	array[second] = temp
End Procedure

Function partition_array(array, start, end) Begin:
	// Place the pivot in the middle, this tends to have better performance
	Let pivot_index = ((end - start)/2 Rounded Down) + start
	Let pivot = array[pivot_index]
	
	// Initialise pointers
	Let i = start - 1
	Let j = end + 1
	
	While True:
		// Increment i then break if the targeted element is swappable
		While True:
			Increment i
			If array[i] >= pivot:
				Break
			End If
		End While
		
		// Decrement j then break if the targeted element is swappable
		While True:
			Decrement j
			If array[j] <= pivot:
				Break
			End If
		End While
		
		// Return the partition point if i and j meet/cross, otherwise swap their values
		If i >= j:
			Return j
		Else:
			swap(array, i, j)
		End If
	End While
End Function

Procedure quick_sort(array, start, end) Begin:
	// Return if there is nothing to sort
	If start >= end:
		Return
	End If
	
	// Perform first sorting pass over current whole array
	Let split_index = partition_array(array, start, end)
	
	// Perform subsorts on partitioned arrays
	quick_sort(array, start, split_index)
	quick_sort(array, split_index + 1, end)
End Procedure
```

- this is an implementation of the quicksort algorithm, using Hoare's pivot choice and pair-of-pointers method
- it makes use of recursive quicksorts to sort a list by swapping items so that they effectively end up grouped (in each sublist) in groups of larger and smaller items; these sublists can then be sorted using the same method, until there is only one item in each sublist (this is the base case)
- this is an example of a divide-and-conquer approach, as the subsequent quicksorts can be parallelised
- quicksort, depending on implementation (particularly choice of pivot) as well as how sorted data already is, usually has worst-case complexity $O(n^2)$, however with Hoare's partitioning scheme using the middle-pivot (as opposed to pivoting at the start or end value) tends to have worst-case complexity of $O(n \log_2(n))$
## task 3
![[Greedy strategy]]
```
Let all_nodes = {"alpha", "beta", "gamma", "delta", "epsilon"}
Let cargo_weights = {20, 40, 70, 10, 30}
Let adjacency_matrix = {{0,10,15,12,20}, {10,0,12,25,14}, {15,12,0,16,28}, {12,25,16,0,17}, {20,14,28,17,0}}

// State variables
Let unvisited_nodes = {"alpha", "beta", "gamma", "delta", "epsilon"}
Let weight = 0
Let fuel_cost = 0
Let path = {}

// Bubble sort unvisited nodes according to their cargo weights
Let changed = True
While changed = True:
	Let counter = 0
	changed = False
	While counter < size of sorted_list:
		Let first_node_index = Index of unvisited_nodes[counter] in all_nodes
		Let second_node_index = Index of unvisited_nodes[counter+1] in all_nodes
		If cargo_weights[first_node_index] > cargo_weights[second_node_index]:
			changed = True
			Let temp = unvisited_nodes[counter]
			unvisited_nodes[counter] = unvisited_nodes[counter+1]
			unvisited_nodes[counter+1] = temp
		End If
		Increment counter
	End While
End While

// Enter graph
Append unvisited_nodes[0] to path
weight = cargo_weights[Index of unvisited_nodes[0] in all_nodes]

// Traverse graph
Let index = 1
While index < Length of unvisited_nodes:
	Let next_node = unvisited_nodes[index]
	
	Let next_node_index = Index of next_node in all_nodes
	Let last_node_index = Index of (Last of path) in all_nodes
	
	Let journey_cost = adjacency_matrix[next_node_index][last_node_index] * weight
	fuel_cost = fuel_cost + journey_cost
	
	weight = weight + cargo_weights[next_node_index]
	
	Append next_node to path
	Remove next_node from unvisited_nodes
End While

Output "Total fuel cost:"
Output fuel_cost * 25
Output path
```

```
#include <iostream>
#include <vector>
#include <string>
#include <queue>

using namespace std;

int find_index(string value, vector<string> list)
{
	for (int i = 0; i < list.size(); i++) if (value == list[i]) return i;
	return -1;
}

int main()
{
	vector<string> all_nodes = { "alpha", "beta", "gamma", "delta", "epsilon" };
	vector<int> cargo_weights = { 20, 40, 70, 10, 30 };
	vector<vector<int>> adjacency_matrix = { {0,10,15,12,20}, {10,0,12,25,14}, {15,12,0,16,28}, {12,25,16,0,17}, {20,14,28,17,0} };

	// state variables
	vector<string> unvisited_nodes = all_nodes;
	int weight = 0;
	int fuel_cost = 0;
	vector<string> path = {};

	// sort unvisited_nodes
	bool changed = true;
	while (changed)
	{
		changed = false;
		for (int i = 0; i < unvisited_nodes.size() - 1; i++)
		{
			int first_node_index = find_index(unvisited_nodes[i], all_nodes);
			int second_node_index = find_index(unvisited_nodes[i + 1], all_nodes);
			if (cargo_weights[first_node_index] > cargo_weights[second_node_index])
			{
				string swap = unvisited_nodes[i];
				unvisited_nodes[i] = unvisited_nodes[i + 1];
				unvisited_nodes[i + 1] = swap;
				changed = true;
			}
		}
	}

	// enter graph
	path.push_back(unvisited_nodes[0]);
	weight = cargo_weights[find_index(unvisited_nodes[0], all_nodes)];

	// traverse graph
	for (int index = 1; index < unvisited_nodes.size(); index++)
	{
		string next_node = unvisited_nodes[index];

		int next_node_index = find_index(next_node, all_nodes);
		int last_node_index = find_index(path.back(), all_nodes);

		int journey_cost = adjacency_matrix[next_node_index][last_node_index];
		fuel_cost += journey_cost * weight;

		weight += cargo_weights[next_node_index];

		path.push_back(next_node);
	}

	int total_fuel_cost = fuel_cost * 25;

	cout << "Found a route costing " << total_fuel_cost << endl;
	cout << "Path: " << endl;
	cout << "  ";
	for (string s : path) cout << s << " ";
	cout << endl;

	return 0;
}
```
output:
```
Found a route costing 69000
Path:
  delta alpha epsilon beta gamma
```

bearing in mind a greedy strategy chooses the best option in the short term and does not look ahead, i experimented with two different techniques: first, to traverse the graph choosing to move along the **cheapest weighted edge** (excluding any which lead to already visited nodes) at every node; second, to traverse along the edge to the **lowest cargo mass** (using mass here to be distinct from edge weights) **adjacent unvisited** node.
the second of these produced a resulting route (starting at delta, since it has the lowest cargo mass to collect) of `delta -> alpha -> epsilon -> beta -> gamma`, costing **69000** intergalactic Vbucks, which happens to also be the optimal path found by the brute-force method.
the first approach by contrast, starting at the same place, ended up choosing a `delta -> gamma -> beta -> alpha -> epsilon` route, which cost almost double the other method at **126500** intergalactic Vbucks.
it makes sense that a mass-focussed route is better, since mass accumulates during the graph traversal, whereas the edge weightings (distances between planets) do not.

using this approach, i wrote an algorithm in pseudocode which follows the mass-focussed traversal method, with the slight improvement of pre-sorting the unvisited nodes list to be ordered by low mass first (saving searching for the next lowest mass planet each step of traversal). i also then converted the algorithm to C++, and verified that it gave the correct result.
it's worth noting that i could have handled referencing planets in this the same as in my python script for brute-forcing in the first task, considerably reducing the cost of managing the 5 planets' data, but i decided to use the string names for clarity.

since this algorithm includes the bubble sort (i chose this sort because it has a $O(n)$ space complexity, and is easy to implement for a situation where we need to compare values in one list and use that to swap values in another list), it must have time complexity of at least $O(n^2)$. since we have to find the index of a planet from its string name each iteration, which could require counting all the way through the `n` planets, the worst-case complexity is raised to $O(n^3)$, though this could be improved with the use of proper data structures (i.e. limited by pseudocode). the final loop traversing the graph has a similar problem, requiring `n` iterations, each time searching the `n` planets to find the right index for mass lookups, making that also $O(n^2)$. we can simplify the overall time complexity of approximately $O(n^3 + n^2 + n^2)$ (there are two index lookups in the final loop) down to $O(n^3 + 2n^2)$ or just $O(n^3)$ if we take only the greatest time complexity. using indices to reference planets and a binary search method, or having each one be a pointer to a struct containing name, cargo mass, and edge weightings, and also making use of a better sorting algorithm such as quicksort, we could reduce the worst-case time complexity to $O(n\log_2(n))$ .


i decided to come back to this exercise during a seminar (and after it), since i wasn't happy with $O(n^3)$ complexity, and the general unclearness of the algorithm. i rewrote the greedy strategy using the same basic method, but with a better algorithm. now planets are stored as **structures**, containing all the information about them and how they connect. meaning the amount of look-ups in lists is significantly reduced.

i found that, surprisingly, when constructing the list of connections one node (i.e. planet) has with other nodes, it's actually better to not bother sorting the list by cargo mass (i.e. to reduce searching later). this is because in the later code not only do we need to find the next lowest cargo mass planet, we need to find one which has not already been visited, which means we end up doing a linear search through the connected planets anyway. we would be choosing between either an $O(n^3)$ sorting pass with an $O(n^2)$ traversal pass, or an $O(n^2)$ preparation pass with an $O(n^2)$ traversal pass, the latter of which is clearly much better. pseudocode and C++ implementation are below.

```
Let NUM_PLANETS = 5
Let FUEL_COST = 25

// structure holding data about a planet (i.e. a node)
Structure planet
	Let name = ""
	Let index = 0
	Let cargo_mass = 0
	Let links = {}
End Structure

// starting data about the planets
Let node_names = { "alpha", "beta", "gamma", "delta", "epsilon" }
Let cargo_masses = { 20,40,70,10,30 }
Let adjacency_matrix = { {0,10,15,12,20}, {10,0,12,25,14}, {15,12,0,16,28}, {12,25,16,0,17}, {20,14,28,17,0} }

// initialise the nodes in the graph
Let planets = {}
Let i = 0
While i < NUM_PLANETS
	Let p = Create planet
	name Of p = node_names[i]
	cargo_mass Of p = cargo_masses[i]
	index Of p = i
	Append p To planets
	
	Increment i
End While

Let p_minimum = planets[0]

// setup links between nodes
For p_origin In planets

	// update the lowest cargo mass planet
	// since we want to start at this planet
	// and this saves using a second loop
	If cargo_mass Of p_origin < cargo_mass Of p_minimum
		p_minimum = p_origin
	End If

	// add links from this node to all other nodes
	// but not itself
	Let i = 0
	While i < NUM_PLANETS
		If planets[i] Not p_origin
			Let distance = adjacency_matrix[i][index Of p_origin]
			Append {planets[i], distance} To links Of p_origin
		End If
		Increment i
	End While
End For

// traverse the graph, keeping track of which planets
// have been visited, and which haven't
Let visited = {}
Fill visited With False NUM_PLANETS Times

Let spaceship_mass = 0
Let fuel_cost = 0
Let sequence = ""

Let p_current = p_minimum
Let p_next Be Empty

Loop Forever

	// find the unvisited planet from the current
	// with the lowest cargo mass, via linear search
	Let minimum_mass = Infinity
	Let d_min_mass = -1
	Let p_min_mass Be Empty

	For l_candidate In links Of p_current
		Let p_candidate = l_candidate[0]
		If visited[index Of p_candidate] = False
			If cargo_mass Of p_candidate < minimum_mass
				minimum_mass = cargo_mass Of p_candidate
				p_min_mass = p_candidate
				d_min_mass = l_candidate[1]
			End If
		End If
	End For

	// if there were no unvisited planets
	// other than the current one, break from the loop
	If p_min_mass Is Empty
		Break Loop
	End If

	// update the next planet we want to visit
	// this will be the one with the next lowest cargo mass
	p_next = p_min_mass
	d_next = d_min_mass

	// add on the calculate fuel cost for the journey between
	// the current planet and the next
	spaceship_mass = spaceship_mass + cargo_mass Of p_current
	fuel_cost = fuel_cost + spaceship_mass * d_next * FUEL_COST

	// update the sequence string
	sequence = sequence + name Of p_current + " -> "

	// mark this planet as visited
	visited[index Of p_current] = true

	// move onto the next planet
	p_current = p_next
End Loop

// finalise and output the result
sequence = sequence + name Of p_current

Output "Found sequence: " + sequence
Output "Costing: " + fuel_cost
```

```
#include <string>
#include <vector>
#include <iostream>

#define NUM_PLANETS 5
#define FUEL_COST 25

using namespace std;

// data about a planet
struct planet
{
	string name;
	int index;
	int cargo_mass;
	vector<pair<planet*, int>> links;
};

int main()
{
	// starting data about planets
	string node_names[NUM_PLANETS] = { "alpha", "beta", "gamma", "delta", "epsilon" };
	int cargo_masses[NUM_PLANETS] = { 20,40,70,10,30 };
	int adjacency_matrix[NUM_PLANETS][NUM_PLANETS] = { {0,10,15,12,20}, {10,0,12,25,14}, {15,12,0,16,28}, {12,25,16,0,17}, {20,14,28,17,0} };

	// create nodes
	vector<planet*> planets;
	for (int i = 0; i < NUM_PLANETS; i++)
	{
		planet* p = new planet();
		p->name = node_names[i];
		p->cargo_mass = cargo_masses[i];
		p->index = i;

		planets.push_back(p);
	}

	planet* p_minimum = planets[0];

	// setup links between nodes
	for (planet* p_origin : planets)
	{
		// update lowest cargo planet while we're here
		// saves having another loop
		if (p_origin->cargo_mass < p_minimum->cargo_mass)
		{
			p_minimum = p_origin;
		}

		// add links to other nodes
		// not sorted, since sorting them would
		// actually take more time (O(n^2) inside an n-loop)
		for (int i = 0; i < NUM_PLANETS; i++)
		{
			if (planets[i] == p_origin) continue;

			p_origin->links.push_back(pair<planet*, int>(planets[i], adjacency_matrix[i][p_origin->index]));
		}
	}

	// traverse, keep list of visited
	bool visited[NUM_PLANETS] = { false };

	int spaceship_mass = 0;
	int fuel_cost = 0;
	string sequence = "";

	planet* p_current = p_minimum;
	planet* p_next = NULL;
	int d_next = 0;

	while (true)
	{
		// find the unvisited planet with the lowest cargo mass
		int minimum_mass = INT_MAX;
		int d_min_mass = -1;
		planet* p_min_mass = NULL;
		for (pair<planet*, int> l_candidate : p_current->links)
		{
			planet* p_candidate = l_candidate.first;
			if (visited[p_candidate->index]) continue;
			if (p_candidate->cargo_mass < minimum_mass)
			{
				minimum_mass = p_candidate->cargo_mass;
				p_min_mass = p_candidate;
				d_min_mass = l_candidate.second;
			}
		}

		// if there were no unvisited planets,
		// other than the current one, break out
		if (p_min_mass == NULL) break;

		// set the planet we intend to visit
		// next (the one with the lowest cargo mass)
		p_next = p_min_mass;
		d_next = d_min_mass;

		// add on the calculated fuel cost
		spaceship_mass += p_current->cargo_mass;
		fuel_cost += spaceship_mass * d_next * FUEL_COST;

		// update the sequence string
		sequence += p_current->name;
		sequence += " -> ";

		// mark it as visited
		visited[p_current->index] = true;

		// move onto the next
		p_current = p_next;
	}

	// output the result
	sequence += p_current->name;

	cout << "Found sequence: " << sequence << endl;
	cout << "Costing: " << fuel_cost << endl;

	return 0;
}
```

the output from the second version of the algorithm is, aside from cosmetic modification, exactly the same. the resulting algorithmic complexity of this solution is $O(n^2)$, due to the two occurrences of traversing lists of length `n`, `n` times over.

the only further optimisation i think could be made would be using a system of sorted lookup tables for planet data and cargo masses to eliminate the need for searching for the next lowest *unvisited* cargo mass planet. this might reduce complexity to $O(n\log_2(n))$ in the best case if sorted with quicksort.

## task 4

![[alpha.csv]]

![[beta.csv]]

![[delta.csv]]

![[epsilon.csv]]

![[gamma.csv]]

i wrote a short C++ program to produce these tables, in other words i not only followed the dynamic programming approach but also implemented the algorithm.
my code primarily makes use of a **tree structure** which represents the data which is eventually placed in the table, but which is **more compact and easier to traverse**. i made use of a `std::queue` to keep track of the next block of possible sequences to test, and a `std::map` to keep track of the cheapest version of similar routes (used for carrying forward only the better routes). my tree structure makes use of **pointers** to other nodes allocated on the heap. code is below:
```
#include <map>
#include <string>
#include <queue>
#include <iostream>
#include <fstream>

#define NODE_ZERO 65

using namespace std;

// only supports up to 255 nodes
#define NUM_NODES 5

const int adjacency[NUM_NODES][NUM_NODES] = { {  0, 10, 15, 12, 20 },
												{ 10,  0, 12, 25, 14 },
												{ 15, 12,  0, 16, 28 },
												{ 12, 25, 16,  0, 17 },
												{ 20, 14, 28, 17,  0 }
};

const int weight[NUM_NODES] = { 20, 40, 70, 10, 30 };
const string names[NUM_NODES] = { "alpha", "beta", "gamma", "delta", "epsilon" };

struct cost_tree_node
{
	int cumulative_cost = 0;
	int cumulative_weight = 0;
	string planets_sequence = "";
	unsigned char last_planet = 0;
	cost_tree_node** children = NULL;
	cost_tree_node* parent = NULL;
};

string sort_sequence(string seq)
{
	if (seq.length() <= 3) return seq;

	string to_sort = seq;

	bool changed = true;
	while (changed)
	{
		changed = false;
		for (int i = 1; i < to_sort.length() - 2; i++)
		{
			if (to_sort[i] > to_sort[i + 1])
			{
				changed = true;
				unsigned char tmp = to_sort[i];
				to_sort[i] = to_sort[i + 1];
				to_sort[i + 1] = tmp;
			}
		}
	}
	return to_sort;
}

void write_out_table(cost_tree_node* root, int nodes_total)
{
	string output = "prefix,";
	for (int i = NODE_ZERO; i < NODE_ZERO + NUM_NODES; i++)
	{
		output += names[i - NODE_ZERO];
		output += ",";
	}
	output += "\n";

	queue<cost_tree_node*> row_queue;
	row_queue.push(root);

	int block = 0;
	while (!row_queue.empty())
	{
		cost_tree_node* row_starter = row_queue.front();
		row_queue.pop();

		if (row_starter->children == NULL) continue;

		if (row_starter->planets_sequence.length() - 1 > block)
		{
			for (int i = 0; i < NUM_NODES + 1; i++)
			{
				output += " ,";
			}
			output += "\n";
			block = row_starter->planets_sequence.length() - 1;
		}

		for (unsigned char c : row_starter->planets_sequence)
			output += toupper(names[c - NODE_ZERO][0]);
		output += ",";

		for (int i = 0; i < NUM_NODES; i++)
		{
			if (row_starter->children[i] == NULL)
			{
				output += "-,";
				continue;
			}
			output += to_string(row_starter->children[i]->cumulative_cost);
			output += ",";
			row_queue.push(row_starter->children[i]);
		}
		output += "\n";
	}

	ofstream file;
	file.open(names[root->planets_sequence[0] - NODE_ZERO] + ".csv");
	file << output;
	file.close();
}

cost_tree_node* build_dynamic_cost_tree(unsigned char start_node_index)
{
	string root_sequence; root_sequence.push_back(start_node_index);
	cost_tree_node* root = new cost_tree_node
	{
		0,
		weight[start_node_index - NODE_ZERO],
		root_sequence,
		start_node_index,
		NULL,
		NULL
	};

	queue<cost_tree_node*> this_block_nodes; // nodes that need to have their children populated
	map<string, cost_tree_node*> next_block_routes; // new child nodes which are the best route starting at string[0] and ending at string[-1]

	int total_nodes = 0;

	this_block_nodes.push(root);

	for (int block = 0; block < NUM_NODES - 1; block++)
	{
		// current block, i.e. a level in the tree
		while (!this_block_nodes.empty())
		{
			total_nodes++;
			// populate the children of a node
			cost_tree_node* parent = this_block_nodes.front();
			this_block_nodes.pop();

			parent->children = new cost_tree_node * [NUM_NODES];

			for (unsigned char c = NODE_ZERO; c < NUM_NODES + NODE_ZERO; c++)
			{
				if (parent->planets_sequence.find(c) != string::npos)
				{
					parent->children[c - NODE_ZERO] = NULL;
				}
				else
				{
					string node_sequence = parent->planets_sequence;
					node_sequence += c;
					cost_tree_node* node = new cost_tree_node
					{
						parent->cumulative_cost + (parent->cumulative_weight * adjacency[parent->last_planet - NODE_ZERO][c - NODE_ZERO]),
						parent->cumulative_weight + weight[c - NODE_ZERO],
						node_sequence,
						c,
						NULL,
						parent
					};
					parent->children[c - NODE_ZERO] = node;
					string sorted_seq = sort_sequence(node->planets_sequence);
					if (block >= 2)
					{
						auto current_best = next_block_routes.find(sorted_seq);
						if (current_best == next_block_routes.end()) next_block_routes.insert({ sorted_seq, node });
						else if (node->cumulative_cost < (*current_best).second->cumulative_cost) next_block_routes[sorted_seq] = node;
					}
					else
					{
						next_block_routes.insert({ sorted_seq, node });
					}
				}
			}

		}

		// queue up the best routes from the last block for the next one
		for (pair<string, cost_tree_node*> pr : next_block_routes)
		{
			this_block_nodes.push(pr.second);
		}

		next_block_routes.clear();
	}

	write_out_table(root, total_nodes);

	cost_tree_node* best_route_through_table = this_block_nodes.front();
	while (!this_block_nodes.empty())
	{
		cost_tree_node* front = this_block_nodes.front();
		this_block_nodes.pop();
		if (front->cumulative_cost < best_route_through_table->cumulative_cost)
		{
			best_route_through_table = front;
		}
	}

	return best_route_through_table;
}

int main()
{
	for (int i = NODE_ZERO; i < NUM_NODES + NODE_ZERO; i++)
	{
		cost_tree_node* res = build_dynamic_cost_tree(i);
		cout << res->cumulative_cost * 25 << endl;
		for (unsigned char c : res->planets_sequence) cout << names[c - NODE_ZERO] << " ";
		cout << endl << endl;
	}
}
```

as can be seen from the console output of the code, by looking at the lowest cost table cell in the last block of each table (i'm defining a block as a set of rows which have the same number of previously visited planets shown in the far left column), we can find the cheapest route starting at the origin node of the table:
- starting at alpha: 69750 (alpha -> delta -> epsilon -> beta -> gamma)
- starting at beta: 105250 (beta -> epsilon -> delta -> alpha -> gamma)
- starting at gamma: 12600 (gamma -> delta -> alpha -> beta -> epsilon)
- starting at delta: 69000 (delta -> alpha -> epsilon -> beta -> gamma)
- starting at epsilon: 69750 (epsilon -> delta -> alpha -> beta -> gamma)
and then the best route overall can be found by taking the cheapest of these optimal routes, DAEBG for 69000. this is the same optimal route found by brute force, as we would expect (in fact, we can verify that the optimal route costs starting from other planets are also the best routes found starting from those planets by the brute force method).

we can see that this dynamic approach is guaranteed to find the optimal route, because we only prune routes which visit the **same planets** (and thus have the same weight) but with a **worse cost than other routes covering the same planets**.

in terms of complexity, it's evident to see that this is faster than the brute force approach, for two reasons, which correspond to the two main techniques the dynamic approach uses:
1. memoisation - each time we want to calculate the cost of traversing from one node to another, we don't recalculate the entire cost, just the progressive cost, and previous calculations are saved and reused (reduces time cost to calculate multiple branching routes)
2. pruning - by pruning provably inferior routes at early stages, we massively reduce the search space. in fact, we reduce our search space all the way down to just 60 full routes covered, from 120 before. as tested below with different numbers of nodes:

| nodes | routes checked to completion | nodes evaluated | total possible routes | nodes evaluated in brute force (equivalent) |
| ----- | ---------------------------- | --------------- | --------------------- | ------------------------------------------- |
| 5     | 60                           | 145             | 120                   | 600                                         |
| 6     | 120                          | 456             | 720                   | 4320                                        |
| 7     | 210                          | 1309            | 5040                  | 35280                                       |
| 8     | 336                          | 3536            | 40320                 | 322560                                      |
| 9     | 504                          | 9153            | 362880                | 3265920                                     |

with this table we can see the huge benefit to pruning compared with the brute force approach. we can also see that the pattern formed is that the number of routes checked to completion is $n(n-1)(n-2)$. in fact this makes sense since at each step, we prune such that the number of routes to examine in the next block is halved, thirded, etc, leaving only $n(n-1)(n-2)=\frac{n!}{(n-3)!}$ routes checked to completion.

we can also see, with some calculation, that the number of actual evaluations (i.e. calculating the cost of a node, and deciding if we should prune it or carry it forward) is equal to $\sum_{r=1}^{n-1} \frac{n!}{(r-2)!(n-r)!}$, this represents the total number of rows in the table plus the number of filled cells in the last block. the equivalent in brute-force is just the number of routes multiplied by the number of nodes to represent the time taken to calculate the cost of a particular route ($n!$ routes, each of length $n$). again we can see that our algorithm is much, much better than brute force in terms of complexity

since we do not need to iteratively calculate the cost of routes at the end, it's done at each step progressively instead, we only need to include the complexity of the process of checking for alternative routes with the same nodes ('ABGD' vs 'AGBD'). my implementation uses a simple $O(n^2)$ bubble sort, so we can say that this implementation has an overall time complexity of $O(n^3\times\sum_{r=1}^{n-1} \frac{n!}{(r-2)!(n-r)!})$, or on the order of $O(n^5)$. generally however this algorithm can be considered $O(\sum_{r=1}^{n-1} \frac{n!}{(r-2)!(n-r)!})$ as described above.

## task 5

![[Art Gallery Problem]]