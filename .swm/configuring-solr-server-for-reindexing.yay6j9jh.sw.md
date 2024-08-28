---
title: Configuring Solr Server for Reindexing
---
In this document, we will explain the process of determining and configuring the Solr server for reindexing. The process involves checking the system's configuration, setting up the Solr client for a specific site, and ensuring the necessary Solr infrastructure is in place.

The flow starts by checking if the system is in site collections mode and Solr Cloud mode. If it is, it configures the Solr client for the specific site by retrieving the site context and connecting the Solr client. It then ensures that the necessary collection and alias exist for the site. If the system is not in site collections mode, it returns either the primary server or the reindex server based on whether the system is in single-core mode.

# Flow drill down

```mermaid
graph TD;
      8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle --> bc7df526d2e7b829068cc7d926c303198303639bb77bff8e1ec0b15c323ccf53(getSiteReindexServer):::mainFlowStyle

bc7df526d2e7b829068cc7d926c303198303639bb77bff8e1ec0b15c323ccf53(getSiteReindexServer):::mainFlowStyle --> 90256325d77e14722066cb207c13c15aa18b25d0a6c4ca4a2c3aee23a20db56a(createAliasIfNotExist)

bc7df526d2e7b829068cc7d926c303198303639bb77bff8e1ec0b15c323ccf53(getSiteReindexServer):::mainFlowStyle --> 65e075b09dc59554382de4aed4f0475789f314d3334babafc61cb89674461787(createCollectionIfNotExist):::mainFlowStyle

65e075b09dc59554382de4aed4f0475789f314d3334babafc61cb89674461787(createCollectionIfNotExist):::mainFlowStyle --> 07be8e3b39afc6486443b9326f143450c408a0f131286ec025238f936252b298(refineException):::mainFlowStyle

07be8e3b39afc6486443b9326f143450c408a0f131286ec025238f936252b298(refineException):::mainFlowStyle --> 0ec01205c95856bf4ee8999c8ab37c04f4a9a00c5d0c9a5f5afe0b01d0918396(wrapException):::mainFlowStyle


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" line="274">

---

## <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="273:5:5" line-data="    public SolrClient getReindexServer() {">`getReindexServer`</SwmToken>

The <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="273:5:5" line-data="    public SolrClient getReindexServer() {">`getReindexServer`</SwmToken> method determines which Solr server to use for reindexing based on the current configuration. If the system is in site collections mode and Solr Cloud mode, it delegates to <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="275:3:3" line-data="            return getSiteReindexServer();">`getSiteReindexServer`</SwmToken>. Otherwise, it returns either the primary server or the reindex server depending on whether the system is in single-core mode.

```java
        if (isSiteCollections() && isSolrCloudMode()) {
            return getSiteReindexServer();
        }
        
        return isSingleCoreMode() ? primaryServer : reindexServer;
    }
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" line="611">

---

## <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="611:5:5" line-data="    public SolrClient getSiteReindexServer() {">`getSiteReindexServer`</SwmToken>

The <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="611:5:5" line-data="    public SolrClient getSiteReindexServer() {">`getSiteReindexServer`</SwmToken> method configures the Solr client for a specific site. It retrieves the current site context, connects the Solr client, and ensures that the necessary collection and alias exist for the site. This involves calling <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="622:1:1" line-data="            createCollectionIfNotExist(client, collectionName);">`createCollectionIfNotExist`</SwmToken> and <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="623:1:1" line-data="            createAliasIfNotExist(client, collectionName, collectionName);">`createAliasIfNotExist`</SwmToken> to set up the Solr infrastructure for the site's reindexing process.

