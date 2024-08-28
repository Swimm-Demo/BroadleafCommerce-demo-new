---
title: Exploring Admin Functionality
---
```mermaid
graph TD;
 A[AdminPageController] -->|/pages| B[viewEntityForm];
 A -->|/pages/{id}| C[saveEntity];
 D[AdminAssetUploadController] -->|/{sectionKey}/{id}/chooseAsset| E[chooseMediaForMapKey];
 D -->|/{sectionKey}/{id}/uploadAsset| F[upload];
```

# Exploring Admin Functionality

Admin in the Broadleaf content management module refers to the administrative functionalities provided for managing content within the system. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="46:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminStructuredContentController.SECTION_KEY)">`AdminStructuredContentController`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`AdminAssetController`</SwmToken>, and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`AdminPageController`</SwmToken> are key components in this module, responsible for handling structured content, assets, and pages respectively.

## <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`AdminPageController`</SwmToken>

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`AdminPageController`</SwmToken> handles admin operations for the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="70:4:4" line-data="            .withSecurityCeilingClassName(Page.class.getName())">`Page`</SwmToken> entity. It extends <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="54:8:8" line-data="public class AdminPageController extends AdminBasicEntityController {">`AdminBasicEntityController`</SwmToken> and provides functionalities such as viewing and managing entity forms. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:11:11" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`SECTION_KEY`</SwmToken> constant defines the section as 'pages'. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="59:5:5" line-data="    protected String getSectionKey(Map&lt;String, String&gt; pathVars) {">`getSectionKey`</SwmToken> method allows external links to work for <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="60:14:14" line-data="        //allow external links to work for ToOne items">`ToOne`</SwmToken> items, and the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="62:5:5" line-data="    public String viewEntityForm(HttpServletRequest request, HttpServletResponse response, Model model,">`viewEntityForm`</SwmToken> method manages the dynamic fields and forms associated with the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="70:4:4" line-data="            .withSecurityCeilingClassName(Page.class.getName())">`Page`</SwmToken> entity.

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" line="52">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`AdminPageController`</SwmToken> is annotated with <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="52:0:1" line-data="@Controller(&quot;blAdminPageController&quot;)">`@Controller`</SwmToken> and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:0:1" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`@RequestMapping`</SwmToken> to map the URL pattern `/pages`.

```java
@Controller("blAdminPageController")
@RequestMapping("/" + AdminPageController.SECTION_KEY)
public class AdminPageController extends AdminBasicEntityController {
    
    public static final String SECTION_KEY = "pages";
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" line="58">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="59:5:5" line-data="    protected String getSectionKey(Map&lt;String, String&gt; pathVars) {">`getSectionKey`</SwmToken> method allows external links to work for <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="60:14:14" line-data="        //allow external links to work for ToOne items">`ToOne`</SwmToken> items by returning the section key.

```java
    @Override
    protected String getSectionKey(Map<String, String> pathVars) {
        //allow external links to work for ToOne items
        if (super.getSectionKey(pathVars) != null) {
            return super.getSectionKey(pathVars);
        }
        return SECTION_KEY;
    }
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" line="67">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="67:5:5" line-data="    protected DynamicEntityFormInfo getDynamicForm(EntityForm ef, String id) {">`getDynamicForm`</SwmToken> method manages the dynamic fields and forms associated with the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="70:4:4" line-data="            .withSecurityCeilingClassName(Page.class.getName())">`Page`</SwmToken> entity.

```java
    protected DynamicEntityFormInfo getDynamicForm(EntityForm ef, String id) {
        return new DynamicEntityFormInfo()
            .withCeilingClassName(PageTemplate.class.getName())
            .withSecurityCeilingClassName(Page.class.getName())
            .withCriteriaName("constructForm")
            .withPropertyName("pageTemplate")
```

---

</SwmSnippet>

## <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`AdminAssetController`</SwmToken>

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`AdminAssetController`</SwmToken> handles admin operations for the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="46:17:17" line-data=" * Handles admin operations for the {@link Asset} entity. This is mostly to support displaying image assets inline ">`Asset`</SwmToken> entity, primarily to support displaying image assets inline in list grids. It extends <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="54:8:8" line-data="public class AdminPageController extends AdminBasicEntityController {">`AdminBasicEntityController`</SwmToken> and includes services like <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="58:3:3" line-data="    protected AssetFormBuilderService formService;">`AssetFormBuilderService`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="61:3:3" line-data="    protected StaticAssetService staticAssetService;">`StaticAssetService`</SwmToken>, and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="64:3:3" line-data="    protected StaticAssetStorageService staticAssetStorageService;">`StaticAssetStorageService`</SwmToken>. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:11:11" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`SECTION_KEY`</SwmToken> constant defines the section as 'assets'. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="81:5:5" line-data="    public String viewEntityList(HttpServletRequest request, HttpServletResponse response, Model model,">`viewEntityList`</SwmToken> method customizes the entity list view to include an upload asset button and a hidden form for uploading images.

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" line="51">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`AdminAssetController`</SwmToken> is annotated with <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="51:0:1" line-data="@Controller(&quot;blAdminAssetController&quot;)">`@Controller`</SwmToken> and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:0:1" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`@RequestMapping`</SwmToken> to map the URL pattern `/assets`.

```java
@Controller("blAdminAssetController")
@RequestMapping("/" + AdminAssetController.SECTION_KEY)
public class AdminAssetController extends AdminBasicEntityController {
    
    public static final String SECTION_KEY = "assets";
    
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" line="57">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="52:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminAssetController.SECTION_KEY)">`AdminAssetController`</SwmToken> includes services like <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="58:3:3" line-data="    protected AssetFormBuilderService formService;">`AssetFormBuilderService`</SwmToken>, <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="61:3:3" line-data="    protected StaticAssetService staticAssetService;">`StaticAssetService`</SwmToken>, and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="64:3:3" line-data="    protected StaticAssetStorageService staticAssetStorageService;">`StaticAssetStorageService`</SwmToken> to manage assets.

```java
    @Resource(name = "blAssetFormBuilderService")
    protected AssetFormBuilderService formService;
    
    @Resource(name = "blStaticAssetService")
    protected StaticAssetService staticAssetService;

    @Resource(name = "blStaticAssetStorageService")
    protected StaticAssetStorageService staticAssetStorageService;

    @Resource(name = "blStaticAssetMultiTenantExtensionManager")
    protected StaticAssetMultiTenantExtensionManager staticAssetExtensionManager;
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" line="69">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="70:5:5" line-data="    protected String getSectionKey(Map&lt;String, String&gt; pathVars) {">`getSectionKey`</SwmToken> method allows external links to work for <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="71:14:14" line-data="        //allow external links to work for ToOne items">`ToOne`</SwmToken> items by returning the section key.

```java
    @Override
    protected String getSectionKey(Map<String, String> pathVars) {
        //allow external links to work for ToOne items
```

---

</SwmSnippet>

## <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="46:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminStructuredContentController.SECTION_KEY)">`AdminStructuredContentController`</SwmToken>

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="46:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminStructuredContentController.SECTION_KEY)">`AdminStructuredContentController`</SwmToken> handles admin operations for the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="20:12:12" line-data="import org.broadleafcommerce.cms.structure.domain.StructuredContent;">`StructuredContent`</SwmToken> entity. It extends <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="54:8:8" line-data="public class AdminPageController extends AdminBasicEntityController {">`AdminBasicEntityController`</SwmToken> and manages fields dependent on the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="21:12:12" line-data="import org.broadleafcommerce.cms.structure.domain.StructuredContentType;">`StructuredContentType`</SwmToken>. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminPageController.java" pos="53:11:11" line-data="@RequestMapping(&quot;/&quot; + AdminPageController.SECTION_KEY)">`SECTION_KEY`</SwmToken> constant defines the section as <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="49:14:16" line-data="    protected static final String SECTION_KEY = &quot;structured-content&quot;;">`structured-content`</SwmToken>. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="62:5:5" line-data="    public String viewEntityForm(HttpServletRequest request, HttpServletResponse response, Model model,">`viewEntityForm`</SwmToken> method attaches dynamic fields to the form, ensuring that the structured content type cannot be changed once an item exists.

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" line="46">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="46:9:9" line-data="@RequestMapping(&quot;/&quot; + AdminStructuredContentController.SECTION_KEY)">`AdminStructuredContentController`</SwmToken> is annotated with <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="46:0:1" line-data="@RequestMapping(&quot;/&quot; + AdminStructuredContentController.SECTION_KEY)">`@RequestMapping`</SwmToken> to map the URL pattern `/structured-content`.

```java
@RequestMapping("/" + AdminStructuredContentController.SECTION_KEY)
public class AdminStructuredContentController extends AdminBasicEntityController {
    
    protected static final String SECTION_KEY = "structured-content";
    
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" line="52">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="52:5:5" line-data="    protected String getSectionKey(Map&lt;String, String&gt; pathVars) {">`getSectionKey`</SwmToken> method allows external links to work for <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="53:14:14" line-data="        //allow external links to work for ToOne items">`ToOne`</SwmToken> items by returning the section key.

```java
    protected String getSectionKey(Map<String, String> pathVars) {
        //allow external links to work for ToOne items
        if (super.getSectionKey(pathVars) != null) {
            return super.getSectionKey(pathVars);
        }
        return SECTION_KEY;
    }
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" line="61">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminStructuredContentController.java" pos="62:5:5" line-data="    public String viewEntityForm(HttpServletRequest request, HttpServletResponse response, Model model,">`viewEntityForm`</SwmToken> method attaches dynamic fields to the form, ensuring that the structured content type cannot be changed once an item exists.

```java
    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public String viewEntityForm(HttpServletRequest request, HttpServletResponse response, Model model,
            @PathVariable  Map<String, String> pathVars,
            @PathVariable(value="id") String id) throws Exception {
        // Get the normal entity form for this item
        String returnPath = super.viewEntityForm(request, response, model, pathVars, id);
```

---

</SwmSnippet>

## <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="63:4:4" line-data="public class AdminAssetUploadController extends AdminAbstractController {">`AdminAssetUploadController`</SwmToken>

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="63:4:4" line-data="public class AdminAssetUploadController extends AdminAbstractController {">`AdminAssetUploadController`</SwmToken> handles uploading or selecting assets. It provides endpoints for choosing media for a map key and uploading assets. The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="78:5:5" line-data="    public String chooseMediaForMapKey(HttpServletRequest request, HttpServletResponse response, Model model, ">`chooseMediaForMapKey`</SwmToken> method is mapped to the URL pattern `/{sectionKey}/{id}/chooseAsset` and the <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetController.java" pos="86:23:23" line-data="        // Remove the default add button and replace it with an upload asset button">`upload`</SwmToken> method is mapped to `/{sectionKey}/{id}/uploadAsset`.

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" line="61">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="63:4:4" line-data="public class AdminAssetUploadController extends AdminAbstractController {">`AdminAssetUploadController`</SwmToken> is annotated with <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="61:0:1" line-data="@Controller(&quot;blAdminAssetUploadController&quot;)">`@Controller`</SwmToken> and <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="62:0:1" line-data="@RequestMapping(&quot;/{sectionKey}&quot;)">`@RequestMapping`</SwmToken> to map the URL pattern <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="62:4:7" line-data="@RequestMapping(&quot;/{sectionKey}&quot;)">`/{sectionKey}`</SwmToken>.

```java
@Controller("blAdminAssetUploadController")
@RequestMapping("/{sectionKey}")
public class AdminAssetUploadController extends AdminAbstractController {

    @Resource(name = "blEntityConfiguration")
    protected EntityConfiguration entityConfiguration;
    
    @Resource(name = "blStaticAssetStorageService")
    protected StaticAssetStorageService staticAssetStorageService;
    
    @Resource(name = "blStaticAssetService")
    protected StaticAssetService staticAssetService;
    
    @Resource(name = "blAdminAssetController")
    protected AdminAssetController assetController;
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" line="77">

---

The <SwmToken path="admin/broadleaf-contentmanagement-module/src/main/java/org/broadleafcommerce/cms/admin/web/controller/AdminAssetUploadController.java" pos="78:5:5" line-data="    public String chooseMediaForMapKey(HttpServletRequest request, HttpServletResponse response, Model model, ">`chooseMediaForMapKey`</SwmToken> method is mapped to the URL pattern `/{sectionKey}/{id}/chooseAsset`.

```java
    @RequestMapping(value = "/{id}/chooseAsset", method = RequestMethod.GET)
    public String chooseMediaForMapKey(HttpServletRequest request, HttpServletResponse response, Model model, 
            @PathVariable(value = "sectionKey") String sectionKey, 
            @PathVariable(value = "id") String id,
            @RequestParam MultiValueMap<String, String> requestParams) throws Exception {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
