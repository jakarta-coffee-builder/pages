* TOC
{:toc}

# Jakarta Coffee Builder Plugin 
![Maven Central Version](https://img.shields.io/maven-central/v/com.apuntesdejava/jakarta-coffee-builder-plugin)
![GitHub last commit](https://img.shields.io/github/last-commit/jakarta-coffee-builder/jakarta-coffee-builder-plugin)
[![GitHub](https://img.shields.io/badge/maven-plugin-darkgreen?logo=github)](https://github.com/jakarta-coffee-builder/jakarta-coffee-builder-plugin)

This plugin allows you to add Jakarta EE functionality, including dependencies (if missing) and sample code in a light, fast and clear way.

You do not need to add the plugin description in the `pom.xml` file. You can run it from the command line as follows:


## Jakarta Faces

### Add Jakarta Faces Configuration

Add Jakarta Faces Servlet configuration in `web.xml` file

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-faces 
```

**Parameters**

| Parameter      | Definition                                                                                                                | Default value |
|----------------|---------------------------------------------------------------------------------------------------------------------------|---------------|
| `url-pattern`  | This parameter defines the URL pattern for all Faces pages. This value will be included in the servlet configuration.     | `*.faces`     |
| `welcome-file` | This parameter indicates which page is displayed at startup by default. It must be related to the `url-pattern` parameter | `index.faces` |

**Result**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="6.0" xmlns="https://jakarta.ee/xml/ns/jakartaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd">
    <servlet>
        <description>Jakarta Faces Servlet Definition</description>
        <servlet-name>JakartaServlet</servlet-name>
        <servlet-class>jakarta.faces.webapp.FacesServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>JakartaServlet</servlet-name>
        <url-pattern>*.faces</url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file>index.faces</welcome-file>
    </welcome-file-list>
</web-app>

```

**Showing**
[![asciicast](https://asciinema.org/a/30Zyd628az3toF03XtZ5eSLRc.svg)](https://asciinema.org/a/30Zyd628az3toF03XtZ5eSLRc)


### Add Jakarta Faces Page

Add a Face page, associating it with a Managed Bean. It can also be done by using a specified Facelet template

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-page
```

**Parameters**

| Parameter      | Definition                                                                                            | Default value |
|----------------|-------------------------------------------------------------------------------------------------------|---------------|
| `name`         | Name of the Face page to create                                                                       |               |
| `managed-bean` | Boolean value indicating whether or not the Managed Bean class associated with the Face is created.   | `true`        |
| `template`     | Path of the Facelet template to be implemented for the Face to be created. This parameter is optional |               |


**Example**
```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-page \
    -Dname=hello-world \
    -Dmanaged-bean=false  
    
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-page \
    -Dname=persons \
    -Dmanaged-bean=true  
    
```

**Showing**

Creating page with / without Managed Bean:
[![asciicast](https://asciinema.org/a/And0N0LueNSaMCKV9VnyKm1gr.svg)](https://asciinema.org/a/And0N0LueNSaMCKV9VnyKm1gr)


### Create Jakarta Face Facelet (Template)
Add a Facelet template to be used in the Face page

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-template
```

**Parameters**

| Parameter | Definition                                                                       | Example                            |  
|-----------|----------------------------------------------------------------------------------|------------------------------------|
| `name`    | Name of the Facelet template to create                                           | `/WEB-INF/template/template.xhtml` |      
| `inserts` | List of block names to be used for insertion. Names must be separated by commas. | `block1,block2,block3`             |

**Example**
```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-template \
    -Dname=/WEB-INF/template/main.xhtml \
    -Dinserts=header,body,footer
```
**Showing**
[![asciicast](https://asciinema.org/a/tD2VpNkH5EHSQaTYRu9pasArc.svg)](https://asciinema.org/a/tD2VpNkH5EHSQaTYRu9pasArc)


### Using Facelet template in Face page

To use the Facelet template in the Face page, you need to run this command (by example, to use the template created in the previous step):

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-face-page \
    -Dname=products \
    -Dtemplate=/WEB-INF/template/main.xhtml
```
**Showing**
[![asciicast](https://asciinema.org/a/YZie5pQs2igDZAuBeHWgfkdBM.svg)](https://asciinema.org/a/YZie5pQs2igDZAuBeHWgfkdBM)

## Jakarta Persistence

### Add Jakarta Persistence Configuration

Add Jakarta Persistence configuration in `persistence.xml` file

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-persistence
```

**Parameters**

| Parameter               | Definition                                                                                                             | Default value |
|-------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|
| `persistence-unit-name` | This parameter defines the name of the persistence unit. This value will be included in the persistence configuration. | `defaultPU`   |

### Add DataSource configuration

Add DataSource configuration

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-datasource
```

**Parameters**

| Parameter          | Definition                                                                                                              | Default value                 |
|--------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------------|
| `name`             | This parameter defines the JNDI name of the DataSource. This value will be included in the DataSource configuration.    |                               |
| `class-name`       | This parameter defines the driver class of the DataSource. This value will be included in the DataSource configuration. | `org.h2.jdbcx.JdbcDataSource` |
| `url`              | This parameter defines the URL of the DataSource. This value will be included in the DataSource configuration.          |                               |
| `username`         | This parameter defines the username of the DataSource. This value will be included in the DataSource configuration.     |                               |
| `password`         | This parameter defines the password of the DataSource. This value will be included in the DataSource configuration.     |                               |
| `coordinates-jdbc` | This parameter defines the coordinates of the JDBC driver. This value will be included in the DataSource configuration. | `com.h2database:h2:1.4.200`   |
| `declare`          | Indicates how the DataSource is to be declared in the application. Possible values are `web.xml` `class`                | `class`                       |
| `server-name`      | This parameter defines the server name of the DataSource. This value will be included in the DataSource configuration.  |                               |
| `port-number`      | This parameter defines the port number of the DataSource. This value will be included in the DataSource configuration.  |                               |
| `properties`       | This parameter defines the properties of the DataSource. This value will be included in the DataSource configuration.   |                               |
| `persistence-unit` | This parameter defines the name of the persistence unit. This value will be included in the persistence configuration.  |                               | 


### Add Jakarta Persistence Entity
```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:add-entities

```

**Parameters**

| Parameter       | Definition                                                                                        | Example                                                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `entities-file` | The name of the json file that contains the list of entities and their definitions to be created. | [entities.json](https://github.com/jakarta-coffee-builder/jakarta-coffee-builder-plugin/blob/main/examples/entities.json) |

**Example JSON File**
```json
[
  {
    "name": "Coffee",
    "repository": "crud",
    "fields": [
      {
        "name": "id",
        "type": "Long",
        "isId": true
      },
      {
        "name": "name",
        "type": "String",
        "column": {
          "name": "coffee_name",
          "length": 100,
          "unique": true,
          "nullable": false
        }
      },
      {
        "name": "price",
        "type": "Double"
      }
    ]
  },
  {
    "name": "Order",
    "table": "order_",
    "repository": "data",
    "fields": [
      {
        "name": "id",
        "type": "Long",
        "isId": true
      },
      {
        "name": "coffee",
        "type": "Coffee",
        "manyToOne": true,
        "joinColumn": {
          "name": "coffee_id",
          "nullable": false
        }
      },
      {
        "name": "quantity",
        "type": "Integer"
      }
    ]
  }
]
```

## Jakarta RESTful Web Services

### Create REST services with OpenAPI specifications

```shell
mvn com.apuntesdejava:jakarta-coffee-builder-plugin:create-openapi 
```

**Parameters**

| Parameter        | Definition                                                                        | Example                                                                                                                 |
|------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `openapi-server` | The name of the yml file is specified with the server-side OpenAPI specification. | [openapi.yaml](https://github.com/jakarta-coffee-builder/jakarta-coffee-builder-plugin/blob/main/examples/openapi.yaml) |

**Note**
- Each endpoint must be identified by a label