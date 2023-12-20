Count distinct element in an array in C
In this section, we will learn, the program to count distinct element in an array in C programming language. Given an integer array, we have to print all the distinct element of the input array. input array may contain duplicate elements, we have to print count of distinct number in an array.

C program to count distinct element in an array
Count of Distinct Numbers in C
Example
Input : arr[6] = {30, 50, 30, 10, 20, 40, 10, 20}
Output : 5
Explanation : The distinct elements are 30, 50, 10, 20, 40
Method 1 :
In this method, we will use to for loops.

Create an auxiliary array named visited of the same size as the original array.
Mark all items of the visited array as 0. Which means they are unvisited.
Starting from the leftmost, for each item that is marked unvisited start traversing its succeeding elements.
If you encounter any element with the same value mark it visited i.e. change visited[i] = 1
Once you traverse all succeeding items increase the count by 1
Repeat same steps for other unvisited items in the array
count number of distinct elements in an array in c
Related Pages
Sorting elements of an array by frequency

Finding the Longest Palindrome in an Array

Finding  Repeating elements in an Array

Finding Non Repeating elements in an Array

Removing Duplicate elements from an array

Method 1 Code in C
Run
// Time Complexity : O(N^2)
// Space Complexity : O(N)

#include<stdio.h>
#include<stdlib.h>

// Main function to run the program
int main() 
{ 
    int arr[] = {30, 50, 30, 10, 20, 40, 10, 20}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    int visited[n] = {0};// marking all items 0(unvisited)
    int count_dis=0;
    
    for(int i=0; i < n; i++)
    {
        // only if unvisited
        if(visited[i]==0)
        {
            for(int j = i+1; j < n; j++){
                // if item appears again in the array
                if(arr[i] == arr[j]){
                    // mark visited
                    visited[j] = 1;
                }
            }
            // increase count as current array item counted
            // and future indexes with same value marked visited
            count_dis++;
        }
    }
   printf("Distinct items : %d ",count_dis);
   return 0; 
}
Output
Distinct items : 5
Method 2 (without extra space)
In the previous method, we were using extra N space for another visited array which is not ideal. In this method, we will do it without extra space. The whole logic behind this method lies on the following principle –
Traverse the array, there may be duplicates
Make the decision to increase the count of the distinct item only at the last occurrence of an item
Example : {10, 20, 30, 10, 40, 50} Count for 10 will not be increased for 0th index traversal but will be increased for 3rd index.
Method 2 Code
Run
// Time Complexity : O(n^2)
// Space Complexity : O(1)
#include<stdio.h>

int countDistinct(int *array, int size){
    int count = 0;
    
    // Increase count only at last occurrence of item in array
    for (int i = 0; i < size; i++){
        
        int j = 0;
        // traverse rightwards
        for (j = i+1; j < size; j++)
        {   
            // if found duplicated found rightwards in the array
            if (array[i] == array[j]){
                break;
            }
        }
        // if traversed till the end of the array no break happenned
        //  thus, this must have been last occurrence of arr[i]
        if (j == size)
            count++;
    }
    return count;
}

int main()
{
    int arr[] = {5, 8, 5, 7, 8, 10};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    printf("Distinct items: %d",countDistinct(arr, size));
    
    return 0;
}
Output
Distinct items: 4
While loop in C
Method 3 (Using sorting)
If the array is sorted already then the time complexity to find distinct reduces to O(N). However, if we get an unsorted array we may have to sort the array first to use the below approach. We have used bubble sort(Time complexity: O(N^2). But you can use Merge Sort or Quick Sort, which will reduce the sorting time complexity to O(n log(n))
Method 3 Code
Run
// Time Complexity : O(n^2)
// O(n^2) : sort the array and O(n) to count distincts
// Space Complexity : O(1)
#include<stdio.h>

// we use a sorted array to count distincts
// again, decision to count happens 
// at the last occurrence in sorted array
int countDistinct(int arr[], int n){
    
    // Traverse the sorted array
    // arr = {5, 5, 7, 8, 8, 10}
    int count = 0;
    for (int i = 0; i < n; i++) {
 
        // Move the index ahead whenever
        // you encounter duplicates
        while (i < n - 1 && arr[i] == arr[i + 1])
            i++;
 
        count++;
    }
 
    return count;
}

// using bubble sort to sort the array
// you can use a better sorting algorithm to reduce 
// time complexity to O(n log n) to sort
int bubbleSort(int arr[], int size){
    for (int i = 0; i < size-1; i++){       

    // Since, after each iteration righmost i elements are sorted   
    for (int j = 0; j < size-i-1; j++) if (arr[j] > arr[j+1]) 
        {
            int temp = arr[j]; // swap the element
            arr[j] = arr[j+1]; 
            arr[j+1] = temp; 
        }
    }
}
int main()
{
    int arr[] = {5, 8, 5, 7, 8, 10};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    bubbleSort(arr, size);

    printf("Distict items: %d",countDistinct(arr, size));
    
    return 0;
}
Output
Distict items: 4
