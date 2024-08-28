---
title: Maven Configuration in core/broadleaf-profile
---
# Intro

This document explains how Maven is used in the <SwmPath>[core/broadleaf-profile/](core/broadleaf-profile/)</SwmPath> directory. It will cover the configuration steps in the <SwmPath>[pom.xml](pom.xml)</SwmPath> file.

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="1">

---

# Project Declaration

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts with the XML declaration, specifying the version and encoding.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="2">

---

The root element `<project>` defines the project and its configuration.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="3">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="3:1:3" line-data="    &lt;parent&gt;">`<parent>`</SwmToken> element specifies the parent project from which this project inherits. It includes the <SwmToken path="core/broadleaf-profile/pom.xml" pos="4:2:2" line-data="        &lt;artifactId&gt;core&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="5:2:2" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`groupId`</SwmToken>, and <SwmToken path="core/broadleaf-profile/pom.xml" pos="6:2:2" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`version`</SwmToken> of the parent.

```xml
    <parent>
        <artifactId>core</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="8">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="8:1:3" line-data="    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;">`<modelVersion>`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="9:1:3" line-data="    &lt;artifactId&gt;broadleaf-profile&lt;/artifactId&gt;">`<artifactId>`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="10:1:3" line-data="    &lt;name&gt;BroadleafCommerce Profile&lt;/name&gt;">`<name>`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="11:1:3" line-data="    &lt;description&gt;BroadleafCommerce Profile&lt;/description&gt;">`<description>`</SwmToken>, and <SwmToken path="core/broadleaf-profile/pom.xml" pos="12:1:3" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`<url>`</SwmToken> elements provide basic metadata about the project.

```xml
    <modelVersion>4.0.0</modelVersion>
    <artifactId>broadleaf-profile</artifactId>
    <name>BroadleafCommerce Profile</name>
    <description>BroadleafCommerce Profile</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="13">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="13:1:3" line-data="    &lt;properties&gt;">`<properties>`</SwmToken> element defines project-specific properties, such as <SwmToken path="core/broadleaf-profile/pom.xml" pos="14:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="16">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="16:1:3" line-data="    &lt;licenses&gt;">`<licenses>`</SwmToken> element specifies the licensing information for the project, including the license name, URL, distribution method, and comments.

```xml
    <licenses>
        <license>
            <name>Broadleaf Fair Use 1.0</name>
            <url>http://license.broadleafcommerce.org/fair_use_license-1.0.txt</url>
            <distribution>repo</distribution>
            <comments>Fair Use Community License</comments>
        </license>
    </licenses>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="24">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="24:1:3" line-data="    &lt;developers&gt;">`<developers>`</SwmToken> element lists the developers involved in the project, including their ID, email, organization, organization URL, and timezone.

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

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="33">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="33:1:3" line-data="    &lt;profiles&gt;">`<profiles>`</SwmToken> element defines build profiles. In this case, the <SwmToken path="core/broadleaf-profile/pom.xml" pos="35:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken> profile is defined, which includes a build configuration with the <SwmToken path="core/broadleaf-profile/pom.xml" pos="40:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> plugin.

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

<SwmSnippet path="/core/broadleaf-profile/pom.xml" line="56">

---

The <SwmToken path="core/broadleaf-profile/pom.xml" pos="56:1:3" line-data="    &lt;dependencies&gt;">`<dependencies>`</SwmToken> element lists the project's dependencies, including <SwmToken path="core/broadleaf-profile/pom.xml" pos="59:4:6" line-data="            &lt;artifactId&gt;broadleaf-common&lt;/artifactId&gt;">`broadleaf-common`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="62:4:6" line-data="            &lt;groupId&gt;commons-validator&lt;/groupId&gt;">`commons-validator`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="66:4:4" line-data="            &lt;groupId&gt;junit&lt;/groupId&gt;">`junit`</SwmToken>, <SwmToken path="core/broadleaf-profile/pom.xml" pos="70:6:6" line-data="            &lt;groupId&gt;org.easymock&lt;/groupId&gt;">`easymock`</SwmToken>, and <SwmToken path="core/broadleaf-profile/pom.xml" pos="75:4:4" line-data="            &lt;artifactId&gt;easymockclassextension&lt;/artifactId&gt;">`easymockclassextension`</SwmToken>.

```xml
    <dependencies>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-common</artifactId>
        </dependency>
        <dependency>
            <groupId>commons-validator</groupId>
            <artifactId>commons-validator</artifactId>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymock</artifactId>
        </dependency>
        <dependency>
            <groupId>org.easymock</groupId>
            <artifactId>easymockclassextension</artifactId>
        </dependency>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
