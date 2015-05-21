# css-splitter-gem
Standalone gem for CSS splitter.
Mega-props to https://gist.github.com/10thfloor/3559165. 

Simply abstracts the config into a gem that can be included in config.rb file.

# Usage


On config.rb, ensure you include:

```
on_stylesheet_saved do |path|
  CssSplitter.split(path) unless path[/\d+$/]
end
```