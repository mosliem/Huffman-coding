#include <iostream>
#include <string>
#include <queue>
#include <unordered_map>
#include <conio.h>
using namespace std;

#define EMPTY_STRING ""

// A Tree node
struct Node
{
	char ch;
	int freq;
	Node* left, * right;
};

// Function to allocate a new tree node
Node* getNode(char ch, int freq, Node* left, Node* right)
{
	Node* node = new Node();
	
	node->ch = ch;
	node->freq = freq;
	node->left = left;
	node->right = right;

	return node;
}

// Comparison object to be used to order 
struct comp
{
	bool operator()(Node* l, Node* r)
	{
		return l->freq > r->freq;
	}
};

//check if Huffman Tree contains only a single node
bool isLeaf(Node* root) {
	return root->left == nullptr && root->right == nullptr;
}

// Traverse the Huffman Tree and store Huffman Codes in a map.
void encode(Node* root, string str, unordered_map<char, string>& huffmanCode)
{
	if (root == nullptr) {
		return;
	}
	if (isLeaf(root)) {
		huffmanCode[root->ch] = (str != EMPTY_STRING) ? str : "1";
	}

	encode(root->left, str + "0", huffmanCode); // assign 0 for left node
	encode(root->right, str + "1", huffmanCode); // assign 1 to the right node
}

// Traverse the Huffman Tree and decode the encoded string
void decode(Node* root, int& index, string str)
{
	if (root == nullptr) {
		return;
	}

	// found a leaf node
	if (isLeaf(root)) {
		cout << root->ch;
		return;
	}

	index++;
	// if the index is 0 then the path is left and the opposite is true
	if (str[index] == '0')
	{
		decode(root->left, index, str);
	}
	else 
	{
		decode(root->right, index, str);
	}
}

void HuffmanTree(string text)
{
	// empty string
	if (text == EMPTY_STRING) {
		return;
	}

	unordered_map<char, int> freq;

	for (char ch : text) 
	{
		freq[ch]++;
	}
   
	priority_queue<Node*, vector<Node*>, comp> pq; // create a piority queue

	//creating the tree nodes and assign it to the piority queue
	for (auto pair : freq) {
		pq.push(getNode(pair.first, pair.second, nullptr, nullptr));
	}

	while (pq.size() != 1)
	{

		Node* left = pq.top();
		pq.pop();
		Node* right = pq.top();
		pq.pop();

		int sum = left->freq + right->freq;
		pq.push(getNode('\0', sum, left, right));
	}

	Node* root = pq.top(); // assign the root to the final element in the queue

	unordered_map<char, string> huffmanCode; // create a map to assign the code to each char
	encode(root, EMPTY_STRING, huffmanCode);

	string str;
	cout << "Huffman Codes are: " << endl;

	for (auto pair : huffmanCode) {
		cout << pair.first << " " << pair.second << '\n';
	}


	for (char ch : text) {
		str += huffmanCode[ch]; //assign codes of char to the sting to print it
	}
	cout << "\nEncoded text is: " << endl << str << endl;


	cout << endl << "Decoded text is: " << endl;
	// special case for one char string like aaaaa or a sigle node
	 
	if (isLeaf(root))
	{
		while (root->freq--) {
			cout << root->ch;
		}
	}
	else
	{
		int index = -1;
		while (index < (int)str.length() - 1)
		{
			//cout << index << endl;
			decode(root, index, str);
		}
	}
}

int main()
{
	cout << "Welecome !" << endl;
	cout << "Enter The text you want to encode it : " << endl;
	string text;
	getline(cin, text);
	system("cls");
	HuffmanTree(text);
}
