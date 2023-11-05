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


