---
title: Maven Configuration in admin/broadleaf-contentmanagement-module
---
# Intro

This document explains how Maven is used in the <SwmPath>[admin/broadleaf-contentmanagement-module/](admin/broadleaf-contentmanagement-module/)</SwmPath> directory. It will cover the configuration steps in the <SwmPath>[pom.xml](pom.xml)</SwmPath> file.

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="1">

---

# Project Definition

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts by defining the project model version and the XML namespaces required for Maven.

```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="4">

---

The project inherits from the <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="5:4:4" line-data="        &lt;artifactId&gt;admin&lt;/artifactId&gt;">`admin`</SwmToken> parent project, specifying the <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="5:2:2" line-data="        &lt;artifactId&gt;admin&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="6:2:2" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`groupId`</SwmToken>, and <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="7:2:2" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`version`</SwmToken>.

```xml
    <parent>
        <artifactId>admin</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="9">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;broadleaf-contentmanagement-module&lt;/artifactId&gt;">`artifactId`</SwmToken> for this module is <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="9:4:8" line-data="    &lt;artifactId&gt;broadleaf-contentmanagement-module&lt;/artifactId&gt;">`broadleaf-contentmanagement-module`</SwmToken>, and it is packaged as a JAR file. The project name and description are also provided.

```xml
    <artifactId>broadleaf-contentmanagement-module</artifactId>
    <packaging>jar</packaging>
    <name>BroadleafCommerce CMS Module</name>
    <description>BroadleafCommerce CMS Module</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="14">

---

Project properties are defined, including the <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="15:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken> property.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="17">

---

The licensing information is specified, including the license name, URL, distribution method, and comments.

```xml
    <licenses>
        <license>
            <name>Broadleaf Fair Use 1.0</name>
            <url>http://license.broadleafcommerce.org/fair_use_license-1.0.txt</url>
            <distribution>repo</distribution>
            <comments>Fair Use Community License</comments>
        </license>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="25">

---

Developer information is provided, including the developer ID, email, organization, organization URL, and timezone.

```xml
    <developers>
        <developer>
            <id>architect</id>
            <email>architect@broadleafcommerce.org</email>
            <organization>Broadleaf Commerce</organization>
            <organizationUrl>https://www.broadleafcommerce.com</organizationUrl>
            <timezone>-6</timezone>
        </developer>
    </developers>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="34">

---

The build section specifies the resources to be included in the build. It includes resources from <SwmPath>[admin/broadleaf-admin-functional-tests/src/main/resources/](admin/broadleaf-admin-functional-tests/src/main/resources/)</SwmPath> and excludes Java files from <SwmPath>[admin/broadleaf-admin-module/src/main/java/](admin/broadleaf-admin-module/src/main/java/)</SwmPath>.

```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <excludes>
                    <exclude>**/*.java</exclude>
                </excludes>
            </resource>
        </resources>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="47">

---

A Maven profile named <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="49:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken> is defined. This profile includes the <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="54:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> to generate `rebel.xml` during the <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="58:4:6" line-data="                                &lt;phase&gt;process-resources&lt;/phase&gt;">`process-resources`</SwmToken> phase.

```xml
    <profiles>
        <profile>
            <id>blc-development</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.zeroturnaround</groupId>
                        <artifactId>jrebel-maven-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>generate-rebel-xml</id>
                                <phase>process-resources</phase>
                                <goals>
                                    <goal>generate</goal>
                                </goals>
                            </execution>
                        </executions>

                    </plugin>
                </plugins>
            </build>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/pom.xml" line="70">

---

Dependencies for the project are listed. These include <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="73:4:10" line-data="            &lt;artifactId&gt;broadleaf-open-admin-platform&lt;/artifactId&gt;">`broadleaf-open-admin-platform`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="77:4:6" line-data="            &lt;artifactId&gt;tika-core&lt;/artifactId&gt;">`tika-core`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="81:4:6" line-data="            &lt;artifactId&gt;broadleaf-common&lt;/artifactId&gt;">`broadleaf-common`</SwmToken> (for tests), <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="86:6:6" line-data="            &lt;groupId&gt;org.easymock&lt;/groupId&gt;">`easymock`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="91:4:4" line-data="            &lt;artifactId&gt;mvel2&lt;/artifactId&gt;">`mvel2`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="94:4:4" line-data="            &lt;groupId&gt;junit&lt;/groupId&gt;">`junit`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="99:4:8" line-data="            &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;">`javax.servlet-api`</SwmToken>, and <SwmToken path="admin/broadleaf-contentmanagement-module/pom.xml" pos="103:4:6" line-data="            &lt;artifactId&gt;spring-test&lt;/artifactId&gt;">`spring-test`</SwmToken> (for tests).

```xml
    <dependencies>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-open-admin-platform</artifactId>
        </dependency>
        <dependency>
            <groupId>org.apache.tika</groupId>
            <artifactId>tika-core</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-common</artifactId>
            <classifier>tests</classifier>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mvel</groupId>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
