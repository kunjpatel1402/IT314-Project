# Lab 7 - Testing

###  Submitted by - Kunj Rakesh Patel 202001421

#### Consider a program for determining the previous date. Its input is triple of day, month and year with the following ranges $1 \leq month \leq 12$, $1 \leq day \leq 31$, $1900 \leq year \leq 2015$.The possible output dates would be previous date or invalid date. Design the equivalence class test cases?

|Equivalence Class | Constraints|
|------------------|------------|
|E1|$1 \leq day \leq 31$|
|E2|$day \lt 1$|
|E3|$day \gt 31$|
|E4|$1 \leq month \leq 12$|
|E5|$month \lt 1$|
|E6|$month \gt 12$|
|E7|$1900 \leq year \leq 2015$|
|E8|$year \lt 1900$|
|E9|$year \gt 2015$|

##### Weak normal equivalence class test cases:

|Equivalence Class|Day|Month|Year|Output|
|-----------------|---|-----|----|------|
|E1|2|3|2011|1/3/2011|
|E2|-1|4|2022|Invalid date|
|E3|39|4|2022|Invalid date|
|E4|3|3|2011|2/3/2011|
|E5|2|-7|1976|Invalid date|
|E6|2|17|1976|Invalid date|
|E7|3|3|2011|2/3/2011|
|E8|2|7|1876|Invalid date|
|E9|2|7|2023|Invalid date|


##### Boundary Value Analysis:

|Input|Remarks|
|-----|-------|
|15/6/2030|Year outside accepted range (Invalid Date)|
|15/13/2011|Month outside accepted range (Invalid Date)|
|45/6/2011|Day outside accepted range (Invalid Date)|
|15/6/2011|All constraints satisfied (Valid Date)|
|31/4/2011|Boundary Value (Invalid Date)|
|30/2/2011|Boundary Value (Invalid Date)|
|13/2/1910|All constraints satisfied (Valid Date)|
|36/1/2011|Day outside accepted range (Invalid Date)|
|29/2/2000|Leap year (Valid Date)|
|31/12/2010|All constraints satisfied (Valid Date)|
|1/1/2010|All constraints satisfied (Valid Date)|


#### Programs

##### P1. The function linearSearch searches for a value v in an array of integers a. If v appears in the array a, then the function returns the first index i, such that a[i] == v; otherwise, -1 is returned.

```java
int linearSearch(int v, int a[])
{
  int i = 0;
  while (i < a.length)
  {
    if (a[i] == v)
    return(i);
    i++;
  }
  return (-1);
}
```
Boundary Partitions

|Tester Action and Input Data|Expected Output|
|----------------------------|---------------|
|v is in-valid and empty array|-1|
|v is in-valid and non-empty array|-1|
|v exists in array|index of v in array|
|v doesn't exist in array|-1|

Boundary Value Analysis

|Tester Action and Input Data|Expected Output|
|----------------------------|---------------|
|v is in-valid and empty array|-1|
|v is in-valid and non-empty array|-1|
|v is valid and array length is 0|-1|
|v is valid , exists in array and array length is 1|1|
|v is valid , does not exists in array and array length is 1|-1|
|v is valid , exists in array and array length $\gt$ 1|last index of v in array|

```java
public class UnitTesting1 {
  @Test
  public void test1() {
  int arr[] = { 1, 2, 3, 4, 5 };
  Programs program = new Programs();
  int output = program.linearSearch(1, arr);
  System.out.println(output);
  assertEquals(0, output);
  }
  @Test
  public void test2() {
    int arr[] = { };
    Programs program = new Programs();
    int output = program.linearSearch(11, arr);
    System.out.println(output);
    assertEquals(-1, output);
  }
  @Test
  public void test3() {
    int arr[] = { 5 };
    Programs program = new Programs();
    int output = program.linearSearch(5, arr);
    System.out.println(output);
    assertEquals(0, output);
  }
  @Test
  public void test4() {
    int arr[] = { 10 };
    Programs program = new Programs();
    int output = program.linearSearch(11, arr);
    System.out.println(output);
    assertEquals(-1, output);
  }
  @Test
  public void test5() {
    int arr[] = { 1, 2, 3, 4, 5 };
    Programs program = new Programs();
    int output = program.linearSearch(7, arr);
    System.out.println(output);
    assertEquals(-1, output);
  }
}
```

##### P2. The function countItem returns the number of times a value v appears in an array of integers
```java
int countItem(int v, int a[]){
  int count = 0;
  for (int i = 0;i < a.length;i++){
  if (a[i] == v)
    count++;
  }
  return (count);
}
```
Equivalence Partitions

|Tester Action and Input Data|Expected Output|
|----------------------------|---------------|
|v is in-valid and empty array|0|
|v is in-valid and non-empty array|0|
|v exists in array|number of occurences of v in array|
|v doesn't exist in array|0|


