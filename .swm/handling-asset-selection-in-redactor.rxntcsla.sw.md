---
title: Handling Asset Selection in Redactor
---
This document will cover the process of handling asset selection in the Redactor editor within the Broadleaf Commerce admin platform. We'll cover:

1. Initiating the asset selection process
2. Displaying the asset selection modal
3. Selecting and inserting an asset
4. Finalizing the asset selection

Technical document: <SwmLink doc-title="Handling Asset Selection in Redactor">[Handling Asset Selection in Redactor](/.swm/handling-asset-selection-in-redactor.zmztyks1.sw.md)</SwmLink>

# [Initiating the Asset Selection Process](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/zmztyks1#handling-modal-display-and-interaction)

When the user clicks the select button in the Redactor editor, the system saves the current selection and sets up an event listener for when the user selects an asset. This ensures that the user's current work is preserved and can be restored after the asset is selected.

# [Displaying the Asset Selection Modal](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/zmztyks1#displaying-the-modal)

The system displays a modal window where the user can browse and select an asset. Initially, a loading message is shown to indicate that the modal is being prepared. The modal is then populated with the actual content for asset selection.

# [Selecting and Inserting an Asset](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/zmztyks1#handling-modal-display-and-interaction)

Once the user selects an asset, the system restores the previous selection in the Redactor editor. The selected asset's URL and alternative text are retrieved, and an image element is created and inserted into the editor at the saved selection point. This allows the user to seamlessly integrate the selected asset into their content.

# [Finalizing the Asset Selection](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/zmztyks1#handling-modal-display-and-interaction)

After the asset is inserted into the editor, the modal window is hidden. This final step ensures that the user can continue editing their content without any interruptions, with the newly inserted asset now part of their document.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
