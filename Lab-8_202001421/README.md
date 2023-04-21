# Lab 8 - JUnit Testing

###  Submitted by - Kunj Rakesh Patel 202001421


#### Boa Class

```java
package pkg;

public class Boa {
	private String name;
	private int length; 
	private String favoriteFood;
	
	public Boa (String name, int length, String favoriteFood){
		this.name = name;
		this.length = length;
		this.favoriteFood = favoriteFood;
	}
	
	public boolean isHealthy(){
		return this.favoriteFood.equals("granola bars");
	}
	
	public boolean fitsInCage(int cageLength){
		return this.length < cageLength;	
	}
}
```


The @Before ensures that objects are intialised before tests are run

```java
package pkg;

import static org.junit.Assert.*;
import org.junit.Before;
import org.junit.Test;

class Testcases {

	private Boa jen;
	private Boa ken;
	
	@Before
	public void setUp() throws Exception {
		jen = new Boa("Jennifer", 2, "grapes");
		ken = new Boa ("Kenneth", 3, "granola bars");
	}
	@Test
	public void testIsHealthy() {
		assertTrue(ken.isHealthy());
		assertFalse(jen.isHealthy());
	}
	@Test
	public void testFitsInCage() {
		assertFalse(jen.fitsInCage(1));
		assertTrue(jen.fitsInCage(3));
		assertFalse(jen.fitsInCage(2));
	}

}

```

On running the test we get a green bar indicating all test cases have passed.

![image](https://user-images.githubusercontent.com/75675988/233603333-bb011b63-2af8-4ed9-ab5a-b9fa0891d6a1.png)

Adding new methods and appropriate tests to class

method
```java
public int lengthInInches(){
  return this.length*12;
}
```

Test
```java
@Test
public void testLengthInInches() {
  assertEquals(24, jen.lengthInInches());
  assertEquals(36, ken.lengthInInches());
}

```
