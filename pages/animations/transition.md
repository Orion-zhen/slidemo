# 过渡动画

在 frontmatter 中可以为每张幻灯片设置切换动画, 在 headmatter 中设置全局动画. 在第 x 张幻灯片中设置的切换动画将作用于从第 x 张切换到第 x+1 张. Slidev 内置的切换动画有:

- `fade`: 淡入淡出
- `fade-out`: 淡出再淡入
- `slide-left`: 从左侧滑出
- `slide-right`: 从右侧滑出
- `slide-up`: 从上方滑出
- `slide-down`: 从下方滑出
- `view-transition`: 使用 View Transitions API 过渡

---

```yaml
layout: statement
transition: fade
```

# `fade`

---

```yaml
layout: statement
transition: fade-out
```

# `fade-out`

---

```yaml
layout: statement
transition: slide-left
```

# `slide-left`

---

```yaml
layout: statement
transition: slide-right
```

# `slide-right`

---

```yaml
layout: statement
transition: slide-up
```

# `slide-up`

---

```yaml
layout: statement
transition: slide-down
```

# `slide-down`
