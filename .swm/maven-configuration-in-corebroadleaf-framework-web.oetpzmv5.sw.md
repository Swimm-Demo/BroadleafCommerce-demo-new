---
title: Maven Configuration in core/broadleaf-framework-web
---
# Intro

This document explains how Maven is used in the <SwmPath>[core/broadleaf-framework-web/](core/broadleaf-framework-web/)</SwmPath> directory. It will go through the <SwmPath>[pom.xml](pom.xml)</SwmPath> configuration file step by step.

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="1">

---

# Project Definition

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts with the XML declaration and the project definition, specifying the XML namespace and schema location.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="3">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="3:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> section defines the parent project from which this project inherits. It specifies the <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="4:2:2" line-data="        &lt;artifactId&gt;core&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="5:2:2" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`groupId`</SwmToken>, and <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="6:2:2" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`version`</SwmToken> of the parent project.

```xml
    <parent>
        <artifactId>core</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="8">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="8:2:2" line-data="    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;">`modelVersion`</SwmToken>, <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;broadleaf-framework-web&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="10:2:2" line-data="    &lt;name&gt;BroadleafCommerce Framework Web&lt;/name&gt;">`name`</SwmToken>, <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="11:2:2" line-data="    &lt;description&gt;BroadleafCommerce Framework Web&lt;/description&gt;">`description`</SwmToken>, and <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="12:2:2" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`url`</SwmToken> elements provide basic information about the project.

```xml
    <modelVersion>4.0.0</modelVersion>
    <artifactId>broadleaf-framework-web</artifactId>
    <name>BroadleafCommerce Framework Web</name>
    <description>BroadleafCommerce Framework Web</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="13">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="13:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> section defines project-specific properties, such as <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="14:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="16">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="16:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> section specifies the licensing information for the project, including the license name, URL, distribution method, and comments.

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

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="23">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="24:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> section lists the developers involved in the project, providing their ID, email, organization, organization URL, and timezone.

```xml
    </licenses>
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

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="33">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="33:2:2" line-data="    &lt;profiles&gt;">`profiles`</SwmToken> section defines build profiles. In this case, the <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="35:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken> profile is defined, which includes a build configuration with the <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="40:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> plugin.

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
        </profile>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework-web/pom.xml" line="55">

---

The <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="55:2:2" line-data="    &lt;dependencies&gt;">`dependencies`</SwmToken> section lists all the dependencies required by the project. This includes various Spring and Broadleaf Commerce modules, as well as other libraries like <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="86:4:6" line-data="            &lt;groupId&gt;commons-collections&lt;/groupId&gt;">`commons-collections`</SwmToken>, <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="90:4:4" line-data="            &lt;groupId&gt;junit&lt;/groupId&gt;">`junit`</SwmToken>, and <SwmToken path="core/broadleaf-framework-web/pom.xml" pos="94:6:6" line-data="            &lt;groupId&gt;org.easymock&lt;/groupId&gt;">`easymock`</SwmToken>.

```xml
    <dependencies>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.social</groupId>
            <artifactId>spring-social-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-profile</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-profile-web</artifactId>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
