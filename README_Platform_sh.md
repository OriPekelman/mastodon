# Mastodon on Platform.sh

To make this more easily updatable from upstream, until we figure-out the libidn question we:

1. Most everything is configured .environment
2. Some environment variables set through the API (vapid)

# Specificities

You may need to set
``` 
platform project:variable:set env.SECRET_KEY_BASE 4809d{redacted.. choose your own please}bfe107
```
prior to build as devise requires this.


After install you can create a first user:
```
RAILS_ENV=production bin/tootctl accounts create \
  alice \
  --email alice@example.com \
  --confirmed \
  --role Owner
```

OR

```
RAILS_ENV=production bin/tootctl accounts modify alice --role Owner
```
