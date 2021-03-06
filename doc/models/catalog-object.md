## Catalog Object

The wrapper object for the Catalog entries of a given object type. 

The type of a particular `CatalogObject` is determined by the value of the
`type` attribute and only the corresponding data attribute can be set on the `CatalogObject` instance.
For example, the following list shows some instances of `CatalogObject` of a given `type` and
their corresponding data atrribute that can be set:
- For a `CatalogObject` of the `ITEM` type, set the `item_data` attribute to yield the `CatalogItem` object. 
- For a `CatalogObject` of the `ITEM_VARIATION` type, set the `item_variation_data` attribute to yield the `CatalogItemVariation` object.
- For a 'CatalogObject' of the `MODIFIER` type, set the `modifier_data` attribute to yield the `CatalogModifier` object.
- For a 'CatalogObject' of the `MODIFIER_LIST` type, set the `modifier_list_data` attribute to yield the `CatalogModifierList` object.
- For a 'CatalogObject' of the `CATEGORY` type, set the `category_data` attribute to yield the `CatalogCategory` object.
- For a 'CatalogObject' of the `DISCOUNT` type, set the `discount_data` attribute to yield the `CatalogDiscount` object.
- For a 'CatalogObject' of the `TAX` type, set the `tax_data` attribute to yield the `CatalogTax` object.
- For a 'CatalogObject' of the `IMAGE` type, set the `image_data` attribute to yield the `CatalogImageData`  object.
- For a 'CatalogObject' of the `QUICK_AMOUNTS_SETTINGS` type, set the `quick_amounts_settings_data` attribute to yield the `CatalogQuickAmountsSettings` object.
- For a 'CatalogObject' of the `PRICING_RULE` type, set the `pricing_rule_data` attribute to yield the `CatalogPricingRule` object.
- For a 'CatalogObject' of the `TIME_PERIOD` type, set the `time_period_data` attribute to yield the `CatalogTimePeriod` object.
- For a 'CatalogObject' of the `PRODUCT_SET` type, set the `product_set_data` attribute to yield the `CatalogProductSet`  object.

