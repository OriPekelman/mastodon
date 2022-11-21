# Mastodon on Platform.sh

This comes with just a bit of bells and whistles:

1. Redis, Elastic Search and an NFS service for locally storing uploaded assets
2. Configured Sidekiq

## Configuration

1. Most everything is configured `.environment`
2. Some environment variables set through the API - see "Getting Started"

## Getting started

Please set secrets with:

``` 
platform project:variable:set env:SECRET_KEY_BASE {redacted.. choose your own please}
platform project:variable:set env:OTP_SECRET {redacted.. choose your own please}
```

prior to build as devise requires this. 

And use:

```
rake mastodon:webpush:generate_vapid_key
```

to set values for:

```
platform project:variable:set env:VAPID_PRIVATE_KEY {redacted.. see above}
platform project:variable:set env:VAPID_PUBLIC_KEY {redacted.. see above}
```

After install you can create a first user:
```
platform ssh
bin/tootctl accounts create \
  alice \
  --email alice@example.com \
  --confirmed \
  --role Owner
```

OR

```
platform ssh bin/tootctl accounts modify alice --role Owner
```

## Change paranoid defaults

In `.environment` you should comment the following lines to be able 
to get out of single user mode and to start federating.

```
export DISALLOW_UNAUTHENTICATED_API_ACCESS=true
export SINGLE_USER_MODE=true
```
