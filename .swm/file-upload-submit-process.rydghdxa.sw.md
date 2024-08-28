---
title: File Upload Submit Process
---
In this document, we will explain the process of submitting a file upload. The process involves several steps, including initiating the upload, preparing the AJAX request, and handling the upload in chunks if necessary.

The submit process starts when a file upload is initiated. First, it checks if the current state is valid. If it is, it triggers the submit event and calls the function to handle the actual sending of the file. The function prepares the AJAX request and either sends it immediately or queues it based on the upload settings. If the file needs to be uploaded in chunks, it splits the file into smaller parts and uploads each part sequentially until the entire file is uploaded.

Here is a high level diagram of the flow, showing only the most important functions:

```mermaid
graph TD;
      d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle --> d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle

d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 0481ec250854477c03ef35a67399579566c30f1654fb0ef9795824650874976b(_getAJAXSettings)

d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)

d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle

88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)

88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle

58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)

58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 0deeaa034b1681b5a29ba03b362330aa439f50f2556f2b717027e32d57eda554(upload):::mainFlowStyle

0deeaa034b1681b5a29ba03b362330aa439f50f2556f2b717027e32d57eda554(upload):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9
```

# Flow drill down

First, we'll zoom into this section of the flow:

```mermaid
graph TD;
      subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle --> d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 0481ec250854477c03ef35a67399579566c30f1654fb0ef9795824650874976b(_getAJAXSettings)
end

subgraph common/src/main/resources/common_style/js/BLC.js
d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> f7rkh(...)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
0481ec250854477c03ef35a67399579566c30f1654fb0ef9795824650874976b(_getAJAXSettings) --> 502154e4acc065b2f27781e16210c062db21cbed122a2d812061327261766b17(_initDataSettings)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle --> d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 0481ec250854477c03ef35a67399579566c30f1654fb0ef9795824650874976b(_getAJAXSettings)
%% end
%% 
%% subgraph <SwmPath>[common/src/main/resources/common_style/js/BLC.js](common/src/main/resources/common_style/js/BLC.js)</SwmPath>
%% d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% d91b58de8bcee409a18d491461925510e05defcb6b7781c3b03f992be8224c5a(_onSend):::mainFlowStyle --> 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> f7rkh(...)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 0481ec250854477c03ef35a67399579566c30f1654fb0ef9795824650874976b(_getAJAXSettings) --> 502154e4acc065b2f27781e16210c062db21cbed122a2d812061327261766b17(_initDataSettings)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="532">

---

## Submit Function

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="532:3:3" line-data="            data.submit = function () {">`submit`</SwmToken> function initiates the file upload process. It first checks if the current state is not 'pending'. If the state is valid, it triggers the <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="532:3:3" line-data="            data.submit = function () {">`submit`</SwmToken> event and calls the <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="536:3:3" line-data="                        that._onSend(e, this);">`_onSend`</SwmToken> function to handle the actual sending of the file.

```javascript
            data.submit = function () {
                if (this.state() !== 'pending') {
                    data.jqXHR = this.jqXHR =
                        (that._trigger('submit', e, this) !== false) &&
                        that._onSend(e, this);
                }
                return this.jqXHR || that._getXHRPromise();
            };
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="736">

---

## <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="736:1:1" line-data="        _onSend: function (e, data) {">`_onSend`</SwmToken> Function

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="736:1:1" line-data="        _onSend: function (e, data) {">`_onSend`</SwmToken> function is responsible for preparing and sending the AJAX request. It first adds convenience methods to the data object if they are not already present. It then retrieves the AJAX settings using <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="745:7:7" line-data="                options = that._getAJAXSettings(data),">`_getAJAXSettings`</SwmToken>, and either sends the request immediately or queues it based on the upload settings.

