# Lab 7 - Testing

###  Submitted by - Kunj Rakesh Patel 202001421

#### Consider a program for determining the previous date. Its input is triple of day, month and year with the following ranges $1 \leq month \leq 12$, $1 \leq day \leq 31$, $1900 \leq year \leq 2015$.The possible output dates would be previous date or invalid date. Design the equivalence class test cases?

|Equivalence Class | Constraints|
|------------------|------------|
|E1|$1 \leq date \leq 31$|
|E2|$date \lt 1$|
|E3|$date \gt 31$|
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
