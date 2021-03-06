#SpinCommerce Liquid Documentation

- [Tags](#tags)
 - [Paginate](#paginate)
- [Global variables](#global-variables)
- [Objects](#objects)
 - [Cart](#cart)
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

## Iterating through specific categories products 

List products with 'food' category 

```liquid
{% for product in categories.food.products %}
  {{ product.name }} - {{ product.formatted_price }}
{% endfor %}
```

## Iterating through categories and subcategories

```liquid
<ul class="categories">
  {% for category in categories %}
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
  {% endfor %}
</ul>
```

## Iterating through categories and subcategories using Menus

List categories from a menu with slug 'categorias'. If the MenuItem links a category (link.is_category? returns true) and the category (link.category) has subcategories, show its links.

```liquid
<ul>
  {% for link in menus.categorias.links %}
    <li class="menuitem">
      <a href="{{link.url}}" {% if link.target %} target="blank"{% endif %}>{{link.name}}</a>
      {% if link.is_category? %}
          {% if link.category.has_subcategories %}
            <ul class="submenu">
            {% for subcategory in link.category.subcategories %}
              <li><a href="{{subcategory.url}}">{{subcategory.name}}</a></li>
            {% endfor %}
            </ul>
          {% endif %}
      {% endif %}
    </li>
  {% endfor %}
</ul>
```
