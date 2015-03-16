# Change logs #

## 1.0.6 ##
  * fixed an error in `adjustIframe` function, which is used in IE6,
  * updated jQuery version to 1.4.1.

## 1.0.5 ##
  * renamed 'cacheVariants' parameter to 'enableVariantCaching',
  * renamed 'userVariantFilter' parameter to 'enableVariantFilter',
  * renamed 'variantHTMLParser' parameter to 'variantHTMLRenderer',
  * added checking of dropdown height after adding of each element (to prevent box 'jumping' on big lists),
  * fixed some CSS properties,
  * fixed variant switching with arrow keys in Safari and Chrome,
  * added match highlighting (can be turned on and off),
  * added automatic switching to the first variant (can be turned on and off),
  * made demo page a little more informative.

## 1.0 ##
All of the basic functionality presents:
  * selecting values from a list of variants,
  * input of variants by a user,
  * limiting maximum amount of selected values,
  * getting variant list from AJAX request or from local array,
  * etc.