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
