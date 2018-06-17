Single Sign-On for PHP (Ajax compatible)
---

This sso client it is based on the [LegalThings/SSO](https://github.com/legalthings/sso) developed by [Jasny](https://github.com/jasny).

For a more indepth explanation of the SSO implementation, please [read this article](https://github.com/jasny/sso/wiki)


## Installation

Install this library through composer

    composer require smoothbytes/sso

## Usage

### Broker (Client)

When creating a Jasny\SSO\Broker instance, you need to pass the server url, broker id and broker secret. The broker id
and secret needs to be registered at the server (so fetched when using `getBrokerInfo($brokerId)`).

**Be careful**: *The broker id SHOULD be alphanumeric. In any case it MUST NOT contain the "-" character.*

Next you need to call `attach()`. This will generate a token an redirect the client to the server to attach the token
to the client's session. If the client is already attached, the function will simply return.

When the session is attached you can do actions as login/logout or get the user's info.

```php
$broker = new Sal\SSO\Broker($serverUrl, $brokerId, $brokerSecret);
$broker->attach();

$user = $broker->getUserInfo();
echo json_encode($user);
```

For more information, checkout the `broker` and `ajax-broker` examples in [sso-examples](https://github.com/SmoothBytes/sso-examples).


##Notes

- This is only for login and logout to be able to register new clients you need to use SAL api 