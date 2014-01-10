# mate的一些配置

# 查看
`dconf-editor`

> http://www.reddit.com/r/linux4noobs/comments/1kss09/keyboard_shortcuts_command/

比如"键盘快捷键(mate-keybinding-properties)"的配置

`/org/mate/desktop/keybindings/`

# 重置为默认
```
dconf reset -f /org/mate/desktop/keybindings/
```

# 文件位置

a single file located at ~/.config/dconf/user - you cannot edit that directly, but either via dconf-editor or 