```javascript
        _onSend: function (e, data) {
            if (!data.submit) {
                this._addConvenienceMethods(e, data);
            }
            var that = this,
                jqXHR,
                aborted,
                slot,
                pipe,
                options = that._getAJAXSettings(data),
                send = function () {
                    that._sending += 1;
                    // Set timer for bitrate progress calculation:
                    options._bitrateTimer = new that._BitrateTimer();
                    jqXHR = jqXHR || (
                        ((aborted || that._trigger('send', e, options) === false) &&
                        that._getXHRPromise(false, options.context, aborted)) ||
                        that._chunkedUpload(options) || $.ajax(options)
                    ).done(function (result, textStatus, jqXHR) {
                        that._onDone(result, textStatus, jqXHR, options);
                    }).fail(function (jqXHR, textStatus, errorThrown) {
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="483">

---

### Retrieving AJAX Settings

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="483:1:1" line-data="        _getAJAXSettings: function (data) {">`_getAJAXSettings`</SwmToken> function merges the default options with the data-specific options. It initializes form and data settings before returning the final options object.

```javascript
        _getAJAXSettings: function (data) {
            var options = $.extend({}, this.options, data);
            this._initFormSettings(options);
            this._initDataSettings(options);
            return options;
        },
```

---

</SwmSnippet>

<SwmSnippet path="/common/src/main/resources/common_style/js/BLC.js" line="135">

---

## AJAX Function

The <SwmToken path="common/src/main/resources/common_style/js/BLC.js" pos="135:3:3" line-data="    function ajax(options, callback) {">`ajax`</SwmToken> function is a wrapper around <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="138:7:9" line-data="            // handlers using jQuery&#39;s Deferred callbacks:">`jQuery's`</SwmToken> <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="753:10:11" line-data="                        that._chunkedUpload(options) || $.ajax(options)">`$.ajax`</SwmToken> method. It sets default values for the request type and URL parameters, handles CSRF and state version tokens, and defines success and error callbacks.

```javascript
    function ajax(options, callback) {
        if (options.type == null) {
            options.type = 'GET';
        }

        var baseUrl = window.location.href;
        if (baseUrl.indexOf('isPostAdd') != -1) {
            if (options.url.indexOf('isPostAdd') < 0) {
                if (options.url.indexOf('?') > 0) {
                    options.url += "&";
                } else {
                    options.url += "?";
                }
                options.url += "isPostAdd=true";
            }
        }
        var savedCatalogElement = $('input[name ="catalogEntityCatalogDiscriminatorId"]');
        var savedCatalog=null;

        if(savedCatalogElement.length){
            //0 should be the one we need, other can be from the modal form
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/blc-admin-init.js" line="33">

---

## Callback Function

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/blc-admin-init.js" pos="33:1:1" line-data="            callback: function() {">`callback`</SwmToken> function is used to initialize and update fields in the admin interface after an AJAX request completes. It calls <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/blc-admin-init.js" pos="34:3:3" line-data="                BLCAdmin.initializeFields(BLCAdmin.getActiveTab());">`initializeFields`</SwmToken> and <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/blc-admin-init.js" pos="35:3:3" line-data="                BLCAdmin.updateFields(BLCAdmin.getActiveTab());">`updateFields`</SwmToken> on the active tab.

```javascript
            callback: function() {
                BLCAdmin.initializeFields(BLCAdmin.getActiveTab());
                BLCAdmin.updateFields(BLCAdmin.getActiveTab());
            }
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="415">

---

## Initializing Data Settings

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="415:1:1" line-data="        _initDataSettings: function (options) {">`_initDataSettings`</SwmToken> function initializes the data settings for the AJAX request. It checks if the upload is an XHR upload and sets up the necessary data and progress listeners. If the upload is not an XHR upload, it initializes iframe settings.

```javascript
        _initDataSettings: function (options) {
            if (this._isXHRUpload(options)) {
                if (!this._chunkedUpload(options, true)) {
                    if (!options.data) {
                        this._initXHRData(options);
                    }
                    this._initProgressListener(options);
                }
                if (options.postMessage) {
                    // Setting the dataType to postmessage enables the
                    // postMessage transport:
                    options.dataType = 'postmessage ' + (options.dataType || '');
                }
            } else {
                this._initIframeSettings(options, 'iframe');
            }
        },
```

---

</SwmSnippet>

Now, lets zoom into this section of the flow:

