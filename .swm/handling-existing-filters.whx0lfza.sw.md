---
title: Handling Existing Filters
---
This document will cover the process of handling existing filters in a filter builder component. We'll cover:

1. Checking for existing filters
2. Updating the applied filters view
3. Generating filter item HTML
4. Making AJAX requests.

Technical document: <SwmLink doc-title="Handling Existing Filters Flow">[Handling Existing Filters Flow](/.swm/handling-existing-filters-flow.1pxbz0gv.sw.md)</SwmLink>

# [Checking for Existing Filters](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/1pxbz0gv#handling-existing-filters)

The process begins by checking if there are any existing filters on the page. This involves retrieving existing filter data and processing each field to check for existing rules. If any rules are found, the filter builder is updated accordingly. This step ensures that any previously applied filters are recognized and maintained, providing a consistent user experience.

# [Updating the Applied Filters View](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/1pxbz0gv#updating-the-applied-filters-view)

Next, the visual representation of the applied filters is updated. This involves parsing the filter data, clearing the current filter container, and appending HTML elements for each filter rule. If no rules are present, the filter wrapper is hidden. This step ensures that the user can see which filters are currently applied, making it easier to manage and adjust them as needed.

# [Generating Filter Item HTML](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/1pxbz0gv#generating-filter-item-html)

For each filter rule, HTML is generated to visually represent the filter. This includes constructing the filter item's label, operator, and value based on the rule's properties. The generated HTML is then appended to the filter container. This step ensures that each filter is clearly displayed with its corresponding details, enhancing the user's ability to understand and interact with the filters.

# [Making AJAX Requests](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/1pxbz0gv#ajax-requests)

Finally, AJAX requests are used to fetch data asynchronously, such as retrieving filter options. This involves setting default options, appending necessary parameters like CSRF tokens, and handling the success and error callbacks. This step ensures that the filter options are dynamically updated without requiring a page reload, providing a smoother and more responsive user experience.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
