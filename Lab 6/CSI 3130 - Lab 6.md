# CSI 3130 - Lab 6

Class: CSI 3130
Created: October 31, 2022 12:30 PM
Type: Lab

# Lab 6 - **C  Programming: Pointers, Structures and Dynamic Memory Allocation**

## Pointers

A pointer is merely an address of where a datum or structure is stored

- All pointers are typed based on the type of entity that they point to.
- To declare a pointer, use * preceding the variable name as in int *x;
    
    (** with a pointer variable indicates a deferencing operation)*
    
- To set a pointer to a variable’s address use & before the variable. Eg. x = &y;
*& means “return the memory address of” in this example, x will now point to y, that is, x stores y’s address*
- If you access x, you merely get the address. To get the value that x points to, use * as in *x
*x = *x + 1; will add 1 to y

### Using pointers with arrays

- Consider a pointer **int *ip ****and an array **int z[10]**
- **ip = &z[0];** sets our pointer to point at the first element of the array
In fact, z is a pointer as well and we can access **z[0]** either using **z[0], *ip, or *z**
- To access **z[1]**, we can do **z[1]** as usual, or we can add 1 to the location pointed to by **ip** or **z**, that is ***(ip+1)** or ***(z+1)**
    
    Note: While we can reset ip to be ip = ip+1, we cannot reset z to be z = z+1. Adding 1 to ip will point to z[1], but if z = z + 1 were legal, we would lose access to the first array location since z is our array variable.
    
- Iterating through the array:
    
    ```c
    int j, n=5, a[]={1,2,3,4,5};
                                             
    for(j = 0; j < n; j++){
    		a[j]++;
    }
    
    int *pj;
    for(pj = a; pj < a + n; pj++){
       (*pj)++;
    }    
    ```
    

### Programming examples

You can go through the code examples and try implementing your own functions.

```c
/*Developed by Johan Fernandes
Revised by Daniel Lobo
Course: CSI 3130*/
#include <stdio.h>
#define MAX 5  //constant

//Function declarations
void printArray(int size, int n[size]);
void print2DArray(int size, int n[][size]);
void swap(int *x1, int *x2);
void bubbleSort(int size, int n[size]);

int main(void) {

  int *pc;
  int c;
  int n_ary[MAX] = {0};

  int m1[2][2] = {{4,7},{6,9}};
  int m2[2][2] = {{0}};

  printf("Enter an integer value \n");
  scanf("%d", &c);

  /* Note: * with a pointer variable indicates a deferencing operation */
  //Pointers to numerical values
  pc = &c;
  printf("Value of c : %d\n",c);
  printf("Adress of c : %p\n",&c);
  printf("Value of pointer pc : %p\n", pc);
  //Changing the value of c through pointer pc
  printf("Value of c : %d\n", *pc);
  printf("Value of c : %d\n", ++(*pc));
  printf("Value of c : %d\n", (*pc)--);
  //Displaying the final changes
  printf("Value of c : %d\n",c);

  /*Dealing with Arrays*/
  //Print an all 0 array
  printArray(MAX,n_ary);
  
  //Get inputs from user:
  printf("Enter a sequence of 5 numbers\n");
  for (int i = 0; i < MAX; i++){
    /*Although n_ary is a static pointer you must provide the 
			address of the pointer where the value is to be stored*/
    scanf("%d", &n_ary[i]);  
  }

  //Print new array with user provided values
  printArray(MAX,n_ary);

  //increment the values of each element by 1
  for (int i = 0; i < MAX; i++){
    n_ary[i]++;
    //Alternative by dereferencing the pointer
    //(*(n_ary + i))++ ; 
  }

  //Print newly updated array
  printArray(MAX,n_ary);

  //Decrement the values of each element by 10
  for (int i = 0; i < MAX; i++){
    n_ary[i] -= 10;
    //Alternative by dereferencing the pointer
    // *(n_ary + i) -= 10;
  }

  //Print newly updated array
  printArray(MAX,n_ary);

  //Sort the array in ascending order.
  //The sorting will be inplace so you don't need
  //another array to store the sorted values.
  //All thanks to the fact that an array act as pointer 
	//and thus use the call by reference property. 
  bubbleSort(MAX,n_ary);

  //Print new sorted array
  printArray(MAX,n_ary);

  //Print 2D array we initialized earlier
  print2DArray(2,m1);

  //Enter the values for the second 2D array
  printf("Enter values for a 2 x 2 array\n");
  for (int i = 0; i < 2; i++){
    for (int j = 0; j < 2; j++){
      scanf("%d",&m2[i][j]);
    }
  }

  //Print the new 2D array as well
  print2DArray(2,m2);

  //Matrix addition
  for (int i = 0; i < 2; i++){
    for (int j = 0; j < 2; j++){
      m1[i][j] += m2[i][j] ;
    }
  }

  printf("\n");
  
  //Print the new contents of the first 2D array. 
  print2DArray(2,m1);
}

//Function to print the entire 1d array
void printArray(int size, int n[size]){
  printf("Here's the array : ");
  for (int i = 0; i < size; i++){
    printf("%d ",n[i]);
    //Alternative by dereferencing the pointer
    // printf("%d ",*(n + i));
  }
  printf("\n");
}

//Function to print the entire 2D array
void print2DArray(int size, int n[][size]){
  printf("Here's the 2d array : \n");
  for (int i = 0; i < size; i++){
    for (int j = 0; j < size; j++){
      printf("%d ",n[i][j]);
    }
    printf("\n");
  }
  printf("\n");
}

//Swap two integer values using call by reference
void swap(int *x1, int *x2){
  int temp;
  temp = *x1;
  *x1 = *x2;
  *x2 = temp;
}

//Sort the contents of the array in ascending order
void bubbleSort(int size, int n[size]){
  for (int i = 0; i < size - 1; i++){
    for(int j = 0; j < size - i - 1; j++){
      if (n[j] > n[j+1]){
        swap(&n[j], &n[j+1]);
      }
    }
  }
}
```

