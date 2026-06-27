# Creating a Theme for Your Workshop!

## What we've set in this template
At the moment, the repo is loaded with the themes provided by mdbook, with the default set to `coal`.
If you wish to change to another one of the default themes, feel free to make that change in `book.toml`. All the themes should be in `theme/css/variables.css`. That leads us onto the next part...

## Creating your own custom theme!
In `theme/css/variables.css`, there's an extra theme called `.workshop`. Feel free to experiment and play around with the colours in this block. If you choose to use this for your workshop, update the `default_theme` entry in `book.toml`, and replace the name with whatever you want in `theme/index.hbs`. Also uncomment the below code block:
```css
{{!-- Enable your custom theme here! --}}
{{!-- <li role="none"><button role="menuitem" class="theme" id="mdbook-theme-workshop">Your Custom Theme</button></li> --}}
```

## Poco Cursor
By default, we have a Poco cursor enabled in the template. If you want to remove it, head over to `theme/variables.css` and set the below variables to `auto`:
```css
--plain-poco-cursor: url("../assets/plain-poco-xs.png"), auto;
--active-poco-cursor: url("../assets/active-poco-xs.png"), auto;
```