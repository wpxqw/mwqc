
## Introduction
WooCommerce Product Catalog and/or Inquiry is a multi-purpose plugin to let you set all or selected products in catalog mode by revoking cart and optionally hiding product price. It also lets you receive inquiry for any product regardless of its catalog mode status by adding an inquiry cart to your store and showing inquiry button for the product. What you call this inquiry (order, request a quote, info query) and which form (Contact Form 7, Gravity Forms, etc.) you use to receive this inquiry is up to you. You can receive inquiry cart's content in the email sent to you by the inquiry form. You can also customize product price text and inquiry button label.

### Features
- For all or selected products
  - Enable catalog mode
  - Receive inquiry from registered or guest user
  - Hide price and/or customize price text
  - Revoke cart (deny add-to-cart request and hide add-to-cart button)
  - Show inquiry button and/or customize button label
- Global and Product level settings
    - Override global settings at product level or just configure at product level
- Inquiry Cart Page
  - Use auto-created inquiry cart page or create a new one
  - Add inquiry cart to a page using shortcode - *[mwqc_cart]*
  - Customize inquiry cart by hiding table columns, total section or its rows and/or update button using [shortcode's attributes](#shortcode-attributes "Read more about shortcode attributes")
  - Customze inquiry cart by overriding its template file in your theme just like any other WooCommerce template
  - Add inquiry form to inquiry cart page using shortcode
  - Customize inquiry cart name (e.g reservation cart) for front-end
  - Customize inquiry cart page title and slug (e.g https://webiste.com/reservation-cart)
  - Show cross-sells of the inquiry cart's products on the inquiry cart page
- Inquiry Form
  - Use any shortcode-rendered form (Contact Form 7, Gravity Forms, etc.) as inquiry form [Details](#inquiry-form "Read more about inquiry form")
  - Add inquiry cart contents in the email template of the inquiry form using shortcode - *[mwqc_cart_4_email]*
  - Clear inquiry cart on inquiry form submission using *[mwqc_clear_cart]* shortcode in the form's confirmation
  - Hide inquiry form for empty inquiry cart by wrapping it in *[mwqc_if_non_empty_cart]* shortcode
- Inquiry Button Behavior
  - If simple product is added to shopping cart via AJAX on shop page, it will also be added to inquiry cart via AJAX on shop page
  - if user is redirected to shopping cart after add-to-cart, they will also be redirected to inquiry cart after add-to-inquiry
- Allows shopping cart and checkout with orginal price for non-catalog-mode product
- Prevents the inferring of the price of a hidden-priced-product by hiding the prices in the inquiry cart's total section

## Installation

### Minimum Requirements

- PHP 7 or greater is recommended
- Wordpress 5.0 or greater
- Woocommerce 4.1 or greater

### Manual installation

Manual installation method requires downloading this plugin and uploading it to your web server via your favorite FTP application. The WordPress codex contains [instructions on how to do this here](https://wordpress.org/support/article/managing-plugins/#manual-plugin-installation).

### Updating

Please use [Evneto Market WordPress](https://envato.com/market-plugin/) plugin to update the plugin. If you need help in using this plugin, please read [Update themes automatically using Envato Market plugin](https://seventhqueen.com/support/general/article/update-themes-automatically-using-envato-market-plugin).

## Configuration

Plugin let you configure itself at multiple levels. Each level covers a particular set of products. A lower level covers a subset of the products being covered by the level on top of it. These levels are:
- Global
- Prodouct Category
- Product

**Please note**, only Global and Product levels are available as of now (version 1.0.0).

This level based settings make it possible to configure a set of products at a certain level and then override this configuration for a subset of products at a lower level. For example, you can hide price of all products at Global level and show price of selected products by configuring them at Product level.

### Global Level
- Open "WooCommerce Settings" page in Dashboard (Dashboard -> WooCommerce -> Settings).
- Switch to "Products" tab and then open "Catalog and/or Inquiry" sub-tab.
![alt Woocommerce Quote Inquiry & Management plugin settings](images/global-settings-v1.2.jpg)

### Product Level
- Open "Product Edit" page in Dashboard (Dashboard -> Products).
- Open the product you want to edit from the product list.
- Scroll down to data panels and open "Catalog and/or Inquiry" data panel.
![alt Woocommerce Quote Inquiry & Management plugin settings](product-settings.jpg)

## Usage
- **Configure for all products**
  - Open "WooCommerce Settings" page in back-end, switch to "Product" tab and then switch to "Catalog and/or Inquiry" sub-tab.
  - Enable "Configure all products" and based on your requirements for front-end:
    - Enable "Hide Price" to hide price of all products.
    - Optionally, set custom text in "Price Text" to show as price.
    - Enable "Inquiry Button" to show inquiry button for all products.
    - Optionally, set custom text in "Inquiry Button Label" to show as inquiry button label. Default label is "Add to inquiry".
    - Enable "Revoke Cart" to deny add-to-cart request and hide "Add to cart" button.
  - Save changes.

- **Configure individual product or override global settings for that product**
  - Open "Product Edit" page in back-end, scroll down to data panels and then switch to "Catalog and/or Inquiry" data panel.
  - Same settings as at global level.
  - Save product.

**Note**, External products can not be added to inquiry cart. That's why both global and product level "Inquiry Button" settings will be ignored for them.

- **Add inquiry form to inquiry cart page**
  - Create form with any form plugin (Contact Form 7, Gravity Forms, etc.)
  - See form plugin's documentation to know the shortcode to render the form.
  - Edit inquiry cart page in back-end.
  - Add the form shortcode while wrapping it in [mwqc_if_non_empty_cart] shortcode.
    - Example: *[mwqc_if_non_empty_cart][contact-form-7 id="58"][/mwqc_if_non_empty_cart]*
    - Explanation: *[contact-form-7 id="58"]* shortcode renders the inquiry form. *[mwqc_if_non_empty_cart]* shortcode hides the inquiry form for empty inquiry cart.
    - Wrapping form shortcode is optional. If not wrapped, your inquiry form will remain visible on inquiry cart page when inquiry cart is empty.
  - If you want to hide columns of inquiry cart table, update button or total section's rows, add attributes to *[mwqc_cart]* shortcode [Read More](#shortcode-attributes "Read more about configuration").
  - Save the inquiry cart page.

- **Receive inquiry cart's contents in the email sent to you by the inquiry form on form submission**
  - Open inquiry form. 
  - Add *[mwqc_cart_4_email]* shortcode in its email template.
  - Save form.

- **Clear inquiry cart on inquiry form submission**
  - Open inquiry form. 
  - Add *[mwqc_clear_cart]* shortcode in its confirmation template.
  - Save form.

- **Replace auto-created inquiry cart page**
  - Add *[mwqc_cart]* shortcode to new page.
  - Go to global settings as described above and select this new page in "Inquiry Cart Page" dropdown.
  - Save changes.

- **Give a custom name to inquiry cart**
  - Go to global settings as described above and input new name (e.g reservation cart) in "Inquiry Cart Name" field.
  - Save changes.

## Inquiry Form
Any shortcode-rendered form can be used as inquiry form given that it sends email to you on form submission (all popular WordPress Form plugins send email on form submission).

If you want to receive inquiry cart's content in this email, you will need to add *[mwqc_cart_4_email]* shortcode in its email template. To add this shortcode, the inquiry form should support customization of email template and interpretation of shortcode available in the email template. If any Form plugin doesn't directly let you customize email template or interpret shortcode, I shall make it work for my plugin. Please let me know!

Contact Form 7 does not interpret shortcode added to its email and confirmation templates. It has its own mail-tags which look like shortcode. My plugin has necessary code to get my *[mwqc_cart_4_email]* and *[mwqc_clear_cart]* shortcodes interpreted by Contact  Form 7.

## Shortcode Attributes
```
[mwqct_cart hide_table="1" hide_table_cols="1,2,3,4,5,6" hide_update_button="1" hide_totals="1" hide_total_rows="1,2,3"]
```

- **hide_table**
Hides the cart items table. Doesn't effect Cart Totals section. Allowed value is "1".
- **hide_table_columns**
Hides the columns of cart items table. Use comma separated column indexes as its value. There are 6 columns. Allowed value is any non-empty subset of [1,2,3,4,5,6], where 1 represents the left most column and 6 represents the right most column.
- **hide_update_button**
Hides the Update button. Allowed value is "1".
- **hide_totals**
Hides the Cart Totals section. Allowed value is "1".
- **hide_totals_rows**
Hides the rows of Cart Totals section. Use comma separated row numbers as its value. There are 3 rows, Subtotal, Tax and Total. Allowed value is any non-empty subset of [1,2,3] where 1 represents the Subtotal row and 3 represents the Total row.

## Localization
WooCommerce Product Catalog and/or Inquiry plugin is localization ready and compatible with [WPML](https://wpml.org/ "WPML Home Page").

### WPML
This section describes how to translate WooCommerce Product Catalog and/or Inquiry plugin in [WPML](https://wpml.org/ "WPML Home Page").

#### Prerequisite
- Install [WPML Multilingual CMS "Buy WPML Multilingual CMS"](https://wpml.org/purchase/) and make sure [Woocommerce Multilingual](https://wpml.org/documentation/related-projects/woocommerce-multilingual/) is activated.
- Install and optionally configure WooCommerce Product Catalog and/or Inquiry.

#### Localize Global Level Settings
1. Open "Catalog and/or Inquiry" sub-tab of Product tab on WooCommerce Settings page [Read how to open it](#global-level "Read more about how to open global settings").
2. Make sure, "Price Text" and "Inquiry Button Label" fields are not blank.
   - WPML doesn't allow translating empty fields.
   - It doesn't matter whether you leave "Enable Configuration" checked or unchecked.
![alt Global Settings of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-my-global-settings.jpg)
3. Open "String Translation" page in Dashboard (Dashboard -> WPML -> String Translation).
4. Select "admin_texts_mwqc_price_text" from "domain" dropdown to translate "Price Text".
![alt Translate Global Price Text setting of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-global-price-text-translation.jpg)
4. Select "admin_texts_mwqc_add2quote_text" from "domain" dropdown to translate "Inquiry Button Label".
![alt Translate Global Inquiry Buton Label setting of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-global-inquiry-button-label-translation.jpg)

#### Localize Product Level Settings
1. Open "Catalog and/or Inquiry" data panel on product edit screen [Read how to open it](#product-level "Read more about how to open product settings")
2. Make sure, "Price Text" and "Inquiry Button Label" fields are not blank.
   - WPML doesn't allow translating empty fields.
   - It doesn't matter whether you leave "Enable Configuration" checked or unchecked.
![alt Global Settings of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-my-product-settings.jpg)
3. Open "WooCommerce Multilingual" page in Dashboard (Dashboard -> WooCommerce -> WooCommerce Multilingual).
4. Make sure you are on Products tab.
5. Add/Edit the translation by clicking the icons in the column showing the country flags.
![alt WooCommerce Multilingual page](images/wpml-woocommerce-multilingual.jpg)
6. Depending on your WPML settings configuration, either the Advanced Translation Editor or Classic Translation Editor will open. Please note: [Advanced Translation Editor](https://wpml.org/documentation/translating-your-contents/advanced-translation-editor/ "WPML Advanced Translation Editor") is the recommended option.
7. Translate "Price Text" and "Inquiry Button Label" fields.
![alt Translate Product Settings of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-product-translation.jpg)

##### Troubleshoot
- If "Price Text" and "Inquiry Button Label" fields are not blank and Advanced Translation Editor doesn't show them, resave the product (edit it and click update - it is not necessary to change any thing).
- if above step doesn't work, open WPML settings page and make sure "\_mwqc_settings" field is set to "Translate" under "Custom Fields" section. See [Translating Custom Fields](https://wpml.org/documentation/getting-started-guide/translating-custom-fields/) in WMPL documentation for more info.

#### Localize Messages
WooCommerce Product Catalog and/or Inquiry plugin shows messages in response to user actions. For example, when user updates the inquiry cart, "Inquiry Cart updated." message is shown. You can translate these messages too.
1. Open "Theme and plugins localization" page (Dashboard -> WPML -> Theme and plugins localization).
2. Scroll down to "Strings in the plugins" section.
3. Select "WooCommerce Product Catalog and/or Inquiry" from the list.
4. Click "Scan selected plugins for strings" button at the bottom of the list.
![alt Scan Messages of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-scan-messages.jpg)
5. After scan is completed, open "String Translation" page in Dashboard (Dashboard -> WPML -> String Translation).
6. Select "ms-wc-catalog-inquiry" domain from "in domain" dropdown.
7. WPML will list only the strings of WooCommerce Product Catalog and/or Inquiry plugin.
8. Translate.
![alt Translate Messages of WooCommerce Product Catalog and/or Inquiry plugin](images/wpml-translate-messages.jpg)

**Note:** After the scan, WPML will show you two domains - ms-wc-catalog-inquiry and woocommerce - next to "WooCommerce Product Catalog and/or Inquiry" in "Strings in the plugins" section. You don't need to translate the string in woocommerce domain because their translation will be provided by the WooCommerce. WPML shows them here because they are being used in "WooCommerce Product Catalog and/or Inquiry" plugin.

## FAQS
- **How to hide inquiry form when inquiry cart is empty?**
Enclose your form's shortcode in my *[mwqc_if_non_empty_cart]* shortcode.
Example: ***[mwqc_if_non_empty_cart]***[contact-form-7 id="58"]***[/mwqc_if_non_empty_cart]***

- **How do you prevent inference of hidden-priced product's price from the inquiry cart totals?**
By replacing prices in the totals section with the price (replacement) text set in backend for that hidden-priced product.

- **If inquiry cart has multiple hidden-priced products, which product's price text is used in the inquiry cart totals?**
The text of the first hidden-priced product that was added to the inquiry cart.

- **Can customer add a hidden-priced product to shopping cart?**
Yes. If you don't want to allow it, enable "Revoke Cart" for that product.

- **Will the price of a hidden-priced product hidden or visible during checkout?**
It will be visible. Plugin doesn't disturb shopping cart and checkout form in any way. Once a product is added to cart, it can be checked out.

- **Is output of *[mwqc_cart_4_email]* shortcode plain text or HTML?**
It is HTML. If inquiry form is made in Contact Form 7, you will need to check the "Use HTML content type" checkbox on the mail tab on the form edit screen in backend. Gravity Forms by default sends HTML email.

- **Are product prices hidden/visible in the output of *[mwqc_cart_4_email]* shortcode?**
This output is a trimmed version of the inquiry cart. If a product price is hidden in the inquiry cart, it will also be hidden in the output of this shortcode. Please note, currently inquiry cart's total and tax are not available in this output.

## Changelog
**2022-03-25 - Version 1.2.2**
 - reloaded inquiry cart page when product is added to cart via ajax from inquiry cart page (e.g. cross-sells). 

**2022-03-20 - Version 1.2.1**
- Fixed compatibility of [mwqc_cart_4_email] shortcode with WooCommerce 6.3.
- [Release Notes 1.2.1](./release-notes-1.2.1.md "Release Notes 1.2.1")

**2021-11-07 - Version 1.2.0**
  - Added [mwqc_clear_cart] shortcode. This shortcode can be placed in the confirmation message of the inquiry form to clear the inquiry cart on form submission.
  - Added global setting to customize the name for inquiry cart - e.g reservation cart, inquiry basket.
  - Showed cross-sells of the inquiry cart's products on the inquiry cart page.

**2021-07-03 - Version 1.0.1**
  - Made localization ready.
  - Added WPML Compatibility.
  - Made layout of the inquiry cart configurable by hiding UI elements (e.g price column, total section) using attributes in [mwqc_cart] shortcode.

**2021-06-22 - Version 1.0.0**
  - Initial Release
