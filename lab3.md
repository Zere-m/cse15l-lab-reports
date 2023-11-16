# Lab Report 3
# Part 1
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

# Part 2
**find command**
**Using -name**

```java
[user@sahara ~/docsearch/technical]$ find -name "*10.txt"
./biomed/1471-2288-2-10.txt
./biomed/1477-7525-1-10.txt
./biomed/1472-6963-2-10.txt
./biomed/1471-2156-4-10.txt
./biomed/1471-230X-1-10.txt
./biomed/1471-2121-2-10.txt
./biomed/1471-2180-3-10.txt
./biomed/1475-4924-1-10.txt
./biomed/1471-2199-2-10.txt
./biomed/1471-2091-2-10.txt
./biomed/1471-2334-3-10.txt
./biomed/1475-2867-2-10.txt
./biomed/1472-6882-2-10.txt
./biomed/1472-6882-1-10.txt
./biomed/1471-2202-2-10.txt
./biomed/1471-2199-3-10.txt
./biomed/1477-7819-1-10.txt
./biomed/1475-925X-2-10.txt
./biomed/1475-2875-2-10.txt
./biomed/1471-2202-4-10.txt
./biomed/1468-6708-3-10.txt
./biomed/1471-2121-3-10.txt
./biomed/1471-213X-1-10.txt
./biomed/1472-6750-2-10.txt
./biomed/1471-2172-3-10.txt
./biomed/1471-2202-3-10.txt
./biomed/1471-2334-1-10.txt
./biomed/1471-2210-1-10.txt
./biomed/1471-2369-3-10.txt
./biomed/1471-2156-3-10.txt
./biomed/1471-2172-2-10.txt
./biomed/1471-2164-3-10.txt
./911report/chapter-10.txt
```
*Using the command with "*java" indicates that the search that we are performing will be based on the file name(-name) and "*java" specifies that the file should end in "java". 
The asterisk * represents any sequence of characters, so it will accurately display all files ending with "java", no matter what the preceeding characters were. This example searches 
through the directory and gives a path to all files ending with "java"

```java
[user@sahara ~/docsearch/technical]$ find -name "1477-7819-1-10.txt"
./biomed/1477-7819-1-10.txt
```
*Using the command with a specific file name, "ArrayTest.java" will search the current directory for for a file with that exact name and return a path to that file. This is case sensitive
only files that match "ArrayTest.java" exactly will be counted as found. It will not return anything if the file is not found. 

**Using -type**


```java
[user@sahara ~/docsearch/technical]$ find -type d
.
./biomed
./911report
```
*Using "-type d" tells find to find all the directories in the specified starting directory, which in this case is home/lab3. It returns the paths of all directories within 
the lab3 folder/directory


