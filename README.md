# List of predefined Maven properties

*This list originated from a wiki page from Codehaus (http://docs.codehaus.org/display/MAVENUSER/MavenPropertiesGuide) which unfortunately has been gone with the shutdown of Codehaus*

## Command to list the JVM system properties and environment variables, and their values

```
mvn help:system
```

## Command to get the value of a given property, e.g. `${project.basedir}`

```
mvn help:evaluate -Dexpression=project.basedir -q -DforceStdout
```

## Built-in properties

**Note:** In Maven 3.0, all `${pom.*}` properties are deprecated. Use `${project.*}` instead!

`${project.basedir}` represents the directory containing `pom.xml` (deprecated: `${basedir}`)
`${project.baseUri}` the directory containing the `pom.xml` file as URI
`${project.version}` (deprecated: `${pom.version}` and `${version}`)
`${maven.home}` The path to the current Maven home
`${maven.version}` The version number of the current Maven execution (since 3.0.4)
`${maven.build.version}` The full build version of the current Maven execution (since 3.0.4). For example, `Apache Maven 3.2.2 (r01de14724cdef164cd33c7c8c2fe155faf9602da; 2013-02-19T14:51:28+01:00)`.

## Pom/Project properties
All elements in the `pom.xml`, can be referenced with the project. prefix. This list is just an example of some commonly used elements. (deprecated: `${pom.}` prefix)
`${project.build.directory}` results in the path to your `target` directory
`${project.build.outputDirectory}` results in the path to your `target/classes` directory
`${project.name}` refers to the name of the project (deprecated: `${pom.name}` ).
`${project.version}` refers to the version of the project (deprecated: `${pom.version}`).
`${project.groupId}` refers to the groupId of the project
`${project.build.finalName}` refers to the final name of the file created when the built project is packaged

## Local user settings
Similarly, values in the user's settings.xml can be referenced using property names with `settings.` prefix.
`${settings.localRepository}` refers to the path of the user's local repository

## Environment variables
Environment variables can be referenced using the env prefix
`${env.M2_HOME}` returns the Maven2 installation path.
`${java.home}` specifies the path to the current JRE_HOME environment use with relative paths to get for example:
```xml
<jvm>${java.home}../bin/java.exe</jvm>
```

## Java system properties
All Java System Properties defined by the JVM:
`${file.separator}`
`${java.class.path}`
`${java.home}`
`${java.vendor}`
`${java.vendor.url}`
`${java.version}`
`${line.separator}`
`${os.arch}`
`${os.name}`
`${os.version}`
`${path.separator}`
`${user.dir}`
`${user.home}`
`${user.name}`
...

## Custom properties in the POM
User defined properties in the `pom.xml`.
```xml
<project>
...
  <properties>
    <my.filter.value>hello</my.filter.value>
  </properties>
...
</project>
```

`${my.filter.value}` will result in `hello` if you inserted the above XML fragment in your `pom.xml`

## Build Information
`${build.timestamp}` or `${maven.build.timestamp}` UTC timestamp of build start (default format: `yyyy-MM-dd'T'HH:mm:ss'Z'`), format can be overridden with `${maven.build.timestamp.format}`

## Parent Project variables
How can parent project variables be accessed?
You can use the prefix: `${project.parent}`.
A good way to determine possible variables is to have a look directly at the API. I'm currently using Maven 2.2.1, and to access the Parent you can use `${project.parent}`. This will return an org.apache.maven.project.MavenProject instance.
To access the parent version: `${parent.version}.`

## Reflection Properties
The pattern `${someX.someY.someZ}` can simply sometimes mean `getSomeX().getSomeY().getSomeZ()`. Thus, properties such as `${project.build.directory}` is translated to `getProject().getBuild().getDirectory()`.

## Further information
http://maven.apache.org/components/ref/3-LATEST/maven-model-builder/
