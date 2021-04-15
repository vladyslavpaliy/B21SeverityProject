Serenity BDD is an open source library that aims to make the idea of living documentation a reality.

Here is the link for simple intro

Steps to create a project

Create a maven project called B21SerenityProject
under pom.xml
add below into property section <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
Add dependencies
<dependencies>
<!--        This is for base support for anything we do with serenity-->
        <dependency>
            <groupId>net.serenity-bdd</groupId>
            <artifactId>serenity-core</artifactId>
            <version>2.4.4</version>
        </dependency>
<!--        this is the dependency that wrap up rest assured with additional serenity support-->
        <dependency>
            <groupId>net.serenity-bdd</groupId>
            <artifactId>serenity-rest-assured</artifactId>
            <version>2.4.4</version>
        </dependency>

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.7.1</version>
            <scope>test</scope>
        </dependency>
        <!--Junit 5 support for serenity -->
        <dependency>
            <groupId>io.github.fabianlinz</groupId>
            <artifactId>serenity-junit5</artifactId>
            <version>1.6.0</version>
        </dependency>

    </dependencies>
Add Build plugins
<build>
<plugins>
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-compiler-plugin</artifactId>
<version>3.8.1</version>
<configuration>
<source>8</source>
<target>8</target>
</configuration>
</plugin>
<!--            This is where the report is being generated after the test run -->
<plugin>
<groupId>net.serenity-bdd.maven.plugins</groupId>
<artifactId>serenity-maven-plugin</artifactId>
<version>2.4.4</version>
<executions>
<execution>
<id>serenity-reports</id>
<phase>post-integration-test</phase>
<goals>
<goal>aggregate</goal>
</goals>
</execution>
</executions>
</plugin>
<!--         We want to run all the tests then generate one report -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-surefire-plugin</artifactId>
<version>3.0.0-M5</version>
<configuration>
<testFailureIgnore>true</testFailureIgnore>
</configuration>
</plugin>
</plugins>
</build>
Create a package called b21 under src/test/java

under this package create a package called github
Create a class called GitHubUserTest
Write A simple Get single user request test with RestAssured you already know. This is how it looks like

This is just a regular test , in order to make it recognized by serenity report

Add annotation add class level : @SerenityTest
It's coming from this import import net.serenitybdd.junit5.SerenityTest;
Add a properties file with exact name serenity.properties right under project level

Add below two line to specify report name and test root folder
serenity.project.name=B21 Awesome Report
serenity.test.root=b21