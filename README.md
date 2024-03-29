# ashokvarma.com

Blog posts, presentations, podcasts, and other things...

# Development

Ensure you have the correct version of Ruby installed (per `.ruby-version`). Also ensure you have the Bundler gem installed.

## Ruby Setup
`brew install chruby ruby-install`
add following to .zshrc
```zsh
source /opt/homebrew/opt/chruby/share/chruby/chruby.sh
source /opt/homebrew/opt/chruby/share/chruby/auto.sh
```
Install latest ruby
`ruby-install ruby`
`ruby-install <version from .ruby-version>`
Navigate to folder and Change version of ruby
`chruby <version from .ruby-version>`

## One-time setup

    bundle install --path vendor/bundle

_Note: If you're on Mac OS and this fails installing nokogiri, run `brew unlink xz`, install, and then `brew link xz`._

## Running the site

Local development:
    `bundle exec jekyll serve`

Update (dependencies) GitHub Pages gem:
    `bundle update github-pages`
    `bundle update --bundler`

# License

The content of the site (blog posts, presentation slides, etc.) are licensed as [Creative Commons CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode).

The code powering the site is licensed as:

    Copyright 2017 Ashok Varma

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
