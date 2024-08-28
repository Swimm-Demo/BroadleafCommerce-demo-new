---
title: Building the Admin Platform with Maven
---
# Intro

This document explains how Maven is used in the <SwmPath>[admin/broadleaf-open-admin-platform/](admin/broadleaf-open-admin-platform/)</SwmPath> directory. It will cover the configuration steps in the <SwmPath>[pom.xml](pom.xml)</SwmPath> file.

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="1">

---

# Project Definition

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file begins by defining the XML schema and model version for the Maven project.

```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="4">

---

The project inherits from a parent POM with the artifact ID <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="5:4:4" line-data="        &lt;artifactId&gt;admin&lt;/artifactId&gt;">`admin`</SwmToken>, group ID <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="6:4:6" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`org.broadleafcommerce`</SwmToken>, and version <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="7:4:10" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`6.2.12-SNAPSHOT`</SwmToken>.

```xml
    <parent>
        <artifactId>admin</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="9">

---

The artifact ID for this project is <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="9:4:10" line-data="    &lt;artifactId&gt;broadleaf-open-admin-platform&lt;/artifactId&gt;">`broadleaf-open-admin-platform`</SwmToken>, and it is packaged as a JAR file. The project name and description are also provided.

```xml
    <artifactId>broadleaf-open-admin-platform</artifactId>
    <packaging>jar</packaging>
    <name>BroadleafCommerce Open Admin Platform</name>
    <description>BroadleafCommerce Open Admin Platform</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="14">

---

Project properties are defined, including the <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="15:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../../&lt;/project.uri&gt;">`project.uri`</SwmToken> property.

```xml
    <properties>
        <project.uri>${project.baseUri}/../../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="17">

---

License information is specified, including the name, URL, distribution method, and comments about the license.

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

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="25">

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

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="34">

---

# Build Configuration

The build section defines the plugins and resources used in the build process.

```xml
    <build>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="35">

---

The <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="38:4:10" line-data="                &lt;artifactId&gt;build-helper-maven-plugin&lt;/artifactId&gt;">`build-helper-maven-plugin`</SwmToken> is configured to generate a timestamp property during the <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="42:4:6" line-data="                        &lt;phase&gt;generate-sources&lt;/phase&gt;">`generate-sources`</SwmToken> phase.

```xml
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>build-helper-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <id>timestamp-property</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>timestamp-property</goal>
                        </goals>
                        <configuration>
                            <name>openAdminBuildDate</name>
                            <pattern>yyyy-MM-dd HH:mm:ss</pattern>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="53">

---

The <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="55:4:8" line-data="                &lt;artifactId&gt;maven-jar-plugin&lt;/artifactId&gt;">`maven-jar-plugin`</SwmToken> is configured to create a test JAR during the build process.

```xml
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

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="64">

---

The <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="66:4:6" line-data="                &lt;artifactId&gt;gmavenplus-plugin&lt;/artifactId&gt;">`gmavenplus-plugin`</SwmToken> is included in the build plugins.

```xml
            <plugin>
                <groupId>org.codehaus.gmavenplus</groupId>
                <artifactId>gmavenplus-plugin</artifactId>
            </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="69">

---

Resource directories are specified, including <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/)</SwmPath>, <SwmPath>[admin/broadleaf-admin-functional-tests/src/main/resources/](admin/broadleaf-admin-functional-tests/src/main/resources/)</SwmPath>, and <SwmPath>[admin/broadleaf-admin-module/src/main/java/](admin/broadleaf-admin-module/src/main/java/)</SwmPath>. Filtering and exclusion rules are also defined.

```xml
        <resources>
            <resource>
                <directory>src/main/resources/open_admin_style</directory>
                <filtering>false</filtering>
                <targetPath>open_admin_style</targetPath>
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

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="89">

---

Plugin management is configured, including settings for the <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="95:4:6" line-data="                    &lt;artifactId&gt;lifecycle-mapping&lt;/artifactId&gt;">`lifecycle-mapping`</SwmToken> plugin used by Eclipse <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="92:1:1" line-data="                    m2e settings only. It has no influence on the Maven build itself. --&gt;">`m2e`</SwmToken>.

```xml
        <pluginManagement>
            <plugins>
                <!--This plugin's configuration is used to store Eclipse
                    m2e settings only. It has no influence on the Maven build itself. -->
                <plugin>
                    <groupId>org.eclipse.m2e</groupId>
                    <artifactId>lifecycle-mapping</artifactId>
                    <version>1.0.0</version>
                    <configuration>
                        <lifecycleMappingMetadata>
                            <pluginExecutions>
                                <pluginExecution>
                                    <pluginExecutionFilter>
                                        <groupId>
                                            org.codehaus.mojo
                                        </groupId>
                                        <artifactId>
                                            build-helper-maven-plugin
                                        </artifactId>
                                        <versionRange>
                                            [1.7,)
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="128">

---

# Profiles

A profile named <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="130:4:6" line-data="            &lt;id&gt;blc-development&lt;/id&gt;">`blc-development`</SwmToken> is defined, which includes the <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="135:4:8" line-data="                        &lt;artifactId&gt;jrebel-maven-plugin&lt;/artifactId&gt;">`jrebel-maven-plugin`</SwmToken> for generating rebel.xml files during the <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="139:4:6" line-data="                                &lt;phase&gt;process-resources&lt;/phase&gt;">`process-resources`</SwmToken> phase.

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

<SwmSnippet path="/admin/broadleaf-open-admin-platform/pom.xml" line="150">

---

# Dependencies

Dependencies are listed, including <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="153:4:6" line-data="            &lt;artifactId&gt;broadleaf-common&lt;/artifactId&gt;">`broadleaf-common`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="156:4:4" line-data="            &lt;groupId&gt;junit&lt;/groupId&gt;">`junit`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="160:4:6" line-data="            &lt;groupId&gt;commons-pool&lt;/groupId&gt;">`commons-pool`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="164:4:6" line-data="            &lt;groupId&gt;commons-fileupload&lt;/groupId&gt;">`commons-fileupload`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="169:4:8" line-data="            &lt;artifactId&gt;javax.servlet-api&lt;/artifactId&gt;">`javax.servlet-api`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="173:4:6" line-data="            &lt;artifactId&gt;validation-api&lt;/artifactId&gt;">`validation-api`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="177:4:6" line-data="            &lt;artifactId&gt;imageio-jpeg&lt;/artifactId&gt;">`imageio-jpeg`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="181:4:4" line-data="            &lt;artifactId&gt;pngtastic&lt;/artifactId&gt;">`pngtastic`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="186:4:8" line-data="            &lt;artifactId&gt;spring-security-config&lt;/artifactId&gt;">`spring-security-config`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="190:4:6" line-data="            &lt;artifactId&gt;groovy-all&lt;/artifactId&gt;">`groovy-all`</SwmToken>, <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="153:4:6" line-data="            &lt;artifactId&gt;broadleaf-common&lt;/artifactId&gt;">`broadleaf-common`</SwmToken> (tests), and <SwmToken path="admin/broadleaf-open-admin-platform/pom.xml" pos="201:4:6" line-data="            &lt;artifactId&gt;spock-core&lt;/artifactId&gt;">`spock-core`</SwmToken>.

```xml
    <dependencies>
        <dependency>
            <groupId>org.broadleafcommerce</groupId>
            <artifactId>broadleaf-common</artifactId>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </dependency>
        <dependency>
            <groupId>commons-pool</groupId>
            <artifactId>commons-pool</artifactId>
        </dependency>
        <dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
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
