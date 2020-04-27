> 根据 https://github.com/ryanmcdermott/clean-code-javascript#table-of-contents
> 总结的一些常用的编码规范
> 上面是 bad，下面是 good

**对功能类似的变量名采用统一的命名风格**
> 我在业务代码中，似乎一直忠于第一种写法，得改改了
```js
getUserInfo();
getClientData();
getCustomerRecord();
-----------------------
getUser();
```

**使用易于检索名称**
> 命名别怕长，一定要能懂
```js
// 525600 是什么?
for (var i = 0; i < 525600; i++) {
  runCronJob();
}
-==========================
var MINUTES_IN_A_YEAR = 525600;
for (var i = 0; i < MINUTES_IN_A_YEAR; i++) {
  runCronJob();
}
```

**使用说明变量(即有意义的变量名)**
> 别为了省代码
```js
const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
saveCityState(cityStateRegex.match(cityStateRegex)[1], cityStateRegex.match(cityStateRegex)[2]);
---------------
const ADDRESS = 'One Infinite Loop, Cupertino 95014';
var cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
var match = ADDRESS.match(cityStateRegex)
var city = match[1];
var state = match[2];
saveCityState(city, state);
```

**避免无意义的条件判断**
```js
function createMicrobrewery(name) {
  var breweryName;
  if (name) {
    breweryName = name;
  } else {
    breweryName = 'Hipster Brew Co.';
  }
}
==================
function createMicrobrewery(name) {
  var breweryName = name || 'Hipster Brew Co.'
}
```

**函数功能的单一性**
> 特别是 vue 一些请求函数中，容易会写很多厚重的代码，职责声明很重要呀
```js
function emailClients(clients) {
  clients.forEach(client => {
    let clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
================================================================
function emailClients(clients) {
  clients.forEach(client => {
    emailClientIfNeeded(client);
  });
}

function emailClientIfNeeded(client) {
  if (isClientActive(client)) {
    email(client);
  }
}

function isClientActive(client) {
  let clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

**函数应该只做一层抽象**
> 当函数的需要的抽象多于一层时通常意味着函数功能过于复杂，需将其进行分解以提高其可重用性和可测试性。
```js
function parseBetterJSAlternative(code) {
  let REGEXES = [
    // ...
  ];

  let statements = code.split(' ');
  let tokens;
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    })
  });

  let ast;
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  })
}
================================================================
function tokenize(code) {
  let REGEXES = [
    // ...
  ];

  let statements = code.split(' ');
  let tokens;
  REGEXES.forEach((REGEX) => {
    statements.forEach((statement) => {
      // ...
    })
  });

  return tokens;
}

function lexer(tokens) {
  let ast;
  tokens.forEach((token) => {
    // lex...
  });

  return ast;
}

function parseBetterJSAlternative(code) {
  let tokens = tokenize(code);
  let ast = lexer(tokens);
  ast.forEach((node) => {
    // parse...
  })
}
```

**移除重复的代码**
> 我学习前端时间不长，代码质量挺差的，感觉，因为也容易被喷；这个也是我经常犯的错误
> 永远、永远、永远不要在任何循环下有重复的代码。重复的代码意味着逻辑变化时需要对不止一处进行修改
```js
function showDeveloperList(developers) {
  developers.forEach(developer => {
    var expectedSalary = developer.calculateExpectedSalary();
    var experience = developer.getExperience();
    var githubLink = developer.getGithubLink();
    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      githubLink: githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    var expectedSalary = manager.calculateExpectedSalary();
    var experience = manager.getExperience();
    var portfolio = manager.getMBAProjects();
    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      portfolio: portfolio
    };

    render(data);
  });
}
==================
function showList(employees) {
  employees.forEach(employee => {
    var expectedSalary = employee.calculateExpectedSalary();
    var experience = employee.getExperience();
    var portfolio;

    if (employee.type === 'manager') {
      portfolio = employee.getMBAProjects();
    } else {
      portfolio = employee.getGithubLink();
    }

    var data = {
      expectedSalary: expectedSalary,
      experience: experience,
      portfolio: portfolio
    };

    render(data);
  });
}
```

**采用默认参数精简代码**
```js
function writeForumComment(subject, body) {
  subject = subject || 'No Subject';
  body = body || 'No text';
}
==================
function writeForumComment(subject = 'No subject', body = 'No text') {
  ...
}
```

**使用 Object.assign 设置默认对象**
> 这个例子对我打击很多，因为我很容易犯错
```js
var menuConfig = {
  title: null,
  body: 'Bar',
  buttonText: null,
  cancellable: true
}

