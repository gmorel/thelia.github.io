---
layout: loop
title: Product sale elements Loop
description: Product sale elements loop lists product sale elements from your shop. You may need to use the <a href="/documentation/loop/attribute_combination.html">attribute combination loop</a> inside your product sale elements loop.
sidebar: loop
lang: en
subnav: loop_product_sale_elements
uses_global_argument: true
returns_global_outputs: { countable : true, timestampable : true, versionable : false }
type: loop_product_sale_elements
arguments :
    - {name: "currency", description: "A currency id", example: "currency=\"1\""}
    - {name: "product", description: "A single product id.", example: "product=\"2\"", mandatory: "true"}
    - {
            name: "order", description: "A list of values", example: "order=\"promo,min_price\"", default: "random",
            expected_values: [
                {name: "min_price",         description: "ascending price"},
                {name: "max_price",         description: "descending price"},
                {name: "promo",             description: "promo products first"},
                {name: "new",               description: "new products first"},
                {name: "random",            description: ""}
            ]
          }
outputs :
    - {name: "$ID", description: "the product sale elements id"}
    - {name: "$PRICE", description: "the product sale elements price"}
    - {name: "$PRICE_TAX", description: "the product sale elements price tax"}
    - {name: "$TAXED_PRICE", description: "the product sale elements taxed price"}
    - {name: "$PROMO_PRICE", description: "the product sale elements promo price"}
    - {name: "$PROMO_PRICE_TAX", description: "the product sale elements promo price tax"}
    - {name: "$TAXED_PROMO_PRICE", description: "the product sale elements taxed promo price"}
    - {name: "$IS_PROMO", description: "returns if the product sale element is in promo"}
    - {name: "$IS_NEW", description: "returns if the product sale element is new"}
    - {name: "$WEIGHT", description: "the product sale elements weight"}
    - {name: "$QUANTITY", description: "the product sale elements stock quantity"}
    - {name: "$EAN_CODE", description: "the product sale elements EAN Code"}
---

<div class="description large-12">
    I want to display all products sale elements for current product and show all the attribute combinations which matched it.
</div>

<div class="code large-12">

{% highlight smarty %}


{loop name="pse" type="product_sale_elements" product="$PRODUCT_ID"}
    <div>
        {loop name="combi" type="attribute_combination" product_sale_elements="$ID"}
        {$ATTRIBUTE_TITLE} = {$ATTRIBUTE_AVAILABILITY_TITLE}<br />
        {/loop}
        <br />{$WEIGHT} g
        <br /><strong>{if $IS_PROMO == 1} {$PROMO_PRICE} € (instead of {$PRICE}) {else} {$PRICE} € {/if}</strong>
        <br /><br />
        Add
        <select>
            {for $will=1 to $QUANTITY}
            <option>{$will}</option>
            {/for}
        </select>
        to my cart
    </div>
{/loop}


{% endhighlight %}

</div>&nbsp;