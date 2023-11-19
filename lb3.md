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

```
$ grep -i "as the" technical/plos/*.txt
technical/plos/journal.pbio.0020001.txt:        Other relative indicators of scientific productivity, such as the number of publications
technical/plos/journal.pbio.0020001.txt:            Why has the number of publications per dollar invested in research and
technical/plos/journal.pbio.0020001.txt:        versus 6% in the top 20, ecological journals, whereas the United States and Canada had 81%
technical/plos/journal.pbio.0020010.txt:        readers. As the number of journal articles accessible over the networks increases, JSTOR
...
```
The following command `grep -i technical/plos/*.txt` in the terminal searches for the string "as the" irrespective of case, in all text files with the particular path. It's useful when you're not sure about the casing of the search pattern within files. I included `...` at the end to show that there are several more lines that include "as the", but were not included in the paste because of how much space it would take up considering, it is a very general search term.

#### On directories

Since it does not work directly for path of directories, we would have to obtain the subdirectories using a different command first, then search:

```
$ ls technical/government | grep -t "gen"
Env_Prot_Agen/
Gen_Account_Office/
```
In this case, grep is used to filter the output of the `ls techinical/government` command to find filenames in the  `./technical/governemnt` that match "gen", regardless of case. It is useful when listing files and you're unsure of their exact naming.

`grep -v` option

Examples:
#### On files

```
$ grep -v "guidelines" technical/plos/pmed.0020191.txt



        The excellent article by Jordan Paradise, Lori B. Andrews, and colleagues, "Ethics.
        Constructing Ethical Guidelines for Biohistory" [1], neither advocates nor argues against
        biohistorical research; instead, it points out that such investigations are currently
        governments, medical examiners, family members, or intrepid biographers are to be given
        permission? Who is to decide what is "historically significant"? Not to mention the
        meta-question: who is to decide who is to decide? I apologize to the authors if my brief
        comments [2] implied that they took a position on this issue.
```
This command filters out lines containing "guidelines" (case-sensitive). Useful for excluding certain patterns from output in files.

#### On directories

Since grep does not work on directory paths, we can use `ls` first:

```
// this is the command and output to see all the files in the directory first
$ ls techincal/911report
chapter-1.txt     chapter-11.txt    chapter-13.1.txt    chapter-13.3.txt    chapter-13.5.txt chapter-3.txt    chapter-6.txt    chapter-8.txt    preface.txt
chapter-10.txt    chapter-12.txt    chapter-13.2.txt    chapter-13.4.txt    chapter-2.txt    chapter-5.txt    chapter-7.txt    chapter-9.txt
```
```
$ ls technicla/911report | grep -v "chapter"
preface.txt
```
This would return a list of all files in in the `./technical/911report` directory that does not have "chapter" in its name.

`grep -o` option

Examples:
#### On files

```
$ grep -o "guideline" technical/plos/pmed.0020191.txt
guideline
guideline
```
This extracts just the word "guideline" from each line. It is useful to know how many instances or lines which contian the matching pattern, with nothing else since you just want to know the count.

#### On directories

```
$ ls technical/911report | grep -o "chapter"
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
chapter
```

Since we cannot call it on the directory directly, we must use `ls` or another command to list the file names in the directory. Here, we extract all files in technical/911report with the name "chapter" and prints only those lines. It is useful to quickly know how many files in a directory contain the search pattern, but for more specific details, other commands may be more useful.

`grep -c` options

Examples:
#### On files

```
$ grep -c "decide" technical/plos/pmed.0020191.txt
2
```
This prints out all the lines containing the search pattern "decide" with the file path. This is useful if we know what exactly we are looking for and are only trying to see what number of instances the search pattern occurs in file(s).

#### On directories

```
$ ls technical/911report | grep -c -v "chapter"
1
```
Again we have to use `ls` first list the files in the directory we want. This prints out the number of files in the directory `technical/911report` that do not have the search pattern "chapter" in the file name. This is used in combination with `-v` option to first exclude a particular pattern, which is why the output is 1 here.

---

Works Cited:

[List of all grep options, includes those that were used in this lab report](https://man7.org/linux/man-pages/man1/grep.1.html)




