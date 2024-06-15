# QuickSort

Credits: w3schools, Medium

### What is it?

This is an algorithm used to sort arrays, it is one of the fastest. It's worst case running time may make this algorithm appear rather slow (scales quadratically with array length), its average case running time is faster than most (scales as n*log(n), where n is array length). It is often faster than most algorithms in real world applications.

### What do we use it for?

Quicksort is used in several applications, such as: image rendering, data visualization, and matrix sorting.

### How does it work?

Quicksort works by first selecting a pivot element, common convention is to select the last element in the array as the pivot element. There are other heuristics for selecting the pivot element but they will not be discussed here.

Once the pivot element is selected the array is sorted/re-ordered such that every element less than or equal to the pivot is on the left of the pivot, and every element greater than the pivot is placed on the right of the pivot. 

This process is then repeated on the sub-array from the start of the array to the pivot and the sub-array from the pivot to the end of the array. This algorithm is recursive.

Code Example:

```

# create recursive function to create the new position of the pivot
# input_list = the array to be worked on
# start = starting index of the sub-list currently being worked on
# end = ending index of the sub-list 

def locate_pivot_index(input_list, start, end):

    # get value of the pivot (assume pivot is the last element in the list)
    pivot = input_list[end]
    
    # Strategy:
    #   Locate the first element from the left that is larger than the pivot
    #   Locate first element from the right that is smaller than the pivot
    #   Swap them
    #   Stop iterating when the index of the right element is smaller than the index of the right element
    
    # index of first item from the right that is smaller than pivot
    indexRight = end - 1
    
    # index of first item from left that is bigger than the pivot
    indexLeft = start

    # go through the list and check if each element is bigger or smaller than the pivot
    while indexRight >= indexLeft:
        
        # if the current left number is smaller than the pivot, move on
        if input_list[indexLeft] <= pivot:
            indexLeft += 1
        # if the current right number is bigger than pivot, move on
        elif input_list[indexRight] >= pivot:
            indexRight -= 1
        # if neither is the case, then the elements must be swapped
        else:
            input_list[indexLeft], input_list[indexRight] = input_list[indexRight], input_list[indexLeft]
    
    # put the pivot between the left and right sections
    input_list[end], input_list[indexLeft] = input_list[indexLeft], input_list[end]
    
    return indexLeft

# quicksort main function
def quickSort(input_list, start, end):
    
    # if we have not sorted entire list
    if start < end:
        pivot_index = locate_pivot_index(input_list, start, end)
        # recurse on left side
        quickSort(input_list, start, pivot_index - 1)
        # recurse on right side
        quickSort(input_list, pivot_index + 1, end)

# sort the input heights list
test_list = [2, 5, 7, 1, 8, 6, 7, 5]
quickSort(test_list, 0, len(test_list) - 1) 

```