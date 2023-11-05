# Part 1 - Bugs

For the first part of the lab, I'm going to discuss a bug from the ```reverseInPlace``` method in the ```ArrayExamples.java``` class.

* A failure-inducing input for the buggy program, as a JUnit test and any associated code

```
@Test 
public void testReverseInPlace()
{
  int[] input1 = { 1, 2, 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3, 2, 1 }, input1);
}
```

* An input that doesn’t induce a failure, as a JUnit test and any associated code
```
@Test 
public void testReverseInPlace1()
{
  int[] input1 = { 2 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 2 }, input1);
}
```
* The symptom, as the output of running the tests

![Image](symptoms(1).png)

As a result of running the tests with the two inputs above, we see a symptom for testReverseInPlace() due to the last element ending up being 3 instead of 1 as the expected result. In short, the input array was changed to {3,2,3} instead of {3,2,1}.

* The bug, as the before-and-after code change required to fix it 

**Before the code change**
```
static void reverseInPlace(int[] arr)
{
  for(int i = 0; i < arr.length; i += 1)
  {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
In this original code, the ```reverseInPlace``` method is prompted to change the input array ```arr``` to be in reversed order. However, the bug occurs since we are overwriting the original values of the same array. Through each iteration, we are using the same array ```arr``` to store the reversed values, and therefore, the array ```arr``` will be incorrectly reversed. 

**After code change**
```
static void reverseInPlace(int[] arr)
{
  int[] origin_array = arr.clone();
    
  for(int i = 0; i < arr.length; i += 1) 
  {
    arr[i] = origin_array[arr.length - i - 1];
  }
}
```

After some changes, the bug in the code has been fixed because we've created a new array called ```origin_array```, which stores all the original input values of the array ```arr``` through the ```clone()``` method. By doing this, the original input values of the array ```arr``` have been preserved before it is being reversed. Therefore, it will be reversed correctly based on the original values stored in ```origin_array```.

# Part 2 - Researching Commands

For the second part of the lab, I researched grep command-line options and found four interesting alternate ways to use this command.

1. -c: count the number of lines that match the given string/pattern

```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -c "American" 911report/chapter-1.txt
81
```

The command ```grep -c``` is used to count the number of lines that contain the word **American** in ```chapter-1.txt``` file, which is located in the 911report directory. It is useful because it gives a quick determination of the frequency of the word within the document.  

```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -c "American" 911report
grep: 911report: Is a directory
0
```
We cannot use the command ```grep -c``` on the directory directly. Although it attempted to count the number of lines that have the word **American** within the ```911report``` directory, it returned an error message saying that ```911report``` is a directory and counts the number of lines as 0 since the ```911report``` directory does not contain the text content. One useful thing is that it helps identify that the target is a directory and not a file.

2. -i: enables to search for a string case insensitivity

```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -i "Reduction" biomed/1468-6708-3-3.txt
        Ischemia Reduction with Aggressive Cholesterol Lowering
        2.6% absolute reduction in the risk of the primary endpoint
        reduction was primarily driven by the 2.2% absolute
        reduction in incidence of emergent rehospitalization for
        concern that statin-mediated reductions in vascular smooth
        demonstrates significant reductions in the incidence of
        serum cholesterol 'floor' below which reductions are
        = Myocardial Ischemia Reduction with Aggressive Cholesterol
```


```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -i "Reduction" biomed
grep: biomed: Is a directory
```

3. -l: display the file names that contain the given string/pattern.
```

```

```

```
4. -n: show the line number of file with the line matched.
```

```

```

```