```java
    public SolrClient getSiteReindexServer() {
        BroadleafRequestContext ctx = BroadleafRequestContext.getBroadleafRequestContext();
        Site site = ctx.getNonPersistentSite();

        CloudSolrClient client = (CloudSolrClient) primaryServer;
        client.connect();
        
        String aliasName = getSiteReindexAliasName(site);
        if (aliasName != null) {
            String collectionName = getSiteReindexCollectionName(site);

            createCollectionIfNotExist(client, collectionName);
            createAliasIfNotExist(client, collectionName, collectionName);
        }

        return client;
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" line="642">

---

### <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="642:5:5" line-data="    protected void createAliasIfNotExist(CloudSolrClient client, String collectionName, String aliasName) {">`createAliasIfNotExist`</SwmToken>

The <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="642:5:5" line-data="    protected void createAliasIfNotExist(CloudSolrClient client, String collectionName, String aliasName) {">`createAliasIfNotExist`</SwmToken> method checks if an alias for a Solr collection exists. If not, it creates the alias using Solr's <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="647:1:1" line-data="                CollectionAdminRequest.createAlias(aliasName, collectionName).process(client);">`CollectionAdminRequest`</SwmToken>. This ensures that the alias points to the correct collection, facilitating easier management of Solr collections.

```java
    protected void createAliasIfNotExist(CloudSolrClient client, String collectionName, String aliasName) {
        Aliases aliases = client.getZkStateReader().getAliases();
        Map<String, String> aliasCollectionMap = aliases.getCollectionAliasMap();
        if (!aliasCollectionMap.containsKey(aliasName)) {
            try {
                CollectionAdminRequest.createAlias(aliasName, collectionName).process(client);
            } catch (SolrServerException e) {
                throw ExceptionHelper.refineException(e);
            } catch (IOException e) {
                throw ExceptionHelper.refineException(e);
            }
        }
    }
```

---

</SwmSnippet>

<SwmSnippet path="/core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" line="629">

---

### <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="629:5:5" line-data="    protected void createCollectionIfNotExist(CloudSolrClient client, String collectionName) {">`createCollectionIfNotExist`</SwmToken>

The <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="629:5:5" line-data="    protected void createCollectionIfNotExist(CloudSolrClient client, String collectionName) {">`createCollectionIfNotExist`</SwmToken> method ensures that a Solr collection exists for the site. If the collection does not exist, it creates it using Solr's <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="632:1:1" line-data="                CollectionAdminRequest.createCollection(collectionName, getSolrCloudConfigName(), getSolrCloudNumShards(), getSolrCloudNumReplicas())">`CollectionAdminRequest`</SwmToken>. This is crucial for setting up the necessary infrastructure for site-specific indexing.

```java
    protected void createCollectionIfNotExist(CloudSolrClient client, String collectionName) {
        if (!client.getZkStateReader().getClusterState().hasCollection(collectionName)) {
            try {
                CollectionAdminRequest.createCollection(collectionName, getSolrCloudConfigName(), getSolrCloudNumShards(), getSolrCloudNumReplicas())
                        .setMaxShardsPerNode(getSolrCloudNumShards()).process(client);
            } catch (SolrServerException e) {
                throw ExceptionHelper.refineException(e);
            } catch (IOException e) {
                throw ExceptionHelper.refineException(e);
            }
        }
    }
```

---

</SwmSnippet>

<SwmSnippet path="/common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" line="34">

---

### <SwmToken path="common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" pos="34:22:22" line-data="    public static &lt;G extends Throwable, J extends RuntimeException&gt; RuntimeException refineException(Class&lt;G&gt; refineType, Class&lt;J&gt; wrapType, String message, Throwable e) {">`refineException`</SwmToken>

The <SwmToken path="common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" pos="34:22:22" line-data="    public static &lt;G extends Throwable, J extends RuntimeException&gt; RuntimeException refineException(Class&lt;G&gt; refineType, Class&lt;J&gt; wrapType, String message, Throwable e) {">`refineException`</SwmToken> method refines exceptions by checking their type and wrapping them in a more appropriate runtime exception. This helps in providing more meaningful error messages and handling specific exception types more gracefully.

```java
    public static <G extends Throwable, J extends RuntimeException> RuntimeException refineException(Class<G> refineType, Class<J> wrapType, String message, Throwable e) {
        if (refineType.isAssignableFrom(e.getClass())) {
            return wrapException(e, wrapType, message);
        }
        if (e.getCause() != null) {
            return refineException(refineType, wrapType, message, e.getCause());
        }
        if (e instanceof UndeclaredThrowableException) {
            return refineException(refineType, wrapType, message, ((UndeclaredThrowableException) e).getUndeclaredThrowable());
        }
        if (e instanceof InvocationTargetException) {
            return refineException(refineType, wrapType, message, ((InvocationTargetException) e).getTargetException());
        }
        return wrapException(e, wrapType, message);
    }
