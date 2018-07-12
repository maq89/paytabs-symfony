# Paytabs Symfony

## Installation
Begin by installing this package through Composer. Just run following command to terminal-

```php
composer require maq89/paytabs-symfony
```

Enable the bundle in the kernel, goto app/AppKernel.php
```php
$bundles = array(
	// ...
	new Damas\PaytabsBundle\DamasPaytabsBundle(),
	// ...
);
```


## Example:
### Create Payment Page:
```php
$pt = Paytabs::getInstance("MERCHANT_EMAIL", "SECRET_KEY");
$result = $pt->create_pay_page(array(
	"merchant_email" => "MERCHANT_EMAIL",
	'secret_key' => "SECRET_KEY",
	'title' => "John Doe",
	'cc_first_name' => "John",
	'cc_last_name' => "Doe",
	'email' => "customer@email.com",
	'cc_phone_number' => "973",
	'phone_number' => "33333333",
	'billing_address' => "Juffair, Manama, Bahrain",
	'city' => "Manama",
	'state' => "Capital",
	'postal_code' => "97300",
	'country' => "BHR",
	'address_shipping' => "Juffair, Manama, Bahrain",
	'city_shipping' => "Manama",
	'state_shipping' => "Capital",
	'postal_code_shipping' => "97300",
	'country_shipping' => "BHR",
	"products_per_title"=> "Mobile Phone",
	'currency' => "BHD",
	"unit_price"=> "10",
	'quantity' => "1",
	'other_charges' => "0",
	'amount' => "10.00",
	'discount'=>"0",
	"msg_lang" => "english",
	"reference_no" => "1231231",
	"site_url" => "https://your-site.com",
	'return_url' => "http://127.0.0.1:8000/paytabs-response",
	"cms_with_version" => "API USING PHP"
));


if($result->response_code == 4012){
	return $this->redirect($result->payment_url);
}
else{
	throw new \Exception($result->result);	
}
```
### Verify Payment:
```php
$pt = Paytabs::getInstance("MERCHANT_EMAIL", "SECRET_KEY");
$result = $pt->verify_payment($request->request->get('payment_reference'));
if($result->response_code == 100){
	// Payment Success
}
else{
	throw new \Exception($result->result);	
}

```
