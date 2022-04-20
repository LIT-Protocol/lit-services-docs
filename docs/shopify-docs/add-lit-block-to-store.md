---
sidebar_position: 2
---

# Add Lit App Block to store

**Note:** older themes may not support adding theme-app-extensions.  An indicator would be if there is no **Product information** dropdown or **Add block** button as described in step 4.
[In this case, instructions on how to add the code directly to the **product-template.liquid** file can be found here.](add-code-to-product-template.md)
Developers who would like to customize the look of the app block may also find value in adding code directly to product-template.liquid.

---

The Lit App Block is an theme-app-extension used to show customers which products have been gated.

On products with an associated **discount**, the block will render in addition to the **Buy** and **Add to cart** buttons.

On products with an associated **exclusive**, the block will remove the **Buy** and **Add to cart** buttons, but this could possibly be circumvented.
**We recommend creating a new product template for 'exclusives' with the Shopify purchase options removed.** Instructions to do so can be found in the **[Creating a new product template](creating-a-new-product-template.md)** section.

1. Go to the nav in Shopify Admin and go to the **Online Store**.
![step1](/img/shopify_add_block/shopify_add_block_1.png)

2. Select **Customize**
![step2](/img/shopify_add_block/shopify_add_block_2.png)

3. Click a product to visit the product page.
![step3](/img/shopify_add_block/shopify_add_block_3.png)

4. Once at the product page, look to the menu on the left side.  Under the **Product information** dropdown, select **Add block**.
![step4](/img/shopify_add_block/shopify_add_block_4.png)

5. Select the **Lit App Block** to add it.  It can be placed anywhere, but we recommend having it next to the **Buy buttons**.
![step5](/img/shopify_add_block/shopify_add_block_5.png)
![step5-5](/img/shopify_add_block/shopify_add_block_5-5.png)


7. Click the **Save** button in the very top right of the screen. The **Lit App Block** will now render on product pages that have been gated with Token Access.
![step6](/img/shopify_add_block/shopify_add_block_6.png)

8. Optional -  The colors and text of the block can now be customized to match your store's theme.
![step7](/img/shopify_add_block/shopify_add_block_7.png)


