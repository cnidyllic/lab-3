### Bugs and Commands

---

### Part 1: Bugs

**`ArrayExamples.java`** has several methods that are buggy, but I will be focusing on the bugs within the `reversed` method. To expose these bugs, I have provided JUnit tests that should induce a failure and should not induce failures below:

```
// JUnit Tests that should induce a failure
@Test
public void testReversed_MultipleElements() {
    int[] input = { 1, 2, 3, 4, 5 };
    int[] result = ArrayExamples.reversed(input);
    assertArrayEquals(new int[]{ 5, 4, 3, 2, 1 }, result);
}

@Test
public void testReversed_EvenNumberOfElements() {
    int[] input = { 1, 2, 3, 4 };
    int[] result = ArrayExamples.reversed(input);
    assertArrayEquals(new int[]{ 4, 3, 2, 1 }, result);
}
```
```
//JUnit Test that should NOT induce a failure
@Test
public void testReversed_OnlyZeros(){
    int[] input = { 0, 0, 0, 0 };
    int[] result = ArrayExamples.reversed(input);
    assertArrayEquals(new int[]{ 0, 0, 0, 0 }, result);
}
```

Here is the output of running the tests using the buggy method:
![image](https://github.com/cnidyllic/lab-3/assets/146884284/36fc12d5-b1da-42dc-b600-3726c9c50219)

The bug before and after change:

```
// Method that should return a new array with all the elements of the input array in reversed order
// Before
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
```
// Method that should return a new array with all the elements of the input array in reversed order
// After
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

The issue  of the code above (before) was that it was changing the values of our input array `arr` to consists of the values in reverse order of the `newArray` which we initialized as being empty (have `0` at each index). This is why the input of all `0`'s in our array did not induce an error, but for all other values it did. The fix in the code below (after) was changing the values of `newArray` to be the values in reverse order of our input `arr` and returning this `newArray`, as opposed to returning the `arr`.

---

### Part 2: Researching Commands

`grep -i` option

Examples:
#### On files

![image](https://github.com/cnidyllic/lab-3/assets/146884284/246d1df0-9a4b-4fed-88df-d7349eeb0c54)
The following command `grep -i technical/plos/*.txt` in the terminal searches for the string "as the" irrespective of case, in all text files with the particular path. It's useful when you're not sure about the casing of the search pattern within files.

#### On directories

Since it does not work directly for path of directories, we would have to obtain the subdirectories using a different command first, then search:
![image](https://github.com/cnidyllic/lab-3/assets/146884284/a50ca19a-65ab-494a-821f-6286140ab614)
In this case, grep is used to filter the output of the `ls techinical/government` command to find filenames in the  `./technical/governemnt` that match "gen", regardless of case. It is useful when listing files and you're unsure of their exact naming.

`grep -v` option

Examples:
#### On files

![image](https://github.com/cnidyllic/lab-3/assets/146884284/74501d43-1688-46ff-b4e4-ec24497f0dd1)
This command filters out lines containing "guidelines". Useful for excluding certain patterns from output in files.

#### On directories

Since grep does not work on directory paths, we can use `ls` first:
![image](https://github.com/cnidyllic/lab-3/assets/146884284/e1fb1300-4cee-4897-838a-1d822dccc6a7)
This would return a list of all files in in the `./technical/911report` directory that does not have "chapter" in its name.

`grep -o` option

Examples:
#### On files

![image](https://github.com/cnidyllic/lab-3/assets/146884284/7a43fa69-41c7-4462-aae6-5bee307f51fa)
This extracts just the word "guideline" from each line. It is useful to know how many instances or lines which contian the matching pattern, with nothing else.

#### On directories

![image](https://github.com/cnidyllic/lab-3/assets/146884284/405dee86-2a60-44dd-8848-fcf49aa33a23)
Here, we extract all files in technical/911report with the name "chapter" and prints only those lines. It is useful to quickly know how many files in a directory contain the search pattern, but for more specific details, other commands may be more useful.

`grep -c` options

Examples:
#### On files

![image](https://github.com/cnidyllic/lab-3/assets/146884284/645378f4-3f7d-4071-8b41-5e0d1cb0e0d3)
This prints out all the lines containing the search pattern "decide" with the file path. This is useful if we know what exactly we are looking for and are only trying to see what number of instances the search pattern occurs in file(s).

#### On directories
![image](https://github.com/cnidyllic/lab-3/assets/146884284/7f9baaa0-0c42-4bb8-a478-571d913c3663)
This prints out the number of files in the directory `technical/911report` that do not have the search pattern "chapter" in the file name. This is used in combination with `-v` option to first exclude a particular pattern, which is why the output is 1 here.

---

Works Cited:

https://man7.org/linux/man-pages/man1/grep.1.html




