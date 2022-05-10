---
sidebar_position: 6
---

# Add code directly to product-template.liquid

Some Shopify themes require the app block to be added directly to the liquid template.  Instructions to do so can be found here, as well as an example app-block component. 
The component can be customized to match the theme of your store or change rendering conditions.

On products with an associated **discount**, the block will render in addition to the **Buy** and **Add to cart** buttons.

On products with an associated **exclusive**, the block will remove the **Buy** and **Add to cart** buttons, but this could possibly be circumvented.
**We recommend creating a new product template for 'exclusives' with the Shopify purchase options removed.** Instructions to do so can be found in the **[Creating a new product template](creating-a-new-product-template.md)** section.

1. Go to the nav in Shopify Admin and go to the **Online Store**.
![step1](/img/shopify_add_block/shopify_add_block_1.png)

2. Select **Customize**
![step2](/img/shopify_add_code_to_template/shopify_add_code_to_template_2.png)

3. On the top left of the page there will be menu (labeled with the red 1).  Click it to open, and select **Edit code** (labeled as 2).
![step3](/img/shopify_add_code_to_template/shopify_add_code_to_template_3.png)

4. Once in the coder editor, open the **Sections** folder (labeled as 1), and open the **product-template.liquid** file (labeled as 2).
![step4](/img/shopify_add_code_to_template/shopify_add_code_to_template_4.png)

5. Copy the code from the bottom of this page and paste it into template wherever you would like the block to appear. We recommend keeping it near the **Add to cart** and **Buy it now** buttons.
![step5](/img/shopify_add_code_to_template/shopify_add_code_to_template_5.png)

---

## Shopify App Block example

Paste this into the **product-template.liquid** or the equivalent file.

```
{% comment %}
Start Lit Token Block
{% endcomment %}
 <div>
  <script>
    const forwardToLitPromotion = () => {
      window.open(
        `https://oauth-app.litgateway.com/shopify?shop=${window.Shopify["shop"]}&productId=${window.ShopifyAnalytics?.meta?.product["gid"]}`
      );
    };
  </script>
  {% if product.available == true %}
    {% for tag in product.tags %}
      {% if tag == "lit-discount" %}
        <div id="lit-promotional-container" style="border: 2px solid #757575;cursor: pointer;" onclick="forwardToLitPromotion()">
          <div class="discount-container" style="background:#ffffff;padding: 0.5rem 0.8rem;display: flex;flex-direction: column;justify-content: center;align-items: center;cursor: pointer;">
            <p class="redeem-text" style="color:#757575;margin-top: 0.3rem;margin-bottom: 0.5rem;cursor: pointer;text-align: center;">This product qualifies for a token-based discount!</p>
            <button id="log-discounts" class="redeem-button" style="color:#2c0c72;border: none;background-color: transparent;margin-bottom: 0.7rem;cursor: pointer;text-align: center;">
              Click to connect wallet and view discount
            </button>
          </div>
        </div>
      {% else if tag == "lit-exclusive" %}
        <div id="lit-promotional-container" style="border: 2px solid #757575" onclick="forwardToLitPromotion()">
          <div class="discount-container" style="background:#ffffff;padding: 0.5rem 0.8rem;display: flex;flex-direction: column;justify-content: center;align-items: center;cursor: pointer;">
            <p class="redeem-text" style="color:#757575;margin-top: 0.3rem;margin-bottom: 0.5rem;cursor: pointer;text-align: center;">This product is token-gated and only available to qualified users.</p>
            <button id="log-discounts" class="redeem-button" style="color:#2c0c72;border: none;background-color: transparent;margin-bottom: 0.7rem;cursor: pointer;text-align: center;">
              Click to connect wallet and check access
            </button>
          </div>
          <script type="text/javascript">
            const paymentButtons = document.getElementsByClassName("shopify-payment-button");
            const addToCartButtons = document.getElementsByClassName("product-form__cart-submit");
            for (let i = 0; i < paymentButtons.length; i++) {
                paymentButtons[i].remove();
            }
            for (let i = 0; i < addToCartButtons.length; i++) {
                addToCartButtons[i].remove();
            }
          </script>
        </div>
      {% endif %}
    {% endfor %}
  {% endif %}
</div>
{% comment %}
End Lit Token Block
{% endcomment %}
```
