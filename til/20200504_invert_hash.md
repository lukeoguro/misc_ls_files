# Swapping keys and values in a hash

I decided to start writing down some tips and tricks I learn while I code.
The first one is, how do you swap keys and values in a hash?

You could use the `#map` method, but what's easier is:

```ruby
hash.invert
```

You'll run into issues if some keys have the same values, so beware.
