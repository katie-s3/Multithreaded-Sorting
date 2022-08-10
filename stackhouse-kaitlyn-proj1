//Kaitlyn Stackhouse
//COMP323 Project 1

#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <pthread.h>

//global variables
int size;
int half;
int *nums;
int *finalNums;

//define structs to pass to threads
typedef struct {
  int idx;
  int *arr;
} params;

typedef struct {
  int *arr1;
  int *arr2;
} params2;

//pointers to functions
void* halfSort(void *arg);
void* merge(void *arg);

int main(void) {
  printf("Kaitlyn Stackhouse\nProject 1\n");
  printf("-------------\n");

  
  //Get array size
  printf("Enter array size: ");
  scanf("%d", &size);
  printf("\n");

  
  //Initialize variables
  half = size / 2;
  nums = (int*)malloc(size * sizeof(int));
  finalNums = (int*)malloc(size * sizeof(int));
  pthread_t tid1, tid2, tid3;

  
  //Populate array with random numbers
  srand(time(0));
  printf("Before Sort: ");
  for (int i = 0; i < size; i++) {
    nums[i] = rand() % (20 + 1 - 5) + 5;
    printf("%d, ", nums[i]);
  }
  printf("\n\n");

  
  //Populate data structures
  params *firstHalf = (params *) malloc(sizeof(params));
  firstHalf->idx = 0;
  firstHalf->arr = nums;

  params *secondHalf = (params *) malloc(sizeof(params));
  secondHalf->idx = half;
  secondHalf->arr = nums;

  params2 *mergeData = (params2 *) malloc(sizeof(params2));
  mergeData->arr1 = firstHalf->arr;
  mergeData->arr2 = secondHalf->arr;
  

  //Thread creation and joining
  pthread_create(&tid1, NULL, halfSort, (void*) firstHalf);
  pthread_create(&tid2, NULL, halfSort, (void*) secondHalf);
  pthread_join(tid1, NULL);
  pthread_join(tid2, NULL);
  
  pthread_create(&tid3, NULL, merge, (void*) mergeData);
  pthread_join(tid3, NULL);


  //Print sorted array
  printf("\nAfter Sort: ");
  for (int i = 0; i < size; i++) {
    printf("%d, ", finalNums[i]);
  }
  printf("\n");

  free(nums);
  return 0;
}

//Helper function to swap elements
void swap(int *x, int *y) {
  int temp = *x;
  *x = *y;
  *y = temp;
}

//Sorting functions
void *halfSort(void *arg) {
  params *data = (params *) arg;
  int stop;

  //determine which half of array to sort
  if (data->idx < half) {
    stop = half;
  }
  else {
    stop = size;
  }

  //sort half of array
  int i, j, min;
    for (i = data->idx; i < stop; i++) {
      min = i;
      for (j = i + 1; j < stop; j++)
        if (data->arr[j] < data->arr[min])
          min = j;
 
      swap(&data->arr[min], &data->arr[i]);
    }

  //print half of the array that was sorted
  printf("Half Sorted: ");
  for (i = data->idx; i < stop; i++) {
    printf("%d, ", data->arr[i]);
  }
  printf("\n");
  
  pthread_exit(0);
}

void *merge(void *arg) {
  params2 *data = (params2 *) arg;
  int *fHalf = data->arr1;
  int *sHalf = data->arr2;

  //merge to sorted halves into final array
  int i = 0, j = half, k = 0;
  while (i < half && j < size) {
    if (fHalf[i] < sHalf[j]) {
      finalNums[k++] = fHalf[i++];
    }
    else {
      finalNums[k++] = sHalf[j++];
    }
  }

  //populate rest of final array with remaining elements
  while (i < half) {
    finalNums[k++] = fHalf[i++];
  }

  while (j < size) {
    finalNums[k++] = sHalf[j++];
  }
  
  pthread_exit(0);
}
