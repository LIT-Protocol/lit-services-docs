---
sidebar_position: 1
---

# Introduction
**Lit Protocol: Token Access** is a Shopify app that allows merchants to gate exclusive content and discounts, ensuring access to select parties only.

## Install
Although a public version is in the works, **Lit Protocol: Token Access** is currently a custom app and available by request only. 

## Uninstall
Go to the **Apps** section of your store's Shopify Admin and click the **Delete** button in the **Lit Protocol: Token Access** app listing.

## Caveats
This is early in development, and there are a few things to be aware of.  As development continues, multiple products and conditions will be supported, but for now:
- Each product can only have one discount or exclusive Token Access associated with it.
- Each discount or exclusive can only have one product.
- Each discount or exclusive can only have one access control condition.
- After a product is token gated, a **lit-exclusive** or **lit-discount** tag will be appended to the product. 
This is how the app knows what content is gated and when to show the customer.  Removing the tags will stop the app block from rendering.
The tags will be automatically removed when the Token Access entry is deleted.
- **We highly recommend cloning a product template for use with products marked 'exclusive'.**  Directions can be found under the **[Creating a new product template](creating-a-new-product-template.md)** entry.
