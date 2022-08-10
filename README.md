# Multithreaded-Sorting
This program uses multithreading to sort an array of random integers. 

The program accepts user input to determine the size of the array, which is then populated with random integers between 5 and 20. The array is then split in half, and each half is passed to a separate thread for sorting. The two halves are passed to a final thread, which merges the two halves into a final sorted array. 