For a more detailed discussion of the Catalog data model, please see the
[Design a Catalog](https://developer.squareup.com/docs/catalog-api/design-a-catalog) guide.

### Structure

`CatalogObject`

### Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `Type` | [`string`](/doc/models/catalog-object-type.md) |  | Possible types of CatalogObjects returned from the Catalog, each<br>containing type-specific properties in the `*_data` field corresponding to the object type. |
| `Id` | `string` |  | An identifier to reference this object in the catalog. When a new `CatalogObject`<br>is inserted, the client should set the id to a temporary identifier starting with<br>a "`#`" character. Other objects being inserted or updated within the same request<br>may use this identifier to refer to the new object.<br><br>When the server receives the new object, it will supply a unique identifier that<br>replaces the temporary identifier for all future references. |
| `UpdatedAt` | `string` | Optional | Last modification [timestamp](https://developer.squareup.com/docs/build-basics/working-with-dates) in RFC 3339 format, e.g., `"2016-08-15T23:59:33.123Z"`<br>would indicate the UTC time (denoted by `Z`) of August 15, 2016 at 23:59:33 and 123 milliseconds. |
| `Version` | `long?` | Optional | The version of the object. When updating an object, the version supplied<br>must match the version in the database, otherwise the write will be rejected as conflicting. |
| `IsDeleted` | `bool?` | Optional | If `true`, the object has been deleted from the database. Must be `false` for new objects<br>being inserted. When deleted, the `updated_at` field will equal the deletion time. |
| `CustomAttributeValues` | [`IDictionary<string, Models.CatalogCustomAttributeValue>`](/doc/models/catalog-custom-attribute-value.md) | Optional | A map (key-value pairs) of application-defined custom attribute values. The value of a key-value pair <br>is a [CatalogCustomAttributeValue](#type-CatalogCustomAttributeValue) object. The key is the `key` attribute <br>value defined in the associated [CatalogCustomAttributeDefinition](#type-CatalogCustomAttributeDefinition) <br>object defined by the application making the request. <br><br>If the `CatalogCustomAttributeDefinition` object is <br>defined by another application, the `CatalogCustomAttributeDefinition`'s key attribute value is prefixed by <br>the defining application ID. For example, if the `CatalogCustomAttributeDefinition` has a `key` attribute of <br>"cocoa_brand" and the defining application ID is "abcd1234", the key in the map is "abcd1234:cocoa_brand" if the<br>application making the request is different from the application defining the custom attribute definition. <br>Otherwise, the key used in the map is simply "cocoa-brand".<br><br>Application-defined custom attributes that are set at a global (location-independent) level.<br>Custom attribute values are intended to store additional information about a catalog object<br>or associations with an entity in another system. Do not use custom attributes<br>to store any sensitive information (personally identifiable information, card details, etc.). |
| `CatalogV1Ids` | [`IList<Models.CatalogV1Id>`](/doc/models/catalog-v1-id.md) | Optional | The Connect v1 IDs for this object at each location where it is present, where they<br>differ from the object's Connect V2 ID. The field will only be present for objects that<br>have been created or modified by legacy APIs. |
| `PresentAtAllLocations` | `bool?` | Optional | If `true`, this object is present at all locations (including future locations), except where specified in<br>the `absent_at_location_ids` field. If `false`, this object is not present at any locations (including future locations),<br>except where specified in the `present_at_location_ids` field. If not specified, defaults to `true`. |
| `PresentAtLocationIds` | `IList<string>` | Optional | A list of locations where the object is present, even if `present_at_all_locations` is `false`. |
| `AbsentAtLocationIds` | `IList<string>` | Optional | A list of locations where the object is not present, even if `present_at_all_locations` is `true`. |
| `ImageId` | `string` | Optional | Identifies the `CatalogImage` attached to this `CatalogObject`. |
| `ItemData` | [`Models.CatalogItem`](/doc/models/catalog-item.md) | Optional | An item (i.e., product family) in the Catalog object model. |
| `CategoryData` | [`Models.CatalogCategory`](/doc/models/catalog-category.md) | Optional | A category to which a `CatalogItem` belongs in the `Catalog` object model. |
| `ItemVariationData` | [`Models.CatalogItemVariation`](/doc/models/catalog-item-variation.md) | Optional | An item variation (i.e., product) in the Catalog object model. Each item<br>may have a maximum of 250 item variations. |
| `TaxData` | [`Models.CatalogTax`](/doc/models/catalog-tax.md) | Optional | A tax in the Catalog object model. |
| `DiscountData` | [`Models.CatalogDiscount`](/doc/models/catalog-discount.md) | Optional | A discount in the Catalog object model. |
| `ModifierListData` | [`Models.CatalogModifierList`](/doc/models/catalog-modifier-list.md) | Optional | A modifier list in the Catalog object model. A `CatalogModifierList`<br>contains `CatalogModifier` objects that can be applied to a `CatalogItem` at<br>the time of sale.<br><br>For example, a modifier list "Condiments" that would apply to a "Hot Dog"<br>`CatalogItem` might contain `CatalogModifier`s "Ketchup", "Mustard", and "Relish".<br>The `selection_type` field specifies whether or not multiple selections from<br>the modifier list are allowed. |
| `ModifierData` | [`Models.CatalogModifier`](/doc/models/catalog-modifier.md) | Optional | A modifier in the Catalog object model. |
| `TimePeriodData` | [`Models.CatalogTimePeriod`](/doc/models/catalog-time-period.md) | Optional | Represents a time period - either a single period or a repeating period. |
| `ProductSetData` | [`Models.CatalogProductSet`](/doc/models/catalog-product-set.md) | Optional | Represents a collection of catalog objects for the purpose of applying a<br>`PricingRule`. Including a catalog object will include all of its subtypes.<br>For example, including a category in a product set will include all of its<br>items and associated item variations in the product set. Including an item in<br>a product set will also include its item variations. |
| `PricingRuleData` | [`Models.CatalogPricingRule`](/doc/models/catalog-pricing-rule.md) | Optional | Defines how discounts are automatically applied to a set of items that match the pricing rule <br>during the active time period. |
| `ImageData` | [`Models.CatalogImage`](/doc/models/catalog-image.md) | Optional | An image file to use in Square catalogs. Can be associated with catalog<br>items, item variations, and categories. |
| `MeasurementUnitData` | [`Models.CatalogMeasurementUnit`](/doc/models/catalog-measurement-unit.md) | Optional | Represents the unit used to measure a `CatalogItemVariation` and<br>specifies the precision for decimal quantities. |
| `ItemOptionData` | [`Models.CatalogItemOption`](/doc/models/catalog-item-option.md) | Optional | A group of variations for a `CatalogItem`. |
| `ItemOptionValueData` | [`Models.CatalogItemOptionValue`](/doc/models/catalog-item-option-value.md) | Optional | An enumerated value that can link a<br>`CatalogItemVariation` to an item option as one of<br>its item option values. |
| `CustomAttributeDefinitionData` | [`Models.CatalogCustomAttributeDefinition`](/doc/models/catalog-custom-attribute-definition.md) | Optional | Contains information defining a custom attribute. Custom attributes are<br>intended to store additional information about a catalog object or to associate a<br>catalog object with an entity in another system. Do not use custom attributes<br>to store any sensitive information (personally identifiable information, card details, etc.).<br>[Read more about custom attributes](https://developer.squareup.com/docs/catalog-api/add-custom-attributes) |
| `QuickAmountsSettingsData` | [`Models.CatalogQuickAmountsSettings`](/doc/models/catalog-quick-amounts-settings.md) | Optional | A parent Catalog Object model represents a set of Quick Amounts and the settings control the amounts. |

### Example (as JSON)

```json
{
  "type": "CUSTOM_ATTRIBUTE_DEFINITION",
  "id": "id0",
  "updated_at": null,
  "version": null,
  "is_deleted": null,
  "custom_attribute_values": null,
  "catalog_v1_ids": null,
  "present_at_all_locations": null,
  "present_at_location_ids": null,
  "absent_at_location_ids": null,
  "image_id": null,
  "item_data": null,
  "category_data": null,
  "item_variation_data": null,
  "tax_data": null,
  "discount_data": null,
  "modifier_list_data": null,
  "modifier_data": null,
  "time_period_data": null,
  "product_set_data": null,
  "pricing_rule_data": null,
  "image_data": null,
  "measurement_unit_data": null,
  "item_option_data": null,
  "item_option_value_data": null,
  "custom_attribute_definition_data": null,
  "quick_amounts_settings_data": null
}
```

