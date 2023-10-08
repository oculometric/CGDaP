## task 1
![[Assignment planets diagram]]

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
    csv_data += str(calculate_fuel_cost(seq[0], seq[1], seq[2], seq[3], seq[4])) + "\n"

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

This approach isn't a good way to find the shortest path since it requires checking the cost of `n!` possible routes, `n` being the number of planets. Factorial time, O(n!) is a very very bad time complexity and building a route with many destinations would take a very long time.

## task 2

10 15 12 12 25 16 20 14 28 17
10 12 12 15 16 20 14 25 17 28
10 12 12 15 16 14 20 17 25 28
10 12 12 15 14 16 17 20 25 28
10 12 12 14 15 16 17 20 25 28

sorted using bubble sort

```
Let edge_weights = [10, 15, 12, 12, 25, 16, 20, 14, 28, 17]
Let changed = True
While changed = True:
	Let counter = 0
	changed = False
	While counter < 9:
		If edge_weights[counter] > edge_weights[counter+1]:
			changed = True
			Let temp = edge_weights[counter]
			edge_weights[counter] = edge_weights[counter+1]
			edge_weights[counter+1] = temp
		End If
		Increment counter
	End While
End While
```

this is an implementation of the bubble sort algorithm, which works by going through a list in pairs (bubbles), and swapping the items in the pair according to the sorting rule (e.g. smallest first). by iterating over a list again and again until an iteration is completed without changing the list (at which point it must be sorted). complexity of `O(n^2)`, since the algorithm must pass through the list (of length `n`) at most `n` times (i.e. moving the smallest value from the opposite end of the list), `n*n` gives `O(n^2)` as the complexity.

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

since this algorithm includes the bubble sort, it must be at least `O(n^2)`. since we have to find the index of a planet from its string name, which could require counting all the way through the `n` planets, the worst-case complexity is raised to `O(n^3)`. the final loop traversing the graph has a similar problem, requiring `n` iterations, each time searching the `n` planets to find the right index for mass lookups, making that `O(n^2)`. we can simplify the overall complexity of approximately `O(n^3 + n^2 + n^2)` (there are two index lookups in the final loop) down to `O(n^3 + n^2)` or just `O(n^3)`. using indices to reference planets, or having each one be a pointer to a struct containing name, cargo mass, and edge weightings, we could reduce the complexity to `O(n^2)` at worst.

## task 4
