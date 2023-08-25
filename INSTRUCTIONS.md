Copy the contents of https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine locally.

If your intent is to build with gradle this is all that is necessary.

If your intent is to build with maven:
- Generate a pom.xml with the command `mvn archetype:generate -DgroupId=org.jetbrains.java.decompiler -DartifactId=fernflower -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`.
- Add build section to set the source directory and main class.
```
  <build>
    <sourceDirectory>src</sourceDirectory>
    <plugins>
      <plugin>
        <!-- Build an executable JAR -->
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.1.0</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler</mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
```
- Add properties to use the appropriate Java version
```
  <properties>
     <maven.compiler.source>17</maven.compiler.source>
     <maven.compiler.target>17</maven.compiler.target>
  </properties>
```
- Convert dependencies from build.gradle to pom.xml. For instance these gradle deps:
```
dependencies {
  implementation 'org.jetbrains:annotations:20.1.0'
  testImplementation 'junit:junit:4.12'
  testImplementation 'org.assertj:assertj-core:3.23.1'
}
```
become:
```
  <dependencies>
    <dependency>
      <groupId>org.jetbrains</groupId>
      <artifactId>annotations</artifactId>
      <version>20.1.0</version>
    </dependency>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.assertj</groupId>
      <artifactId>assertj-core</artifactId>
      <version>3.23.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
```
