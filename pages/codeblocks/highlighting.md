# 高亮代码行

想要高亮特定行, 只需要在代码块的代码语言标识后面的第一个 `{}` 中加上行号即可. 行号默认从 1 开始, 用 `,` 分割:

```ts {2,3}
function add(
    a: Ref<number> | number,
    b: Ref<number> | number
) {
    return computed(() => unref(a) + unref(b))
}
```

使用 `|` 分隔行号则可以随着鼠标点击依此高亮这些行:

```ts {2-3|5|all}
function add(
    a: Ref<number> | number,
    b: Ref<number> | number
) {
    return computed(() => unref(a) + unref(b))
}
```

> 可以使用通配符 `*` 或关键字 `all` 来代表所有行; `hide` 隐藏代码块; `none` 不使用任何高亮.

---

# 滚动代码块

如果代码无法适应幻灯片的大小, 则可以使用 `{maxHeight: 'xxpx'}` 来设置固定高度并启用滚动:

```ts {2,3,5}{maxHeight:'100px'}
function add(
    a: Ref<number> | number,
    b: Ref<number> | number
    ) {
    return computed(() => unref(a) + unref(b))
}
/// ...很多行代码
const c = add(1, 2)
```
