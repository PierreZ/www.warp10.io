---
title: "filter.last.eq"
layout: "function"
isPage: "true"
link: "/warpscript/framework_filter"
desc: "Selects the geo time series whose last value equals the filter parameter"
categoryTree: ["reference","frameworks"]
oldPath: ["20-frameworks","401-framework-filter","filter_last_eq.html.md"]
category: "reference"
---


This filter function only selects the Geo Time Series<sup>TM</sup> whose last value equals the filter parameter.

The filter parameter is a *long*, a *double*, a *boolean* or a *string*.

## Example ##

Stack:

    TOP:  [{"c":"GTS1","l":{"label0":"42"},"a":{},"v":[[10,42],[20,123]]},{"c":"GTS2","l":{"label0":"42"},"a":{},"v":[[10,211],[20,42]]}]

WarpScript commands:

    []             // labels of the partition being filtered. For example 'label0' 1 ->LIST
    123            // filter parameter
    filter.last.eq
    3 ->LIST
    FILTER

Stack: 

    TOP: [{"c":"GTS1","l":{"label0":"42"},"a":{},"v":[[10,42],[20,123]]}]

## Let's play with it ##

{% raw %}
<warp10-warpscript-widget>NEWGTS "GTS1" RENAME 
{ 'label0' '42' } RELABEL
10 NaN NaN NaN  42  ADDVALUE
20 NaN NaN NaN 123  ADDVALUE
NEWGTS "GTS2" RENAME 
{ 'label0' '43' } RELABEL
10 NaN NaN NaN 211 ADDVALUE
20 NaN NaN NaN  42 ADDVALUE
2 ->LIST
[]
123
filter.last.eq
3 ->LIST
FILTER
</warp10-warpscript-widget>
{% endraw %}    


## Unit test ##

{% raw %}
<warp10-warpscript-widget>NEWGTS "GTS1" RENAME 
{ 'label0' '42' } RELABEL
10 NaN NaN NaN  42  ADDVALUE
20 NaN NaN NaN 123  ADDVALUE
NEWGTS "GTS2" RENAME 
{ 'label0' '43' } RELABEL
10 NaN NaN NaN 211 ADDVALUE
20 NaN NaN NaN  42 ADDVALUE
2 ->LIST
[]
123
filter.last.eq
3 ->LIST
FILTER
LIST-> DROP
VALUES LIST-> 
2 == ASSERT   // values list size
123 == ASSERT
42 == ASSERT
'unit test successful'
</warp10-warpscript-widget>
{% endraw %}