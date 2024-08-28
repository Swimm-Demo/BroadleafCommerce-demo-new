---
title: Maven Configuration in admin/broadleaf-admin-module
---
# Intro

This document explains how Maven is used in the <SwmPath>[admin/broadleaf-admin-module/](admin/broadleaf-admin-module/)</SwmPath> directory. It will go through the <SwmPath>[pom.xml](pom.xml)</SwmPath> configuration file step by step.

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="1">

---

# Project Definition

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts by defining the XML version and the project model version. The project is defined using the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="2:1:1" line-data="&lt;project xmlns=&quot;http://maven.apache.org/POM/4.0.0&quot; xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xsi:schemaLocation=&quot;http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd&quot;&gt;">`project`</SwmToken> tag with the appropriate namespaces.

```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="4">

---

# Parent Project

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="4:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> tag specifies that this module inherits from the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="5:4:4" line-data="        &lt;artifactId&gt;admin&lt;/artifactId&gt;">`admin`</SwmToken> project with the group ID <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="6:4:6" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`org.broadleafcommerce`</SwmToken> and version <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="7:4:10" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`6.2.12-SNAPSHOT`</SwmToken>.

```xml
    <parent>
        <artifactId>admin</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="9">

---

# Artifact and Packaging

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;broadleaf-admin-module&lt;/artifactId&gt;">`artifactId`</SwmToken> is set to <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="9:4:8" line-data="    &lt;artifactId&gt;broadleaf-admin-module&lt;/artifactId&gt;">`broadleaf-admin-module`</SwmToken>, and the packaging type is defined as <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="10:4:4" line-data="    &lt;packaging&gt;jar&lt;/packaging&gt;">`jar`</SwmToken>.

```xml
    <artifactId>broadleaf-admin-module</artifactId>
    <packaging>jar</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="11">

---

# Project Metadata

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="11:2:2" line-data="    &lt;name&gt;BroadleafCommerce Admin Module&lt;/name&gt;">`name`</SwmToken>, <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="12:2:2" line-data="    &lt;description&gt;BroadleafCommerce Admin Module&lt;/description&gt;">`description`</SwmToken>, and <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="13:2:2" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`url`</SwmToken> tags provide metadata about the project, including its name, description, and URL.

```xml
    <name>BroadleafCommerce Admin Module</name>
    <description>BroadleafCommerce Admin Module</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="14">

---

# Properties

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="14:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> tag defines project-specific properties, such as <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="15:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="17">

---

# Licenses

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="17:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> tag specifies the licensing information for the project, including the license name, URL, distribution method, and comments.

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

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="25">

---

# Developers

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="25:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> tag lists the developers involved in the project, including their ID, email, organization, organization URL, and timezone.

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

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="34">

---

# Build Resources

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="34:2:2" line-data="    &lt;build&gt;">`build`</SwmToken> tag contains the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="35:2:2" line-data="        &lt;resources&gt;">`resources`</SwmToken> tag, which specifies the directories and filtering options for the project's resources. It includes multiple <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="36:2:2" line-data="            &lt;resource&gt;">`resource`</SwmToken> tags for different directories and filtering settings.

```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/resources/admin_style</directory>
                <filtering>false</filtering>
                <targetPath>admin_style</targetPath>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
                <excludes>
                    <exclude>open_admin_style/**</exclude>
                </excludes>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <excludes>
                    <exclude>**/*.java</exclude>
                </excludes>
            </resource>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="55">

---

# Build Plugins

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="55:2:2" line-data="        &lt;plugins&gt;">`plugins`</SwmToken> tag within the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="34:2:2" line-data="    &lt;build&gt;">`build`</SwmToken> section specifies the Maven plugins used in the project. Here, the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="58:4:8" line-data="                &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;">`maven-compiler-plugin`</SwmToken> is configured to use Java 8 for both the source and target.

```xml
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="66">

---

# Profiles

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="66:2:2" line-data="    &lt;profiles&gt;">`profiles`</SwmToken> tag defines build profiles for the project. The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="68:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken> profile includes the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="73:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> for generating Rebel XML during the <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="77:4:6" line-data="                                &lt;phase&gt;process-resources&lt;/phase&gt;">`process-resources`</SwmToken> phase.

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

<SwmSnippet path="/admin/broadleaf-admin-module/pom.xml" line="89">

---

# Dependencies

The <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="89:2:2" line-data="    &lt;dependencies&gt;">`dependencies`</SwmToken> tag lists the project's dependencies, including <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="92:4:6" line-data="            &lt;artifactId&gt;broadleaf-framework&lt;/artifactId&gt;">`broadleaf-framework`</SwmToken>, <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="96:4:10" line-data="            &lt;artifactId&gt;broadleaf-open-admin-platform&lt;/artifactId&gt;">`broadleaf-open-admin-platform`</SwmToken>, <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="99:4:4" line-data="            &lt;groupId&gt;junit&lt;/groupId&gt;">`junit`</SwmToken>, <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="104:4:6" line-data="            &lt;artifactId&gt;commons-lang3&lt;/artifactId&gt;">`commons-lang3`</SwmToken>, and <SwmToken path="admin/broadleaf-admin-module/pom.xml" pos="108:4:8" line-data="            &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;">`javax.servlet-api`</SwmToken>.

```xml
    <dependencies>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-framework</artifactId>
        </dependency>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-open-admin-platform</artifactId>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </dependency>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
