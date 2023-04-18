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
|v is non existent and empty array|-1|
|v is non existent and non-empty array|-1|
|v exists in array|index of v in array|
|v doesn't exist in array|-1|

