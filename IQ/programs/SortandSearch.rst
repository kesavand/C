================================================================================
what is Sorting ?
Sorting is arranging data in a particular order.
================================================================================
what are the important sorting algorithms and explain ?
Important sorting algorithms
1. Insertion sort
2. Bubble sort
3. merge sort 
4. Quick sort
5. Heap sort

================================================================================
1. Insertion Sort
-----------------
Insertion sort is th most basic sorting technique, 
it can be if the data is small.
Algorithm
----------
// Sort an arr[] of size n
insertionSort(arr, n)
Loop from i = 1 to n-1.
Pick element arr[i] and insert it into sorted sequence arr[0…i-1]

Program
-------
/* Function to sort an array using insertion sort*/
void insertionSort(int arr[], int n)
{
   int i, key, j;
   for (i = 1; i < n; i++)
   {
       key = arr[i];
       j = i-1;
 
       /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
       while (j >= 0 && arr[j] > key)
       {
           arr[j+1] = arr[j];
           j = j-1;
       }
       arr[j+1] = key;
   }
}
================================================================================
A Insertion sort that uses binary search is more efficient, below is the 
implementation for insertion sort using binary search
// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;
 
    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];
 
        // find location where selected sould be inseretd
        loc = binarySearch(a, selected, 0, j);
 
        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j+1] = a[j];
            j--;
        }
        a[j+1] = selected;
    }
}
================================================================================
2. Bubble Sort 

Bubble Sort is the simplest sorting algorithm that works by repeatedly 
swapping the adjacent elements if they are in wrong order.
The Bubble sort is also like the insertion sort in the sense it can be used 
only for small data sets

Program
-------
void swap(int *xp, int *yp)
{
    int temp = *xp;
    *xp = *yp;
    *yp = temp;
}
 
// A function to implement bubble sort
void bubbleSort(int arr[], int n)
{
   int i, j;
   for (i = 0; i < n-1; i++)      
 
       // Last i elements are already in place   
       for (j = 0; j < n-i-1; j++) 
           if (arr[j] > arr[j+1])
              swap(&arr[j], &arr[j+1]);
}
 
/* Function to print an array */
void printArray(int arr[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", arr[i]);
    printf("n");
}
 
// Driver program to test above functions
int main()
{
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    bubbleSort(arr, n);
    printf("Sorted array: \n");
    printArray(arr, n);
    return 0;
}

================================================================================

2. Merge Sort 
-------------
Merge Sort is a Divide and Conquer algorithm. It divides input array in two 
halves, calls itself for the two halves and then merges the two sorted halves. 
The merge() function is used for merging two halves. The merge(arr, l, m, r) 
is key process that assumes that arr[l..m] and arr[m+1..r] are sorted and merges
the two sorted sub-arrays into one. See following C implementation for details.

The merge sort is fast for arrays with huge data say for example in lakhs.

Algorithm
---------
MergeSort(arr[], l,  r)
If r > l
     1. Find the middle point to divide the array into two halves:  
             middle m = (l+r)/2
     2. Call mergeSort for first half:   
             Call mergeSort(arr, l, m)
     3. Call mergeSort for second half:
             Call mergeSort(arr, m+1, r)
     4. Merge the two halves sorted in step 2 and 3:
             Call merge(arr, l, m, r)

			 
Program:
-------
// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    /* create temp arrays */
    int L[n1], R[n2];
 
    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];
 
    /* Merge the temp arrays back into arr[l..r]*/
    i = 0; // Initial index of first subarray
    j = 0; // Initial index of second subarray
    k = l; // Initial index of merged subarray
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
 
    /* Copy the remaining elements of L[], if there
       are any */
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }
 
    /* Copy the remaining elements of R[], if there
       are any */
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}
 
/* l is for left index and r is right index of the
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
    if (l < r)
    {
        // Same as (l+r)/2, but avoids overflow for
        // large l and h
        int m = l+(r-l)/2;
 
        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
 
        merge(arr, l, m, r);
    }
}
 
/* UTILITY FUNCTIONS */
/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", A[i]);
    printf("\n");
}
 