```

---

</SwmSnippet>

<SwmSnippet path="/common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" line="90">

---

### <SwmToken path="common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" pos="90:15:15" line-data="    private static &lt;J extends RuntimeException&gt; RuntimeException wrapException(Throwable e, Class&lt;J&gt; wrapType, String message) {">`wrapException`</SwmToken>

The <SwmToken path="common/src/main/java/org/broadleafcommerce/common/exception/ExceptionHelper.java" pos="90:15:15" line-data="    private static &lt;J extends RuntimeException&gt; RuntimeException wrapException(Throwable e, Class&lt;J&gt; wrapType, String message) {">`wrapException`</SwmToken> method wraps a given exception in a specified runtime exception type. This is used by <SwmToken path="core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/SolrConfiguration.java" pos="635:5:5" line-data="                throw ExceptionHelper.refineException(e);">`refineException`</SwmToken> to ensure that exceptions are consistently wrapped and logged, providing better error handling and debugging capabilities.

```java
    private static <J extends RuntimeException> RuntimeException wrapException(Throwable e, Class<J> wrapType, String message) {
        if (e instanceof RuntimeException) {
            return (RuntimeException) e;
        }
        try {
            if (StringUtils.isEmpty(message)) {
                return wrapType.getConstructor(Throwable.class).newInstance(e);
            } else {
                return wrapType.getConstructor(String.class, Throwable.class).newInstance(message, e);
            }
        } catch (Exception e1) {
            LOG.error("Could not wrap exception", e1);
            throw new RuntimeException(e);
        }
    }
```

---

</SwmSnippet>

# Where is this flow used?

This flow is used multiple times in the codebase as represented in the following diagram:

```mermaid
graph TD;
      subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
174366e7fb638daf17b2b39ef946145b1e59e702fffed5078f76ae062c74b92a(destroy):::rootsStyle --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
end

subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
bcc1bbb2eb9ee6f2b5ee38a88da4d462003ef5d80f0cfdded471d32049bf4407(execute):::rootsStyle --> 700e033f3f106991f5b8f357ebc5d884d15accaed23cc2c5ac4e045626375ea0(commit)
end

subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
700e033f3f106991f5b8f357ebc5d884d15accaed23cc2c5ac4e045626375ea0(commit) --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
end

subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
5db0774efc18b443bde8e79e62c6ee275b0a8649100da7548e4c4485f8e81571(deleteByQueries):::rootsStyle --> 22811d1233b577f3b7a6970e0c0eae420e6dead5b4634c8bc50c1eef68c9a2db(deleteByQuery)
end

subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
22811d1233b577f3b7a6970e0c0eae420e6dead5b4634c8bc50c1eef68c9a2db(deleteByQuery) --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
end

subgraph core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr
d5cc5023489d2e1b3b982f11d423689fb4fb500edb1ee264146e713ca00bf6e5(addDocument):::rootsStyle --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% 174366e7fb638daf17b2b39ef946145b1e59e702fffed5078f76ae062c74b92a(destroy):::rootsStyle --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% bcc1bbb2eb9ee6f2b5ee38a88da4d462003ef5d80f0cfdded471d32049bf4407(execute):::rootsStyle --> 700e033f3f106991f5b8f357ebc5d884d15accaed23cc2c5ac4e045626375ea0(commit)
%% end
%% 
%% subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% 700e033f3f106991f5b8f357ebc5d884d15accaed23cc2c5ac4e045626375ea0(commit) --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% 5db0774efc18b443bde8e79e62c6ee275b0a8649100da7548e4c4485f8e81571(deleteByQueries):::rootsStyle --> 22811d1233b577f3b7a6970e0c0eae420e6dead5b4634c8bc50c1eef68c9a2db(deleteByQuery)
%% end
%% 
%% subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% 22811d1233b577f3b7a6970e0c0eae420e6dead5b4634c8bc50c1eef68c9a2db(deleteByQuery) --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/](core/broadleaf-framework/src/main/java/org/broadleafcommerce/core/search/service/solr/)</SwmPath>
%% d5cc5023489d2e1b3b982f11d423689fb4fb500edb1ee264146e713ca00bf6e5(addDocument):::rootsStyle --> 8d30075ee2673e23b0a4fda4558a74470c28290eb65fbaeeebcbf577d633fa81(getReindexServer):::mainFlowStyle
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
