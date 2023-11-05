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

1. ```-c```: count the number of lines that match the given string/pattern

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

2. ```-i```: enables to search for a string case insensitivity

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

3. ```-n```: show the line number of the file with the line matched.
```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -n "publications" plos/journal.pbio.0020001.txt
20:        88% of all scientific and technical publications registered by the Science Citation Index
21:        (SCI). North America and Europe clearly dominate the number of scientific publications
26:            publications produced annually.
30:        and therefore account for the largest number of publications. It is also likely that there
32:        represents North American and European publications far better than those of the rest of
38:        respectively, only 1.8% and 2% of scientific publications worldwide, have increased the
39:        number of their publications between 1990 and 1997 by 36% and 70%, respectively, which is a
41:        (26%). The percentage of global scientific publications from North America actually
49:        publications between the developed world and the developing world from 1990 until 2000,
51:        the number of publications from 1990 until 2000, with the United States contributing the
53:        only 5.45% to the total number of scientific publications in these ten years (RICYT
55:        The total number of publications, however, is not necessarily the best measure for
58:        publications and the total number of publications when corrected for investment in research
59:        and development (May 1997). The proportional change in the number of publications, using
62:        Further analyses, correcting the number of overall publications for the amount of money
70:        of publications per amount of money allocated to research and development in Latin America,
72:        Other relative indicators of scientific productivity, such as the number of publications
87:        respectively, 6.8, 5.3, 5.2, and 3.4 publications per million dollars of research and
94:            Why has the number of publications per dollar invested in research and
104:        of this region. Indeed, this would explain the rapid rise in the number of publications in
107:        important question, however, is why the number of publications per dollar invested in
115:        may also have increased the relative number of publications in Latin America. In contrast,
116:        the decreasing trends in the number of publications per investment dollar in Canada and
123:        scientific community? We used SCI 2001 data to examine the proportion of publications in
135:        North America accounted for 62% of the publications worldwide. Within the Americas,
137:        respectively, for 13% and 82% of the top 20 ecological publications. When we examined the
140:        twice as many publications to journals in the second category (8% in the top 11–20 compared
141:        with 4% in the top 10). These findings suggest that publications from such developing
143:        United States contributed somewhat more publications to the top 10 journals (84%) than the
144:        top 11–20 journals (79%). The difference in the proportion of publications contributed by
146:        examined it in respect to worldwide publications. In this case, the United States
147:        contributed 60% of the publications to the top 10 journals and only 40% of the publications
149:        Interestingly, the proportion of publications from Latin America, the United States, and
155:        Nature , Latin America had 7% of the publications within the Americas
169:        publications per researcher funding amount. Similar findings were also reported for Asia
202:        critical for the developing world to promote, through research and publications, those
220:        publications, especially when corrected for the amount of money available in research and
225:        publications as a measure of scientific output, particularly if these publications can
```

```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -n "publications" plos
grep: plos: Is a directory
```

4. ```-h```: Display the matched lines, but do not display the filenames.
```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -h "Hungerford" government/Alcohol_Problems/DraftRecom-PDF.txt
        Daniel Hungerford opened the final session of the conference by
        Hungerford stated that the goal of the conference was not to
        that would be instructive. Hungerford then opened the floor for
        Daniel Hungerford noted that the supporting text could provide
        Hungerford replied that screening for specific medical care
        Hungerford added that the trauma care setting should be included
        Hungerford answered that the summary of the conference would be
        Hungerford emphasized that research on screening is needed.
        Hungerford said he understood. If we do not pre-define "SBIR,"
        Hungerford proposed that just as screening research should be
        Pollock and Hungerford concurred. Hungerford added that the
        Hungerford thought that work in the ED needed a higher priority
        proposed recommendations, Hungerford asked if they had general
```

```
DELL@DESKTOP-A31SQJ0 MINGW64 ~/Documents/GitHub/lab4/docsearch/technical (main)
$ grep -h "Hungerford" government/Alcohol_Problems
grep: government/Alcohol_Problems: Is a directory
```

## Work Cited
“Grep Command in Unix/Linux", *www.geeksforgeeks.org/grep-command-in-unixlinux/amp/*. Accessed 5 Nov. 2023. 