Boundary Value Analysis

|Tester Action and Input Data|Expected Output|
|----------------------------|---------------|
|v is in-valid and empty array|0|
|v is in-valid and non-empty array|0|
|v is valid and array length is 0|0|
|v is valid , exists in array and array length is 1|1|
|v is valid , does not exists in array and array length is 1|0|
|v is valid , exists in array and array length $\gt$ 1|number of occurences of v in array|
|v is valid , exists in array (with first element as v) and array length $\gt$ 1|number of occurences of v in array|
|v is valid , exists in array (with last element as v)and array length $\gt$ 1|number of occurences of v in array|

```java
public class UnitTesting2 {
  @Test
  public void test1() {
    int input[] = { };
    Programs program = new Programs();
    int output = program.countItem(0, input);
    assertEquals(output, 0);
  }
  @Test
  public void test2() {
    int input[] = { 21, 21, 22, 23, 21 };
    Programs program = new Programs();
    int output = program.countItem(10, input);
    assertEquals(output, 0);
  }
  @Test
  public void test3() {
    int input[] = { 41, 41, 42, 43, 41 };
    Programs program = new Programs();
    int output = program.countItem(41, input);
    assertEquals(output, 3);
  }
  @Test
  public void test4() {
    int input[] = { 51, 51, 52, 53, 51 };
    Programs program = new Programs();
    int output = program.countItem(52, input);
    assertEquals(output, 1);
  }
  @Test
  public void test5() {
    int input[] = { 1 };
    Programs program = new Programs();
    int output = program.countItem(1, input);
    assertEquals(output, 1);
  }
  @Test
  public void test6() {
    int input[] = { 1 };
    Programs program = new Programs();
    int output = program.countItem(2, input);
    assertEquals(output, 0);
  }
  @Test
  public void test7() {
    int input[] = { 71, 71, 72, 73, 71, 71, 71 };
    Programs program = new Programs();
    int output = program.countItem(71, input);
    assertEquals(output, 5);
  }
}
```

##### P3. The function binarySearch searches for a value v in an ordered array of integers a. If v appears in the array a, then the function returns an index i, such that a[i] == v; otherwise, -1 is returned.

```java
int binarySearch(int v, int a[]){
  int lo, mid, hi;
  lo = 0;
  hi = a.length-1;
  while (lo <= hi)
  {
    mid = (lo+hi)/2;
    if (v == a[mid])
      return (mid);
    else if (v < a[mid])
      hi = mid-1;
    else
      lo = mid+1;
  }
  return(-1);
}
```
Equivalence Partioning:
|Test Input|Expected output|
|----------|---------------|
|v = 26 a = [2, 14, 26, 38, 510]|2|
|v = 2 a = [2, 14, 26, 38, 510]|0|
|v = 510 a = [2, 14, 26, 38, 510]|4|
|v = 510 a = [2, 14, 26, 38, 510]|-1|
|v = 511 a = [2, 14, 26, 38, 510]|-1|

Boundary Value Analysis:

|Test Input|Expected Output|
|----------|---------------|
|v = 10 a = [10]|0|
|v = 5 a = []|-1|
|v = 5 a = [5, 7, 9]|0|
|v = 5 a = [1, 2, 3]|2|

```java
public class UnitTesting3 {
  @Test
  public void test1() {
    int input[] = { 2, 14, 26, 38, 510 };
    Programs program = new Programs();
    int output = program.binarySearch(26, input);
    assertEquals(2, output);
  }
  @Test
  public void test2() {
    int input[] = { 2, 14, 26, 38, 510 };
    Programs program = new Programs();
    int output = program.binarySearch(2, input);
    assertEquals(0, output);
  }
  @Test
  public void test3() {
    int input[] = { 2, 14, 26, 38, 510 };
    Programs program = new Programs();
    int output = program.binarySearch(510, input);
    assertEquals(4, output);
  }
  @Test
  public void test4() {
    int input[] = { 2, 14, 26, 38, 510 };
    Programs program = new Programs();
    int output = program.binarySearch(1, input);
    assertEquals(-1, output);
  }
  @Test
  public void test5() {
    int input[] = { };
    Programs program = new Programs();
    int output = program.binarySearch(511, input);
    assertEquals(-1, output);
  }
  @Test
  public void test6() {
    int input[] = { 5, 7, 9 };
    Programs program = new Programs();
    int output = program.binarySearch(5, input);
    assertEquals(0, output);
  }
  @Test
  public void test9() {
    int input[] = { 5, 7, 9 };
    Programs program = new Programs();
    int output = program.binarySearch(9, input);
    assertEquals(2, output);
  }
}
```
