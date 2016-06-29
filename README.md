Spotify Checkstyle Configuration
================================
[![Maven Central](https://img.shields.io/maven-central/v/com.spotify/spotify-checkstyle-config.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.spotify%22%20spotify-checkstyle-config)
[![License](https://img.shields.io/github/license/spotify/spotify-checkstyle-config.svg)](LICENSE.txt)



This project provides a default configuration for checkstyle at Spotify.

To use it, configure your maven-checkstyle-plugin like so:

```
   <plugin>
     <artifactId>maven-checkstyle-plugin</artifactId>
     <version>2.17</version>
     <dependencies>
       <dependency>
         <groupId>com.spotify.checkstyle</groupId>
         <artifactId>spotify-checkstyle-config</artifactId>
         <version>THEVERSIONYOUWANT</version>
       </dependency>
       <dependency>
         <groupId>com.puppycrawl.tools</groupId>
         <artifactId>checkstyle</artifactId>
         <version>6.19</version>
       </dependency>
     </dependencies>
     <configuration>
       <configLocation>spotify_checks.xml</configLocation>
       <!-- The things above this line are required, the rest is 'bonus' -->
       <!------------------------------------------------------------------>
       <consoleOutput>true</consoleOutput>
       <!-- Remove or switch to false to keep building even with checkstyle errors -->
       <failOnViolation>true</failOnViolation>
       <logViolationsToConsole>true</logViolationsToConsole>
       <!-- change to 'warning' to be more strict about following checkstyle conventions -->
       <violationSeverity>error</violationSeverity>
     </configuration>
     <executions>
       <execution>
         <id>validate</id>
         <phase>validate</phase>
         <goals>
           <goal>check</goal>
         </goals>
       </execution>
     </executions>
   </plugin>
```

See the [maven-checkstyle-plugin docs](https://maven.apache.org/plugins/maven-checkstyle-plugin/) 
for more information about what the configuration settings mean.

Internally, we have the above configuration in the `<pluginManagement/>` section of a 
company-wide parent pom, meaning that projects only need to specify the below in their
`<build><plugins>` section:

```
   <plugin>
      <artifactId>maven-checkstyle-plugin</artifactId>
   </plugin>
```

# Configuration

## Suppressions

The configuration of the checkstyle plugin you get from `spotify_checks.xml` tells it to 
optionally look for a file named `suppressions.xml` as per the
[SuppressionFilter docs](http://checkstyle.sourceforge.net/config_filters.html#SuppressionFilter). 
This means you can configure suppressions by providing such a file on your
project's classpath or in the current directory where you build it - note 
that for multi-module projects, it's probably a good idea to use something
like [this solution](http://stackoverflow.com/a/19690484/1659929) to share
the configuration among each sub-module.

# Code of conduct
This project adheres to the [Open Code of Conduct][code-of-conduct]. By participating, you are expected to honor this code.

[code-of-conduct]: https://github.com/spotify/code-of-conduct/blob/master/code-of-conduct.md
