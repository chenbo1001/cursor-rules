
# [key] 动态属性名的优点​

- 在 JavaScript/TypeScript 中，使用 [] 定义对象的动态属性（Computed Property Names）有以下几个核心优势：
- ​何时用 [] 动态属性名​​：
- 需要动态键名、枚举映射、非标识符键名或与变量绑定时。

## ✅ 优点1：当属性名需要根据变量、表达式或枚举值动态生成时

```js
// 当属性名需要根据变量、表达式或枚举值动态生成时。
const key = 'Enterprise';
const roleMap = {
  [key]: 'VIP' // 动态计算属性名
};
console.log(roleMap.Enterprise); // 输出 "VIP"
```

## ✅ 优点2：直接使用枚举值作为键​

```js
// 避免硬编码字符串（如 'enterprise'），提高代码可维护性。
// TypeScript 会检查枚举值的有效性，拼写错误会导致编译报错。
enum USER_CUSTOMER_TYPE {
  Enterprise = 'enterprise',
  Person = 'person'
}

const roleMap = {
  [USER_CUSTOMER_TYPE.Enterprise]: 'VIP', // 使用枚举值作为键
  [USER_CUSTOMER_TYPE.Person]: '普通用户'
};

// 以下两个是等价的
const obj = {
  ['key-with-hyphen']: 'value', // 合法
  ['123数字开头']: 'value'      // 合法
}

// 对象中的属性在顺序是不固定的，先安照数字排列，再按照字母排列
const obj = {
  'key-with-hyphen': 'value', // 合法
  '123数字开头': 'value'      // 合法
}

```

✅ 优点4：与解构赋值结合使用​

```js
const { [someKey]: value } = obj; // 动态解构属性
```

## ​​场景1：API 响应数据转换​

```js
const apiResponse = [
  { id: 1, type: 'admin' },
  { id: 2, type: 'user' }
];

// 转换为 { admin: { id: 1 }, user: { id: 2 } }
const result = apiResponse.reduce((acc, item) => ({
  ...acc,
  [item.type]: { id: item.id } // 动态键名
}), {});

```

## i18n映射

```js
const LANGUAGE = {
  EN: 'en',
  ZH: 'zh'
};

const translations = {
  [LANGUAGE.EN]: { hello: 'Hello' },
  [LANGUAGE.ZH]: { hello: '你好' }
};

const currentLang = LANGUAGE.ZH;
console.log(translations[currentLang].hello); // 输出 "你好"

// 动态生成样式名称
const STATUS = {
  LOADING: 'loading',
  SUCCESS: 'success'
};

function getButtonClass(status) {
  return {
    [STATUS.LOADING]: 'btn-loading',
    [STATUS.SUCCESS]: 'btn-success'
  }[status] || 'btn-default';
}

// 缓存计算结果

const cache = {};

function expensiveCalculation(input) {
  if (cache[input] !== undefined) {
    return cache[input]; // 直接返回缓存结果
  }

  const result = /* 复杂计算 */;
  cache[input] = result; // 动态键名缓存
  return result;
}

```

```js
// 假设 API 返回的数据结构如下：
const apiResponse = {
  "enterprise": "VIP",
  "person": "普通用户"
};

// 我们希望将其转换为以下结构：
const roleMap = {
  "VIP": "enterprise",
  "普通用户": "person"
};

// 使用动态属性名实现转换：

const roleMap = {};
for (const [key, value] of Object.entries(apiResponse)) {
  roleMap[value] = key;
}
```

## ​​场景2：动态添加属性​

```js
// 动态添加属性
const obj = {};
const key = 'dynamicKey';
const value = 'dynamicValue';

obj[key] = value;
console.log(obj); // 输出: { dynamicKey: 'dynamicValue' }
```
