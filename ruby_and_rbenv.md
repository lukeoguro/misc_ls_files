# Ruby and rbenv

I thought installing Ruby on the M1 Mac would be complicated, but it turned out to be much easier than expected!

## Installing Ruby with Homebrew

Follow [documentation](https://brew.sh/) to install Homebrew if you haven't already. Installing Command Line Tools for Xcode might also be necessary with:

```shell
xcode-select --install
```

Then, run:

```shell
brew install ruby
```

The documentation for this can be found [here](https://formulae.brew.sh/formula/ruby#default).
Be sure to have Ruby first in your path, so the shell doesn't run the system version of Ruby.

```shell
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
```

I didn't have any issues with having to installing Rosetta 2 (for now).

## Using rbenv to run multiple versions of Ruby

[Rbenv](https://github.com/rbenv/rbenv) can be helpful when running multiple versions of Ruby.
To install, run:

```shell
brew install rbenv
```

This will also install `ruby-build` by default.
Then, run `rbenv init`, which will tell you to append some code to `~/.zshrc`.
You can do this with:

```shell
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
```

Now that you're done installing rbenv, you can install various versions of Ruby.
You can list the available versions with `rbenv install -l`, and install with:

```shell
rbenv install 3.0.0
```

You can set your preferred Ruby version with:

```shell
rbenv global 3.0.0
````

This will write the default version to `~/.rbenv/version`.
(Note that this can be overrode with `rbenv local 3.0.0`, which writes the version to `.ruby-version` in the current directory, or `rbenv shell 3.0.0`, which sets a shell-specific Ruby version).

You can confirm the default Ruby and see which versions are installed with:

```shell
rbenv versions
```

Confirming which Ruby version is running with `rbenv which` can be helpful too.

```shell
rbenv which ruby
rbenv which irb
```
