# SSL Enforcer

**SSL Enforcer** was created to make it dead simple to force SSL connections for specific subdomains in your rails application.  Although it was designed to support rails applications built with modularized sections separated by subdomains, it can also be used to force SSL connections on a single domain site as well.

## Installation

Add it to your Gemfile:

`gem "ssl_enforcer"`

And then run `bundle install` to install it.

## Usage

To use SSL Enforcer after installing it open `config/environments/production.rb` and add the following line:

```rb
# Force SSL Connections
config.middleware.use SSLEnforcer
```

This will force SSL connections for the entire application.

If you would like to force SSL connections for a specific subdomain only, you can use the `:subdomain` option:

```rb
# Force SSL Connections
config.middleware.use SSLEnforcer, :subdomain => %w( secure )
```

By specifying the *secure* subdomain as the one to force SSL on, all connections to "https://secure.mydomain.com" will be forced redirected using a 301 redirect to "https://secure.mydomain.com".  Connections to "http://www.mydomain.com/" would be left untouched.

If you have several different subdomains in your application that you would like to force SSL connections on, you can do so by providing an array of the subdomains to be enforced.

```rb
# Force SSL Connections
config.middleware.use SSLEnforcer, :subdomain => %w( secure checkout protected)
```

This will enforce SSL connections for "secure.mydomain.com", as well as "checkout.mydomain.com" and "protected.mydomain.com".

*NOTE* SSL Enforcer will not provide SSL certificates.  You should first configure your server environment to properly support SSL connections before using SSL Enforcer.

## Bug Reports

If you run into any issues feel free to create an issue on GitHub.  The more information you can provide about the issue and your environment the better.  We'll do the best we can to resolve issues quickly.

## Credit where credit is due

This Gem was inspired by [rack-www](https://github.com/stjhimy/rack-www/ "rack-www") by [stjhimy](https://github.com/stjhimy/ "Jhimy Fernandes Villar").

## License

MIT License. Copyright &copy; 2012 Digital Opera, LLC.  [www.digitalopera.com](http://www.digitalopera.com/ "Digital Opera, LLC")