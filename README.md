Single Sign-On for PHP (Ajax compatible)
---

This sso client it is based on the [LegalThings/SSO](https://github.com/legalthings/sso) developed by [Jasny](https://github.com/jasny).

For a more indepth explanation of the SSO implementation, please [read this article](https://github.com/jasny/sso/wiki)


## Installation

Install this library through composer

    composer require sal/sso

## Usage

### Broker (Client)

When creating a Jasny\SSO\Broker instance, you need to pass the server url, broker id and broker secret. The broker id
and secret needs to be registered at the server (so fetched when using `getBrokerInfo($brokerId)`).

**Be careful**: *The broker id SHOULD be alphanumeric. In any case it MUST NOT contain the "-" character.*

Next you need to call `attach()`. This will generate a token an redirect the client to the server to attach the token
to the client's session. If the client is already attached, the function will simply return.

When the session is attached you can do actions as login/logout or get the user's info.

```php
$broker = new Jasny\SSO\Broker($serverUrl, $brokerId, $brokerSecret);
$broker->attach();

$user = $broker->getUserInfo();
echo json_encode($user);
```

For more information, checkout the `broker` and `ajax-broker` example.

## Examples

There is two example brokers. One with normal redirects and one using
[JSONP](https://en.wikipedia.org/wiki/JSONP) / AJAX.

To proof it's working you should setup the server and two or more brokers, each on their own machine and their own
(sub)domain. However you can also run both server and brokers on your own machine, simply to test it out.

On *nix (Linux / Unix / OSX) run:

    $ export SSO_SERVER=https://yourclub.socialandloyal.com
    $ export SSO_BROKER_ID={id in your club config}
    $ export SSO_BROKER_SECRET={secret in your club config}
    
    $ php -S localhost:9001 -t examples/broker/
    $ php -S localhost:9002 -t examples/ajax-broker/

Now open some tabs and visit http://localhost:9001, http://localhost:9002.

_Note that after logging in, you need to refresh on the other brokers to see the effect._

##Notes

- This is only for login and logout to be able to register new clients you need to use SAL api 