## Structures

- A structure is a user-defined datatype in C language which allows us to combine data of different types together.
- Structures helps to construct a complex data type which is more meaningful.
- It is somewhat similar to an Array, but an array holds data of similar type only. But structure on the other hand, can store data of any type, which is practical more useful.

```c
// Example:

struct Student
{
    char name[25];
    int age;
    char branch[10];
};
```

Here struct Student declares a structure to hold the details of a student which consists of 3 data fields, namely name, age, and branch. These fields are called structure elements or members.

Each member can have different datatype, like in this case, name is an array of char type and age is of int type etc. Student is the name of the structure and is called as the structure tag.

- Declaring Structure variables

```c
struct Student
{
    char name[25];
    int age;
    char branch[10];
};

struct Student S1, S2;

//---------------------------------------------------------

struct Student
{
    char name[25];
    int age;
    char branch[10];
}S1, S2;
```

- Initializing a structure

```c
struct Patient
{
    float height;
    int weight;  
    int age; 
};

struct Patient p1 = { 180.75 , 73, 23 };    //initialization

//---------------------------------------------------------

struct Patient p1;
p1.height = 180.75;     //initialization of each member separately
p1.weight = 73;
p1.age = 23;
```

### Programming examples

```c
/*Developed by Johan Fernandes
Revised by Daniel Lobo
Course: CSI 3130*/
#include <stdio.h>
#include <string.h>

/*Alternative way to declare strucutres*/
//struct Student { .....};
//You can then use this in the main function as:
//struct student a1. Here a1 is a variable of type student
typedef struct Student
{
    char name[50];
    int id;
    char univ[50];
}student;

int main(void) {

  student a1;         //Just one student
  student list[3];    //Array of students

  student *pt1 = &a1; //Access via pointer

  //Different ways to provide the values to elements of
  //a structure variable
  printf("Enter the name of the person : ");
  scanf("%s",a1.name);
  a1.id = 23425;
  printf("Enter the univ of the person : ");
  scanf("%s",a1.univ);

  //Print the contents of that variable
  printf("%d : %s : %s \n",a1.id,a1.name,a1.univ);

  //Change the contents of the variable
  //The below line is a quick way to edit string as we
  //normally would in Java
  strncpy((pt1)->name, "jane",5); 
  printf("Enter the new univ of the person : ");
  scanf("%s",(pt1)->univ);
  printf("Enter the new id of the person : ");
  //Look I've passed the address.
  //This is because id unlike name and univ is an int 
  //and not an array/pointer.
  scanf("%d",&(pt1)->id); 

  //Print the contents using the pointer and not the 
  //variable
  printf("%d : %s : %s \n",
    (pt1)->id,(pt1)->name,(pt1)->univ);

  //Fill the contents of the array of student structure
  for (int i = 0; i < 3; i++){
      printf("Enter the name of the person : ");
      scanf("%s",list[i].name);
      printf("Enter the id of the person : ");
      scanf("%d",&list[i].id);
      printf("Enter the univ of the person : ");
      scanf("%s",list[i].univ);
  }

  //Print the entire list
  for (int i = 0; i < 3; i++){
    printf("%d : %s : %s \n",
    (list + i)->id,(list + i)->name,(list + i)->univ);
  }
}
```

