- [Tags](#tags)
 - [Paginate](#paginate)
- [Global variables](#global-variables)
- [Objects](#objects)
 - [Product](#product)
- [Iterating through categories and subcategories](#iterating-through-categories-and-subcategories)


## Tags 

### Paginate

The paginate tag allows you to split a collection into different pages.

```liquid
{% paginate products by 2 %}
  {% for product in paginate.collection %}
    {{product.name}}
  {% endfor %}
  {{ paginate | default_pagination }}
{% endpaginate %}
```

## Global variables

The following variables are available in all the templates.

|Variable|Type|Description|
|---|---|---|
|cart_count|Integer|Current cart product quantity.|
|categories|Category Array|All categories sorted by name.|
|css_content|String|CSS content from styles.css template.|
|menus|Menu Array|All menus sorted by name.|
|products|Product Array|All products sorted by name.|
|shop|Shop|Current Shop.|
|template|String|Current template name.|

## Objects

### Cart

The Cart Object represents the current cart. 

It is available as the variable `cart` in the *cart.liquid* template.

An example can be found at <https://github.com/Corpspin/spincommerce-store/blob/master/themes/basic/cart.liquid>.


|Attribute|Type|Description
|---|---|---|
|update_url|String|The URL where the cart form should POST to.|
|has_items|Boolean|True if the cart has one or more items.|
|items|Cart Item Object Collection|Collection of products/variants added to the current cart.|
|subtotal|Integer|Subtotal in cents.|
|formatted_subtotal|String|Subtotal with two decimals and currency Symbol. Example: `$ 3.99`.|


### Product

The Product Object represents a visible product in the current shop.

It is available as the variable `product` in the `product.liquid` template and as the global variable `products`(collection) in all the templates.

An example can be found at <https://github.com/Corpspin/spincommerce-store/blob/master/themes/basic/products.liquid>.

|Attribute|Type|Description
|---|---|---|
|name|String|Name|
|slug|String|Slug|
|description|String|Description.|
|price|Integer|Price in cents.|
|formatted_price|String|Price with two decimals and currency symbol. Example: `$ 3.99`.|
|comparison_price|Integer|Comparison price in cents.|
|formatted_comparison_price|String|Comparison price with two decimals and currency symbol. Example: `$ 3.99`.|
|url|String|Product URL. Example: `http://shopname.spincommerce.com/products/product-slug`.|
|variants|Variant Object Collection|Collection of variants.|
|first_variant|Variant Object|First variant.|
|has_categories|Boolean|True if the product belongs to one or more categories.|
|categories|Category Object Collection|Collection of product categories sorted by name.|
|has_images|Boolean|True if the products has one or more images.|
|images|Product Image Object Collection|Collection of product images.|
|first_image|Product Image Object|First product image.|

## Iterating through categories and subcategories

```liquid
{% for category in categories %}
  <ul class="categories">
    <li>
      <a href="{{category.url}}">{{category.name}}</a>
      {% if category.has_subcategories %}
        <ul class="subcategories">
          {% for subcategory in category.subcategories %}
            <li><a href="{{subcategory.url}}">{{subcategory.name}}</a></li>
          {% endfor %}
        </ul>
      {% endif %}
    </li>
  </ul>
{% endfor %}
```
