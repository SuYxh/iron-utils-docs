---
title : 模拟instanceof
---

## 模拟instanceof

### API 相关

- 语法: myInstanceOf(obj, Type)
- 功能: 判断obj是否是Type类型的实例
- 实现: Type的原型对象是否是obj的原型链上的某个对象, 如果是返回tru, 否则返回false

### 编码实现

- `src/object/myInstanceOf.js`

```js
export function myInstanceOf(obj, Type) {
  // 得到原型对象
  let protoObj = obj.__proto__

  // 只要原型对象存在
  while(protoObj) {
    // 如果原型对象是Type的原型对象, 返回true
    if (protoObj === Type.prototype) {
      return true
    }
    // 指定原型对象的原型对象
    protoObj = protoObj.__proto__
  }
  
  return false
}
```

### 测试

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>自定义instanceof</title>
</head>
<body>
  <script src="../dist/atguigu-utils.js"></script>
  <script>
    function Person(name, age) {
      this.name = name
      this.age = age
    }
    const p = new Person('tom', 12)
    
    console.log(aUtils.myInstanceOf(p, Object), p instanceof Object)
    console.log(aUtils.myInstanceOf(p, Person), p instanceof Person)
    console.log(aUtils.myInstanceOf(p, Function), p instanceof Function)
  </script>
</body>
</html>
```