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

All test cases pass succesfully.

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

All test cases pass succesfully.

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
  public void test7() {
    int input[] = { 5, 7, 9 };
    Programs program = new Programs();
    int output = program.binarySearch(9, input);
    assertEquals(2, output);
  }
}
```

All test cases pass succesfully.

##### P4. The following problem has been adapted from The Art of Software Testing, by G. Myers (1979). The function triangle takes three integer parameters that are interpreted as the lengths of the sides of a triangle. It returns whether the triangle is equilateral (three lengths equal), isosceles (two lengths equal), scalene (no lengths equal), or invalid (impossible lengths)

```java
final int EQUILATERAL = 0;
final int ISOSCELES = 1;
final int SCALENE = 2;
final int INVALID = 3;
int triangle(int a, int b, int c){
  if (a >= b+c || b >= a+c || c >= a+b)
    return(INVALID);
  if (a == b && b == c)
    return(EQUILATERAL);
  if (a == b || a == c || b == c)
    return(ISOSCELES);
  return(SCALENE);
}
```
Equivalence Partitioning:
|Input Data|Expected Output|
|----------|---------------|
|(2, 2, 2) |0|
|(3, 3, 4) |1|
|(6, 5, 4) |2|
|(0, 0, 0) |3|
|(-1, -1, 5) |3|
|(2, 2, 1) |1|
|(0, 1, 1) |3|
|(1, 0, 1) |3|
|(1, 1, 0) |3|

Boundary Value Analysis:
|Input Data|Expected Output|
|----------|---------------|
|(0, 0, 0) |3|
|a + b = c or b + c = a or c + a = b |3|
|(5, 5, 5) |0|
|a = b != c = 3| 1|
|a != b = c = 3| 1|
|a = c != b = 3| 1|
|{a = b + c - 1} or {b = a + c - 1} or {c = a + b - 1}|2|
|a = b = c = Integer.MAX_VALUE or a = b = c = Integer.MIN_VALUE|3|

```java
public class UnitTesting4 {
  @Test
  public void test1() {
    int a = 2, b = 2, c = 2;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 0);
  }
  @Test
  public void test2() {
    int a = 3, b = 3, c = 4;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 1);
  }
  @Test
  public void test3() {
    int a = 6, b = 5, c = 4;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 2);
  }
  @Test
  public void test4() {
    int a = 0, b = 0, c = 0;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test5() {
    int a =-1, b =-1, c = 5;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test6() {
    int a = 2, b = 2, c = 1;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 1);
  }
  @Test
  public void test7() {
    int a = 0, b = 1, c = 1;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test8() {
    int a = 1, b = 0, c = 1;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test9() {
    int a = 1, b = 1, c = 0;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  public void test10() {
    int a = 1, b = 2, c = 3;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test11() {
    int a = 3, b = 1, c = 3;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 1);
  }
  @Test
  public void test12() {
    int a = 5, b = 4, c = 2;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 2);
  }
  @Test
  public void test13() {
    int a = Integer.MAX_VALUE, b = Integer.MAX_VALUE, c =
    Integer.MAX_VALUE;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
  @Test
  public void test14() {
    int a = Integer.MIN_VALUE, b = Integer.MIN_VALUE, c =
    Integer.MIN_VALUE;
    Programs program = new Programs();
    int output = program.triangle(a, b, c);
    assertEquals(output, 3);
  }
}
```

Here test fail where input values are extreme values from integer range.

##### P5. The function prefix (String s1, String s2) returns whether or not the string s1 is a prefix of string s2 (you may assume that neither s1 nor s2 is null).

```java
public static boolean prefix(String s1, String s2){
  if (s1.length() > s2.length())
  {
    return false;
  }
  for (int i = 0; i < s1.length(); i++)
  {
  if (s1.charAt(i) != s2.charAt(i))
    {
      return false;
    }
  }
  return true;
}
```

Equivalence Partioning:
|Input Format |Expected Output|
|-------------|---------------|
|("good", "good morning") |true|
|("a", "abc") |true|
|("", "good morning") |true|
|("morning", "good morning") |false|
|("abc", "def")|false|

Boundary Partioning:
| Input Data | Expected Output|
|------------|----------------|
|("", "software") |true|
|("soft", "software") |true|
|("software", "soft") |false|
|("a", "ab") |true|
|("software", "softwareeee") |true|
|("abc", "abc") |true|
|("a", "b") |false|
|("a", "a") |true|
|("", "") |true|
|("a", "")|false|

```java
public class UnitTesting6 {
  @Test
  public void test1() {
    String str1 = "good", str2 = "good morning";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test2() {
    String str1 = "a", str2 = "abc";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test3() {
    String str1 = "", str2 = "good morning";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test4() {
    String str1 = "morning", str2 = "good morning";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, false);
  }
  @Test
  public void test5() {
    String str1 = "soft", str2 = "software";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test6() {
    String str1 = "software", str2 = "soft";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, false);
  }
  @Test
  public void test7() {
    String str1 = "a", str2 = "ab";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test8() {
    String str1 = "software", str2 = "softwareee";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test9() {
    String str1 = "abc", str2 = "abc";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test10() {
    String str1 = "a", str2 = "b";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, false);
  }
  @Test
  public void test11() {
    String str1 = "a", str2 = "a";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test12() {
    String str1 = "", str2 = "";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, true);
  }
  @Test
  public void test13() {
    String str1 = "a", str2 = "";
    Programs program = new Programs();
    boolean output = program.prefix(str1, str2);
    assertEquals(output, false);
  }
}
```
All test cases are passed successfully.

##### P6. Consider again the triangle classification program (P4) with a slightly different specification:
The program reads floating values from the standard input. The three values A, B, and C are
interpreted as representing the lengths of the sides of a triangle. The program then prints a
message to the standard output that states whether the triangle, if it can be formed, is scalene, isosceles, equilateral, or right angled.

|Equivalent Classes |Expected Output|
|-------------------|---------------|
|E1: a + b ≤ c |Invalid|
|E2: a + c ≤ b |Invalid|
|E3: b + c ≤ a |Invalid|
|E4: a = b, b = c, c = a and sum of any 2 sides is greater than the 3rd side|Equilateral|
|E5: a = b, a != c  and sum of any 2 sides is greater than the 3rd side|Isosceles|
|E6: a = c, a != b  and sum of any 2 sides is greater than the 3rd side|Isosceles|
|E7: b = c, b != a  and sum of any 2 sides is greater than the 3rd side|Isosceles|
|E8: a != b, b != c, c != a  and sum of any 2 sides is greater than the 3rd side|Scalene|
|E9: a^2 + b^2 = c^2  and sum of any 2 sides is greater than the 3rd side|Right angled triangle|
|E10: b^2 + c^2 = a^2  and sum of any 2 sides is greater than the 3rd side|Right angled triangle|
|E11: c^2 + a^2 = b^2  and sum of any 2 sides is greater than the 3rd side|Right angled triangle|



|Input format |Output|Equivalence Class Covered|
|-------------|------|-------------------------|
|(2.5, 4.6, 6.1)| Invalid| E1|
|(-2.6, 5, 6)| Invalid| E2|
|(7.1, 6.1, 1)| Invalid| E3|
|(3.1, 3.1, 3.1)| Equilateral| E4|
|(3.5, 3.5, 5)| Isosceles| E5|
|(6, 4, 6)| Isosceles| E6|
|(8, 5, 5)| Isosceles| E7|
|(6, 7, 8)| Scalene| E8|
|(3, 4, 5)| Right angled triangle| E9|
|(0.13, 0.12, 0.05)| Right angled triangle| E10|
|(7, 25, 23)| Right angled triangle| E11|

c.
- (5, 5, 10) (a + b = c)
- (5, 4.9, 10) (a + b < c)
- (5, 5.1, 10) (a + b > c)

d.
- (2, 2, 2) (a=c=b)
- (4.4, 4.4, 4.6) (a just less than c)
- (5.5, 5.5, 5.3) (a just greater than c)

e.
- (10, 10, 10) (a=b=c)
- (10, 10, 9) (a=b, a < c)
- (10, 10, 8) (a=b, a > c)

g.
- (4, 5, 6)
- (5, 5, 10)
- (0, 0, 0)

h.
- (-4, 4.2, 4.5)
- (52, -24.2, -3.2)
- (7, 15, -10)

###  Section-B

![Untitled Diagram drawio](https://user-images.githubusercontent.com/75675988/232791442-04a73677-3164-4dea-9087-71e6bee1a5a5.png)

- p = [ ( x = 12, y = 12 ), ( x = 12, y = 13 ), ( x = 11, y = 13 ), ( x = 11, y = 14 ) ]
    - Statement Covered: { 1, 2, 3, 4, 5, 7, 8 }
    - Branches Covered: { 5, 8 }
    - Basic Conditions Covered: { 5 - false, 8 - false }
- p = [ ( x = 22, y = 23 ), ( x = 23, y = 24 ), ( x = 21, y = 22 ), ( x = 25, y = 26 ) ]
    - Statements covered = { 1, 2, 3, 4, 5, 6, 7}
    - Branches covered = { 5, 8 }
    - Basic conditions covered = {5-false,true, 8-false}
- p = [ ( x = 51, y = 55 ), ( x = 52, y = 57 ), ( x = 53 , y = 55 ), ( x = 54, y = 55 ), ( x = 55, y = 56 ) ]
    - Statements covered = { 1, 2, 3, 4, 5, 6, 7, 8, 9}
    - Branches covered = { 5, 8 }
    - Basic conditions covered = { 5 - false, true, 8 - false, true }
- p = [ ( x = 1, y = 2 ) ]
    - Statements covered = { 1, 2, 3, 7, 8 }
    - Branches covered = { 8 }
    - Basic conditions covered = { }
- p=[ ]
    - Statements covered = { 1, 2, 3 }
    - Branches covered = {}
    - Basic conditions covered = {}
  Thus, the above 5 test cases are covering all statements, branches and conditions
