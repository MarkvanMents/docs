# Page Template
Creating new pages *(default)* | The page template is available when creating new pages from most contexts, such as from the Project Explorer.
Generating edit pages | The page template is available when a user generates a new page from a new or edit button.
Generating select pages | The page templates is available when the user generates a new page from a select button.

This setting may also place extra restrictions on the template. Page templates intended as new or edit pages require exactly one top-level data view be present. Page templates intended as Select pages require exactly one list view, data grid, or template grid. 

### 5.4 Layout Type

[Layouts](layout) are all assigned a type in their properties. This type determines in which profiles the layout can be used. To ensure that a user can always map a page template to a compatible layout during page creation, a page template must be assigned one of these same layout types. In practice, this setting will affect in which profile tab of the **Create Page** wizard the page template is displayed. Additionally, it will automatically restrict the default layout setting to layouts of the same type.

### 5.5 Preview Layout

Although page templates and layouts can be mixed and matched, this setting will determine which layout will be used to display the template in the editor. It also has a minor effect on the page creation process: if the template describes contents for layout [placeholders](placeholder) that are not present in the previously selected layout, the first compatible layout will be pre-selected in the **Create Page** wizard. For a full description of the interaction between a page template and its preview layout, see [Layout](layout).

The options available for this setting are regulated by the layout type setting. If you are having trouble finding the layout you are looking for, check if the layout type of the template and the desired layout match.