/* Driver program to test above functions */
int main()
{
    int arr[] = {12, 11, 13, 5, 6, 7};
    int arr_size = sizeof(arr)/sizeof(arr[0]);
 
    printf("Given array is \n");
    printArray(arr, arr_size);
 
    mergeSort(arr, 0, arr_size - 1);
 
    printf("\nSorted array is \n");
    printArray(arr, arr_size);
    return 0;
}
3. QuickSort 
------------
Like Merge Sort, QuickSort is a Divide and Conquer algorithm. It picks an element as pivot and partitions the given array around the picked pivot. 
There are many different versions of quickSort that pick pivot in different ways.

Always pick first element as pivot.
Always pick last element as pivot (implemented below)
Pick a random element as pivot.
Pick median as pivot.

Program
TBD

4. Heap Start 
-------------

Heap sort is a comparison based sorting technique based on Binary Heap data structure.A Binary Heap is a Complete Binary Tree where items are stored 
in a special order such that value in a parent node is greater(or smaller) than the values in its two children nodes. 
The former is called as max heap and the latter is called min heap. The heap can be represented by binary tree or array.

NOTE: A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled,and all nodes are as far left as possible 

Heap Sort Algorithm for sorting in increasing order:
1. Build a max heap from the input data.
2. At this point, the largest item is stored at the root of the heap. Replace it with the last item of the heap followed by reducing the size of heap by 1. Finally, heapify the root of tree.
3. Repeat above steps while size of heap is greater than 1.

// C++ program for implementation of Heap Sort
#include <iostream>
using namespace std;
 
// To heapify a subtree rooted with node i which is
// an index in arr[]. n is size of heap
void heapify(int arr[], int n, int i)
{
    int largest = i;  // Initialize largest as root
    int l = 2*i + 1;  // left = 2*i + 1
    int r = 2*i + 2;  // right = 2*i + 2
 
    // If left child is larger than root
    if (l < n && arr[l] > arr[largest])
        largest = l;
 
    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest])
        largest = r;
 
    // If largest is not root
    if (largest != i)
    {
        swap(arr[i], arr[largest]);
 
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}
 
// main function to do heap sort
void heapSort(int arr[], int n)
{
    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
 
    // One by one extract an element from heap
    for (int i=n-1; i>=0; i--)
    {
        // Move current root to end
        swap(arr[0], arr[i]);
 
        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}
 
/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i=0; i<n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}
 
// Driver program
int main()
{
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);
 
    heapSort(arr, n);
 
    cout << "Sorted array is \n";
    printArray(arr, n);
}


==============================================
Searching Algorithms
====================
what are the different searching algorithms 
Liner search 
Binary search 
sublist search
substring search
Front&Back Search


Binary Search
-------------
Program
-------
int binarySearch(int a[], int item, int low, int high)
{
    if (high <= low)
        return (item > a[low])?  (low + 1): low;
 
    int mid = (low + high)/2;
 
    if(item == a[mid])
        return mid+1;
 
    if(item > a[mid])
        return binarySearch(a, item, mid+1, high);
    return binarySearch(a, item, low, mid-1);
}

Front & Back Search 
-------------------
Front and Back search algorithm for finding element with value x works the following way:

Initialize indexes front and back pointing to first and last element respectively of the array.
If front is greater than rear, return false.
Check the element x at front and rear index.
If element x is found return true.
Else increment front and decrement rear and go to step 2.

Key Points:
The worst case complexity is O(n/2) (equivalent to O(n)) when element is in the middle or not present in the array.
The best case complexity is O(1) when element is first or last element in the array.

Program
-------
// CPP program to implement front and back
// search
#include<iostream>
using namespace std;
 
bool search(int arr[], int n, int x)
{
    // Start searching from both ends
    int front = 0, back = n - 1;
 
    // Keep searching while two indexes
    // do not cross.
    while (front <= back)
    {
        if (arr[front] == x || arr[back] == x)
          return true;
        front++;
        back--;
    }
    return false;
}
 
int main()
{
   int arr[] = {10, 20, 80, 30, 60, 50,
                     110, 100, 130, 170};
   int x = 130;
   int n = sizeof(arr)/sizeof(arr[0]);
   if (search(arr, n, x))
      cout << "Yes";
   else
      cout << "No";
   return 0;
}



