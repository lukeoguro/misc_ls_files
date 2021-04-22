# Heredoc

Today I learned something new from TA Mia that I wanted to quickly jot down.
Essentially, I was staying away from using `HEREDOC` for multi-line strings because I was getting spacing issues, but after reading [Ruby Docs](https://docs.ruby-lang.org/en/2.7.0/doc/syntax/literals_rdoc.html), I now realize this can easily be resolved.

## Variations to heredoc

There are three ways of using a heredoc: `<<HEREDOC`, `<<-HEREDOC`, and `<<~HEREDOC`.
I was using `<<-HEREDOC`, but unless I flushed all strings left, the spacing would appear.
To get rid of the spacing, I had to write:

```ruby
  expected_result = <<-INDENTED_HEREDOC
This would contain specially formatted text.

That might span many lines
  INDENTED_HEREDOC
```

This isn't exactly elegant.

Instead, I can use:

```ruby
expected_result = <<~SQUIGGLY_HEREDOC
  This would contain specially formatted text.

  That might span many lines
SQUIGGLY_HEREDOC
```

This treats all my content as flush left as default.
I'll now use `<<~` primarily, and `<<-` only when I want my spacing to be preserved.
