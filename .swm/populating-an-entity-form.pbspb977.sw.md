---
title: Populating an Entity Form
---
This document will cover the process of populating an entity form, which includes:

1. Initializing the entity form
2. Organizing the form into tabs and groups
3. Populating form fields
4. Handling dropdown fields.

Technical document: <SwmLink doc-title="Populating an Entity Form">[Populating an Entity Form](/.swm/populating-an-entity-form.cak7r368.sw.md)</SwmLink>

# [Initializing the Entity Form](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/cak7r368#setting-entity-form-fields)

The process begins by initializing the entity form with basic properties. This includes setting the class name of the entity and the section key, which helps in identifying the form's context within the application. The section key can be derived from the section crumbs, which are breadcrumbs that help in navigation. This step ensures that the form is correctly associated with the entity it represents.

# [Organizing the Form into Tabs and Groups](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/cak7r368#setting-entity-form-fields)

Once the basic properties are set, the form is organized into tabs and groups. This organization helps in structuring the form in a user-friendly manner, making it easier for users to navigate and fill out the form. Tabs can represent different sections of the form, while groups can cluster related fields together. This step enhances the usability of the form by providing a clear and logical layout.

# [Populating Form Fields](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/cak7r368#setting-entity-form-fields)

The next step involves populating the form fields with the necessary data. Each field in the form is configured based on the metadata provided. This includes setting attributes such as visibility, required status, and default values. Fields can be standalone or part of a group, and special cases like enumerations and rule builders are handled appropriately. This step ensures that all the necessary data is available in the form fields for the user to interact with.

# [Handling Dropdown Fields](https://app.swimm.io/repos/Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v/docs/cak7r368#populating-dropdown-fields)

Finally, the form handles dropdown fields to ensure they have the correct options. This involves identifying fields that require dropdown options and fetching the relevant records. The options are then built into a map and set on the corresponding combo field in the form. This step is crucial for providing users with the correct choices in dropdown fields, enhancing the accuracy and efficiency of data entry.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQnJvYWRsZWFmQ29tbWVyY2UtZGVtby1uZXclM0ElM0FTd2ltbS1EZW1v" repo-name="BroadleafCommerce-demo-new" doc-type="product-flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
