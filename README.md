# Overview

In this assignment, we will explore binary search trees and their applications. The goal is to build a search structure with fast look-up times, and in this instance, functionality to prove the speed of searches in the tree. As an application of the structure, we will create a program that uses a small real-world data set and presents this data to users on the Java console.

## Objectives

Here is what we'd like you take out of this assignment.

### Course

- Develop a binary search tree and implement pre-, post-, and in-order traversals.
- Demonstrate an understanding of self-balancing routines in a balanced binary search tree.

### Assignment

- To write a search structure based on a binary search tree (BST).
- To calculate the height and depth of nodes in a BST, using the values as proof of a balanced tree.

## Getting Started

To get started, you should download the following project files from [GitHub](https://github.com/your/project/link). Inside of the project files you will see the following folders and files you will be using for this project:

- `BabyNames`: a class that represents the frequency of baby names chosen in a state for a certain year.
- `INamesTree`: defines a tree structure that works with BabyNames objects.
- `NamesTree`: An implementation of the INamesTree interface.
- `states`: a directory containing files with baby name records for the 50 US states.
- `FileIO`: a helper file that reads records from a file in the states directory and converts each line to BabyNames objects.
- `NamesTreeTest`: a JUnit file that verifies that a structure implementing the INamesTree interface actually follows the documentation of the interface.
- `Console`: A helper class for reading and writing to the Java console.
- `ConsoleProgram`: A class with console IO code to allow a user to inspect and interact with the files in the "states" directory.

## Writing a BST Class

Your job for this assignment is to implement a new binary search tree (BST) structure, implementing the INamesTree interface, and then testing your work. Your BST class will look a bit different from what we have implemented in class. The class will not be a generic structure and should be tailored to work primarily with BabyNames objects. For example, the INamesTree interface and BST class should not be generic:

`bst_babies_1.png`
`bst_babies_2.png`

Within the BST, a BabyNames object should be Comparable and sorted based on the name of the baby.

`bst_babies_3.png`

While writing the BST structure you should use the provided unit tests to verify your work, as well as the input files that have been provided. Each file can be read using the static method in the FileIO class to provide large groups of input records to test your tree. To be ready for part #2 of this assignment, your structure should be thoroughly tested and you should be familiar with how to use the FileIO class.

## Writing a BST Iterator

Writing the iterator for a BST can be challenging to do right. If possible, an iterator have the following properties:

- Efficiently access each element in the tree. Care should be taken to avoid redundant traversal of tree elements.
- Avoid using unnecessary space to do the work of the algorithm.

Since the iteration of elements with an iterator is broken up over different calls to hasNext() and next(), you cannot use recursion with your iterator. Moreover, you should avoid traversing over the tree in preparation of using the iterator. This would result in a double iteration. Instead we can simulate the use of the call stack by using the Stack class in Java's Collection framework.

To write your iterator, you should do the following:

- Create a stack of Node objects.
- In the Iterator constructor, traverse from the root to the smallest element in the tree, adding Nodes to the Stack when encountered. The top Node of the Stack will be the first element returned from the Iterator.
- Whenever the next() method is called you will pop() the top element off the Stack, then:
    - If the Node has a right child, add it to the Stack as well. From the right child repeatedly follow any left references to the smallest element beneath it, adding each Node to the Stack as you encounter it. This will ensure that the next element to return from the Iterator is still at the top of the Stack.
    - If there is no right child, then do nothing. The next Node to return is now at the top of the Stack.

For example:

`bst_babies_4.png`
`bst_babies_5.png`

## The Importance of Tree Balance

Maintaining a balanced tree is essential to having a logarithmic growth rates in the following common BST methods: add(), remove(), and contains(). To track how balanced our tree is, we will maintain the height and depth of each Node, by storing these values within fields in the Node itself.

`bst_babies_9.png`

Once these fields are created, you can then update the height or depth of a Node while inserting it into the tree. To calculate the depth of a Node, you will need to count as you traverse to the insertion point. For example:

`bst_babies_6.png`

To calculate the height of a Node, you will need to insert a new Node with a height of zero, and then update the height of all ancestor Node as each recursive call completes. The height of a Node in the tree is calculated as the maximum height of a child Node, plus one. For example:

`bst_babies_7.png`

When complete, you should test the methods related to tree height/depth by assembling a tree and testing your results. You can also run the provided unit tests to verify that the methods are working correctly.

## Writing a Console Program

Lastly, create an interesting console program that allows users to search through the data sets in the inputs files in your project. Each file contains names from different states in the US and should be viewable on the console in a digestible format.

When the program begins the user should be presented with a welcome message.

`bst_babies_13.png`

The user should then be prompted to enter the name of one of the 50 states and a year in the range [1910, 2019].

`bst_babies_14.png`

The user will then be informed that a search tree has been formed with the names of babies found in the input file. The maximum number of comparisons needed to find a name in the tree will be printed, along with the menu for the program.

`bst_babies_15.png`

When the user chooses option #1, all names in the search tree will be printed out to the console.

`bst_babies_16.png`

When the user chooses option #2, they will be prompted to enter a (case-sensitive) name. The data for that name will be identified in the search tree and printed to the console, if found.

`bst_babies_17.png`

If the name is not found an appropriate message will be printed.

`bst_babies_18.png`

When the user chooses option #3, they will be prompted to change the state and year for a new data set. This data set should replace all data in your search tree.

`bst_babies_19.png`

When the user chooses option #4, the program will exit.

`bst_babies_20.png`

## Requirements

This section describes hard requirements for the assignment. Any deviation from these requirements will result in an assignment not being accepted. So please be aware.

- You may not edit any of the provided files that are marked with a "Do not edit this file!" message.
- You may not use any preexisting tree structures to help solve this problem. This includes work we did in class, or previously written BST structures.