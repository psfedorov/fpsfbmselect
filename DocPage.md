# Documentation #

## How to insert the control in a page ##

First, you need to include the files needed by the plugin:

```
<link rel="stylesheet" href="jquery.fpsfbmselect-1.0.6.css" type="text/css"/>
<script type="text/javascript" src="jquery-1.4.1.min.js"></script>
<script type="text/javascript" src="jquery.fpsfbmselect-1.0.6.js"></script>
```

Then you can add the control as easy as this:

```
<div id="mycontrol"></div>
<script type="text/javascript">
    $('#mycontrol').fpsFBMSelect({
        'fieldName': 'myfield',
        'variantsURL': 'http://some/url/for/retrieving/variants/'
    });
</script>
```

## Available options ##

Here's a list of available options:

  * fieldName - required - name for hidden fields which will contain selected values (string),
  * enableUserInput - enable adding of user values (boolean, by default - false),
  * userFieldName - name for hidden fields which will contain values added by user (string, by default - equals to a 'fieldName' argument),
  * selectedValues - preselected values which will be added to a multiselect container immediately (array of objects, by default - empty array),
  * enableVariantCaching - enable caching of variants (boolean, by default - false),
  * variantsURL - URL for getting variants with AJAX request (string, by default - empty string),
  * variants - if variantsURL is not set, this array of variants will be used (array of objects, by default - empty array),
  * enableVariantFilter - enable client side filtering of variants (boolean, by default - false),
  * variantFilter - custom function for filtering variants on the client side (function, by default - null),
  * variantHTMLRenderer - custom function for rendering HTML for variants and selected values (function, by default - null),
  * maxDropDownHeight - maximum height of drop down element in pixels (number, by default - 200),
  * requestPause - pause in milliseconds before triggering AJAX requests (number, by default - 700),
  * requestArgumentName - the name of argument for an URL, which will contain the value of text input (string, by default - 'q'),
  * hintText - text of a hint in the drop down box (string, by default - 'Type and select from variants.'),
  * loadingHintText - text of a hint while loading variant with AJAX request (string, by default - 'Loading list...'),
  * userVariantHintText - text of a hint, which prepends user variant in the drop down box (string, by default - 'Add new value:'),
  * maxSelectedValues - maximum amount of values, which a user can select (number, by default - null, which means there's no limit),
  * focusAfterAddingValue - enable focusing of a text input after selecting a value (boolean, by default - false),
  * enableMatchHighlighting - enable highlighting a part of string that matched a pattern a user has typed (boolean, default - false),
  * enableAutoSwitchingToFirstVariant - enable automatic switching to the first variant in the list (boolean, default - false).

## JSON response format ##

If you have provided 'variantsURL' parameter to the control, it will try to load variant list from that URL. By default, the JSON response from your server should be an array of objects and have the following format:

```
[
    {"value": 1, "title": "One"},
    {"value": 2, "title": "Two"},
    {"value": 3, "title": "Three"}
]
```

You may use as values not only integers, but strings too. That values will be placed in hidden fields when a user will select them.

Titles are shown to a user and used to render variants and selected values. They may contain not only plain text, but HTML code as well.

The variant objects may also have another attribute - `orgn` (that means "origin"), which indicates whether a variant came from your system (when its value is "sys") or from a user (when its value is "user"). User and system variants will be shown slightly different. Also, if you have provided 'userFieldName' parameter to the control, then user variants will be inserted in hidden fields with that name.

## Custom functions for rendering and filtering values ##

If you use the default function for rendering HTML code of variants and values, then your variant objects should have this format: `{"value": "3", "title": "Three"}`. But if you want, for example, show image for every variant in dropdown box or show some additional info (not just plain text), then you can write your custom rendering function and pass it as the `variantHTMLRenderer` parameter, when you initialize the control.

The **rendering function** should return a string (HTML code, which will be directly inserted in an element) and take 2 arguments:
  * variant object,
  * type of an object that is being rendered.
So the format of variant object can be any of your choice, for example, `{"person": "John Doe", "address": "Unknown St., 1", "value": "111"}`. The only required attribute is `"value"`.

There are 4 types of objects that are being rendered:
  * 'systemVariant' - an option for the dropdown box that came from your system,
  * 'userVariant' - an option for the dropdown box that was entered by a user,
  * 'systemValue' - a selected value, that came from your system and is being added to the values container,
  * 'userValue' - a selected value, that was entered by a user and is being added to the values container.

Also note, that if user input is enabled, user variants will always have the default format: `{"value": "3", "title": "Three", "orgn": "user"}`.

If you want to use a custom **function for filtering** variant list on the client side, pass it as the `'variantFilter'` parameter. The function takes the only argument - an array of variant objects, and returns also an array of this objects. You may access the value of text input from the method `$.fn.fpsFBMSelect.getTextInputValue()`.

## Example usage in Django ##

You can find an example of a simple Django widget that uses fpsFBMSelect on the DjangoWidgetExample page.

## A note for PHP coders ##

Please, remember, that if you want to find an array of selected values in `$_POST['yourfield']`, `$_GET['yourfield']` or `$_REQUEST['yourfield']`, you should render that field on the form with the name '`yourfield[]`'. This will tell PHP that 'yourfield' is an array.

## psfmsbs... what's that??? ##

'fpsFBMSelect' stands for:
  * 'fps' are author's initials,
  * 'FB' means 'Facebook', where the original idea has been found,
  * 'MSelect' is 'multiselect'.

You may also want to see the ChangeLog.