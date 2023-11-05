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



* The bug, as the before-and-after code change required to fix it 

 Before the code change
```
static void reverseInPlace(int[] arr)
{
  for(int i = 0; i < arr.length; i += 1)
  {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
 After code change

# Part 2 - Researching Commands
