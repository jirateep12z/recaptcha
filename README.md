## 🐲 requirement

- client side key
- Server side key

## 😺 apply at

https://www.google.com/recaptcha/admin/create | https://www.google.com/recaptcha/admin/

Load the JavaScript API with your client-side key.

```html
<script async src="https://www.google.com/recaptcha/api.js?render=(client side key)></script>
```

## 🐮 reCAPTCHA v2

Box code to confirm, paste it in the desired location.

```html
<div class="g-recaptcha" data-sitekey="(client side key)"></div>
```

## 🐎 reCAPTCHA v3

Add an attribute to your button.

```html
<button class="g-recaptcha" data-sitekey="(client side key)" data-callback="onSubmit" data-action="submit">Submit</button>
```

Server side code (php) / (javascript)

```php
// php
<?php
define("secretkey", "Server side key");
$result = recaptcha();
if ($result["success"]) {
    // Added what to do when verified correctly
} else {
    // Added what to do when incorrect identity verification
}

function recaptcha() {
	$options = [
		"secret" => secretkey,
		"response" => filter_input(INPUT_POST, "g-recaptcha-response"),
		"remoteip" => $_SERVER["REMOTE_ADDR"]
	];
	$url = "https://www.google.com/recaptcha/api/siteverify?" . http_build_query($options);
	$result = json_decode(file_get_contents($url), true);
	return $result;
}
?>
```
```js
// javascript
(() => {
	grecaptcha.ready(function () {
		grecaptcha.execute("Server side key", { action: "submit" }).then(function (token) {
			console.log(token);
		});
	});
})();
```

🙏 Thank Ref : [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display) | [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)
