# 创建模式

创建模式侧重于如何实例化一个对象或一组相关对象。

## 单例模式

单例模式确保只能创建特定类的一个实例对象。

**代码实现**

```js
class Singleton {
  static #instance = null;

  static getInstance() {
    if (Singleton.#instance) {
      return Singleton.#instance;
    }

    Singleton.#instance = new Singleton();
    return Singleton.#instance;
  }

  constructor() {}
}

let s1 = Singleton.getInstance();
let s2 = Singleton.getInstance();
console.log(s1 === s2); // 输出：true
```

**应用**
当一个类必须只有一个实例，而且客户代码只能从一个公开的地方访问它。
例如：

- 管理日志的类
- 管理数据库连接的类
- 管理文件系统的类

## 简单工厂

提供一个封装在名为工厂的类中的静态方法，以隐藏实现逻辑，并使客户端代码专注于使用，而不是初始化新对象。

```js
class WoodDoor {
  constructor() {}

  getName() {
    return 'wood door';
  }
}

class IronDoor {
  constructor() {}

  getName() {
    return 'iron door';
  }
}

class DoorFactory {
  static getDoor(type) {
    switch (type) {
      case 'wood': {
        return new WoodDoor();
      }
      case 'iron': {
        return new IronDoor();
      }
      default:
        return null;
    }
  }
}

let d = DoorFactory.getDoor('wood');
console.log(d.getName()); // 输出：wood door
```

**应用**
当你只关心对象的创建，而不关心如何创建和管理它时，可以使用工厂模式。
