---
title: Maven Configuration in core/broadleaf-framework
---
# Intro

This document explains how Maven is used in the <SwmPath>[core/broadleaf-framework/](core/broadleaf-framework/)</SwmPath> directory of the Broadleaf Commerce project. It will cover the configuration steps in the <SwmPath>[pom.xml](pom.xml)</SwmPath> file.

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="1">

---

# Project Declaration

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts with the XML declaration and the project element, which defines the project and its configuration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="3">

---

# Parent Project

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="3:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> element specifies that this project inherits from the <SwmToken path="core/broadleaf-framework/pom.xml" pos="4:4:4" line-data="        &lt;artifactId&gt;core&lt;/artifactId&gt;">`core`</SwmToken> project with the group ID <SwmToken path="core/broadleaf-framework/pom.xml" pos="5:4:6" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`org.broadleafcommerce`</SwmToken> and version <SwmToken path="core/broadleaf-framework/pom.xml" pos="6:4:10" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`6.2.12-SNAPSHOT`</SwmToken>.

```xml
    <parent>
        <artifactId>core</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="8">

---

# Project Metadata

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="8:2:2" line-data="    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;">`modelVersion`</SwmToken>, <SwmToken path="core/broadleaf-framework/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;broadleaf-framework&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/broadleaf-framework/pom.xml" pos="10:2:2" line-data="    &lt;name&gt;BroadleafCommerce Framework&lt;/name&gt;">`name`</SwmToken>, <SwmToken path="core/broadleaf-framework/pom.xml" pos="11:2:2" line-data="    &lt;description&gt;BroadleafCommerce Framework&lt;/description&gt;">`description`</SwmToken>, and <SwmToken path="core/broadleaf-framework/pom.xml" pos="12:2:2" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`url`</SwmToken> elements provide basic metadata about the project.

```xml
    <modelVersion>4.0.0</modelVersion>
    <artifactId>broadleaf-framework</artifactId>
    <name>BroadleafCommerce Framework</name>
    <description>BroadleafCommerce Framework</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="13">

---

# Properties

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="13:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> element defines custom properties used in the project, such as <SwmToken path="core/broadleaf-framework/pom.xml" pos="14:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="16">

---

# Licenses

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="16:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> element specifies the licensing information for the project, including the name, URL, distribution method, and comments.

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

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="23">

---

# Developers

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="24:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> element lists the developers involved in the project, including their ID, email, organization, organization URL, and timezone.

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

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="33">

---

# Build Plugins

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="33:2:2" line-data="    &lt;build&gt;">`build`</SwmToken> element contains the <SwmToken path="core/broadleaf-framework/pom.xml" pos="34:2:2" line-data="        &lt;plugins&gt;">`plugins`</SwmToken> element, which lists the Maven plugins used in the build process. For example, the <SwmToken path="core/broadleaf-framework/pom.xml" pos="37:4:8" line-data="                &lt;artifactId&gt;maven-jar-plugin&lt;/artifactId&gt;">`maven-jar-plugin`</SwmToken> is configured to create a test JAR.

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>test-jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="46">

---

# Additional Plugins

Another plugin used is the <SwmToken path="core/broadleaf-framework/pom.xml" pos="48:4:6" line-data="                &lt;artifactId&gt;gmavenplus-plugin&lt;/artifactId&gt;">`gmavenplus-plugin`</SwmToken>, which is configured without additional execution goals.

```xml
            <plugin>
                <groupId>org.codehaus.gmavenplus</groupId>
                <artifactId>gmavenplus-plugin</artifactId>
            </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="52">

---

# Profiles

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="52:2:2" line-data="    &lt;profiles&gt;">`profiles`</SwmToken> element defines build profiles, such as <SwmToken path="core/broadleaf-framework/pom.xml" pos="54:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken>, which includes the <SwmToken path="core/broadleaf-framework/pom.xml" pos="59:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> for generating rebel.xml during the <SwmToken path="core/broadleaf-framework/pom.xml" pos="63:4:6" line-data="                                &lt;phase&gt;process-resources&lt;/phase&gt;">`process-resources`</SwmToken> phase.

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

<SwmSnippet path="/core/broadleaf-framework/pom.xml" line="75">

---

# Dependencies

The <SwmToken path="core/broadleaf-framework/pom.xml" pos="75:2:2" line-data="    &lt;dependencies&gt;">`dependencies`</SwmToken> element lists all the dependencies required by the project. This includes various libraries such as <SwmToken path="core/broadleaf-framework/pom.xml" pos="78:4:6" line-data="            &lt;artifactId&gt;solr-solrj&lt;/artifactId&gt;">`solr-solrj`</SwmToken>, <SwmToken path="core/broadleaf-framework/pom.xml" pos="83:4:8" line-data="            &lt;artifactId&gt;jackson-dataformat-smile&lt;/artifactId&gt;">`jackson-dataformat-smile`</SwmToken>, <SwmToken path="core/broadleaf-framework/pom.xml" pos="87:4:4" line-data="            &lt;artifactId&gt;mvel2&lt;/artifactId&gt;">`mvel2`</SwmToken>, and several Broadleaf Commerce modules like <SwmToken path="core/broadleaf-framework/pom.xml" pos="91:4:6" line-data="            &lt;artifactId&gt;broadleaf-common&lt;/artifactId&gt;">`broadleaf-common`</SwmToken> and <SwmToken path="core/broadleaf-framework/pom.xml" pos="101:4:6" line-data="            &lt;artifactId&gt;broadleaf-profile&lt;/artifactId&gt;">`broadleaf-profile`</SwmToken>.

```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.solr</groupId>
            <artifactId>solr-solrj</artifactId>
        </dependency>
        <!-- Solr still needs this dependency, we'll just use the later version -->
        <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-smile</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mvel</groupId>
            <artifactId>mvel2</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-common</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-common</artifactId>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