## Dynamic Memory Allocation

- When a variable or an array of any data type is declared, the space occupied by them in the system's memory remains constant throughout the execution of the program.
- Sometimes the constant space allocated at the compile-time may fall short, and to increase the space during run-time we came through the concept of Dynamic Memory Allocation.
- Allocation and Deallocation of memory at run-time in C are done using the concept of Dynamic Memory Allocation. It is a method in which we use different library functions like malloc(), calloc(), realloc(), and free() to allocate and deallocate a memory block during run-time.
- There are two types of memory in our machines, one is Static Memory and another one is Dynamic Memory. When the memory is allocated during compile-time it is stored in the Static Memory and it is known as Static Memory Allocation, and when the memory is allocated during run-time it is stored in the Dynamic Memory and it is known as Dynamic Memory Allocation.

**malloc() Method:** malloc()  is used to allocate a memory block in the heap section of the memory of some specified size (in bytes) during the run-time of a C program. It is present in <stdlib.h> header file.

```c
//Syntax
(cast-data-type *)malloc(size-in-bytes);

//Example
int *ptr = (int *)malloc(sizeof(int));
```

**calloc() Method:** calloc() is also used to allocate memory blocks in the heap section, but it is generally used to allocate a sequence of memory blocks (contiguous memory) like an array of elements. It is also present in <stdlib.h> header file.

```c
//Syntax
(cast-data-type *)calloc(num, size-in-bytes);

//Example
int *arr = (int *)calloc(5, sizeof(int));
```

**realloc() Method:** realloc() is used to reallocate a memory block, here re-allocate means to increase or decrease the size of a memory block previously allocated using malloc() or calloc() methods.

```c
//Syntax
(cast-data-type *)realloc(ptr, new-size-in-bytes)

//Example
int *arr1 = (int *)malloc(n * sizeof(int));
int *arr3 = (int *)realloc(arr1, (n / 2) * sizeof(int));
```

**free() Method:** free() is used to free or deallocate a memory block previously allocated using malloc() and calloc() functions during run-time of our program.

```c
//Syntax
free( pointer );

//Example
int *arr = (int *)calloc(5, sizeof(int));
free(arr);
```

### Programming examples

```c
//Program for Dynamic Memory Allocation using malloc()

//Below is a program on dynamic memory allocation using malloc() and 
//clearing out memory space using free(). sizeof() returns the number 
//of bytes occupied by any datatype, in this case by an integer. 

#include <stdio.h>

int main()
{
    int n, i, *ptr, sum = 0;

    printf("\n\nEnter number of elements: ");
    scanf("%d", &n);

    // dynamic memory allocation using malloc()
    ptr = (int *) malloc(n*sizeof(int));

    if(ptr == NULL) // if empty array
    {
        printf("\n\nError! Memory not allocated\n");
        return 0;   // end of program
    }

    printf("\n\nEnter elements of array: \n\n");
    for(i = 0; i < n; i++)
    {
        // storing elements at contiguous memory locations
        scanf("%d", ptr+i);    
        sum = sum + *(ptr + i);
    }

    // printing the array elements using pointer to the location
    printf("\n\nThe elements of the array are: ");
    for(i = 0; i < n; i++)
    {
        printf("%d  ",ptr[i]);    // ptr[i] is same as *(ptr + i)
    }

    /* 
        freeing memory of ptr allocated by malloc 
        using the free() method
    */
    free(ptr);

    return 0;
}
```