## Build Instructions

Build using standard hugo theme method

```
$ hugo new site website
$ cd website
$ git clone https://github.com/krish-iyer/krish-iyer.github.io.git theme/focusreadability
```

Now, add this to hugo.toml. Otherwise HTML code in the markdown won't be rendered. I have added this in theme's toml file but seems like it has to added in the website's toml.

```
theme = 'focusreadability'

[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
    [markup.goldmark.extensions]
      [markup.goldmark.extensions.passthrough]
        enable = true
        [markup.goldmark.extensions.passthrough.delimiters]
          block = [['\[', '\]'], ['$$', '$$']]
          inline = [['\(', '\)']]
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 4
 
```
