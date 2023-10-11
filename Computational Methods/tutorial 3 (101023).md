queues
```
// Front points to the first item
// Back points to the next space where an item will be emplaced

Function Enqueue:
	If back == capacity:
		If front == 0:
			Return
		Else
			Shuffle()
		End If
	End If
	queue[back] = new_item
	Increment back
End Function

Function Dequeue:
	If back == front:
		Return Null
	End If
	Let value = queue[front]
	queue[front] = Null
	Increment front
	Return value
End Function

Function Shuffle:
	If front == 0:
		Return
	Let new_index = 0
	Let old_index = front
	While old_index < back:
		queue[new_index] = queue[old_index]
		Increment new_index
		Increment old_index
	End While
	front = 0
	back = new_index
End Function
```

trees
```
Structure tree_node:
	Let value = Null
	Let children = []
End Structure

Function find(value, parent):
	If parent->value == value:
		Return parent
	End If
	Let index = 0
	While index < Length of parent->children:
		Let child = parent->children[index]
		Let result = find(value, child)
		If result Not Null:
			Return result
		End If
	End While
	Return Null
End Function

Function 
```