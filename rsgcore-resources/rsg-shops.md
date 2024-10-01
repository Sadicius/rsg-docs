---
description: Ya'll got doritos?
---

# 🏪 rsg-shops

## Introduction

* Works in conjunction with [rsg-inventory.md](rsg-inventory.md "mention") to let players buy items
* Includes delivery system for players to earn money while refilling stock of shop

## Creating a Shop

{% hint style="warning" %}
Options highlighted in yellow are optional!
{% endhint %}

### Defining Products

You can define a table of items inside a unique product list with multiple options available. The index of our table of items will be our unique product list name that we can use later so make sure to keep them different! Let's go over what needs to be included in our product list

* product list: `string`
* name: `string`
* amount: `number`
* <mark style="color:yellow;">info</mark>: `table`
* <mark style="color:yellow;">requiredJob</mark>: `table | string`
* <mark style="color:yellow;">requiredGang</mark>: `table | string`
* <mark style="color:yellow;">requiredGrade</mark>: `number`
* <mark style="color:yellow;">requiredLicense</mark>: `table | string`&#x20;

#### Example:

```lua
    ['normal'] = {
        [1] = { name = 'consumable_bread_roll',     price = 0.10, amount = 500, info = {}, type = 'item', slot = 1 },
        [2] = { name = 'consumable_water_filtered', price = 0.10, amount = 500, info = {}, type = 'item', slot = 2 },
    },
```

{% hint style="warning" %}
When using a table for requirements, they are EITHER/OR and not both. So if we add police and ambulance as requirements, you will not need both jobs, only one of them!
{% endhint %}

### Defining Locations

You can define a list of shops which are indexed by a unique identifier. These identifier's must be different because it allows for the restocking of the shop if it's set to true.

* label: `string`
* products: `table`
* coords: `vector`
* delivery: `vector`
* <mark style="color:yellow;">ped</mark>: `string`
* <mark style="color:yellow;">scenario</mark>: `string`
* <mark style="color:yellow;">radius</mark>: `float`
* <mark style="color:yellow;">targetIcon</mark>: `string`
* <mark style="color:yellow;">targetLabel</mark>: `string`
* <mark style="color:yellow;">showblip</mark>: `boolean`
* <mark style="color:yellow;">blipsprite</mark>: `number`
* <mark style="color:yellow;">blipscale</mark>: `float`
* <mark style="color:yellow;">blipcolor</mark>: `number`
* <mark style="color:yellow;">radius</mark>: `float`
* <mark style="color:yellow;">useStock</mark>: `boolean`
* <mark style="color:yellow;">requiredJob</mark>: `string | table`
* <mark style="color:yellow;">requiredGang</mark>: `string | table`
* <mark style="color:yellow;">requiredItem</mark>: `string | table`

Example:

```lua
    {
        label = 'Strawberry General Store',
        name = 'gen-strawberry',
        products = 'normal',
        shopcoords = vector3(-1791.49, -386.87, 160.33 -0.8),
        blipsprite = 'blip_shop_store',
        blipscale = 0.2,
        showblip = true
    },
```

{% hint style="danger" %}
{% endhint %}