```mermaid
graph TD;
      subgraph common/src/main/resources/common_style/js/BLC.js
88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> mvnh9(...)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[common/src/main/resources/common_style/js/BLC.js](common/src/main/resources/common_style/js/BLC.js)</SwmPath>
%% 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 88d0856b4da7feb3c7f870bba8bba8c8c34db19f84c92f95f6dcd533951e5bf1(send):::mainFlowStyle --> 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> mvnh9(...)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="746">

---

## Handling the send process

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="746:1:1" line-data="                send = function () {">`send`</SwmToken> function initiates the sending process by incrementing the <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="747:3:3" line-data="                    that._sending += 1;">`_sending`</SwmToken> counter and setting a timer for bitrate progress calculation. It then triggers the <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="746:1:1" line-data="                send = function () {">`send`</SwmToken> event and decides whether to proceed with a chunked upload or a regular AJAX request based on the conditions.

```javascript
                send = function () {
                    that._sending += 1;
                    // Set timer for bitrate progress calculation:
                    options._bitrateTimer = new that._BitrateTimer();
                    jqXHR = jqXHR || (
                        ((aborted || that._trigger('send', e, options) === false) &&
                        that._getXHRPromise(false, options.context, aborted)) ||
                        that._chunkedUpload(options) || $.ajax(options)
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="766">

---

## Managing concurrent uploads

The function also manages concurrent uploads by checking if the number of concurrent uploads is within the limit. If it is, it starts the next queued upload that has not been aborted by resolving the next slot in the queue.

```javascript
                        if (options.limitConcurrentUploads &&
                                options.limitConcurrentUploads > that._sending) {
                            // Start the next queued upload,
                            // that has not been aborted:
                            var nextSlot = that._slots.shift();
                            while (nextSlot) {
                                if (that._getDeferredState(nextSlot) === 'pending') {
                                    nextSlot.resolve();
                                    break;
                                }
                                nextSlot = that._slots.shift();
                            }
```

---

</SwmSnippet>

Now, lets zoom into this section of the flow:

```mermaid
graph TD;
      subgraph common/src/main/resources/common_style/js/BLC.js
58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 0deeaa034b1681b5a29ba03b362330aa439f50f2556f2b717027e32d57eda554(upload):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin
735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[common/src/main/resources/common_style/js/BLC.js](common/src/main/resources/common_style/js/BLC.js)</SwmPath>
%% 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax)
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 58923a25f701069f5acd2d5c89e72cfe3b17759560b40c4ec9a4f4c0733ce1f7(_chunkedUpload):::mainFlowStyle --> 0deeaa034b1681b5a29ba03b362330aa439f50f2556f2b717027e32d57eda554(upload):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/)</SwmPath>
%% 735e8dabf9d808e57e1ae9226d6dc2bbd430d5caf620c06e056b1f2093d3b0a4(ajax) --> 27904be92202cd2eff089cef66b59791d02cebd758830360ad926dbf64c85e2d(callback)
%% end
%% 
%% 
%%       classDef mainFlowStyle color:#000000,fill:#7CB9F4
%% classDef rootsStyle color:#000000,fill:#00FFF4
%% classDef Style1 color:#000000,fill:#00FFAA
%% classDef Style2 color:#000000,fill:#FFFF00
%% classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="566">

---

## <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="571:1:1" line-data="        _chunkedUpload: function (options, testOnly) {">`_chunkedUpload`</SwmToken> Function

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="571:1:1" line-data="        _chunkedUpload: function (options, testOnly) {">`_chunkedUpload`</SwmToken> function is responsible for uploading a file in multiple, sequential requests by splitting the file into multiple blob chunks. This function first checks if the file should be uploaded in chunks and then proceeds to upload each chunk sequentially. It handles the progress of each chunk upload and ensures that the entire file is uploaded by recursively calling the <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="570:3:3" line-data="        // upload requests:">`upload`</SwmToken> function until all chunks are uploaded.

```javascript
        // Uploads a file in multiple, sequential requests
        // by splitting the file up in multiple blob chunks.
        // If the second parameter is true, only tests if the file
        // should be uploaded in chunks, but does not invoke any
        // upload requests:
        _chunkedUpload: function (options, testOnly) {
            var that = this,
                file = options.files[0],
                fs = file.size,
                ub = options.uploadedBytes = options.uploadedBytes || 0,
                mcs = options.maxChunkSize || fs,
                slice = file.slice || file.webkitSlice || file.mozSlice,
                dfd = $.Deferred(),
                promise = dfd.promise(),
                jqXHR,
                upload;
            if (!(this._isXHRUpload(options) && slice && (ub || mcs < fs)) ||
                    options.data) {
                return false;
            }
            if (testOnly) {
```

---

</SwmSnippet>

<SwmSnippet path="/admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" line="597">

---

### The chunk upload method

The <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="597:7:7" line-data="            // The chunk upload method:">`upload`</SwmToken> function within <SwmToken path="admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/jquery.fileupload.js" pos="417:7:7" line-data="                if (!this._chunkedUpload(options, true)) {">`_chunkedUpload`</SwmToken> is the core method that handles the actual uploading of each chunk. It clones the options object for each chunk, slices the file to create a blob for the current chunk, and processes the upload data. It also adds progress listeners and triggers events for each chunk upload. If the upload is not complete, it recursively calls itself to upload the next chunk.

```javascript
            // The chunk upload method:
            upload = function () {
                // Clone the options object for each chunk upload:
                var o = $.extend({}, options),
                    currentLoaded = o._progress.loaded;
                o.blob = slice.call(
                    file,
                    ub,
                    ub + mcs,
                    file.type
                );
                // Store the current chunk size, as the blob itself
                // will be dereferenced after data processing:
                o.chunkSize = o.blob.size;
                // Expose the chunk bytes position range:
                o.contentRange = 'bytes ' + ub + '-' +
                    (ub + o.chunkSize - 1) + '/' + fs;
                // Process the upload data (the blob and potential form data):
                that._initXHRData(o);
                // Add progress listeners for this chunk upload:
                that._initProgressListener(o);
```

---

</SwmSnippet>

# Where is this flow used?

This flow is used multiple times in the codebase as represented in the following diagram:

(Note - these are only some of the entry points of this flow)

```mermaid
graph TD;
      subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins
7738f3e20cd9481f3a3b9a7953b673e2cb36d978facc1cbab08ed005d983ccbe(processSubmitCall):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins
c485b096408b2a47636c40d424a269a0b75898b0026c5e264679bea5503dd47b(add):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins
c485b096408b2a47636c40d424a269a0b75898b0026c5e264679bea5503dd47b(add):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins
b72efa65c1e8e12b42248f48fd5f8df7e85d52b6407c6aa5d13d874a6bd6b567(assetSelected):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
end

subgraph admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins
10c19510986262ace8f57ef8a362ffc3edb7637f90f058bf2e891d262a194c41(_startHandler):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9

%% Swimm:
%% graph TD;
%%       subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/)</SwmPath>
%% 7738f3e20cd9481f3a3b9a7953b673e2cb36d978facc1cbab08ed005d983ccbe(processSubmitCall):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/)</SwmPath>
%% c485b096408b2a47636c40d424a269a0b75898b0026c5e264679bea5503dd47b(add):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/)</SwmPath>
%% c485b096408b2a47636c40d424a269a0b75898b0026c5e264679bea5503dd47b(add):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/)</SwmPath>
%% b72efa65c1e8e12b42248f48fd5f8df7e85d52b6407c6aa5d13d874a6bd6b567(assetSelected):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
%% end
%% 
%% subgraph <SwmPath>[admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/](admin/broadleaf-open-admin-platform/src/main/resources/open_admin_style/js/admin/lib/plugins/)</SwmPath>
%% 10c19510986262ace8f57ef8a362ffc3edb7637f90f058bf2e891d262a194c41(_startHandler):::rootsStyle --> d0cd6b095efedac3da9da17ab0d78c17b947ec2793858509752c7ee690d3c4e8(submit):::mainFlowStyle
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
