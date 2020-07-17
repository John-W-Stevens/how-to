#### Build your first Selenium test with Selenium, ChromeDriver, Java, Maven, JUnit, and IntelliJ IDEA.

This guides assumes zero starting knowledge of Java, IntelliJ, Maven, JUnit, or Selenium. Once IntelliJ, Java, and Maven are installed the total time to complete this guide is about 15 minutes. Instructions are written for macOS users (though they can be easily adapted to Linux of Windows).

#### A user walking through this guide will get hands-on experience/exposure to the following technologies:
1. IntelliJ IDEA - One of the most popluar IDE's for Java
2. Java - One of the most popular programming languages
3. Apache Maven - Project Management Tool for Java projects
4. Selenium - Tool for automating web application testing
5. JUnit - Unit testing framework for Java
6. ChromeDriver - Standalone server which implements W3C WebDriver standard"

##### Step 1. Install Java and Maven
* Run ```javac -version``` in your terminal, if you get an error instead of a response like ```javac 14.0.2``` then you need to install Java, which you can do by following the prompts [here](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html) (which will install the Java SE Development Kit).
* Run ```mvn --version``` in your terminal, if you get an error instead of a response like ```Apache Maven 3.6.3 ...``` then you need to install it. On Mac, using [Homebrew](https://brew.sh/), you can install Maven with this command ```brew install maven```. Otherwise try to decipher the instructions [here](https://maven.apache.org/install.html).

##### Step 2. Install IntelliJ
* Go to the Jet Brains website and follow the instructions for downloading and installing IntelliJ for [Mac](https://www.jetbrains.com/idea/download/#section=mac), [Windows](https://www.jetbrains.com/idea/download/#section=windows), or [Linux](https://www.jetbrains.com/idea/download/#section=linux).
* Make sure you select the Community Edition (its free)

##### Step 3. Install ChromeDriver.
Because macOS Catalina (which is what I use) has some issues with geckodriver (used for firefox), we will use Chrome and ChromeDriver. 
* First, find out what version of Chrome you are using. ```Chrome -> About Google Chrome```. You will see something like ```Version 84.0.4147.89 (Official Build) (64-bit)```, which is the version I am using. Either update to the latest version or just note which version you are using.
* Download the appropriate version of ChromeDriver (based on your version of Chrome) [here](https://chromedriver.chromium.org/downloads).
* Extract the executable file from the zip file you just downloaded and place it somewhere convienient (I put it in the root directory)

##### Step 4. Create a New Maven Project in IntelliJ IDEA
* Open IntelliJ
* Select "Create New Project"
* In the menu on the left, select "Maven"
* Ensure Project SDK (at the top) is pointed to your Java SDK folder
* Click "Next"
* Give the project a name, like (myFirstSeleniumTest)

##### Step 5. Configure Maven pom.xml
* pom.xml should have opened automatically and should look like this:
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>org.example</groupId>
        <artifactId>myFirstSeleniumTest</artifactId>
        <version>1.0-SNAPSHOT</version>


    </project>
    ```
* After ```<version>1.0-SNAPSHOT</version>``` add these lines:
    ```
    <properties>
        <maven.compiler.source>1.14</maven.compiler.source>
        <maven.compiler.target>1.14</maven.compiler.target>
    </properties>
    ```
    * NOTE: Replace the 14 with the version of Java you are using (i.e., version 13 should read "1.13")

* Just below the lines you just added create a dependencies section and add JUnit and Selenium:
    ```
        <dependencies>

            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.13</version>
                <scope>test</scope>
            </dependency>
        
            <dependency>
                <groupId>org.seleniumhq.selenium</groupId>
                <artifactId>selenium-java</artifactId>
                <version>3.141.59</version>
            </dependency>
        
        </dependencies>
    ```
    * You should see that the lines for JUnit and Selenium are red. This is because they haven't been imported yet. Because IntelliJ no longer imports Maven dependencies automatically, you need to import them manually. On the Mac press ```Shift+Cmd+i```. Otherwise follow the instructions [here](https://blog.jetbrains.com/idea/2020/01/intellij-idea-2020-1-eap/?_ga=2.165852535.833965504.1594850075-640107824.1594850075#maven_and_gradle_importing_updates). 
    * Note, the instructions for adding JUnit and Selenium to this file can be found [here](https://maven.apache.org/plugins-archives/maven-surefire-plugin-2.12.4/examples/junit.html) and [here](https://www.selenium.dev/maven/).

##### Step 6. Create Java Test Class
* On the right hand side click ```myFirstSeleniumTest``` (or whatever you named this project)
* Among the options that just appeared click ```src```.
* You should see "main" and "test", click ```test```.
* Rightclick on ```test/java``` and select ```New -> Java Class```
* Name the class ```myFirstTest```.

##### Step 7. Move newly created class into package
* At the top of the file, before ``` public class myFirstTest {```, type ```package com.some_name.webdriver``` where ```some_name``` is anything you want. 
* You will see that ```package com.some_name.webdriver``` is underlined in red.
    * Click anywhere on ```package com.some_name.webdriver``` and press ```option+enter```
    * Click the top option and then press ```okay```

##### Step 8. Create Test
* Inside ```public class myFirstTest()``` write ```@Test```. You will see auto-complete pop up with ```org.Junit``` highlighted. Hit ```enter```.
* On the next line, paste this code:
    ```
        public void startWebDriver(){
            System.setProperty("webdriver.chrome.driver", "/Users/johnstevens/chromedriver");
            WebDriver driver = new ChromeDriver();
            driver.navigate().to("http://www.euler100blog.net/");
            Assert.assertTrue("title should start with Home",
                    driver.getTitle().startsWith("Home"));
            driver.close();
            driver.quit();
        }
    ```
    * Several words will be in red, click on each red word and press ```option+enter```
    * On the word "Assert", press ```option+enter``` and then select the ```org.junit``` option.

##### Step 9. Try it out!
* Rightclick on the ```startWebDriver()``` method and select ```Run startWebDriver()```.
* You should see a new Chrome window open, navigate to www.euler100blog.net, and then close down. In the terminal output at the bottom of IntelliJ you should see ``` Process finished with exit code 0```.
* At the top of the terminal you should see a green checkmark followed by ```Tests passed: 1```

##### Continue learning
* Learn more about [Maven](https://maven.apache.org/).
* Learn more about [JUnit](https://junit.org/junit5/docs/current/user-guide/).
* Learn more about [Selenium](https://www.selenium.dev/documentation/en/).