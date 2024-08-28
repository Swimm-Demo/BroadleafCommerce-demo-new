---
title: Maven Configuration in admin/pom.xml
---
# Intro

This document explains how Maven is used in the admin module of the Broadleaf Commerce project. It will cover the configuration steps in the <SwmPath>[admin/pom.xml](admin/pom.xml)</SwmPath> file.

<SwmSnippet path="/admin/pom.xml" line="1">

---

# Project Declaration

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file starts with the XML declaration and the project element, which defines the Maven POM model version.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/pom.xml" line="4">

---

The <SwmToken path="admin/pom.xml" pos="4:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> element specifies that this project inherits from the <SwmToken path="admin/pom.xml" pos="5:4:4" line-data="        &lt;artifactId&gt;broadleaf&lt;/artifactId&gt;">`broadleaf`</SwmToken> parent project, which is defined by the <SwmToken path="admin/pom.xml" pos="5:2:2" line-data="        &lt;artifactId&gt;broadleaf&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="admin/pom.xml" pos="6:2:2" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`groupId`</SwmToken>, and <SwmToken path="admin/pom.xml" pos="7:2:2" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`version`</SwmToken>.

```xml
    <parent>
        <artifactId>broadleaf</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/pom.xml" line="9">

---

The <SwmToken path="admin/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;admin&lt;/artifactId&gt;">`artifactId`</SwmToken> is set to <SwmToken path="admin/pom.xml" pos="9:4:4" line-data="    &lt;artifactId&gt;admin&lt;/artifactId&gt;">`admin`</SwmToken>, and the packaging type is <SwmToken path="admin/pom.xml" pos="10:4:4" line-data="    &lt;packaging&gt;pom&lt;/packaging&gt;">`pom`</SwmToken>. The <SwmToken path="admin/pom.xml" pos="11:2:2" line-data="    &lt;name&gt;BroadleafCommerce Admin&lt;/name&gt;">`name`</SwmToken> and <SwmToken path="admin/pom.xml" pos="12:2:2" line-data="    &lt;description&gt;BroadleafCommerce Admin Mid Level Project&lt;/description&gt;">`description`</SwmToken> provide metadata about the project.

```xml
    <artifactId>admin</artifactId>
    <packaging>pom</packaging>
    <name>BroadleafCommerce Admin</name>
    <description>BroadleafCommerce Admin Mid Level Project</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/pom.xml" line="14">

---

The <SwmToken path="admin/pom.xml" pos="14:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> section defines project-specific properties, such as <SwmToken path="admin/pom.xml" pos="15:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../&lt;/project.uri&gt;">`project.uri`</SwmToken>.

```xml
    <properties>
        <project.uri>${project.baseUri}/../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/admin/pom.xml" line="17">

---

The <SwmToken path="admin/pom.xml" pos="17:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> section specifies the licensing information for the project, including the name, URL, distribution method, and comments.

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

<SwmSnippet path="/admin/pom.xml" line="25">

---

The <SwmToken path="admin/pom.xml" pos="25:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> section lists the developers involved in the project, including their ID, email, organization, organization URL, and timezone.

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

<SwmSnippet path="/admin/pom.xml" line="34">

---

The <SwmToken path="admin/pom.xml" pos="34:2:2" line-data="    &lt;modules&gt;">`modules`</SwmToken> section lists the sub-modules included in the admin project, such as <SwmToken path="admin/pom.xml" pos="35:4:8" line-data="        &lt;module&gt;broadleaf-admin-module&lt;/module&gt;">`broadleaf-admin-module`</SwmToken>, <SwmToken path="admin/pom.xml" pos="36:4:10" line-data="        &lt;module&gt;broadleaf-open-admin-platform&lt;/module&gt;">`broadleaf-open-admin-platform`</SwmToken>, <SwmToken path="admin/pom.xml" pos="37:4:8" line-data="        &lt;module&gt;broadleaf-contentmanagement-module&lt;/module&gt;">`broadleaf-contentmanagement-module`</SwmToken>, and <SwmToken path="admin/pom.xml" pos="38:4:10" line-data="        &lt;module&gt;broadleaf-admin-functional-tests&lt;/module&gt;">`broadleaf-admin-functional-tests`</SwmToken>.

```xml
    <modules>
        <module>broadleaf-admin-module</module>
        <module>broadleaf-open-admin-platform</module>
        <module>broadleaf-contentmanagement-module</module>
        <module>broadleaf-admin-functional-tests</module>
    </modules>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
