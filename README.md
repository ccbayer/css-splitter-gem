# css-splitter-gem
Standalone gem for CSS splitter code that simply abstracts the config into a gem that can be included in config.rb.

Props to https://gist.github.com/10thfloor/3559165 from which the code was entirely lifted.
All this gem does is saves the convenience of having to add a lot of code into the config file.


# Usage

If your CSS files are bloated and large, they may not render on IE 9 and lower, due to a limit on the number of CSS selectors the browser will render (4095). This utility keeps track of your selector count for you and will split the files at the appropriate place.

# Resources & Additional Tools
http://blogs.msdn.com/b/ieinternals/archive/2011/05/14/10164546.aspx
http://support.microsoft.com/kb/262161


Another resource works slightly differently and is based on node.js:
http://blesscss.com

# Implementation

On config.rb, ensure you include the following:

* to include in the configuration
```
gem 'css-splitter', '=0.0.1'
require 'css-splitter'
```

* to automatically execute the command after compass does its thing:
```
on_stylesheet_saved do |path|
  CssSplitter.split(path) unless path[/\d+$/]
end
```

## Example

* Stylesheet has 5,000 selectors
* `css-splitter` will split this into 2 files:
** css-file.css = full file (will work on modern browsers)
** css-file-1.css = will contain the remaining 5 CSS selectors
* Manually, on your layouts, you will need to include the additional CSS inside of IE conditional tags:

```
<!-- first css contains all css and will work on all new browsers -->
<link href="path-to-css/css-file.css" type="text/css" rel="stylesheet"/> 
<!--[if lte IE 9]>
<link href="path-to-css/css-file-1.css" type="text/css" rel="stylesheet"/>
<![endif]-->
```


