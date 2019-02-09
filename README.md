TypeScript tsconfig "esModuleInterop" Demo
==========================================

```
npm install
npm run demo
```

`esModuleInterop`默认为`false`，但是它是推荐设为`true`的。

原因是，如果`esModuleInterop`为`false`，typescript在处理非es module时，会有两个问题：

1. 像`util.js`这样，如果该模块是es module兼容的（表现为export出来的是一个对象而非函数），且没有提供`default`属性，
则我们必须使用`import * as x from './x'`这样的语法（必须增加`* as`），而不能像babel那样，
直接写成`import x from './x'`

2. 像`toUpper.js`这样，如果该模块是es module不兼容的，那么就不能使用`import from`的语法（否则会报一个non-module的错误），
只能使用`import x = require('./x')`。两种写法不统一

而将`esModuleInterop`设为`true`以后，这两个问题都会同时得到解决。因为typescript将采用与babel类似的做法，
自动给导入的模块增加一个`default`属性指向它自己（如果没有的`default`的话），那么我们就可以简单的采用：

```
import x from './x'
```

这种单一的写法就够了。
