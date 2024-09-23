# Review Notes on Java Arrays
A short review of arrays and array methods in Java programming. This guide is not meant to be comprehensive, rather, a set of basic tips useful for the ICS4U course.

## 1. Arrays

### Characteristics
- **Fixed Size**: Once declared, an array's size is immutable.
- **Data Type Consistency**: All elements must be of the same type (e.g., `int`, `String`).

### Initialization & Declaration
- **With size**:
  ```java
  int[] numbers = new int[5]; // Array of 5 integers, initialized to 0
  ```
- **With values**:
  ```java
  int[] numbers = {1, 2, 3, 4, 5}; // Array initialized with specified values
  ```
- **Accessing elements**:
  ```java
  int firstElement = numbers[0]; // Access first element
  numbers[2] = 10;               // Modify third element
  ```

### Looping Through Arrays
- **Using a `for` loop**:
  ```java
  for (int i = 0; i < numbers.length; i++) {
      System.out.println(numbers[i]);
  }
  ```
- **Using an enhanced `for` loop**:
  ```java
  for (int num : numbers) {
      System.out.println(num);
  }
  ```

<br><br>

## 2. ArrayList (Dynamic Size)

### Characteristics
- **Resizable**: Automatically grows or shrinks as elements are added or removed.
- **Only Stores Objects**: Requires wrapper classes for primitives (e.g., `Integer` for `int`).

### Initialization & Declaration
- **Basic Declaration**:
  ```java
  import java.util.ArrayList;

  ArrayList<Integer> list = new ArrayList<>();
  ```
- **Adding Elements**:
  ```java
  list.add(10);
  list.add(20);
  ```
- **Accessing Elements**:
  ```java
  int firstElement = list.get(0);
  ```
- **Removing Elements**:
  ```java
  list.remove(Integer.valueOf(10)); // Removes the element "10"
  ```

### Converting Between Arrays and ArrayLists
- **Array to ArrayList**:
  ```java
  int[] arr = {1, 2, 3};
  ArrayList<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));
  ```
- **ArrayList to Array**:
  ```java
  Integer[] array = list.toArray(new Integer[0]);
  ```

<br><br>

## 3. JUnit Testing

### Common Assertions
- **Testing Arrays**: Use `assertArrayEquals` for array comparison.
  ```java
  int[] testArray = {10, 42, 15};
  assertArrayEquals(new int[]{10, 42, 15}, testArray); // This will pass as the arrays are the same
  ```
- **Testing Values**:
  ```java
  int[] testArray = {10, 42, 15};
  assertEquals(42, testArray[1]); // This will pass as testArray[1] is 42
  ```

### Example Test Case
```java
import static org.junit.Assert.assertArrayEquals;
import org.junit.Test;

public class ArrayTests {
    @Test
    public void testWithoutTen() {
        assertArrayEquals(new int[]{1, 2, 0, 0}, withoutTen(new int[]{1, 10, 10, 2}));
    }
}
```

<br><br>

## 4. Looping Structures

### Single Loop
- Iterating over a 1D array:
  ```java
  for (int i = 0; i < arr.length; i++) {
      System.out.println(arr[i]);
  }
  ```

### Nested Loop
- Iterating over a 2D array:
  ```java
  for (int i = 0; i < matrix.length; i++) {
      for (int j = 0; j < matrix[i].length; j++) {
          System.out.println(matrix[i][j]);
      }
  }
  ```

<br><br>

## 5. 2D Arrays

### Initialization & Declaration
- **With size**:
  ```java
  int[][] matrix = new int[3][3]; // A 3x3 matrix initialized to 0
  ```
- **With values**:
  ```java
  int[][] matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
  ```
- **Accessing Elements**:
  ```java
  int value = matrix[1][2]; // Access the element at row 1, column 2
  ```

<br><br>


## 6. Comparing Arrays

In Java, you **cannot** use `arr1 == arr2` to compare two arrays, as this only checks if they refer to the **same object** in memory, not whether they have the same elements or length.

To correctly compare the contents of two arrays, you should use:
- `Arrays.equals(arr1, arr2)` for one-dimensional arrays.
- `Arrays.deepEquals(arr1, arr2)` for multi-dimensional arrays.

These methods compare the actual contents of the arrays, element by element, and will return `true` if the arrays are equivalent.

**Example:**
```java
import java.util.Arrays;

int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};

System.out.println(arr1 == arr2);                 // false, different memory references
System.out.println(Arrays.equals(arr1, arr2));    // true, equivalent contents

int[][] multiArr1 = {{1, 2}, {3, 4}};
int[][] multiArr2 = {{1, 2}, {3, 4}};

System.out.println(Arrays.deepEquals(multiArr1, multiArr2)); // true, equivalent contents in multi-dimensional arrays
```

<br><br>

## 7. Edge Cases and Array Length

### Handling Empty Arrays
- Always check for empty arrays:
  ```java
  if (arr.length == 0) {
      return new int[0];
  }
  ```

### Dealing with Single-Element Arrays
- Consider arrays with only one element when writing methods or test cases.

<br><br>

## 8. Static vs Dynamic Behavior

### Modifying Arrays In-Place
- The original array is changed:
  ```java
  public static void modifyInPlace(int[] arr) {
      for (int i = 0; i < arr.length; i++) {
          if (arr[i] == 10) arr[i] = 0;
      }
  }
  ```

### Creating and Returning a New Array
- Original array remains unchanged, and a modified copy is returned:
  ```java
  public static int[] createNewArray(int[] arr) {
      int[] result = new int[arr.length];
      for (int i = 0; i < arr.length; i++) {
          result[i] = (arr[i] == 10) ? 0 : arr[i];
      }
      return result;
  }
  ```

### Why It Matters
- **Memory Efficiency**: In-place modification uses less memory but alters the original array.
- **Functional Programming**: Creating a new array adheres to immutability principles, making code safer and easier to debug.
