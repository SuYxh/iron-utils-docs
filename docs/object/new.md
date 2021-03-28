---
title: 模拟new
---

## 模拟new

### API 相关

- 语法: newInstance(Fn, ...args)
- 功能: 创建Fn构造函数的实例对象
- 实现: 创建空对象obj, 调用Fn指定this为obj, 返回obj

### 编码实现

- `src/object/newInstance.js`

```js
export function newInstance(Fn, ...args) {
  // 创建一个新的对象
  const obj = {}
  // 执行构造函数
  const result = Fn.apply(obj, args) // 相当于: obj.Fn()
  // 如果构造函数执行的结果是对象, 返回这个对象
  if (result instanceof Object) {
    return result
  }
  // 如果不是, 返回新创建的对象
  obj.__proto__.constructor = Fn // 让原型对象的构造器属性指向Fn
  // 返回对象
  return obj
}
```

### 测试

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>自定义new</title>
</head>
<body>
  <script src="../dist/atguigu-utils.js"></script>
  <script>
    function Person(name, age) {
      this.name = name
      this.age = age
      // return {}
      // return []
      // return function (){}
      // return 1
      // return undefined
    }

    const p = new Person('tom', 12)
    console.log(p)

    const p2 = aUtils.newInstance(Person, 'Jack', 13)
    console.log(p2, p2.constructor)
  </script>
</body>
</html>
```
