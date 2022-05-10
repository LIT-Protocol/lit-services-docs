---
sidebar_position: 3
---

# Troubleshooting

### - Discount or exclusive app block does not appear for a product where I've created and saved an offer.

- The app will not work correctly without adding the app block for store themes that are able to use it, [instructions to do so can be found here.](add-lit-block-to-store.md)  Older themes or custom themes that cannot use app blocks can find [example app block code that can be added directly to their product template here.](add-code-to-product-template.md)

- If you have already added the block there is a chance the tag was not added to the product correctly.  Go to the details page for the product which the offer was created, and make sure that the correct tags are appended.  For an exclusive, there should be a **lit-exclusive** tag, and for a discount, there should be a **lit-discount** tag.

### - Discount or exclusive block is still appearing on products that do not have an associated offer.

- Go to the details page for the affected product and check the tags.  If a **lit-exclusive** or **lit-discount** tag is present, delete it.
