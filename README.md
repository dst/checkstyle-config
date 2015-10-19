# Checkstyle
Static code analyzer for Java

## Command line
	$ checkstyle -c checkstyle.xml -r dir

## Plugin for Eclipse
http://eclipse-cs.sf.net/update/

	Window -> Preferences -> Check Style -> New
	Name: My Checks
	Location: checkstyle.xml
	Select all projects -> Mouse right button -> Checkstyle -> Activate Checkstyle

## Maven
We need to add two thins in main pom.xml.

properties section:

	<maven-checkstyle-plugin-version>2.9.1</maven-checkstyle-plugin-version>

build->plugins section:

	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-checkstyle-plugin</artifactId>
		<version>${maven-checkstyle-plugin-version}</version>
		<configuration>
			<configLocation>../setup/checkstyle.xml</configLocation>
			<!-- checkstyle.xml uses basedir variable to work with Eclipse -->
			<propertyExpansion>basedir=${basedir}</propertyExpansion>
			<consoleOutput>true</consoleOutput>
			<failsOnError>true</failsOnError>
		</configuration>
		<executions>
			<execution>
				<id>checkstyle</id>
				<phase>validate</phase>
				<goals>
					<goal>check</goal>
				</goals>
			</execution>
		</executions>
	</plugin>

## Suppress file
How to configure suppress file to work in Eclipse and Maven?

Let's assume that file is located in repo/setup/

checkstyle.xml:

	<module name="SuppressionFilter">
	  <property name="file" value="${basedir}/../setup/checkstyle_suppress.xml"/>
	</module>

pom.xml, maven-checkstyle-plugin configuration:

	<propertyExpansion>basedir=${basedir}</propertyExpansion>
(${basedir} is defined Maven)

## Additional Maven plugin configurations
* http://maven.apache.org/plugins/maven-checkstyle-plugin/examples/multi-module-config.html
* http://jgonian.wordpress.com/2010/12/12/maven-checkstyle-and-eclipse/
