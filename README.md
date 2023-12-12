Bismillah

# notes
Notes for R&amp;D

To globally find and replace text in all .java files during a Maven build process, you can use the maven-resources-plugin with a custom configuration. This plugin allows you to filter and replace text in resource files, and with a bit of configuration, you can apply it to your Java source files as well. Here's a step-by-step guide on how to set this up:

Add the maven-resources-plugin to Your pom.xml:
Add the maven-resources-plugin to the build section of your pom.xml. You need to configure it to include your Java source files in the resources to be filtered.

Configure Source Directory and Filtering:
Specify the source directory (src/main/java typically) and enable filtering. You also need to define the file extension to filter (.java files in your case).

Define Properties for Replacement:
In the properties section of your pom.xml, define the text that needs to be replaced and its replacement. These properties will be used in the filtering process.

Run Maven Build:
When you run your Maven build, the plugin will process the Java files and replace the specified text.

Here is an example configuration for your pom.xml:

`
<project>
<!-- ... other configurations ... -->

    <properties>
        <!-- Define the text to find and its replacement here -->
        <text.to.replace>originalText</text.to.replace>
        <replacement.text>newText</replacement.text>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>3.1.0</version>
                <executions>
                    <execution>
                        <phase>process-resources</phase>
                        <goals>
                            <goal>resources</goal>
                        </goals>
                        <configuration>
                            <resources>
                                <resource>
                                    <directory>${project.basedir}/src/main/java</directory>
                                    <includes>
                                        <include>**/*.java</include>
                                    </includes>
                                    <filtering>true</filtering>
                                </resource>
                            </resources>
                            <!-- Use the delimiters that won't conflict with Java syntax -->
                            <delimiters>
                                <delimiter>@</delimiter>
                            </delimiters>
                            <useDefaultDelimiters>false</useDefaultDelimiters>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>

`