```java
[user@sahara ~/docsearch/technical]$ find -type f -empty 
./biomed/1476-069X-1-3.txt
./biomed/1475-9268-1-1.txt
./biomed/bcr620.txt
./biomed/bcr294.txt
./biomed/1477-7827-1-23.txt
./biomed/1476-5918-1-2.txt
./biomed/ar68.txt
./biomed/1477-7525-1-10.txt
./biomed/1477-7827-1-36.txt
./biomed/1477-7827-1-13.txt
./biomed/ar118.txt
./biomed/1476-4598-2-25.txt
./biomed/bcr583.txt
./biomed/bcr303.txt
./biomed/1478-1336-1-3.txt
./biomed/1478-7954-1-3.txt
./biomed/ar120.txt
./biomed/ar79.txt
./biomed/ar778.txt
./biomed/1477-7827-1-31.txt
./biomed/1476-4598-2-1.txt
./biomed/1476-4598-1-6.txt
./biomed/bcr631.txt
./biomed/1476-069X-2-9.txt
./biomed/bcr635.txt
./biomed/1476-511X-2-2.txt
./biomed/1477-7827-1-9.txt
./biomed/1477-5956-1-1.txt
./biomed/ar93.txt
./biomed/1476-072X-2-3.txt
./biomed/1477-7827-1-43.txt
./biomed/ar149.txt
./biomed/ar328.txt
./biomed/bcr284.txt
./biomed/1476-9433-1-2.txt
./biomed/1477-7819-1-10.txt
./biomed/ar612.txt
./biomed/ar104.txt
./biomed/ar429.txt
./biomed/1475-925X-2-10.txt
./biomed/bcr285.txt
./biomed/ar130.txt
./biomed/1478-1336-1-4.txt
./biomed/1476-4598-2-3.txt
./biomed/1475-925X-2-6.txt
./biomed/bcr317.txt
./biomed/ar408.txt
./biomed/1477-7525-1-12.txt
./biomed/1476-4598-1-8.txt
./biomed/bcr458.txt
./biomed/ar140.txt
./biomed/1477-7525-1-9.txt
./biomed/ar792.txt
./biomed/1476-069X-2-4.txt
./biomed/1477-7827-1-17.txt
./biomed/1477-7827-1-21.txt
./biomed/1475-9276-1-3.txt
./biomed/ar750.txt
./biomed/1477-7827-1-46.txt
./biomed/1476-069X-2-7.txt
./biomed/1476-0711-2-7.txt
./biomed/bcr567.txt
./biomed/bcr607.txt
./biomed/ar309.txt
./biomed/1477-7827-1-6.txt
./biomed/1475-9268-1-2.txt
./biomed/1476-4598-2-22.txt
./biomed/ar430.txt
./biomed/1476-4598-2-20.txt
./biomed/ar422.txt
./biomed/ar387.txt
./biomed/ar624.txt
./biomed/1475-925X-2-12.txt
./biomed/ar745.txt
./biomed/1475-925X-2-11.txt
./biomed/1476-4598-2-24.txt
./biomed/ar615.txt
./biomed/bcr605.txt
./biomed/1476-511X-1-2.txt
./biomed/bcr602.txt
./biomed/1476-4598-1-3.txt
./biomed/bcr588.txt
./biomed/ar407.txt
./biomed/1475-925X-2-1.txt
./biomed/1476-069X-2-2.txt
./biomed/1477-7827-1-48.txt
./biomed/ar774.txt
./biomed/1477-7827-1-54.txt
./biomed/bcr618.txt
./biomed/ar331.txt
./biomed/ar601.txt
./biomed/1476-511X-2-3.txt
./biomed/1478-1336-1-2.txt
./biomed/ar319.txt
./biomed/ar795.txt
./biomed/ar799.txt
./biomed/1476-072X-2-4.txt
./biomed/bcr45.txt
./biomed/1476-4598-1-5.txt
./biomed/1476-0711-2-3.txt
./biomed/ar619.txt
./biomed/1476-4598-2-2.txt
./biomed/ar321.txt
./biomed/bcr571.txt
./biomed/1477-7827-1-27.txt
./biomed/ar383.txt
./biomed/1475-925X-2-3.txt
./biomed/bcr570.txt
./biomed/bcr273.txt
./biomed/1476-9433-1-3.txt
./biomed/bcr568.txt
./biomed/ar297.txt
./biomed/1476-4598-2-28.txt
./biomed/ar409.txt
```
*Using "-type f -empty" tells find to find all the files that are empty in the current directory(lab3). The "f" specifies to only look for regular files, not directories. Paths to all files
with no content are returned, in this case there were no empty files.

Source for above examples(-name and -type): https://www.redhat.com/sysadmin/linux-find-command 

**Using -size**

*This command searches the lab3 directory for files that are exactly 4 kilobytes in size.
```java
[user@sahara ~/docsearch/technical]$ find -size 4k
.
./911report
```

```java
[user@sahara ~/docsearch/technical]$ find -size +1k -size -8k
.
./biomed/1471-2490-3-2.txt
./biomed/1471-2334-3-13.txt
./911report
```
*This command searches the lab3 directory for files that have size in range: larger than 1 kilobyte & smaller than 5 kilobytes

**Using -perm**
This deals with permissions, my source is this website, which explains how permissions work: https://www.grymoire.com/Unix/Permissions.html
They explain that read(4), write(2), execute(1) can all be used to intepret an octal representation of a permission.



**Example 1**
*"-perm 0644" format: (owner, group, others) indicates that the owner can read+write(4+2), the group and others can read only(4). This command outputs all files within the directory
with these specific permissions


**Example 2**
*"-perm -0200 -perm -0400" format: (owner, group, others) indicates that we need files with permissions that allow the owner to write(2) and read(4), however none of these are allowed 
for group or others. this command outputs all files within the directory that allow the owner to read and write, but does not allow that for others.

Source for the above examples (-perm and -size): https://linux.die.net/man/1/find

