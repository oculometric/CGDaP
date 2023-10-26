1. merge sort, quicksort
2. merge sort - break the list in half recursively, until you end up with only one, then merge them with insertion sorting incrementally until you merge the whole list (see quick sort below)
3. 

C - 1
H - 2
A - 3
L - 4
E - 5
N - 6
G - 7
e - 8

L E A L E C G H N
4 5 3 4 8 1 7 2 6

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

| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | start | end | i   | j   | pivot | notes                                                          |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | ----- | -------------------------------------------------------------- |
| 4   | 5   | 3   | 4   | 8   | 1   | 7   | 2   | 6   | 0     | 8   | -1  | 9   | 6     | start sort                                                     |
|     |     |     |     |     |     |     |     |     |       |     | 0   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 1   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 3   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 8   |       |                                                                |
| 4   | 5   | 3   | 4   | 6   | 1   | 7   | 2   | 8   |       |     |     |     |       | swap 4 and 8                                                   |
|     |     |     |     |     |     |     |     |     |       |     | 5   | 8   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 6   | 8   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 6   | 7   |       |                                                                |
| 4   | 5   | 3   | 4   | 6   | 1   | 2   | 7   | 8   |       |     |     |     |       | swap 6 and 7                                                   |
|     |     |     |     |     |     |     |     |     |       |     | 7   | 7   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 7   | 6   |       | partition done                                                 |
| 4   | 5   | 3   | 4   | 6   | 1   | 2   |     |     | 0     | 6   | -1  | 7   | 2     | subsort first half                                             |
|     |     |     |     |     |     |     |     |     |       |     | 0   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     |     |     |       | swap 0 and 6                                                   |
| 2   | 5   | 3   | 4   | 6   | 1   | 4   |     |     |       |     |     |     |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 1   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 1   | 5   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     |     |     |       | swap 1 and 5                                                   |
| 2   | 1   | 3   | 4   | 6   | 5   | 4   |     |     |       |     |     |     |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 5   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 4   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 3   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 2   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 1   |       | partition done                                                 |
| 2   | 1   |     |     |     |     |     |     |     | 0     | 1   | -1  | 2   | 2     | subsort first half of first half                               |
|     |     |     |     |     |     |     |     |     |       |     | 0   | 2   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 0   | 1   |       |                                                                |
| 1   | 2   |     |     |     |     |     |     |     |       |     |     |     |       | swap 0 and 1                                                   |
|     |     |     |     |     |     |     |     |     |       |     | 1   | 1   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 1   | 0   |       | subsort done                                                   |
|     |     | 3   | 4   | 6   | 5   | 4   |     |     | 2     | 6   | 1   | 7   | 6     | subsort second half of first half                              |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 7   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 3   | 7   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 7   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 6   |       |                                                                |
|     |     | 3   | 4   | 4   | 5   | 6   |     |     |       |     |     |     |       | swap 4 and 6                                                   |
|     |     |     |     |     |     |     |     |     |       |     | 5   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 6   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 6   | 5   |       | partition done                                                 |
|     |     | 3   | 4   | 4   | 5   |     |     |     | 2     | 5   | 1   | 6   | 4     | subsort first half of second half of first half                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 3   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 3   | 5   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 3   | 4   |       |                                                                |
|     |     | 3   | 4   | 4   | 5   |     |     |     |       |     |     |     |       | swap 3 and 4                                                   |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 4   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 3   |       | partition done                                                 |
|     |     | 3   | 4   |     |     |     |     |     | 2     | 3   | 1   | 4   | 3     | subsort first half of first half of second half of first half  |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 4   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 3   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 2   | 2   |       | subsort done                                                   |
|     |     |     |     | 4   | 5   |     |     |     | 4     | 5   | 3   | 6   | 4     | subsort second half of first half of second half of first half |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 6   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 5   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 4   | 4   |       | subsort done                                                   |
|     |     |     |     |     |     |     | 7   | 8   | 7     | 8   | 6   | 9   | 7     | subsort second half                                            |
|     |     |     |     |     |     |     |     |     |       |     | 7   | 9   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 7   | 8   |       |                                                                |
|     |     |     |     |     |     |     |     |     |       |     | 7   | 7   |       | subsort done                                                   |
| 1   | 2   | 3   | 4   | 4   | 5   | 6   | 7   | 8   |       |     |     |     |       | sort done                                                      |

C H A L L E N G e

