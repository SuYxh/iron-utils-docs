---
title: 合并多个对象
---

## 合并多个对象

### API 相关

- 语法: object mergeObject(...objs)
- 功能: 合并多个对象, 返回一个合并后对象(不改变原对象)
- 例子: 
  - { a: [{ x: 2 }, { y: 4 }], b: 1}
  - { a: { z: 3}, b: [2, 3], c: 'foo'}
  - 合并后: { a: [ { x: 2 }, { y: 4 }, { z: 3 } ], b: [ 1, 2, 3 ], c: 'foo' }

### 编码实现

- `src/object/mergeObject.js`

```js
export function mergeObject(...objs) {
  return objs.reduce((pre, obj) => {
    return Object.keys(obj).reduce((p, key) => {
      p[key] = !p.hasOwnProperty(key) ? obj[key] : [].concat(p[key], obj[key])
      return p
    }, pre)
  }, {})
}
```

### 测试

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>合并多个对象</title>
</head>
<body>
  <script src="../dist/atguigu-utils.js"></script>
  <script>
    const object = {
      a: [{ x: 2 }, { y: 4 }],
      b: 1
    }
    const other = {
      a: { z: 3},
      b: [2, 3],
      c: 'foo'
    }
    console.log(aUtils.merge(object, other)) 
  </script>
</body>
</html>
```