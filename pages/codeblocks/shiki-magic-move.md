# Shiki Magic Move

[Shiki Magic Move](https://github.com/shikijs/shiki-magic-move) 可以通过动画控制代码块的过渡. 使用 "````md magic-move" 包裹每个步骤的代码块, 使其变为一个根据动画步骤变化的大代码块:

````md magic-move
```js
// step 1
const author = reactive({
    name: 'Orion',
    books: ['Slidev', 'Vue', 'Vite']
})
```
代码块之间的内容视为注释, 被忽略
```js {2|3,4|6|all}
// step 2
export default {
    data() {
        return {
            author: {
                name: 'Orion',
                books: ['Slidev', 'Vue', 'Vite']
            }
        }
    }
}
```
```js
// step 3
export default {
    data: () => ({
        author: {
            name: 'Orion',
            books: ['Slidev', 'Vue', 'Vite']
        }
    })
}
```
```html
<!-- step 4 -->
<script setup>
const author = {
    name: 'Orion',
    books: ['Slidev', 'Vue', 'Vite']
}
</script>
```
````

Magic Move 还可以与高亮代码行以及显示行号混合使用:

````md magic-move {at:4, lines: true}
```js {*|1|2-5}
let count = 1
function add() {
    count++
}
```

在代码块之间的内容会被忽略，可以作为注释。

```js {*}{lines: false}
let count = 1
const add = () => count += 1
```
````
