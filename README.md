# Google Recaptcha

Integrating the Google Recaptcha component into a web project with a `PHP` back-end and a front-end using `jQuery`.

![component](/grecaptcha-light.png "Google recaptcha component")

In this example we'll use two google recaptcha components in the same scope (one for the shopping cart form and one for the user registration form).

`cart.php`
```html
<!-- Shooping cart form -->
<form id="frm-shopping-cart" action="cart.php" method="post">
    <!-- our component's wrapper -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component container --> 
        <div id="login_recaptcha" class="g-recaptcha" data-sitekey=""></div>
    </div>
</form>

<!-- Register form -->
<form class="frm-user-register" action="api/register.php" method="post">
    <!-- our component's wrapper -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component container --> 
        <div id="register_recaptcha" class="g-recaptcha" data-sitekey=""></div>
    </div>
</form>
```

The `div` component container has validation purposes as well. Instead, the wrapper class is only used as a selector to initialize all the recaptcha components of the current page all at once.
```css
.recaptcha {
    margin: 20px 0px 10px;
    text-align: center;
}
```

Store our keys in a server file like `/recaptcha/keys.php`.
```php
<?php
    // NOTE: Get a key from https://www.google.com/recaptcha/admin/create
    $recaptcha_public_sitekey = '7VcngjoUKLMopP8z234cqQb-e2g9xYyogupm9KB2';
    $recaptcha_private_secretkey = "7VcngjoUKLMopBwJ234PWQVi5_to23yogvw9bYcJ";

    // Used for debug porpouses only.
    $ignore_recaptcha = false;
?>
```

`user.js`
```javascript
(function(user, $, window, undefined) {
    user.recaptcha = function() { ... }
}(window.user = window.user || {}, jQuery, window));
```

`user.js`
```javascript
user.recaptcha = new gRecaptcha({
    wrapper: '.frm-user-register .recaptcha',
    selector: 'register_recaptcha',
    theme: 'dark',

    onload: function() {
        console_log('user.recaptcha -> onload');
    },

    success: function() {
        // console_log('user.recaptcha -> success');
        var frm = $('.frm-user-register'); if (frm.length) {
            user.validate(frm);
            user.refresh(frm);
        }
    },

    expired: function() {
        // console_log('user.recaptcha -> expired');
        var frm = $('.frm-user-register'); if (frm.length) {
            user.validate(frm);
            user.refresh(frm);
        }
    }
});
```
