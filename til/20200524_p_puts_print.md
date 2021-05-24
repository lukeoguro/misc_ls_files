# `p`, `puts` and `print`

I missed an easy question about `p` in one of the study sessions, so I wanted to write a quick post to make sure I understand these 3 methods.

## `p`

The method `#p` takes parameter `obj` and directly writes `obj.inspect` to the output.
The return value is `obj`.

## `puts`

The method `#puts` takes parameter `obj` and prints `obj.to_s` to the output followed by a newline sequence.
The return value is always `nil`.

## `print`

The method `#print` is almost the same as `#puts`, but doesn't print a newline sequence.
The return value is also `nil`.
