1. Huffman encoding is essentially a dictionary encoding scheme, but it uses a clever greedy method to minimise the length and number of dictionary entries it needs.
		- to build the dictionary, we start by enumerating the relative numbers of elements
		- then we start pairing up items to build a binary tree of items, starting with the elements with the fewest instances
		- repeat until we build an entire tree
		- we then encode a single symbol using its address in the tree using binary zero or one to decide which (left or right)
		- to read things back, we just read through the bits one by one and use their values to traverse the tree and output the relevant symbol when we reach a leaf node in the tree
2. MP3 files are psychoacoustically encoded (i.e. they compress by removing a lot of out-of-frequency data that humans can't hear), and are lossy.

![[Pasted image 20231102122921.png]]




