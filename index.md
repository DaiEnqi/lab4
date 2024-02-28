Part 1:
1. The failure inducing input for the reversed() method of ArrayExamples:
```
@Test
  public void testReversed() {
    int[] input1 = {1,2,3,4 };
      ArrayExamples.reversed(input1);
        assertArrayEquals(new int[]{ 4,3,2,1 }, input1);
  }
```

The bug is that the method is returning the original array instead of the new one and the old array was getting updated which doesn't have any elements in it.

2. The input doesn't induce a failure:
```
@Test
  public void testReversed() {
    int[] input1 = {1 };
      ArrayExamples.reversed(input1);
        assertArrayEquals(new int[]{ 1 }, input1);
  }

```
3. The symptom for the method
![image](Symptom.png)

4. The bug(two codes blocks)
```
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
        for(int i = 0; i < arr.length; i += 1) {
          newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }

```

```
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
        for(int i = 0; i < arr.length; i += 1) {
            arr[i] = arr[arr.length - i - 1];
    }
    return newArray;
```
The vaiable we want to change is the arr[i], not the newArray[i]. Thus the fix addresses the issue.

part 2: Option 1: -name
Description: This option allows you to search for files and directories with a specific name.

Example 1: Finding directories with a specific name

Command and OutPut:
```
find ./technical -name "biomed"
./technical/biomed
```
Explanation: This command searches the ./technical directory and its subdirectories for directory named biomed.

Example 2: Finding files with a specific name
Command and OutPut:
```
find ./technical -name "chapter-3.txt"
./technical/911report/chapter-3.txt
```
Explanation: This command searches the ./technical directory and its subdirectories for files named chapter-3.txt.

Source: I learned about the -name option from the Linux man page for find: man7.org/linux/man-pages/man1/find.1.html

Option 2: -type
Description: This option allows you to filter results based on file type (regular file, directory, symbolic link, etc.).

Example 1: Finding only directories

Command and output:
```
find ./technical -type d
./technical
./technical/911report
./technical/biomed
```
Explanation: This command searches the ./technical directory and its subdirectories, returning only directories.

Example 2: Finding only symbolic links

Command and Output:
```
find ./technical -type l
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-10.txt
........(too many)
```

Explanation: This command searches the ./technical directory and its subdirectories, returning only files.

Source: The -type option is documented in the find manual page: man7.org/linux/man-pages/man1/find.1.html

Option 3: -mtime
Description: Searches for files modified within a specific number of days.

Example 1: Finding only files
Command and Output:
```
find ./technical -type f -mtime -30
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-13.1.txt
......(too many)
```
Explanation: This command will find all regular files within the specified directory that were modified within the last 30 days.

Example 2: Finding only directories
Command and Output:
```
find ./technical -type d -mtime -30
./technical
./technical/911report
./technical/biomed
```
Explanation: This command will find all directories within the specified directory that were modified within the last 30 days.

Option 4: -size
Description: Searches for files of a specific size.

Example 1: Finding only files
Command and Output:
```
find ./technical -type f -size 0
./technical/biomed/ar149.txt
./technical/biomed/1476-9433-1-3.txt
./technical/biomed/1476-511X-1-2.txt
./technical/biomed/1476-511X-2-3.txt
./technical/biomed/1476-0711-2-3.txt
./technical/biomed/ar331.txt
```
Explanation: This command will find all regular files within the specified directory that have a size of 0 bytes.

Example 2: Finding only dirctories
Command and Output:
```
find ./technical -type d -size 1M
./technical
./technical/911report
./technical/biomed
```
This command will find all directories within the specified directory that are larger than 1MB.