function createMenu(config) {
  config.title = config.title || 'Foo'
  config.body = config.body || 'Bar'
  config.buttonText = config.buttonText || 'Baz'
  config.cancellable = config.cancellable === undefined ? config.cancellable : true;

}

createMenu(menuConfig);
==================
var menuConfig = {
  title: 'Order',
  // User did not include 'body' key
  buttonText: 'Send',
  cancellable: true
}

function createMenu(config) {
  config = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```

**不要使用标记(Flag)作为函数参数**
> 这个方法不好衡量，因为你能节省代码，特别是比较复杂的代码的时候
```js
function createFile(name, temp) {
  if (temp) {
    fs.create('./temp/' + name);
  } else {
    fs.create(name);
  }
}
==================
function createTempFile(name) {
  fs.create('./temp/' + name);
}

function createFile(name) {
  fs.create(name);
}
```

**采用函数式编程**
> 想学，但是一直没时间，这可能是进阶代码质量的必经之路吧
```js
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

var totalOutput = 0;

for (var i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
==================
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

var totalOutput = programmerOutput
  .map((programmer) => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, 0);
```

**封装判断条件**
> 一些比较长的判断逻辑确实有必要进行封装，但是如果只调用了一次，我觉得是不需要的


**Class**
* 单一职责原则 (SRP)
* 开/闭原则 (OCP)
* 利斯科夫替代原则 (LSP)
* 接口隔离原则 (ISP)
* 依赖反转原则 (DIP)
* 使用方法链（特别是装饰模式）
* 优先使用组合模式而非继承


**测试**
* 单一测试原则（mocha 就挺好的）
```js
=============
const assert = require('assert');

describe('MakeMomentJSGreatAgain', function() {
  it('handles 30-day months', function() {
    let date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    date.shouldEqual('1/31/2015');
  });

  it('handles leap year', function() {
    let date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);
  });

  it('handles non-leap year', function() {
    let date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
```

**使用 Promise**
> 正式工作以后，基本上没用过回调了，都是 Promise
> Async/Await 是较 Promises 更好的选择

```js
require('request').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', function(err, response) {
  if (err) {
    console.error(err);
  }
  else {
    require('fs').writeFile('article.html', response.body, function(err) {
      if (err) {
        console.error(err);
      } else {
        console.log('File written');
      }
    })
  }
})
==================
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then(function(response) {
    return require('fs-promise').writeFile('article.html', response);
  })
  .then(function() {
    console.log('File written');
  })
  .catch(function(err) {
    console.error(err);
  })
```

**错误处理**
> try catch 是个好东西，应该学会使用和熟悉使用

* 捕获错误
```js
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
==================
try {
  functionThatMightThrow();
} catch (error) {
  // One option (more noisy than console.log):
  console.error(error);
  // Another option:
  notifyUserOfError(error);
  // Another option:
  reportErrorToService(error);
  // OR do all three!
}
```

* 不要忽略被拒绝的 promises
> 一些前端监控平台，经常会有关于类似 unhandlerejection 的报错
```js
getdata()
.then(data => {
  functionThatMightThrow(data);
})
.catch(error => {
  // One option (more noisy than console.log):
  console.error(error);
  // Another option:
  notifyUserOfError(error);
  // Another option:
  reportErrorToService(error);
  // OR do all three!
});
```


最后就是一些编码规范了，可以根据个人的喜好去配置~