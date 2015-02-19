
##PDP JSON Layouting

###Basic Structure of JSON Layout

We'll refer the following structure as a node. A node is an equivalent of HTML Node (e.g, `<div>`, `<span>` ..)
```json
{
  "type"  : "...",
  "value" : "...",
  "attr"  : {},
  "children": [
     {}
   ]
}
```
`type`, `value`, `attr`, `children`.. are node attributes, where,
> - *`type`* - type of node, which can be one of [type]
> - *`value`* - value of node, which can be one of [value]
> - *`attr`* - the list of attributes for current node
> - *`children`* - list of nodes to be wrapped inside current node

Apart from the above attributes, node type column has special attributes,
> - *`width`* - in case of *type* as column use width to specify the column width e.g, `12`, `{"small": 6, "medium": 12}`
> - *`visible`* - visibility options for column e.g, `["large", "medium"]`
> - *`variations`* - 	used to specify `push`, `pull`, `offset` width e.g, `{"offset": 2}`, `{"push": 3}`
>
> **NOTE**
> - In JSON format `,` will not be there for last attribute, the rest of the lines will end with a `,`

----------
###Analogy between JSON Node and HTML node

Consider the following simpe HTML markup
```html
<div id="title" data-catalog-sku="SM-S3-NEO-I9300">
</div>
```
Lets see the JSON equivalent of following:

1. Create a JSON with type as *html_tag* and value as *div*
```json
{
  "type": "html_tag",
  "value": "div"
}
```
2. Lets add attribute to the node, HTML attributes of a tag can be specified in *attr* attribute of the node
```json
{
  "type" : "html_tag",
  "value": "div",
  "attr" : {
    "id" : "title",
    "data-catalog-sku":"SM-S3-NEO-I9300"
  }
}
```
In the above example to get a `<span>` instead of `<div>` we just need to replace `"value": "div"` with  `"value": "span"`, similarly for any html tag.
Consider a complex html markup,
```html
<div class=" row">
  <div class="col-md-5 col-sm-5">
  </div>
  <div class="col-md-7 col-sm-7">
  </div>
</div>
```
Lets create the JSON equivalent of the above HTML,

1. The below node makes up for a row
```json
{
  "type": "row"
}
```
2. The below node makes up for a 5 column
```json
{
  "type": "column",
  "width": 5
}
```
3. The below node makes up for a 7 column
```json
{
  "type": "column",
  "width": 7
}
```
4. All we have to do is to make 5-column and 7-column node as a children of row. The final JSON will look like
```json
{
  "type": "row",
  "children": [
    {
      "type": "column",
      "width": 5
    },
    {
      "type": "column",
      "width": 7
    }
  ]
}
```
5. What if we needed to add classes for breakpoint like below
```json
<div class=" row">
  <div class="col-md-5 col-sm-6 col-xs-6">
  </div>
  <div class="col-md-7 col-sm-6 col-xs-6">
  </div>
</div>
```
Simple, pass breakpoint widths to width as,
```json
{
  "type": "column",
  "width": {
    "large" : 5,
    "medium": 6,
    "small" : 6
  }
}
```
The equivalent JSON with column breakpoint widths is,
```json
{
  "type": "row",
  "children": [
    {
      "type": "column",
      "width": {
        "large" : 5,
        "medium": 6,
        "small" : 6
      }
    },
    {
      "type": "column",
      "width": {
        "large" : 7,
        "medium": 6,
        "small" : 6
      }
    }
  ]
}
```
> **NOTE**
>
> - The type of children is always Array `[]`
> - In JSON layout,
> - - `large` corresponds to `md`
> - - `medium` corresponds to `sm`
> - - `small` corresponds to `xs`

----------
###Basic Structure of PDP
```json
{
  "type": "root",
  "value":"pdp",
  "children": [
    {}
   ]
}
```
----------
### A Demo PDP
```json
{
  "type": "root",
  "value": "pdp",
  "children": [
    {
      "type": "row",
      "children": [
        {
      "type": "column",
          "width": {
            "large": 6,
            "small": 12,
            "medium": 6
          },
          "visible": ["large"],
          "variations": {"push": 3},
          "children": [
            {
              "type": "block",
              "value": "pdp_breadcrumbs"
            }
          ]
        }
      ]
    },
    {
      "type": "row",
      "children": [
        {
          "type": "column",
          "width": 5,
          "children": [
            {
              "type": "row",
              "children": [
                {
                  "type": "column",
          "width": 10,
                  "children": [
                    {
                      "type": "block",
                      "value": "medium_image"
                    }
                  ]
                },
                {
                  "type": "column",
                  "width": 2,
                  "children": [
                    {
                      "type": "block",
                      "value": "catalog_images_thumb_nails"
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "type": "column",
          "width": 7
        }
      ]
    },
    {
      "type": "row",
      "children": [
        {
          "type": "column",
          "width": 8
        },
        {
          "type": "column",
          "width": 4
        }
      ]
    }
  ]
}
```

----------
###List of Availabe Blocks
* add_to_cart
* add_to_compare
* add_to_wishlist
* also_available_in
* availability_time
* badges
* brand_page_link
* bullet_delivery
* buy_with_plan
* catalog_images
* catalog_images_thumb_nails
* catalog_options
* catalog_title
* check_servicable_area
* cod_charges
* cod_zone_desc
* compare_bar
* description
* disclaimer
* discount_gola
* discussions
* dynamic_badges
* dynamic_bundle
* exchange_policy
* fb_comment_in_sdp
* feature_groups
* features
* flixmedia_plugin
* free_delivery
* iamavailable
* in_stock
* items_by_category
* key_features
* list_price
* medium_image
* nearest_store_finder
* offer_description
* offer_items
* other_offerings
* pdp_banner
* pdp_breadcrumbs
* price_drop_alert
* pricing_summary
* product_bundle_banner
* promotions
* qview_next
* qview_prev
* rating_and_review
* related_items
* related_tags
* reviews
* shipping_details
* shipping_policy
* snippet
* social_buttons
* social_share
* static_bundle
* t_and_c
* variant_link
* warranty
* xsell
