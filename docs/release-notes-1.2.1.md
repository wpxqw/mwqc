**Enviornment**
- WooCommerce 6.3 or later
- WooCommerce Product Catalog and/or Inquiry 1.2 or earlier

**Details**

When inquiry form created using Contact Form 7 (or any other form plugin which uses WP REST API to submit form) is submitted by a logged in user, [mwqc_cart_4_email] shortcode outputs empty cart. It works correctly for guest user and inquiry form created using Gravity Forms, Ninja Forms and WP Forms though.

**Diagnosis**

WooCommerce 6.3 introduced following change:
- Security - Add prefix to identify guest sessions
This change was causing empty cart in the email when the inquiry form is submitted using REST API (like Contact Form 7) by a logged in user.

**Fix**

Made minor change in code to fix it.

**Developer notes**

WooCommerce 6.3 added new code in session handler class to validate session cookie and prefix guest session key by 't_'. This validation was failing for CF7 b/c of its REST based form submission. On validation failure, session was being destroyed and a new guest session was being created which was resulting in empty cart as the cart is initialized after session init while parsing CF7 mail tags.
