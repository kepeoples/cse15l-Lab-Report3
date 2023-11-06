# Lab Report 3
Kevin William Peoples
A17465911

## Part1
One of the bugs from Lab4 is in the ArrayExamples.java file. It has a method called 'reverseInPlace' which returns an array but the elements in the returned array are in the opposite order as compared to the input array.  
Following is the code with bugs:  
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
Now, following is the test-case related to the above code with bugs.  
**NOTE: The tests  are written in ArrayTests.java**  
Also, this is the test case that induces a failure:  

```
 @Test
    public void testReverseInPlace_Buggy() {
        int[] inputArray = {1, 2, 3, 4, 5};
        int[] expectedArray = {5, 4, 3, 2, 1};

        ArrayExamples.reverseInPlace(inputArray);

        assertArrayEquals(expectedArray, inputArray);
    }
```
Following is the Fixed Code:
```
// Fixed code
static void reverseInPlace(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[n - i - 1];
        arr[n - i - 1] = temp;
    }
}
 
```
Now, the corresponding test case that dooesn't induce failure:
```
@Test
    public void testReverseInPlace_Fixed() {
        int[] inputArray = {1, 2, 3, 4, 5};
        int[] expectedArray = {5, 4, 3, 2, 1};

        ArrayExamples.reverseInPlace(inputArray);

        assertArrayEquals(expectedArray, inputArray);
    }
```

***Also, following is the detailed description of the bug:***  
The original code had a flaw where it tries to assign the value of each element to its corresponding element at the opposite end of the array, thereby reversing the array. 
This effectively copies the final half of the array to the first half, resulting in inaccurate values for the first half of the array.

**Synopsis of the Correction:**

The solution is to switch the elements at the beginning and end of the array. 
We assign the value from the appropriate index at the other end of the array to the current index after storing the element's value at the current index in a temporary variable (temp). 
Lastly, we link the transient saved value to the appropriate index on the opposite end. 
As the array approaches the array's center, this guarantees that it is appropriately inverted in place.

## Part2 
1)  **Using the -name option:**  
You can do a name-based search for files and directories by using the -name option. It helps with name-based file or directory searches.  
Example 1: Finding all text files in the ./technical directory.  
Input:     
```find ./technical -type f -name "*.txt" ```  
Output:  
```./technical/file1.txt```   
   ```./technical/subdirectory/file2.txt ```  
Example 2: Finding all directories named "docs" in the ./technical directory.  
Input:   
```find ./technical -type d -name "docs" ```   
Output:   
```./technical/docs ```    
```./technical/subdirectory/docs ```         


3)  **Using the -size option:**
To locate files of a particular size, you can utilize the -size option to search for files based on their size.  
Example 1: Finding all files in the ./technical directory that are larger than 1MB.  
```find ./technical -type f -size +1M ```  
Output: (List of files larger than 1MB)  
Example 2: Finding all files in the ./technical directory that are smaller than 100KB.      
```find ./technical -type f -size -100k ```    
Output: (List of files smaller than 100KB)
  
4)  **Using the -mtime option:**
Finding files that have been modified within a given time range can be facilitated by using the -mtime option to search for files based on their modification time.  
Example 1: Finding all files in the ./technical directory modified within the last 7 days.  
```find ./technical -type f -mtime -7 ```  
Output: (List of files modified within the last 7 days)  
Example 2: Finding all files in the ./technical directory modified exactly 30 days ago.  
```find ./technical -type f -mtime 30 ```  
Output: (List of files modified 30 days ago)

5)  **Using the -exec option:**
If you want to do something with the files you find, you can use the -exec option to run a command on the files that locate.  
Example 1: Finding all text files in ./technical and displaying their contents.  
```find ./technical -type f -name "*.txt" -exec cat {} \; ```  
Output: (Contents of all text files)  
Example 2: Finding all JPEG images in ./technical and moving them to a separate directory.  
```find ./technical -type f -name "*.jpg" -exec mv {} ./images \;```  
Output: (Files moved to the "images" directory)
 
Source: The official GNU find manual, GNU Findutils Manual, is where I obtained this information.

Please be aware that the actual output will vary depending on what is in your./technical directory and how it is organized.


