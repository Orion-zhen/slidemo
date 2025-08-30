# Atomic CSS

Slidev 支持 HTML 格式, 所以可以直接在 tag 的 `class` 属性中调整元素的高度, 宽度, margin 等属性.

## 尺寸调整

前缀 `w-` 表示宽度, `h-` 表示高度. 后缀则标识要调整到的大小. 默认情况下, 后缀是一个基于 `0.25rem` (通常情况下是 `4px`) 的比例尺. 例如 `h-80` 代表高度为 $80 \times 0.25\text{rem} = 20\text{rem}$, 默认浏览器设置下应为 `320px`.

## 间距调整

前缀: `m-` 表示所有 margin 方向, `p-` 表示所有 padding 方向. 方向前缀附加在前缀后面, 有: `t` 上, `r` 右, `b` 下, `l` 左, `x` 左右, `y` 上下. 同样使用 `0.25rem` 的比例尺.

## 任意值

可以在后缀中使用中括号 `[]` 语法来指定任意值.

---

| class 示例 | 说明 |
| --- | --- |
| `w-0` | 宽度为 0 |
| `w-100px` | 宽度为 100px |
| `w-4` | 宽度为 1rem |
| `w-1/2` | 宽度为 50% |
| `w-full` | 宽度为 100% |
| `h-screen` | 高度为视口高度 |
| `h-auto` | 高度为自动 |
| `h-min-content` | 高度为最小内容高度 |

---


| class 示例 | 说明 |
| --- | --- |
| `m-0` | margin 为 0 |
| `mt-8` | margin-top 为 2rem |
| `px-4` | padding-left 和 padding-right 为 1rem |
| `py-2` | padding-top 和 padding-bottom 为 0.5rem |
| `m-auto` | margin 为自动, 常用于居中 |
| `h-[200px]` | 高度为 200px |
| `w-[calc(100%-2rem)]` | CSS 函数, 宽度为 `calc(100%-2rem)` |

---

<div class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-lg flex items-center space-x-4">
  <div class="shrink-0">
    <div class="h-12 w-12 bg-sky-500 rounded-full"></div>
  </div>
  <div>
    <div class="text-xl font-medium text-black">Live Chat</div>
    <p class="text-slate-500">You have a new message!</p>
  </div>
</div>

这是利用 Atomic CSS 语法创建的一个卡片. 其中用到的相关语法:

- `p-6`: 内边距为 6
- `max-w-sm`: 使用最大宽度
- `mx-auto`: 水平居中
- `bg-white`: 背景色为白色
- `h-12`: 高度为 3rem
- `w-12`: 宽度为 3rem
