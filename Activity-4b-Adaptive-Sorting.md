# Adaptive Sorting Selection
In part A provided is the code that creates the array of 50 integers, the implementation for seleciton and insertion sort, and a function to dertmine the thershold the array fits into. In trying to label what makes a best fit or near best fit I decided that it would be best to count
the instances in which which A[i] > A [i+1]. If this count was greater than marginal, the case should be labeled as average, unless the count was represented the worst case in which it should be labeled as such.  I figured that this count should be less than or equal to 10% of the data
or in an array of 50, 5 or less.

``` C++
#include <iostream>
#include <vector>
#include <random>
using namespace std;
//random was implemented to generate arrays rather than relying on input each time.

const int N = 50;

/*  Sorting Algorithms  */

//The selection sort implementation
void selectionSort(vector<int>& arr) {
    for (int i = 0; i < arr.size() - 1; i++) {
          int minIndex = i;
        for (int j = i + 1; j < arr.size(); j++) {
            if (arr[j] < arr[minIndex]) {
                  minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

//The insertion sort implementation
void insertionSort(vector<int>& arr) {
    for (int j = 1; j < arr.size(); j++) {
          int key = arr[j];
          int i = j - 1;

        while (i >= 0 && arr[i] > key) {
            arr[i + 1] = arr[i];
            i--;
        }
        arr[i + 1] = key;
    }
}

/*  Classifying the Array  */

int countGreaterThanNext(const vector<int>& arr) {
    int count = 0;
    for (int i = 0; i < arr.size() - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            count++;
        }
    }
    return count;
}
/* Main */

int main() {

    //creating the array
    vector<int> arr(N);
    //taking input for the array.
    cout << "Enter 50 integers:\n";
    for (int i = 0; i < N; i++) {
        cin >> arr[i];
    }
    //counting the inversion
    int inversionCount = countGreaterThanNext(arr);

    //Decision logic for which sorting algorithm to use


    //best case
    if (inversionCount <= 5) {
        cout << "\nDetected: Best/Nearly Sorted Case\n";
        cout << "Using Insertion Sort (O(n) best case)\n";
        insertionSort(arr);
    }
    //worst case
    else if (inversionCount == N - 1) {
        cout << "\nDetected: Worst Case Descending Order\n";
        cout << "Using Selection Sort (more consistent O(n^2))\n";
        selectionSort(arr);
    }
    //avg case
    else {
        cout << "\nDetected: Average Case\n";
        cout << "Using Selection Sort\n";
        selectionSort(arr);
    }
    //output
    cout << "\nSorted Output:\n";
    for (int num : arr) {
        cout << num << " ";
    }


    return 0;
}

```
Since we are just counting the instances where the current index is greater than the next we are not sorting it but are gathering information about how sorted it is. This runs with complexity O(n).

## Defintions
To iterate, The best case, or nearly best case in when the current index is greater than the next only 10% of the time or in 5 cases. In this case we use insertion sort to run in linear time. In average cases we choose Seleciton Sort as its more predictable. In a worst case or when the current index is greater than the next is true for N - 1 cases or
or descending order we choose selection sort.
