/*!
* jQuery UI Expandable v1.3
*
* Copyright 2011, Tony Kramer
* Dual licensed under the MIT or GPL Version 2 licenses.
* https://github.com/flamewave/jquery-ui-expandable/raw/master/GPL-LICENSE.txt
* https://github.com/flamewave/jquery-ui-expandable/raw/master/MIT-LICENSE.txt
*
* For documentation and for the latest version, see:
* https://github.com/flamewave/jquery-ui-expandable
*/

This widget is similar to the jQuery UI Accordion widget, except that it allows more than one section to be open at a
time. It does not support only keeping one section open at a time, if you need that functionality, use the accordion
provided by jQuery UI.

The default markup is exactly the same as the accordion, but can be customized. Tables are also supported, where the
first, third, fifth (and so on) rows are header rows that when clicked on will show/hide the second, fourth, sixth
(and so on) rows. The content of the sections can also be auto-loaded from an AJAX call the first time the section is
expanded.

****************
* Dependencies *
****************
jQuery (1.4.2 and up)
jQuery-ui (1.8.6 and up - core, widget)

*******
* Use *
*******
JavaScript:
-----------
$('#expandable').expandable([options]);

HTML:
-----
<div id="expandable">
    <h3>Title 1</h3>
    <div>Content 1</div>
    <h3>Title 2</h3>
    <div>Content 2</div>
    <h3>Title 3</h3>
    <div>Content 3</div>
</div>

- or -

<!-- note: titles and content can be either TH or TD elements -->
<table id="expandable">
    <tbody>
        <tr><th>Title 1</th><th>More Title 1</th></tr>
        <tr><td colspan="2">Content 1</td></tr>
        <tr><th colspan="2">Title 2</th></tr>
        <tr><td colspan="2">Content 2</td></tr>
        <tr><th>Title 3</th><th>More Title 3</th></tr>
        <tr><td colspan="2">Content 3</td></tr>
    </tbody>
</table>

*****************
* Documentation *
*****************

---------------------------------------------
Available Options (and their default values):
---------------------------------------------

disabled: false
    Indicates if the widget is disabled.

defaultState: true
    An object representing the expanded state of the expandable items on initial creation. A null or undefined value
    is the same as true.
        - When a boolean value, specifies that all items are expanded or collapsed.
        - When a function value, returns a value indicating an items expanded state.
          Function signature: bool function(index, titleHtmlElement)
        - When an array value, specifies the expanded state of each item and the corresponding array index.
          Example: [ true, false ]
        - When an object value, indicates each item's expanded state on an individual basis. Items not included will
          default to be expanded by default. The object is in the format of: { elementIdOrItemIndex: true|false }
          Example: { 'item_1_id' : true, 'item_2_id': false } -or- { 0: true, 1: false }

titleSelector: '> h3' or for tables '> tbody > tr:even'
    The jQuery selector of the elements that contain the title for each expandable item. The element immediatly
    following (next sibling) each of the title elements is used as the content for each item.

icon: {collapsed: 'ui-icon-triangle-1-e', collapsedTitle: null, expanded: 'ui-icon-triangle-1-s', expandedTitle: null}
    Holds the icons that are inserted before the title text of each item. If null, no icons are used.
        - collapsed      - The icon used when an item is in it's collapsed state.
        - collapsedTitle - The icon title text (tool tip) when an item is in it's collapsed state. When null, the
                           default globalization value is used.
        - expanded       - The icon used when an item is in it's expanded state.
        - expandedTitle  - The icon title text (tool tip) when an item is in it's expanded state. When null, the
                           default globalization value is used.

showFx: { effect: 'slide', options: { direction: 'up' }, duration: 'normal', callback: null }
    Animation options for expanding/showing expandable items. Setting this option to null will disable show
    animations.
        - effect   - Name of jQuery animation.
        - options  - Options for enhanced animations.
        - duration - Animation duration/speed.
        - callback - A function to call once the animation is complete.

hideFx: { effect: 'slide', options: { direction: 'up' }, duration: 'normal', callback: null }
    Animation options for collapsing/hiding expandable items. Setting this option to null will disable hide
    animations.
        - effect   - Name of jQuery animation.
        - options  - Options for enhanced animations.
        - duration - Animation duration/speed.
        - callback - A function to call once the animation is complete.

ajax: { enabled: false, attr: 'rel', cache: true, options: null }
    AJAX options for loading the content of an item from an AJAX request when it is expanded. Settomg this option to
    null will disable AJAX loading.
        - enabled    - Indicates if AJAX loading is enabled.
        - attr       - HTML attribute on the title element that contains the URL to load the content from.
        - cache      - Indicates if content is cached so that it is only loaded once instead of every time the item is
                       expanded.
        - options    - Options to pass to the jQuery AJAX method. Default options used are: { dataType: 'html' }

------
Events
------
All events follow the standard jQuery UI widget event signature: void function(event, ui)
In most cases, the "event" parameter will be null. The "ui" parameter is an object with the following properties:
    - head    - The HTML DOM element that is the header of the item. Null if the event is not associated with a
                specific expandable item.
    - content - The HTML DOM element that is the content of the item. Null if the event is not associated with a
                specific expandable item.

