# Doc_Assignment
Assignmpackage Docsumo;

import java.io.File;
import java.time.Duration;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class DAssignment {
	/*Webdriver Setup*/
	static {
		System.setProperty("webdriver.chrome.driver", "./driver/chromedriver.exe");
	}
	public static void main(String[] args) {
		/*Launching the browser*/
		WebDriver driver=new ChromeDriver();
		/*synchronization
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		/*maximizing the window*/
		driver.manage().window().maximize();
		driver.get("https://www.docsumo.com/");
		/*Locating the tools tab*/
		WebElement tools = driver.findElement(By.xpath("//*[@id=\"w-dropdown-toggle-1\"]/div[2]"));
		/*performing mouse hover on tools tab*/
		Actions a=new Actions(driver);
		a.moveToElement(tools).perform();
		/*clicking on Split pdf by Page. */

		driver.findElement(By.xpath("//div[text()='Split PDF by Page']")).click();
		/*performing file upload action*/
		try
		{
			WebElement fileUploadInput = driver.findElement(By.cssSelector("input[type='file']"));
			fileUploadInput.sendKeys("C:\\\\Users\\\\Pavithra\\\\Desktop\\\\RESUME\\\\Pavithra_Poojary_Resume.pdf");
			System.out.println("File Uploaded successfully");
		}
		catch(Exception e)
		{
			System.out.println("File could not be uploaded");
		}
		/*verifying number of pages*/
		int actualNumberOfPages=2;
		WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(20));
		
		WebElement totalPagesElement = wait.until(ExpectedConditions.presenceOfElementLocated(By.className("f2b2c")));
		int totalPages = Integer.parseInt(totalPagesElement.getText());
		if(totalPages==actualNumberOfPages)
		{
			System.out.println("Number is correct");
		}
		else
		{
			System.out.println("Number is not correct");
		}
		
		driver.findElement(By.xpath("//button[text()='Split PDF']")).click();
		driver.close();
	}

}
ent of selenium coding.
