# Gather text from multiple files

Useful if you have some code (for example a programming assessment) and you need to send through a web form with a single `textarea` input.

```sh
find . -name "*.rb" | xargs -I{} sh -c 'echo "\n# {}"  && cat {}' > ~/code.rb
```
