---
num: "Lecture 18"
desc: "Binary Search Trees cont."
ready: true
lecture_date: 2021-11-30 17:00:00.00-7:00
---

Recorded Lecture: [11-30-21](https://drive.google.com/file/d/1PxESObFUtPfaeRLoREWDRUUrtoVBmyT_/view?usp=sharing)

# BST Deletion

* We can break up deletion in three cases:
	* **Case 1:** When the node to be deleted is a leaf node (no children)
	* **Case 2:** When the node to be deleted has one child
	* **Case 3:** When the node to be deleted has two children

## Case 1: Delete a leaf node
* Find the node that needs to be deleted
* Simply remove the parent reference (either left child or right child) to the deleted node

![BSTDeleteCase1.png](BSTDeleteCase1.png)

## Case 2: Delete a node with one child
* Connect the deleted Node’s parent and the deleted Node’s child together

![BSTDeleteCase2.png](BSTDeleteCase2.png)

## Case 3: Delete a node with two children
* First find the successor (node with next greater value) in the right subtree
	* This can be done by traversing the left children of the node to be deleted’s right subtree
	* Also note that the successor will always only have **at most** one child
		* If the successor had a left child, then it wouldn’t be the successor!
* Temporarily store the successor and delete the successor from the tree
	* Deleting the successor will fall in either Case 1 or Case 2
* Replace the deleted node’s value with the successor’s value

![BSTDeleteCase3.png](BSTDeleteCase3.png)

# BST Deletion Implementation

```
# BinarySearchTree.py (continuing on from last lecture)

def delete(self,key):
	if self.size > 1:
		nodeToRemove = self._get(key,self.root)
		if nodeToRemove:
			self.remove(nodeToRemove) # remove modifies the tree
			self.size = self.size-1
		else:
			raise KeyError('Error, key not in tree')
	elif self.size == 1 and self.root.key == key:
		self.root = None
		self.size = self.size - 1
	else:
		raise KeyError('Error, key not in tree')

# Used to remove the node and account for BST deletion cases
def remove(self,currentNode):
	# Case 1: Node to remove is leaf
	if currentNode.isLeaf():
		if currentNode == currentNode.parent.leftChild:
			currentNode.parent.leftChild = None
		else:
			currentNode.parent.rightChild = None

	# Case 3: Node to remove has both children
	elif currentNode.hasBothChildren():
		# Need to find the successor, remove successor, and replace
		# currentNode with successor's data / payload
		succ = currentNode.findSuccessor()
		succ.spliceOut()
		currentNode.key = succ.key
		currentNode.payload = succ.payload

	# Case 2: Node to remove has one child
	else:
		# Node has leftChild
		if currentNode.hasLeftChild():
			if currentNode.isLeftChild():
				currentNode.leftChild.parent = currentNode.parent
				currentNode.parent.leftChild = currentNode.leftChild
			elif currentNode.isRightChild():
				currentNode.leftChild.parent = currentNode.parent
				currentNode.parent.rightChild = currentNode.leftChild
			else: # currentNode is the Root
				currentNode.replaceNodeData(currentNode.leftChild.key,
					currentNode.leftChild.payload,
					currentNode.leftChild.leftChild,
					currentNode.leftChild.rightChild)
            
		# Node has rightChild
		else:
			if currentNode.isLeftChild():
				currentNode.rightChild.parent = currentNode.parent
				currentNode.parent.leftChild = currentNode.rightChild
			elif currentNode.isRightChild():
				currentNode.rightChild.parent = currentNode.parent
				currentNode.parent.rightChild = currentNode.rightChild
			else:
				currentNode.replaceNodeData(currentNode.rightChild.key,
					currentNode.rightChild.payload,
					currentNode.rightChild.leftChild,
					currentNode.rightChild.rightChild)

# Used for pytesting
def inOrder(self, node):
	ret = ""
	if node != None:
		ret += self.inOrder(node.leftChild)
		ret += str(node.key) + " "
		ret += self.inOrder(node.rightChild)
	return ret
```
```
# TreeNode.py (continuing on from last lecture)

def findSuccessor(self):
	succ = None
	# Check if node has a right subtree...
	if self.hasRightChild():
		# traverse through left children (min)
		succ = self.rightChild.findMin()
	return succ

# Find minimum value in a subtree by walking down the left children
def findMin(self):
	current = self
	while current.hasLeftChild():
		current = current.leftChild
	return current

# Used to delete the successor
def spliceOut(self):
	# Case 1:
	# If node to be removed is a leaf, set parent's left or right
	# child references to None
	if self.isLeaf():
		if self.isLeftChild():
			self.parent.leftChild = None
		else:
			self.parent.rightChild = None

	# Case 2:
	# Not a leaf node. Should only have a right child for BST
	# removal
	elif self.hasAnyChildren():
		if self.hasRightChild():
			if self.isLeftChild():
				self.parent.leftChild = self.rightChild
			else:
				self.parent.rightChild = self.rightChild
			self.rightChild.parent = self.parent

# Note: This code only goes through the findSuccessor and spliceOut functionality necessary
# for BST maintenance. There are more general cases that the textbook covers that you should 
# read through and understand
```
```
# pytests

def test_deleteRoot():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	BST.put(15, "fifteen")
	BST.put(5, "five")
	BST.put(3, "three")
	BST.put(7, "seven")
	BST.put(12, "twelve")
	BST.put(17, "seventeen")
	assert BST.inOrder(BST.root) == "3 5 7 10 12 15 17 "
	BST.delete(10)
	assert BST.inOrder(BST.root) == "3 5 7 12 15 17 "

def test_deleteLeafNode():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	BST.put(15, "fifteen")
	BST.put(5, "five")
	BST.put(3, "three")
	BST.put(7, "seven")
	BST.put(12, "twelve")
	BST.put(17, "seventeen")
	BST.delete(3)
	assert BST.inOrder(BST.root) == "5 7 10 12 15 17 "
	BST.delete(17)
	assert BST.inOrder(BST.root) == "5 7 10 12 15 "

def test_deleteNodeWithTwoChildren():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	BST.put(15, "fifteen")
	BST.put(5, "five")
	BST.put(3, "three")
	BST.put(7, "seven")
	BST.put(12, "twelve")
	BST.put(17, "seventeen")
	BST.delete(15)
	assert BST.inOrder(BST.root) == "3 5 7 10 12 17 "
	BST.delete(5)
	assert BST.inOrder(BST.root) == "3 7 10 12 17 "
```
