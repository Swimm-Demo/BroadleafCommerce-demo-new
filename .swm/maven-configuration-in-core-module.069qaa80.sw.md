---
title: Maven Configuration in Core Module
---
# Intro

This document explains how Maven is used in the core module of the <SwmToken path="core/pom.xml" pos="6:6:6" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`broadleafcommerce`</SwmToken> project. It will go through the configuration steps in the <SwmPath>[core/pom.xml](core/pom.xml)</SwmPath> file.

<SwmSnippet path="/core/pom.xml" line="1">

---

# Project Definition

The <SwmPath>[pom.xml](pom.xml)</SwmPath> file begins with the XML declaration and the project definition, specifying the POM model version.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="4">

---

# Parent Project

The <SwmToken path="core/pom.xml" pos="4:2:2" line-data="    &lt;parent&gt;">`parent`</SwmToken> section defines the parent project from which this project inherits. It specifies the <SwmToken path="core/pom.xml" pos="5:2:2" line-data="        &lt;artifactId&gt;broadleaf&lt;/artifactId&gt;">`artifactId`</SwmToken>, <SwmToken path="core/pom.xml" pos="6:2:2" line-data="        &lt;groupId&gt;org.broadleafcommerce&lt;/groupId&gt;">`groupId`</SwmToken>, and <SwmToken path="core/pom.xml" pos="7:2:2" line-data="        &lt;version&gt;6.2.12-SNAPSHOT&lt;/version&gt;">`version`</SwmToken> of the parent project.

```xml
    <parent>
        <artifactId>broadleaf</artifactId>
        <groupId>org.broadleafcommerce</groupId>
        <version>6.2.12-SNAPSHOT</version>
    </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="9">

---

# Artifact and Packaging

The <SwmToken path="core/pom.xml" pos="9:2:2" line-data="    &lt;artifactId&gt;core&lt;/artifactId&gt;">`artifactId`</SwmToken> and <SwmToken path="core/pom.xml" pos="10:2:2" line-data="    &lt;packaging&gt;pom&lt;/packaging&gt;">`packaging`</SwmToken> elements define the unique identifier for this project and the packaging type, which is <SwmToken path="core/pom.xml" pos="10:4:4" line-data="    &lt;packaging&gt;pom&lt;/packaging&gt;">`pom`</SwmToken> in this case.

```xml
    <artifactId>core</artifactId>
    <packaging>pom</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="11">

---

# Project Metadata

The <SwmToken path="core/pom.xml" pos="11:2:2" line-data="    &lt;name&gt;BroadleafCommerce Core&lt;/name&gt;">`name`</SwmToken>, <SwmToken path="core/pom.xml" pos="12:2:2" line-data="    &lt;description&gt;BroadleafCommerce Core Mid Level Project&lt;/description&gt;">`description`</SwmToken>, and <SwmToken path="core/pom.xml" pos="13:2:2" line-data="    &lt;url&gt;https://www.broadleafcommerce.com&lt;/url&gt;">`url`</SwmToken> elements provide metadata about the project, including its name, a brief description, and the project's website URL.

```xml
    <name>BroadleafCommerce Core</name>
    <description>BroadleafCommerce Core Mid Level Project</description>
    <url>https://www.broadleafcommerce.com</url>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="14">

---

# Properties

The <SwmToken path="core/pom.xml" pos="14:2:2" line-data="    &lt;properties&gt;">`properties`</SwmToken> section defines custom properties used within the POM file. Here, it defines the <SwmToken path="core/pom.xml" pos="15:2:4" line-data="        &lt;project.uri&gt;${project.baseUri}/../&lt;/project.uri&gt;">`project.uri`</SwmToken> property.

```xml
    <properties>
        <project.uri>${project.baseUri}/../</project.uri>
    </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="17">

---

# Licenses

The <SwmToken path="core/pom.xml" pos="17:2:2" line-data="    &lt;licenses&gt;">`licenses`</SwmToken> section specifies the licensing information for the project. It includes the license name, URL, distribution method, and comments.

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

<SwmSnippet path="/core/pom.xml" line="25">

---

# Developers

The <SwmToken path="core/pom.xml" pos="25:2:2" line-data="    &lt;developers&gt;">`developers`</SwmToken> section lists the developers involved in the project. It includes details such as the developer's ID, email, organization, organization URL, and timezone.

```xml
    <developers>
        <developer>
            <id>architect</id>
            <email>architect@broadleafcommerce.org</email>
            <organization>Broadleaf Commerce</organization>
            <organizationUrl>https://www.broadleafcommerce.com</organizationUrl>
            <timezone>-6</timezone>
        </developer>
```

---

</SwmSnippet>

<SwmSnippet path="/core/pom.xml" line="34">

---

# Modules

The <SwmToken path="core/pom.xml" pos="34:2:2" line-data="    &lt;modules&gt;">`modules`</SwmToken> section lists the sub-modules that are part of this project. These modules are built as part of the core project.

```xml
    <modules>
        <module>broadleaf-profile</module>
        <module>broadleaf-profile-web</module>
        <module>broadleaf-framework</module>
        <module>broadleaf-framework-web</module>
  </modules>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
