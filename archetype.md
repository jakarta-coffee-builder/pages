# Jakarta EE Essentials Archetype 
![Maven Central Version](https://img.shields.io/maven-central/v/com.apuntesdejava/jakarta-ee-essentials)
![Maven Central Last Update](https://img.shields.io/maven-central/last-update/com.apuntesdejava/jakarta-ee-essentials) 
[![GitHub](https://img.shields.io/badge/maven-archetype-darkgreen?logo=github)](https://github.com/jakarta-coffee-builder/jakarta-ee-essentials)


With this archetype you can create a Jakarta EE project with minimal dependencies and configurations.

This will allow you to have a clean and clear `pom.xml` file so you can add more configurations as needed.

### Usage

To create a new Jakarta EE project using this archetype, run the following command:

```shell
mvn -DarchetypeGroupId=com.apuntesdejava \
    -DarchetypeArtifactId=jakarta-ee-essentials \
    -DjakartaProfile={jakartaProfile} \
    -DjakartaVersion={jakartaVersion} \
    org.apache.maven.plugins:maven-archetype-plugin:generate 
```

Values for `jakartaProfile` property:
- `core`
- `web`
- `full` (default)

Values for `jakartaVersion` property:
- `10.0.0`
- `11.0.0` (default)

### 📌 Note
As of this post, it is only creating the dependency for Jakarta EE 11, version 11.0.0-M4

### Example

```shell
mvn -DarchetypeGroupId=com.apuntesdejava \
    -DarchetypeArtifactId=jakarta-ee-essentials \
    -DgroupId=com.example \
    -DartifactId=example-app \
    -Dversion=1.0-SNAPSHOT \
    -DjakartaProfile=full \
    -DjakartaVersion=11.0.0 \
    org.apache.maven.plugins:maven-archetype-plugin:generate 
```


***Showing***
[![asciicast](https://asciinema.org/a/86ooZkGxggx6VaxrZlZDje9NO.svg)](https://asciinema.org/a/86ooZkGxggx6VaxrZlZDje9NO)