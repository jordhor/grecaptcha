# grecaptcha

We are going to integrate the Google Recaptcha component into a web project without the help of any framework that does all the work for us, with a back-end using ** PHP ** and a front-end with ** jQuery **

```html
<!-- Login form -->
<form action="login.php" method="post">
    <!-- component's container -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component wrapper --> 
        <div id="login_recaptcha" class="g-recaptcha" data-sitekey=""></div>
    </div>
</form>

<!-- Register form -->
<form action="register.php" method="post">
    <!-- component's container -->
    <div class="recaptcha ctr-invalid">
        <!-- google's recaptcha component wrapper --> 
        <div id="register_recaptcha" class="g-recaptcha" data-sitekey=""></div>
    </div>
</form>
```

```php
<?php
    // NOTE: Get a key from https://www.google.com/recaptcha/admin/create
    $recaptcha_public_sitekey = '7VcngjoUKLMopP8z234cqQb-e2g9xYyogupm9KB2';
    $recaptcha_private_secretkey = "7VcngjoUKLMopBwJ234PWQVi5_to23yogvw9bYcJ";

    // Used for debug porpouses only.
    $ignore_recaptcha = false;
?>
```

