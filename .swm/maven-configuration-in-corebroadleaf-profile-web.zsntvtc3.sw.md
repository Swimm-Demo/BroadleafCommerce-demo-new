---
title: Maven Configuration in core/broadleaf-profile-web
---
# Intro

This document explains how Maven is used in the <SwmPath>[core/broadleaf-profile-web/](core/broadleaf-profile-web/)</SwmPath> directory. It will detail the configuration steps in the <SwmPath>[pom.xml](pom.xml)</SwmPath> file.

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="1">

---

# Project Declaration

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts with the XML declaration and the project element, which defines the project and its configuration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="3">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="3:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> element specifies that this project inherits from the <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="5:4:4" line-data="        &lt;artifactId&gt;core&lt;/artifactId&gt;">`core`</SwmToken> project with group ID <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="4:4:6" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`org.broadleafcommerce`</SwmToken> and version <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="6:4:10" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`6.2.12-SNAPSHOT`</SwmToken>.

```xml
    <parent>
        <groupId>org.broadleafcommerce</groupId>
        <artifactId>core</artifactId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="8">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="8:2:2" line-data="    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;">`modelVersion`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;broadleaf-profile-web&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="10:2:2" line-data="    &lt;name&gt;BroadleafCommerce Profile Web&lt;/name&gt;">`name`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="11:2:2" line-data="    &lt;description&gt;BroadleafCommerce Profile Web&lt;/description&gt;">`description`</SwmToken>, and <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="12:2:2" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`url`</SwmToken> elements provide basic metadata about the project.

```xml
    <modelVersion>4.0.0</modelVersion>
    <artifactId>broadleaf-profile-web</artifactId>
    <name>BroadleafCommerce Profile Web</name>
    <description>BroadleafCommerce Profile Web</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="13">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="13:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> element defines project-specific properties, such as <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="14:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="16">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="16:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> element specifies the licensing information for the project, including the name, URL, distribution method, and comments.

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

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="24">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="24:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> element lists the developers involved in the project, including their ID, email, organization, organization URL, and timezone.

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

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="33">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="33:2:2" line-data="    &lt;profiles&gt;">`profiles`</SwmToken> element defines a build profile named <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="35:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken>. This profile includes a build configuration with a plugin for <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="40:4:4" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel`</SwmToken>, which is used to generate rebel.xml during the <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="44:4:6" line-data="                                &lt;phase&gt;process-resources&lt;/phase&gt;">`process-resources`</SwmToken> phase.

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

<SwmSnippet path="/core/broadleaf-profile-web/pom.xml" line="55">

---

The <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="55:2:2" line-data="    &lt;dependencies&gt;">`dependencies`</SwmToken> element lists the project's dependencies, including <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="58:4:8" line-data="            &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;">`javax.servlet-api`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="62:4:6" line-data="            &lt;artifactId&gt;broadleaf-profile&lt;/artifactId&gt;">`broadleaf-profile`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="66:4:6" line-data="            &lt;artifactId&gt;spring-webmvc&lt;/artifactId&gt;">`spring-webmvc`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="70:4:8" line-data="            &lt;artifactId&gt;spring-security-acl&lt;/artifactId&gt;">`spring-security-acl`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="74:4:8" line-data="            &lt;artifactId&gt;spring-security-taglibs&lt;/artifactId&gt;">`spring-security-taglibs`</SwmToken>, <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="78:4:8" line-data="            &lt;artifactId&gt;spring-security-config&lt;/artifactId&gt;">`spring-security-config`</SwmToken>, and <SwmToken path="core/broadleaf-profile-web/pom.xml" pos="82:4:6" line-data="            &lt;artifactId&gt;spring-oxm&lt;/artifactId&gt;">`spring-oxm`</SwmToken>.

```xml
    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-profile</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-acl</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-taglibs</artifactId>
        </dependency>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
