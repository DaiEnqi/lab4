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
 