create
    Raised when the widget is created. Inherited from the jQuery widget object.

expanded
    Raised when any item is expanded.

collapsed
    Raised when any item is collapsed.

contentSet
    Raised when any item's content has been set.

failedLoad
    Raised when any item's content failed to load. Only used when AJAX loading is enabled.

expandAll
    Raised when all items are expanded (i.e. "expand()" is called with no parameters). This event is not associated
    with any specific item, so the "head" and "content" properties of the "ui" parameter will be null.

collapseAll
    Raised when all items are collapsed (i.e. "collapse()" is called with no parameters). This event is not associated
    with any specific item, so the "head" and "content" properties of the "ui" parameter will be null.

toggleAll
    Raised when all items are toggled (i.e. "toggle()" is called with no parameters). This event is not associated
    with any specific item, so the "head" and "content" properties of the "ui" parameter will be null.

-------
Methods
-------
expandable('collapse'[, items, noFx, reload])
    Collapses the specified items. The "items" parameter can be one of the following values:
     - null or undefined - Collapses all of the items.
     - function          - A function that returns one of the below values to specify the items to collapse. Can not
                           return null or undefined or an error will be thrown.
     - jQuery object     - Collapses the items with the specified title HTML elements represented by the jQuery object.
     - "first" or "last" - Collapses the first or last item.
     - number            - Collapses the item with the specified (zero based) index.
     - array             - Array items can be either number or string values.
         - Number values correspond to the (zero based) indexes to collapse.
         - String values correspond with the HTML ID attribute value of the title of the items to collapse.
    If the "noFx" parameter is "true", then animations will be disabled when collapsing the items (only for this call).
    If the "reload" parameter is "true" and AJAX loading is enabled, then the item's content will be reloaded via AJAX.

expandable('count')
    Returns the number of items in the expandable widget.

expandable('destroy')
    Remove the expandable functionality completely. This will return the element back to it's pre-init state.

expandable('disable'[, items])
    Disables the widget or optionally just the specified items. See the "collapse" method for details on the "items"
    parameter.

expandable('enable'[, items])
    Enables the widget or optionally just the specified items. See the "collapse" method for details on the "items"
    parameter.

expandable('expand'[, items, noFx])
    Expands the specified items. See the "collapse" method for details on the parameters.

expandable('isExpanded'[, items])
    Returns true if all of the specified items are expanded. See the "collapse" method for details on the "items"
    parameter.

expandable('loadContent'[, items, force])
    Loads the content the specified items through AJAX requests. If AJAX loading is disabled, this method does nothing.
    See the "collapse" method for details on the "items" parameter.
    The optional "force" parameter will force the content to be reloaded, even if it has already been loaded. It
    essentially provides a way to refresh the content of one or more sections.

expandable('option', name[, value])
    Gets or sets the value of the specified option.

expandable('option', options)
    Sets the values of multiple options at once.

expandable('refresh')
    Refreshes and rebuilds the items of the expandable widget. Useful for if you want to add or remove items, so you
    don't have to destroy and re-create the widget.

expandable('setContent', items[, content])
    Sets the content of the specified item or items. The "items" parameter can be one of the following values:
     - function      - A function that returns one of the below values to specify the items to set the content of. Can
                       not return null or undefined or an error will be thrown.
     - jQuery object - The items with the title HTML elements represented by the jQuery object will have their content
                       set to the value of the "content" parameter.
     - number        - The item at the specified index will have it's content set to the value of the "content"
                       parameter.
     - "first" or "last" - Sets the content of the first or last item.
     - string        - The item with a header element with the HTML ID attribute value of the string will have it's
                       content set to the value of the "content" parameter.
     - object        - Map of items and content to set. The value of the "content" parameter is ignored.
                       Supported formats:
                       - Header element ID.
                         Example: {
                            "firstItem": "content for the 1st item",
                            "second": function() { return "content for 2nd item"; },
                            ...
                         }
                       - Index of item (zero based).
                         Example: {
                            1: "content for the 2nd item",
                            2: function() { return "content for 3rd item"; },
                            ...
                         }
                       - Mix of the two above.
                         Example: {
                            "firstItem": "content for the 1st item,
                            1: function() { return "content for the 2nd item"; },
                            ...
                         }
    The "content" parameter can be either a string containing the content, or a function that returns the content.

expandable('setItemStates'[, state, noFx, reload])
    Sets the items to the specified state. See the "defaultState" option for details on accepted values of the "state"
    parameter. If the "noFx" parameter is "true", then no animations will be used when setting the item states. If the
    "reload" parameter is "true" and AJAX loading is enabled, then items being expanded will have their content
    reloaded via AJAX.

expandable('toggle'[, items, noFx, reload])
    Toggles the state of the specified items. See the "collapse" method for details on the parameters.

expandable('widget')
    Returns the element.

-------------
Globalization
-------------
There is a globalization object defined that can be used to set default globalization options so that they do not
need to be specified for every instance of the expandable widget. They are as follows:

$.ui.expandable.globalization

    defaultIconCollapsedTitle: 'Click to expand',
        The default icon title text (tool tip) when an item is in it's collapsed state.

    defaultIconExpandedTitle: 'Click to collapse'
        The default icon title text (tool tip) when an item is in it's expanded state.