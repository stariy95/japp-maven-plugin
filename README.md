[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.objectstyle.japp/japp-maven-plugin/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.objectstyle.japp/japp-maven-plugin/)

# japp-maven-plugin

_japp-maven-plugin_ is a plugin to assemble desktop Java applications for different platforms, namely OS X, Windows and Linux. The Linux version is actually a generic runnable jar that works on any platform.

The main motivation for the plugin continuing development is to support the assembly of CayenneModeler application developed by the [Apache Cayenne project](http://cayenne.apache.org/). However there's no Cayenne dependency what so ever. The plugin is generic and anyone is welcome to use it for Java app packaging.

## Supported Environments

The  plugin can package Java apps for the following platforms:

|Target Platform|Build Platform|Build Java Version
|---------------|--------------|-------------------
|OS X - Oracle Java (1.7 and newer)|Any|1.7+
|OS X - Legacy Apple Java (1.5, 1.6)|Any|1.7+
|Windows|Windows|1.7+
|Generic / Cross-Platform|Any|1.7+

## Getting The Plugin

* You may get a released version from Maven Central. 
* You may clone the git repo and do `mvn clean install`

## Examples

Packaging for OS X:
```xml
<plugin>
    <groupId>org.objectstyle.japp</groupId>
    <artifactId>japp-maven-plugin</artifactId>
    <version>3.1</version>
    <executions>
        <execution>
            <id>java7</id>
            <configuration>
                <name>MyApp</name>
                <mainClass>org.foo.Main</mainClass>
                <icon>src/japplication/resources/My.icns</icon>
                <os>mac</os>
                <jvmOptions>-Xmx512m -Dapple.laf.useScreenMenuBar=true</jvmOptions>
            </configuration>
            <phase>install</phase>
            <goals>
                <goal>japp</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Packaging for OS X legacy Apple JVM:

```xml
<plugin>
    <groupId>org.objectstyle.japp</groupId>
    <artifactId>japp-maven-plugin</artifactId>
    <version>3.0</version>
    <executions>
        <execution>
            <id>java6</id>
            <configuration>
                <name>MyApp (legacy)</name>
                <mainClass>org.foo.Main</mainClass>
                <icon>src/japplication/resources/My.icns</icon>
                <os>mac</os>
                <flavor>osx_legacy</flavor>
                <jvm>1.5+</jvm>
                <jvmOptions>-Xmx512m -Dapple.laf.useScreenMenuBar=true</jvmOptions>
            </configuration>
            <phase>install</phase>
            <goals>
                <goal>japp</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

More than one execution can be configured in the same `pom.xml`.

## Creating the Application Package

Packaging requires that the latest version of your application be already installed in your local maven repository. Otherwise, either your application jar will not be included in the final package, or an old version of your application jar will be included. To create your application package and ensure it is using your latest application jar ensure the execution phase is install (as in the above examples) and use the following command:

	mvn install

