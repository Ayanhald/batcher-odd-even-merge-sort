# batcher-odd-even-merge-sort
#include <iostream>

void compareSwap(int &a, int &b) {
    if (a > b) {
        int temp = a;
        a = b;
        b = temp;
    }
}

void batcherMerge(int arr[], int start, int end, int step) {
    int mid = start + step;
    int right = mid + step;
    if (right <= end) {
        batcherMerge(arr, start, end, step * 2);
        batcherMerge(arr, mid, end, step * 2);
        for (int i = start + step; i < end; i += step * 2) {
            compareSwap(arr[i], arr[i + step]);
        }
    } else {
        compareSwap(arr[start], arr[mid]);
    }
}

void oddEvenMergeSort(int arr[], int start, int end) {
    if (end > start) {
        int mid = (start + end) / 2;
        oddEvenMergeSort(arr, start, mid);
        oddEvenMergeSort(arr, mid + 1, end);
        batcherMerge(arr, start, end, 1);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {5, 8, 3, 9, 1, 6, 2, 7, 4};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original array: ";
    printArray(arr, size);

    oddEvenMergeSort(arr, 0, size - 1);

    std::cout << "Sorted array: ";
    printArray(arr, size);

    return 0;
}
