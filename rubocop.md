# Rubocop

A quick writeup on Rubocop and the steps I took to install it.

## Installing Rubocop

Use the code below to install Rubocop.
Launch School asks for version `0.86.0`, which is why we specify this below.

```shell
gem install rubocop --version 0.86.0
```

## A quick tutorial

To use Rubocop, simply type the command `rubocop file_name.rb`.
To find which cop complained, we can use:

```shell
rubocop hello.rb --format offenses
```

In any case you want to find which config file is being used, run:

```shell
rubocop -d
```
