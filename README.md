# List of predefined Maven properties

*This list is based on a wiki page from Codehaus (http://docs.codehaus.org/display/MAVENUSER/MavenPropertiesGuide) which unfortunately has been gone with the shutdown of Codehaus*


Note: In Maven 3.0, all pom.* properties are deprecated. Use project.* instead!

## Built-in properties
`${basedir}` represents the directory containing pom.xml  
`${version}` equivalent to `${project.version}` (deprecated: `${pom.version}`)

## Pom/Project properties
All elements in the pom.xml, can be referenced with the project. prefix. This list is just an example of some commonly used elements. (deprecated: `${pom.}` prefix)  
`${project.build.directory}` results in the path to your "target" directory, this is the same as `${pom.project.build.directory}`  
`${project.build.outputDirectory}` results in the path to your "target/classes" directory  
`${project.name}` refers to the name of the project (deprecated: `${pom.name}` ).  
`${project.version}` refers to the version of the project (deprecated: `${pom.version}`).  
`${project.build.finalName}` refers to the final name of the file created when the built project is packaged

## Local user settings
Similarly, values in the user's settings.xml can be referenced using property names with `settings.` prefix.
`${settings.localRepository}` refers to the path of the user's local repository

## Environment variables
Environment variables can be referenced using the env prefix  
`${env.M2_HOME}` returns the Maven2 installation path.  
`${java.home}` specifies the path to the current JRE_HOME environment use with relative paths to get for example:
`<jvm>${java.home}../bin/java.exe</jvm>`

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
User defined properties in the pom.xml.
```
<project>
...
  <properties>
     <my.filter.value>hello</my.filter.value>
  </properties>
...
</project>
```

`${my.filter.value}` will result in hello if you inserted the above XML fragment in your pom.xml

## Parent Project variables
How can parent project variables be accessed?
You can use the prefix: `${project.parent}`.
A good way to determine possible variables is to have a look directly at the API. I'm currently using Maven 2.2.1, and to access the Parent you can use `${project.parent}`. This will return an org.apache.maven.project.MavenProject instance.  
To access the parent version: `${parent.version}.`

## Reflection Properties
The pattern `${someX.someY.someZ}` can simply sometimes mean getSomeX().getSomeY().getSomeZ(). Thus, properties such as ${project.build.directory} is translated to getProject().getBuild().getDirectory().
