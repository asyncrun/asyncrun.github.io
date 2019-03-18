---
layout: post
title: BinarySearchTree
categories: [算法]
description: BinarySearchTree
keywords: BinarySearchTree
---

# Binary Search Tree

**Binary Search Tree** is a node-based binary tree data structure which has the following properties:

 - The left subtree of a node contains only nodes with keys lesser than the node's key.
 - The right subtree of a node contains only nodes with keys greater than the node's key.
 - The left and right subtree each must also be a binary search tree. There must be no duplicate nodes.


 
```cpp
#pragma once

struct node
{
	int key;
	struct node *left, *right;
};

struct node *newNode(int key)
{
	const auto temp = static_cast<struct node *>(malloc(sizeof(struct node)));
	temp->key = key;
	temp->left = temp->right = nullptr;
	return temp;
}

void inorder(struct node *root)
{
	if(root != nullptr)
	{
		inorder(root->left);
		printf("%d \n", root->key);
		inorder(root->right);
	}
}

struct node* insert(struct node* node, int key)
{
	if (node == nullptr) return newNode(key);
	if(key < node->key)
	{
		node->left = insert(node->left, key);
	}
	else if(key > node->key)
	{
		node->right = insert(node->right, key);
	}

	return node;
}


int BinarySearchTreeTest()
{
	struct node *root = nullptr;
	root = insert(root, 50);
	insert(root, 30);
	insert(root, 20);
	insert(root, 40);
	insert(root, 70);
	insert(root, 60);
	insert(root, 80);

	inorder(root);

	return 0;
}
```