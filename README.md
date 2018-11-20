# Google Recaptcha

![component](/grecaptcha-light.png "Google recaptcha component")

Integrating the Google Recaptcha component into a web project with a `PHP` back-end and a front-end using `jQuery`.

In this example we'll use two google recaptcha components in the same page, one for the shopping cart form and one for the user registration form.

## Front-end

`cart.php`
```html
<!-- Shooping cart form -->
<form id="frm-shopping-cart" action="cart.php" method="post">
    <!-- our component's wrapper -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component container --> 
        <div id="cart_recaptcha" class="g-recaptcha" data-sitekey=""></div>
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

We declare a `div` as a container where google will render the component, with a class `g-recaptcha` that we'll use only for DOM selection purposes. We use another parent `div` as the component's wrapper for validation purposes as well. The classes `ctr-valid` and `ctr-invalid` are established depending on whether the validation has been passed. In order to establish different classes names we can use the options passed in constructor function ([see below for details](#Constructor-options "constructor options") ).
```css
.recaptcha {
    margin: 20px 0px 10px;
    text-align: center;
}
```

 

`cart.js`
```javascript
cart.recaptcha = new gRecaptcha({
    wrapper: '.frm-shopping-cart .recaptcha',
    selector: 'cart_recaptcha',
    theme: 'dark',

    onload: function() {
        // console.log('cart.recaptcha -> onload');
    },

    success: function() {
        // console.log('cart.recaptcha -> success');
        var frm = $('.frm-cart-register'); if (frm.length) {
            cart.validate(frm);
            cart.refresh(frm);
        }
    },

    expired: function() {
        // console.log('cart.recaptcha -> expired');
        var frm = $('.frm-cart-register'); if (frm.length) {
            cart.validate(frm);
            cart.refresh(frm);
        }
    }
});
```

`user.js`
```javascript
user.recaptcha = new gRecaptcha({
    wrapper: '.frm-user-register .recaptcha',
    selector: 'register_recaptcha',
    theme: 'dark',

    onload: function() {
        // console.log('user.recaptcha -> onload');
    },

    success: function() {
        // console.log('user.recaptcha -> success');
        var frm = $('.frm-user-register'); if (frm.length) {
            user.validate(frm);
            user.refresh(frm);
        }
    },

    expired: function() {
        // console.log('user.recaptcha -> expired');
        var frm = $('.frm-user-register'); if (frm.length) {
            user.validate(frm);
            user.refresh(frm);
        }
    }
});
```


## Back-end

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


### Constructor options

```javascript
{
    wrapper: '.recaptcha',
    selector: 'recaptcha',
    theme: 'light',
    valid: 'ctr-valid',
    invalid: 'ctr-invalid',   
    onload: function() { ... },
    success: function() { ... },
    expired: function() { ... }
}
```
