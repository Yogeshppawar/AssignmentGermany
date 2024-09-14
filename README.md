# AssignmentGermany
package mytest;

import static org.testng.Assert.assertEquals;

import java.util.List;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class LoginPage {
WebDriver driver;

	@BeforeMethod
	public void setup() {
		System.setProperty("webdriver.chrome.driver", "E:\\YoGeSH\\Software Testing Notes\\Eclipse Backup\\chromedriver-win64\\chromedriver-win64\\chromedriver.exe");
		driver= new ChromeDriver();
		driver.get("https://app.germanyiscalling.com/common/login/?next=https%3A%2F%2Fapp.germanyiscalling.com%2Fcv%2Fhome%2F");
	driver.manage().window().maximize();
	//driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	
	
	}
	
	   @Test (priority=1)
       public void Successfulllogin() {
	
	    WebElement username =  driver.findElement(By.xpath("//input[@type=\"text\"]"));
	    WebElement password =  driver.findElement(By.xpath("//input[@type=\"password\"]"));
	
	    
	    username.sendKeys("yogesh pawar");
	    password.sendKeys("Yogesh@123");
	    
	  
	    WebElement Submitbtn = driver.findElement(By.xpath("//button[@type=\"submit\"]"));
	    Submitbtn.click();
	    
	    //Assertion
	    
	    String expectedTitle = "Login | Germany Is Calling";
	    String actualTitle = driver.getTitle();
	    assertEquals(expectedTitle, actualTitle);
	    	    
}

	 @Test (priority=2)
	 
	 public void UnSuccessfulllogin() {
			
		    WebElement username =  driver.findElement(By.xpath("//input[@type=\"text\"]"));
		    WebElement password =  driver.findElement(By.xpath("//input[@type=\"password\"]"));
		
		    
		    username.sendKeys("yogesh pawar2");
		    password.sendKeys("Yogesh@1234");
		    
		  
		    WebElement Submitbtn = driver.findElement(By.xpath("//button[@type=\"submit\"]"));
		    Submitbtn.click();
	
	    // Assertion
		    WebElement errorMessage = driver.findElement(By.xpath("//li[text()= \"Please enter a correct username and password. Note that both fields may be case-sensitive.\"]"));
		 //   Assert.assertTrue(errorMessage.isDisplayed();
	
	
		    String actualErrorMessage = errorMessage.getText();
		//    System.out.println("actualErrorMessage");
		    String expectedErrorMessage = "Please enter a correct username and password. Note that both fields may be case-sensitive.";
		   
		    assertEquals(actualErrorMessage, expectedErrorMessage);
		    
		    
	 }
		    
		    
	@AfterMethod
	public void teardown() {
		driver.quit();
		
		
		
	}
}
