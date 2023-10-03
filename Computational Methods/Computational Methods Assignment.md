
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

this is an implementation of the bubble sort algorithm, which works by going through a list in pairs (bubbles), and swapping the items in the pair according to the sorting rule (e.g. smallest first). by iterating over a list again and again until an iteration is completed without changing the list (at which point it must be sorted). complexity of O(n^2), since the algorithm must pass through the list (of length `n`) at most `n` times (i.e. moving the smallest value from the opposite end of the list), `n*n` gives `n^2` as the complexity.

## task 3
