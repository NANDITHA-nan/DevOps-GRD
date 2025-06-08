gradle project
build.grd
plugins {
    id 'application'
}
repositories {
    mavenCentral()
}
dependencies {
    implementation group: 'org.seleniumhq.selenium', name: 'selenium-java', version: '4.33.0' //gradle long
    testImplementation group: 'org.testng', name: 'testng', version: '7.11.0'
}
test{
    useTestNG()
}
application {
    mainClass = 'org.example.Main'
}


or
plugins {
 id 'application'
 }
 repositories {
 mavenCentral()
 }
 dependencies {
 testImplementation 'org.seleniumhq.selenium:selenium-java:4.28.1' // use the latest stable
 version  
testImplementation 'org.testng:testng:7.4.0' // use the latest stable version 
 }
 test {
 useTestNG()
 }
 application {
 mainClass = 'org.example.Main'
}
jar {
 manifest {
 attributes 'Main-Class': 'com.example.Main'  // This tells Java where to start execution
 }
}


main.java
package org.example;

//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    public static void main(String[] args) {
        System.out.print("Hello and welcome!");
    }
}


webpagetest.java
package org.test;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import static org.testng.Assert.assertTrue;

public class WebpageTest {
    private static WebDriver driver;
    @BeforeTest
    public void openBrowser() throws InterruptedException {
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        Thread.sleep(2000);
        driver.get("https://github.com/NANDITHA-nan/DevOps-GRD"); // "Note: You should use your GITHUB-URL here...!!!"
    }
    @Test
    public void titleValidationTest(){
        String actualTitle = driver.getTitle();
        String expectedTitle = "My Simple Website";// title should be match with the index.html title
        Assert.assertEquals(driver.getTitle(), "GitHub - NANDITHA-nan/DevOps-GRD");
        //given github login  username and the repository name with description
        assertTrue(true, "Title should contain 'ci/cd'");
    }
    @AfterTest
    public void closeBrowser() throws InterruptedException {
        Thread.sleep(1000);
        driver.quit();
    }
}


or
 package org.test;
 import org.openqa.selenium.WebDriver;
 import org.openqa.selenium.chrome.ChromeDriver;
 import org.testng.Assert;
 import org.testng.annotations.AfterTest;
  import org.testng.annotations.BeforeTest;
  import org.testng.annotations.Test;
import static org.testng.Assert.assertTrue;
 public class WebpageTest {
 private static WebDriver driver;
 @BeforeTest
 public void openBrowser() throws InterruptedException {
 driver = new ChromeDriver();
 driver.manage().window().maximize();
 Thread.sleep(2000);
 driver.get("https://github.com/NANDITHA-nan/DevOps-GRD");
 }
 @Test
 public void titleValidationTest(){
 String actualTitle = driver.getTitle();
 String expectedTitle = "Tripillar Solutions";
 Assert.assertEquals(actualTitle, expectedTitle);
 assertTrue(true, "Title should contain 'Tripillar'");
 @AfterTest
 public void closeBrowser() throws InterruptedException {
 Thread.sleep(1000);
 driver.quit();
}
}

maven-to-gradle
pom.xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>DevOps-VTU-MVN-To-GRD</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>  <!-- Java version -->
                    <target>1.8</target>
                </configuration>
            </plugin>

            <!-- JAR Plugin -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <mainClass>org.example.Main</mainClass> <!-- Replace with your main class -->
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>

build.gradle
/*
 * This file was generated by the Gradle 'init' task.
 *
 * This project uses @Incubating APIs which are subject to change.
 */

plugins {
    id 'java-library'
    id 'maven-publish'
    id 'java'
}

repositories {
    mavenLocal()
    maven {
        url = uri('https://repo.maven.apache.org/maven2/')
    }
}

group = 'org.example'
version = '1.0-SNAPSHOT'
description = 'DevOps-VTU-MVN-To-GRD'
java.sourceCompatibility = JavaVersion.VERSION_1_8

publishing {
    publications {
        maven(MavenPublication) {
            from(components.java)
        }
    }
}

tasks.withType(JavaCompile) {
    options.encoding = 'UTF-8'
}

tasks.withType(Javadoc) {
    options.encoding = 'UTF-8'
}
dependencies {
    testImplementation 'junit:junit:4.13.2'
}
jar {
    manifest{
        attributes(
                'Main-Class':'org.example.Main'
        )
    }
}
