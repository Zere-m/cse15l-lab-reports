#Lab Report 3
#Part 1
* Failure inducing input: array of 3 or more characters when tring to reverse the array
```java
 @Test
  public void testReverseInPlace2(){
    int[] input = {10 ,20, 30};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{ 30,20,10}, ArrayExamples.reversed(input));
    System.out.println(input);
  }
```
* Successful input: array of 1 character when tring to reverse the array
```java
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
**Symptom:**
![Image](ArrayTestsError.png)

*Bug fixed: 
**Original Code**
```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
**Fixed Code**
```java
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int[] temp = new int[arr.length];
    for(int i = 0; i<arr.length; i++){
      temp[i] = arr[i];
    }
    
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = temp[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
**reverseInPlace:**
The original array was not properly reversed because the method directly modified the array without storing the original elements to reverse. The fix helped because we stores the original elements in the temporary array, so they can be referred to and put into the accurate index in our array, properly reversing it.

**reversed:**
The issue was that the newArray was never filled with elements, so it was empty. The original code kept updating the old/provided array "arr". In addition to that, the method returned the "arr" array back instead of the newArray that was supposed to be created. The fix helped because it updated the newArray, returning it when the method was done.

#Part 2
**find command**
**Using -name**

![Image](find "*java".png)
*Using the command with "*java" indicates that the search that we are performing will be based on the file name(-name) and "*java" specifies that the file should end in "java". 
The asterisk * represents any sequence of characters, so it will accurately display all files ending with "java", no matter what the preceeding characters were. This example searches 
through the directory and gives a path to all files ending with "java"

![Image](find ArrayTests.png)
*Using the command with a specific file name, "ArrayTest.java" will search the current directory for for a file with that exact name and return a path to that file. This is case sensitive
only files that match "ArrayTest.java" exactly will be counted as found. It will not return anything if the file is not found. 

**Using -type**

![Image](find -type d.png)
*Using "-type d" tells find to find all the directories in the specified starting directory, which in this case is home/lab3. It returns the paths of all directories within 
the lab3 folder/directory

![Image](find -type empty.png)
*Using "-type f -empty" tells find to find all the files that are empty in the current directory(lab3). The "f" specifies to only look for regular files, not directories. Paths to all files
with no content are returned, in this case there were no empty files.

Source for above examples(-name and -type): https://www.redhat.com/sysadmin/linux-find-command 

**Using -size**

![Image](find size 4k.png)
*This command searches the lab3 directory for files that are exactly 4 kilobytes in size.

![Image](find size in range.png)
*This command searches the lab3 directory for files that have size in range: larger than 1 kilobyte & smaller than 5 kilobytes

**Using -perm**
This deals with permissions, my source is this website, which explains how permissions work: https://www.grymoire.com/Unix/Permissions.html
They explain that read(4), write(2), execute(1) can all be used to intepret an octal representation of a permission.

![Image](find -perm original.png)
**Example 1**
*"-perm 0644" format: (owner, group, others) indicates that the owner can read+write(4+2), the group and others can read only(4). This command outputs all files within the directory
with these specific permissions

![Image](find -perm owner only.png)
**Example 2**
*"-perm -0200 -perm -0400" format: (owner, group, others) indicates that we need files with permissions that allow the owner to write(2) and read(4), however none of these are allowed 
for group or others. this command outputs all files within the directory that allow the owner to read and write, but does not allow that for others.

Source for the above examples (-perm and -size): https://linux.die.net/man/1/find

