# Lab 8 - JUnit Testing

###  Submitted by - Kunj Rakesh Patel 202001421


#### Boa Class

'''java
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

'''
