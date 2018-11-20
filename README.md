# Google Recaptcha

Integrating the Google Recaptcha component into a web project with a `PHP` back-end and a front-end using `jQuery`.

![component](/grecaptcha-light.png "Google recaptcha component")

In this example we'll use two google recaptcha components (one for the login form and one for the registration form).

`user.html`
```html
<!-- Login form -->
<form action="api/login.php" method="post">
    <!-- component's container -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component wrapper --> 
        <div id="login_recaptcha" class="g-recaptcha" data-sitekey=""></div>
    </div>
</form>

<!-- Register form -->
<form action="api/register.php" method="post">
    <!-- component's container -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component wrapper --> 
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

