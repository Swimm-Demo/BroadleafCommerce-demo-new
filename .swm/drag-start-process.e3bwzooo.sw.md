---
title: Drag Start Process
---
This document will cover the Drag Start Process, which includes:

1. Initializing the drag start
2. Recalculating dimensions
3. Updating helper locations
4. Rendering the color palette.

Technical document: <SwmLink doc-title="Drag Start Process">[Drag Start Process](/.swm/drag-start-process.s2qyrrkz.sw.md)</SwmLink>

# [Initializing the drag start](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/s2qyrrkz#dragstart)

The drag start process begins when the user initiates a drag action. This step checks if the dimensions for dragging are valid. If the dimensions are not valid, it triggers a recalculation. Once the dimensions are confirmed, the system marks the dragging state as active, updates the user interface to reflect this state, and provides visual feedback to the user.

# [Recalculating dimensions](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/s2qyrrkz#reflow)

If the initial dimensions are invalid, the system recalculates the dimensions of the draggable elements. This ensures that all elements involved in the drag process are correctly positioned and visible. The recalculation includes updating the dimensions of the dragger, slider, and alpha slider elements. This step is crucial for maintaining the accuracy and reliability of the drag operation.

# [Updating helper locations](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/s2qyrrkz#updatehelperlocations)

After recalculating the dimensions, the system updates the positions of the helper elements. These helpers provide visual cues to the user about their current selection. The positions are adjusted based on the current color selection, ensuring that the helpers are visible and accurately reflect the user's actions. This step enhances the user experience by providing immediate visual feedback.

# [Rendering the color palette](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/s2qyrrkz#drawpalette)

The final step in the drag start process is rendering the color palette. The system retrieves the current color and generates the HTML for each palette row. It updates the selection palette from storage and appends it to the HTML if it exists. This ensures that the color palette is up-to-date and accurately reflects the user's selections. The updated palette is then displayed to the user, providing a comprehensive view of the available color options.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
