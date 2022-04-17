# clean-code-javascript

## Table of Contents

1. [Introduction](#introduction)
2. [Variables](#variables)
3. [Functions](#functions)
4. [Objects and Data Structures](#objects-and-data-structures)
5. [Classes](#classes)
6. [SOLID](#solid)
7. [Testing](#testing)
8. [Concurrency](#concurrency)
9. [Error Handling](#error-handling)
10. [Formatting](#formatting)
11. [Comments](#comments)
12. [Translation](#translation)

## Introduction

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[_Clean Code_](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for JavaScript. This is not a style guide. It's a guide to producing
[readable, reusable, and refactorable](https://github.com/ryanmcdermott/3rs-of-software-architecture) software in JavaScript.

اصول مهندسی نرم افزار، از کتاب رابرت سی مارتین
_Clean Code_ سازگار با جاوا اسکریپت. این یک راهنمای سبک نیست. این راهنمای تولید نرم‌افزار قابل خواندن، قابل استفاده مجدد و قابل بازسازی در جاوا اسکریپت است.

Not every principle herein has to be strictly followed, and even fewer will be
universally agreed upon. These are guidelines and nothing more, but they are
ones codified over many years of collective experience by the authors of
_Clean Code_.

لازم نیست همه اصول در اینجا به طور دقیق رعایت شوند، و حتی تعداد کمتری از آنها مورد توافق جهانی قرار خواهند گرفت. اینها دستورالعمل ها هستند و نه چیزی بیشتر، اما آنها دستورالعمل هایی هستند که طی سال ها تجربه جمعی توسط نویسندگان کتاب تدوین شده اند.

Our craft of software engineering is just a bit over 50 years old, and we are
still learning a lot. When software architecture is as old as architecture
itself, maybe then we will have harder rules to follow. For now, let these
guidelines serve as a touchstone by which to assess the quality of the
JavaScript code that you and your team produce.

پیشه ما در مهندسی نرم افزار کمی بیش از 50 سال قدمت دارد و ما هنوز در حال یادگیری چیزهای زیادی هستیم. وقتی معماری نرم‌افزار به قدمت خود معماری باشد، شاید قوانین سخت‌تری برای پیروی داشته باشیم. در حال حاضر، اجازه دهید این دستورالعمل ها به عنوان سنگ محک برای ارزیابی کیفیت کد جاوا اسکریپتی که شما و تیمتان تولید می کنید، عمل کنند.

One more thing: knowing these won't immediately make you a better software
developer, and working with them for many years doesn't mean you won't make
mistakes. Every piece of code starts as a first draft, like wet clay getting
shaped into its final form. Finally, we chisel away the imperfections when
we review it with our peers. Don't beat yourself up for first drafts that need
improvement. Beat up the code instead!

یک چیز دیگر: دانستن این موارد فوراً شما را به یک توسعه‌دهنده نرم‌افزار بهتر تبدیل نمی‌کند، و کار کردن با آنها برای سال‌ها به این معنی نیست که اشتباه نخواهید کرد. هر قطعه کد به عنوان اولین پیش نویس شروع می شود، مانند خاک رس مرطوب که به شکل نهایی خود شکل می گیرد. در نهایت، هنگامی که آن را با همتایان خود مرور می کنیم، عیوب را از بین می بریم. برای اولین پیش نویس هایی که نیاز به بهبود دارند، خود را مورد ضرب و شتم قرار ندهید. در عوض کد را شکست دهید!

## **Variables**
## متغیرها
### Use meaningful and pronounceable variable names

### از نام متغیرهای معنی دار و قابل تلفظ استفاده کنید

**Bad:**

```javascript
const yyyymmdstr = moment().format("YYYY/MM/DD");
```

**Good:**

```javascript
const currentDate = moment().format("YYYY/MM/DD");
```

**[⬆ back to top](#table-of-contents)**

### Use the same vocabulary for the same type of variable

### از واژگان یکسان برای همان نوع متغیر استفاده کنید
**Bad:**

```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Good:**

```javascript
getUser();
```

**[⬆ back to top](#table-of-contents)**

### Use searchable names

### از اسامی قابل جستجو استفاده کنید

We will read more code than we will ever write. It's important that the code we
do write is readable and searchable. By _not_ naming variables that end up
being meaningful for understanding our program, we hurt our readers.
Make your names searchable. Tools like
[buddy.js](https://github.com/danielstjules/buddy.js) and
[ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md)
can help identify unnamed constants.

ما بیشتر از آنچه که تا به حال بنویسیم کد می خوانیم. مهم است که کدی که می نویسیم قابل خواندن و جستجو باشد. با نام بردن از متغیرهایی که در نهایت برای درک برنامه ما معنادار هستند، به خوانندگان خود صدمه می زنیم. نام خود را قابل جستجو کنید ابزارهایی مانند buddy.js و ESLint می توانند به شناسایی ثابت های بدون نام کمک کنند.

**Bad:**

```javascript
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);
```

**Good:**

```javascript
// Declare them as capitalized named constants.
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

setTimeout(blastOff, MILLISECONDS_PER_DAY);
```

**[⬆ back to top](#table-of-contents)**

### Use explanatory variables

### از متغیرهای توضیحی استفاده کنید

**Bad:**

```javascript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
);
```

**Good:**

```javascript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

**[⬆ back to top](#table-of-contents)**

### Avoid Mental Mapping

### از نقشه برداری ذهنی خودداری کنید

Explicit is better than implicit.

صریح بهتر از ضمنی است.

**Bad:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

**Good:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```

**[⬆ back to top](#table-of-contents)**

### Don't add unneeded context

### زمینه غیر ضروری را اضافه نکنید

If your class/object name tells you something, don't repeat that in your
variable name.

اگر نام کلاس/شیء شما چیزی به شما می گوید، آن را در نام متغیر خود تکرار نکنید.

**Bad:**

```javascript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car, color) {
  car.carColor = color;
}
```

**Good:**

```javascript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car, color) {
  car.color = color;
}
```

**[⬆ back to top](#table-of-contents)**

### Use default arguments instead of short circuiting or conditionals

### به جای اتصال کوتاه یا شرطی از آرگومان های پیش فرض استفاده کنید

Default arguments are often cleaner than short circuiting. Be aware that if you
use them, your function will only provide default values for `undefined`
arguments. Other "falsy" values such as `''`, `""`, `false`, `null`, `0`, and
`NaN`, will not be replaced by a default value.

آرگومان های پیش فرض اغلب تمیزتر از اتصال کوتاه هستند. توجه داشته باشید که اگر از آنها استفاده کنید، تابع شما فقط مقادیر پیش فرض را برای آرگومان های « undefined» ارائه می دهد. سایر مقادیر "falsy" مانند """، """، "undefined"، "null"، "0" و "NaN" با یک مقدار پیش‌فرض جایگزین نمی‌شوند.

**Bad:**

```javascript
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}
```

**Good:**

```javascript
function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## **Functions**

## **توابع**

### Function arguments (2 or fewer ideally)

### آرگومان های تابع (در حالت ایده آل 2 یا کمتر)

Limiting the amount of function parameters is incredibly important because it
makes testing your function easier. Having more than three leads to a
combinatorial explosion where you have to test tons of different cases with
each separate argument.

محدود کردن مقدار پارامترهای تابع بسیار مهم است زیرا آزمایش عملکرد شما را آسان‌تر می‌کند. داشتن بیش از سه مورد منجر به یک انفجار ترکیبی می شود که در آن باید هزاران مورد مختلف را با هر آرگومان جداگانه آزمایش کنید.

One or two arguments is the ideal case, and three should be avoided if possible.
Anything more than that should be consolidated. Usually, if you have
more than two arguments then your function is trying to do too much. In cases
where it's not, most of the time a higher-level object will suffice as an
argument.

یک یا دو استدلال حالت ایده آل است و در صورت امکان باید از سه استدلال اجتناب شود. هر چیزی بیش از این باید تجمیع شود. معمولاً، اگر بیش از دو آرگومان دارید، تابع شما تلاش می‌کند کارهای زیادی انجام دهد. در مواردی که اینطور نیست، اغلب اوقات یک شی سطح بالاتر به عنوان یک آرگومان کافی است.

Since JavaScript allows you to make objects on the fly, without a lot of class
boilerplate, you can use an object if you are finding yourself needing a
lot of arguments.

از آنجایی که جاوا اسکریپت به شما این امکان را می‌دهد که بدون استفاده از کلاس‌های زیاد، اشیا را بسازید، اگر متوجه شدید که به آرگومان‌های زیادی نیاز دارید، می‌توانید از یک شی استفاده کنید.

To make it obvious what properties the function expects, you can use the ES2015/ES6
destructuring syntax. This has a few advantages:

برای اینکه مشخص شود تابع چه ویژگی هایی را انتظار دارد، می توانید از نحو ساختارشکنی ES2015/ES6 استفاده کنید. این چند مزیت دارد:

1. When someone looks at the function signature, it's immediately clear what
   properties are being used.
2. It can be used to simulate named parameters.
3. Destructuring also clones the specified primitive values of the argument
   object passed into the function. This can help prevent side effects. Note:
   objects and arrays that are destructured from the argument object are NOT
   cloned.
4. Linters can warn you about unused properties, which would be impossible
   without destructuring.
   
   1. وقتی کسی به امضای تابع نگاه می کند، فوراً مشخص می شود که از چه ویژگی هایی استفاده می شود.
2. می توان از آن برای شبیه سازی پارامترهای نامگذاری شده استفاده کرد.
3. و Destructuring همچنین مقادیر اولیه مشخص شده شیء آرگومان ارسال شده به تابع را شبیه سازی می کند. این می تواند به جلوگیری از عوارض جانبی کمک کند. توجه: اشیاء و آرایه هایی که از شی آرگومان تخریب می شوند، کلون نمی شوند.
4. لینترها می توانند به شما در مورد خواص استفاده نشده هشدار دهند که بدون تخریب غیرممکن است.

**Bad:**

```javascript
function createMenu(title, body, buttonText, cancellable) {
  // ...
}

createMenu("Foo", "Bar", "Baz", true);

```

**Good:**

```javascript
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true
});
```

**[⬆ back to top](#table-of-contents)**

### Functions should do one thing

### توابع باید یک کار را انجام دهند

This is by far the most important rule in software engineering. When functions
do more than one thing, they are harder to compose, test, and reason about.
When you can isolate a function to just one action, it can be refactored
easily and your code will read much cleaner. If you take nothing else away from
this guide other than this, you'll be ahead of many developers.

این مهم ترین قانون در مهندسی نرم افزار است. وقتی توابع بیش از یک کار را انجام می دهند، نوشتن، آزمایش و استدلال در مورد آنها سخت تر است. وقتی می‌توانید یک تابع را فقط به یک عمل جدا کنید، می‌توانید آن را به راحتی دوباره فاکتور کنید و کد شما بسیار تمیزتر خوانده می‌شود. اگر به جز این چیز دیگری از این راهنما حذف نکنید، از بسیاری از توسعه دهندگان جلوتر خواهید بود.

**Bad:**

```javascript
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**Good:**

```javascript
function emailActiveClients(clients) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

**[⬆ back to top](#table-of-contents)**

### Function names should say what they do

### نام توابع باید نشان دهند که چه کاری انجام می دهند

**Bad:**

```javascript
function addToDate(date, month) {
  // ...
}

const date = new Date();

// It's hard to tell from the function name what is added
addToDate(date, 1);
```

**Good:**

```javascript
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```

**[⬆ back to top](#table-of-contents)**

### Functions should only be one level of abstraction

### توابع باید فقط یک سطح از انتزاع باشند

When you have more than one level of abstraction your function is usually
doing too much. Splitting up functions leads to reusability and easier
testing.

وقتی بیش از یک سطح از انتزاع دارید، عملکرد شما معمولاً بیش از حد انجام می دهد. تقسیم توابع منجر به قابلیت استفاده مجدد و آزمایش آسان تر می شود.

**Bad:**

```javascript
function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(node => {
    // parse...
  });
}
```

**Good:**

```javascript
function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);
  syntaxTree.forEach(node => {
    // parse...
  });
}

function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
}

function parse(tokens) {
  const syntaxTree = [];
  tokens.forEach(token => {
    syntaxTree.push(/* ... */);
  });

  return syntaxTree;
}
```

**[⬆ back to top](#table-of-contents)**

### Remove duplicate code

### کد تکراری را حذف کنید
Do your absolute best to avoid duplicate code. Duplicate code is bad because it
means that there's more than one place to alter something if you need to change
some logic.

تمام تلاش خود را برای جلوگیری از کد تکراری انجام دهید. کد تکراری بد است زیرا به این معنی است که در صورت نیاز به تغییر منطق، بیش از یک مکان برای تغییر چیزی وجود دارد.

Imagine if you run a restaurant and you keep track of your inventory: all your
tomatoes, onions, garlic, spices, etc. If you have multiple lists that
you keep this on, then all have to be updated when you serve a dish with
tomatoes in them. If you only have one list, there's only one place to update!

تصور کنید اگر رستورانی دارید و موجودی‌های خود را دنبال می‌کنید: همه گوجه‌فرنگی‌ها، پیاز، سیر، ادویه‌ها و غیره. اگر فهرست‌های متعددی دارید که این را در آن نگه می‌دارید، پس وقتی غذا با گوجه‌فرنگی سرو می‌کنید همه باید به‌روزرسانی شوند. اگر فقط یک لیست دارید، فقط یک مکان برای به روز رسانی وجود دارد!

Oftentimes you have duplicate code because you have two or more slightly
different things, that share a lot in common, but their differences force you
to have two or more separate functions that do much of the same things. Removing
duplicate code means creating an abstraction that can handle this set of
different things with just one function/module/class.

اغلب اوقات شما کد تکراری دارید زیرا دو یا چند چیز کمی متفاوت دارید که اشتراکات زیادی دارند، اما تفاوت‌های آنها شما را مجبور می‌کند دو یا چند تابع مجزا داشته باشید که بسیاری از کارهای مشابه را انجام می‌دهند. حذف کد تکراری به معنای ایجاد یک انتزاع است که بتواند این مجموعه از چیزهای مختلف را تنها با یک تابع/ماژول/کلاس مدیریت کند.

Getting the abstraction right is critical, that's why you should follow the
SOLID principles laid out in the _Classes_ section. Bad abstractions can be
worse than duplicate code, so be careful! Having said this, if you can make
a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself
updating multiple places anytime you want to change one thing.

درست کردن انتزاع بسیار مهم است، به همین دلیل است که باید از اصول SOLID که در بخش _Classes_ آمده است پیروی کنید. انتزاعات بد می توانند بدتر از کدهای تکراری باشند، پس مراقب باشید! با گفتن این، اگر می توانید یک انتزاع خوب بسازید، آن را انجام دهید! خودتان را تکرار نکنید، در غیر این صورت متوجه خواهید شد که هر زمان که بخواهید یک چیز را تغییر دهید چندین مکان را به روز می کنید.

**Bad:**

```javascript
function showDeveloperList(developers) {
  developers.forEach(developer => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```

**Good:**

```javascript
function showEmployeeList(employees) {
  employees.forEach(employee => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience
    };

    switch (employee.type) {
      case "manager":
        data.portfolio = employee.getMBAProjects();
        break;
      case "developer":
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
}
```

**[⬆ back to top](#table-of-contents)**

### Set default objects with Object.assign

### اشیاء پیش فرض را با Object.assign تنظیم کنید

**Bad:**

```javascript
const menuConfig = {
  title: null,
  body: "Bar",
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || "Foo";
  config.body = config.body || "Bar";
  config.buttonText = config.buttonText || "Baz";
  config.cancellable =
    config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

**Good:**

```javascript
const menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true
};

function createMenu(config) {
  let finalConfig = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true
    },
    config
  );
  return finalConfig
  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```

**[⬆ back to top](#table-of-contents)**

### Don't use flags as function parameters

### از پرچم ها به عنوان پارامترهای تابع استفاده نکنید

Flags tell your user that this function does more than one thing. Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.

رچم ها به کاربر شما می گویند که این تابع بیش از یک کار را انجام می دهد. توابع باید یک کار را انجام دهند. اگر توابع خود را بر اساس یک بولی مسیرهای کد متفاوتی را دنبال می کنند، تقسیم کنید.

**Bad:**

```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**Good:**

```javascript
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid Side Effects (part 1)

### اجتناب از عوارض جانبی (قسمت 1)

A function produces a side effect if it does anything other than take a value in
and return another value or values. A side effect could be writing to a file,
modifying some global variable, or accidentally wiring all your money to a
stranger.

یک تابع اگر کاری غیر از دریافت مقدار و برگرداندن مقدار یا مقادیر دیگری انجام دهد، یک اثر جانبی ایجاد می کند. یک عارضه جانبی می تواند نوشتن در یک فایل، تغییر برخی از متغیرهای سراسری یا انتقال تصادفی تمام پول خود به یک غریبه باشد.

Now, you do need to have side effects in a program on occasion. Like the previous
example, you might need to write to a file. What you want to do is to
centralize where you are doing this. Don't have several functions and classes
that write to a particular file. Have one service that does it. One and only one.

در حال حاضر، شما نیاز به عوارض جانبی در یک برنامه گاهی اوقات دارید. مانند مثال قبلی، ممکن است لازم باشد در یک فایل بنویسید. کاری که می خواهید انجام دهید این است که در جایی که این کار را انجام می دهید متمرکز شوید. چندین توابع و کلاس که در یک فایل خاص بنویسند ندارند. یک سرویس داشته باشید که این کار را انجام دهد. یک و تنها یکی.

The main point is to avoid common pitfalls like sharing state between objects
without any structure, using mutable data types that can be written to by anything,
and not centralizing where your side effects occur. If you can do this, you will
be happier than the vast majority of other programmers.

نکته اصلی این است که از تله‌های رایج مانند اشتراک‌گذاری حالت بین اشیا بدون هیچ ساختاری، استفاده از انواع داده‌های قابل تغییر که می‌توانند توسط هر چیزی روی آن نوشته شوند، و تمرکز نکردن مکان‌هایی که عوارض جانبی شما رخ می‌دهند، اجتناب کنید. اگر بتوانید این کار را انجام دهید، از اکثریت قریب به اتفاق برنامه نویسان دیگر خوشحال خواهید شد.

**Bad:**

```javascript
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
let name = "Ryan McDermott";

function splitIntoFirstAndLastName() {
  name = name.split(" ");
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**Good:**

```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(" ");
}

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```

**[⬆ back to top](#table-of-contents)**

### Avoid Side Effects (part 2)

### اجتناب از عوارض جانبی (قسمت 2)

In JavaScript, some values are unchangeable (immutable) and some are changeable 
(mutable). Objects and arrays are two kinds of mutable values so it's important 
to handle them carefully when they're passed as parameters to a function. A 
JavaScript function can change an object's properties or alter the contents of 
an array which could easily cause bugs elsewhere.

در جاوا اسکریپت، برخی از مقادیر غیرقابل تغییر (تغییرناپذیر) و برخی قابل تغییر (تغییرپذیر) هستند. اشیا و آرایه ها دو نوع مقدار قابل تغییر هستند، بنابراین مهم است که وقتی به عنوان پارامتر به یک تابع منتقل می شوند، آنها را با دقت مدیریت کنید. یک تابع جاوا اسکریپت می تواند ویژگی های یک شی را تغییر دهد یا محتویات یک آرایه را تغییر دهد که به راحتی می تواند باعث ایجاد اشکال در جاهای دیگر شود.

Suppose there's a function that accepts an array parameter representing a 
shopping cart. If the function makes a change in that shopping cart array - 
by adding an item to purchase, for example - then any other function that 
uses that same `cart` array will be affected by this addition. That may be 
great, however it could also be bad. Let's imagine a bad situation:

فرض کنید تابعی وجود دارد که پارامتر آرایه ای را که نشان دهنده سبد خرید است می پذیرد. اگر تابع تغییری در آرایه سبد خرید ایجاد کند - برای مثال با افزودن یک کالا برای خرید - هر تابع دیگری که از همان آرایه «سبد خرید» استفاده می‌کند تحت تأثیر این اضافه قرار می‌گیرد. ممکن است عالی باشد، با این حال ممکن است بد هم باشد. بیایید یک وضعیت بد را تصور کنیم:

The user clicks the "Purchase" button which calls a `purchase` function that
spawns a network request and sends the `cart` array to the server. Because
of a bad network connection, the `purchase` function has to keep retrying the
request. Now, what if in the meantime the user accidentally clicks an "Add to Cart"
button on an item they don't actually want before the network request begins?
If that happens and the network request begins, then that purchase function
will send the accidentally added item because the `cart` array was modified.

کاربر روی دکمه «خرید» کلیک می‌کند که تابع «خرید» را فراخوانی می‌کند که یک درخواست شبکه ایجاد می‌کند و آرایه «سبد خرید» را به سرور می‌فرستد. به دلیل اتصال شبکه بد، تابع «خرید» باید درخواست را دوباره امتحان کند. حال، اگر در این فاصله زمانی کاربر به طور تصادفی دکمه «افزودن به سبد خرید» را روی کالایی که واقعاً نمی‌خواهد، قبل از شروع درخواست شبکه کلیک کند، چه؟
اگر این اتفاق بیفتد و درخواست شبکه شروع شود، آن تابع خرید موردی که تصادفاً اضافه شده را ارسال می کند زیرا آرایه «سبد خرید» اصلاح شده است

A great solution would be for the `addItemToCart` function to always clone the 
`cart`, edit it, and return the clone. This would ensure that functions that are still
using the old shopping cart wouldn't be affected by the changes.

یک راه حل عالی این است که تابع «addItemToCart» همیشه «سبد خرید» را شبیه سازی کند، آن را ویرایش کند و کلون را برگرداند. این تضمین می کند که عملکردهایی که هنوز از سبد خرید قدیمی استفاده می کنند تحت تأثیر تغییرات قرار نخواهند گرفت

Two caveats to mention to this approach:

دو اخطار برای ذکر این رویکرد

1. There might be cases where you actually want to modify the input object,
   but when you adopt this programming practice you will find that those cases
   are pretty rare. Most things can be refactored to have no side effects!
   
   1. ممکن است مواردی وجود داشته باشد که شما واقعاً بخواهید شی ورودی را تغییر دهید، اما وقتی این روش برنامه نویسی را اتخاذ می کنید، متوجه می شوید که این موارد بسیار نادر هستند. بسیاری از چیزها را می توان بازسازی کرد تا هیچ عارضه ای نداشته باشد!

2. Cloning big objects can be very expensive in terms of performance. Luckily,
   this isn't a big issue in practice because there are
   [great libraries](https://facebook.github.io/immutable-js/) that allow
   this kind of programming approach to be fast and not as memory intensive as
   it would be for you to manually clone objects and arrays.
   
   2. شبیه سازی اشیاء بزرگ می تواند از نظر عملکرد بسیار گران باشد. خوشبختانه، این در عمل مشکل بزرگی نیست، زیرا کتابخانه‌های بزرگی وجود دارند که به این نوع رویکرد برنامه‌نویسی اجازه می‌دهند سریع باشد و آنقدر حافظه فشرده نباشد که شما به صورت دستی اشیا و آرایه‌ها را شبیه‌سازی کنید.

**Bad:**

```javascript
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

**Good:**

```javascript
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

**[⬆ back to top](#table-of-contents)**

### Don't write to global functions

### روی توابع جهانی ننویسید

Polluting globals is a bad practice in JavaScript because you could clash with another
library and the user of your API would be none-the-wiser until they get an
exception in production. Let's think about an example: what if you wanted to
extend JavaScript's native Array method to have a `diff` method that could
show the difference between two arrays? You could write your new function
to the `Array.prototype`, but it could clash with another library that tried
to do the same thing. What if that other library was just using `diff` to find
the difference between the first and last elements of an array? This is why it
would be much better to just use ES2015/ES6 classes and simply extend the `Array` global.

آلاینده کردن جهانی ها یک روش بد در جاوا اسکریپت است زیرا ممکن است با کتابخانه دیگری برخورد کنید و کاربر API شما عاقل تر نخواهد بود تا زمانی که در تولید استثنا پیدا کند. بیایید به یک مثال فکر کنیم: اگر بخواهید روش آرایه اصلی جاوا اسکریپت را گسترش دهید تا یک متد 'diff' داشته باشید که بتواند تفاوت بین دو آرایه را نشان دهد، چه؟ می‌توانید تابع جدید خود را در «Array.prototype» بنویسید، اما می‌تواند با کتابخانه دیگری که تلاش کرده است تداخل داشته باشد.
برای انجام همین کار اگر آن کتابخانه دیگر فقط از "diff" برای یافتن تفاوت بین اولین و آخرین عناصر یک آرایه استفاده می کرد، چه می شد؟ به همین دلیل است که بهتر است فقط از کلاس های ES2015/ES6 استفاده کنیم و به سادگی "آرایه" را جهانی کنیم.

**Bad:**

```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

**Good:**

```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Favor functional programming over imperative programming

### برنامه نویسی تابعی را بر برنامه نویسی ضروری ترجیح دهید

JavaScript isn't a functional language in the way that Haskell is, but it has
a functional flavor to it. Functional languages can be cleaner and easier to test.
Favor this style of programming when you can.

جاوا اسکریپت یک زبان کاربردی مانند Haskell نیست، اما طعمی کاربردی دارد. زبان‌های کاربردی می‌توانند تمیزتر و آسان‌تر برای آزمایش باشند. در صورت امکان از این سبک برنامه نویسی استفاده کنید.
**Bad:**

```javascript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**Good:**

```javascript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000
  }
];

const totalOutput = programmerOutput.reduce(
  (totalLines, output) => totalLines + output.linesOfCode,
  0
);
```

**[⬆ back to top](#table-of-contents)**

### Encapsulate conditionals

**Bad:**

```javascript
if (fsm.state === "fetching" && isEmpty(listNode)) {
  // ...
}
```

**Good:**

```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === "fetching" && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid negative conditionals

**Bad:**

```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**Good:**

```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid conditionals

### از شرطی شدن بپرهیزید

This seems like an impossible task. Upon first hearing this, most people say,
"how am I supposed to do anything without an `if` statement?" The answer is that
you can use polymorphism to achieve the same task in many cases. The second
question is usually, "well that's great but why would I want to do that?" The
answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you
are telling your user that your function does more than one thing. Remember,
just do one thing.

این یک کار غیر ممکن به نظر می رسد. با اولین شنیدن این حرف، اکثر مردم می گویند، "چطور قرار است کاری را بدون عبارت "اگر" انجام دهم؟ پاسخ این است که در بسیاری از موارد می توانید از چندشکلی برای رسیدن به همان کار استفاده کنید. سؤال دوم معمولاً این است: "خوب این عالی است، اما چرا من می خواهم این کار را انجام دهم؟" پاسخ یک مفهوم کد تمیز قبلی است که یاد گرفتیم: یک تابع فقط باید انجام دهد
یک چیز. وقتی کلاس‌ها و توابعی دارید که عبارت «if» دارند، به کاربر خود می‌گویید که تابع شما بیش از یک کار را انجام می‌دهد. به یاد داشته باشید، فقط یک کار را انجام دهید.

**Bad:**

```javascript
class Airplane {
  // ...
  getCruisingAltitude() {
    switch (this.type) {
      case "777":
        return this.getMaxAltitude() - this.getPassengerCount();
      case "Air Force One":
        return this.getMaxAltitude();
      case "Cessna":
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
  }
}
```

**Good:**

```javascript
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid type-checking (part 1)

### از بررسی نوع خودداری کنید (قسمت 1)

JavaScript is untyped, which means your functions can take any type of argument.
Sometimes you are bitten by this freedom and it becomes tempting to do
type-checking in your functions. There are many ways to avoid having to do this.
The first thing to consider is consistent APIs.

جاوا اسکریپت بدون تایپ است، به این معنی که توابع شما می توانند هر نوع آرگومان را بگیرند.
گاهی اوقات شما توسط این آزادی گاز گرفته می شوید و انجام چک کردن تایپ در عملکردهای خود وسوسه انگیز می شود. راه های زیادی برای اجتناب از انجام این کار وجود دارد. اولین چیزی که باید در نظر بگیرید API های سازگار است.

**Bad:**

```javascript
function travelToTexas(vehicle) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(this.currentLocation, new Location("texas"));
  } else if (vehicle instanceof Car) {
    vehicle.drive(this.currentLocation, new Location("texas"));
  }
}
```

**Good:**

```javascript
function travelToTexas(vehicle) {
  vehicle.move(this.currentLocation, new Location("texas"));
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid type-checking (part 2)

### از بررسی نوع خودداری کنید (قسمت 2)

If you are working with basic primitive values like strings and integers,
and you can't use polymorphism but you still feel the need to type-check,
you should consider using TypeScript. It is an excellent alternative to normal
JavaScript, as it provides you with static typing on top of standard JavaScript
syntax. The problem with manually type-checking normal JavaScript is that
doing it well requires so much extra verbiage that the faux "type-safety" you get
doesn't make up for the lost readability. Keep your JavaScript clean, write
good tests, and have good code reviews. Otherwise, do all of that but with
TypeScript (which, like I said, is a great alternative!).

اگر با مقادیر اولیه اولیه مانند رشته ها و اعداد صحیح کار می کنید،
و شما نمی توانید از چند شکلی استفاده کنید، اما همچنان نیاز به بررسی تایپ دارید، باید از TypeScript استفاده کنید. این یک جایگزین عالی برای جاوا اسکریپت معمولی است، زیرا تایپ ایستا را در بالای نحو استاندارد جاوا اسکریپت برای شما فراهم می کند. مشکل چک کردن دستی تایپ جاوا اسکریپت معمولی این است که انجام آن به خوبی نیاز به پرگویی اضافی دارد که "ایمنی نوع" اشتباهی که دریافت می کنید خوانایی از دست رفته را جبران نمی کند. جاوا اسکریپت خود را تمیز نگه دارید، تست های خوبی بنویسید و کدهای خوبی را بررسی کنید. در غیر این صورت، همه این کارها را انجام دهید اما با TypeScript (که همانطور که گفتم جایگزین عالی است!).


**Bad:**

```javascript
function combine(val1, val2) {
  if (
    (typeof val1 === "number" && typeof val2 === "number") ||
    (typeof val1 === "string" && typeof val2 === "string")
  ) {
    return val1 + val2;
  }

  throw new Error("Must be of type String or Number");
}
```

**Good:**

```javascript
function combine(val1, val2) {
  return val1 + val2;
}
```

**[⬆ back to top](#table-of-contents)**

### Don't over-optimize
### بیش از حد بهینه سازی نکنید

Modern browsers do a lot of optimization under-the-hood at runtime. A lot of
times, if you are optimizing then you are just wasting your time. [There are good
resources](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
for seeing where optimization is lacking. Target those in the meantime, until
they are fixed if they can be.

مرورگرهای مدرن در زمان اجرا بهینه سازی های زیادی را در پایین صفحه انجام می دهند. در بسیاری از مواقع، اگر در حال بهینه سازی هستید، فقط وقت خود را تلف می کنید. خوب وجود دارد
منابع برای دیدن جایی که بهینه سازی وجود ندارد. در این بین آن‌ها را مورد هدف قرار دهید، تا زمانی که در صورت امکان برطرف شوند.

**Bad:**

```javascript
// On old browsers, each iteration with uncached `list.length` would be costly
// because of `list.length` recomputation. In modern browsers, this is optimized.
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**Good:**

```javascript
for (let i = 0; i < list.length; i++) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Remove dead code
### کد مرده را حذف کنید

Dead code is just as bad as duplicate code. There's no reason to keep it in
your codebase. If it's not being called, get rid of it! It will still be safe
in your version history if you still need it.

کد مرده به اندازه کد تکراری بد است. دلیلی وجود ندارد که آن را در پایگاه کد خود نگه دارید. اگر نامیده نمی شود، از شر آن خلاص شوید! اگر همچنان به آن نیاز دارید، همچنان در تاریخچه نسخه شما ایمن خواهد بود.

**Bad:**

```javascript
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

**Good:**

```javascript
function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

**[⬆ back to top](#table-of-contents)**

## **Objects and Data Structures**

## **اشیاء و ساختارهای داده**

### Use getters and setters

### از getter و setterها استفاده کنید

Using getters and setters to access data on objects could be better than simply
looking for a property on an object. "Why?" you might ask. Well, here's an
unorganized list of reasons why:

استفاده از گیرنده‌ها و تنظیم‌کننده‌ها برای دسترسی به داده‌های روی اشیا می‌تواند بهتر از جستجوی ساده یک ویژگی روی یک شی باشد. "چرا؟" ممکن است بپرسید خوب، در اینجا یک لیست سازمان نیافته از دلایل وجود دارد:

- When you want to do more beyond getting an object property, you don't have
  to look up and change every accessor in your codebase.
- Makes adding validation simple when doing a `set`.
- Encapsulates the internal representation.
- Easy to add logging and error handling when getting and setting.
- You can lazy load your object's properties, let's say getting it from a
  server.
  
- هنگامی که می خواهید کارهای بیشتری فراتر از دریافت ویژگی شی انجام دهید، لازم نیست به دنبال جستجو و تغییر هر دسترسی در پایگاه کد خود باشید.
- افزودن اعتبارسنجی را هنگام انجام یک «مجموعه» ساده می کند.
- نمایش داخلی را کپسوله می کند.
- اضافه کردن ورود به سیستم و مدیریت خطا هنگام دریافت و تنظیم آسان است.
- می توانید ویژگی های شیء خود را با تنبلی بارگذاری کنید، فرض کنید آن را از a دریافت کنید
   سرور

**Bad:**

```javascript
function makeBankAccount() {
  // ...

  return {
    balance: 0
    // ...
  };
}

const account = makeBankAccount();
account.balance = 100;
```

**Good:**

```javascript
function makeBankAccount() {
  // this one is private
  let balance = 0;

  // a "getter", made public via the returned object below
  function getBalance() {
    return balance;
  }

  // a "setter", made public via the returned object below
  function setBalance(amount) {
    // ... validate before updating the balance
    balance = amount;
  }

  return {
    // ...
    getBalance,
    setBalance
  };
}

const account = makeBankAccount();
account.setBalance(100);
```

**[⬆ back to top](#table-of-contents)**

### Make objects have private members

### اشیاء را دارای اعضای خصوصی کنید

This can be accomplished through closures (for ES5 and below).

این را می توان از طریق بسته شدن (برای ES5 و پایین تر) انجام داد.

**Bad:**

```javascript
const Employee = function(name) {
  this.name = name;
};

Employee.prototype.getName = function getName() {
  return this.name;
};

const employee = new Employee("John Doe");
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: undefined
```

**Good:**

```javascript
function makeEmployee(name) {
  return {
    getName() {
      return name;
    }
  };
}

const employee = makeEmployee("John Doe");
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
```

**[⬆ back to top](#table-of-contents)**

## **Classes**

## **کلاس ها**

### Prefer ES2015/ES6 classes over ES5 plain functions

### کلاس های ES2015/ES6 را به توابع ساده ES5 ترجیح دهید

It's very difficult to get readable class inheritance, construction, and method
definitions for classical ES5 classes. If you need inheritance (and be aware
that you might not), then prefer ES2015/ES6 classes. However, prefer small functions over
classes until you find yourself needing larger and more complex objects.

بدست آوردن وراثت کلاس، ساخت و تعاریف متد قابل خواندن برای کلاس های کلاسیک ES5 بسیار دشوار است. اگر به ارث نیاز دارید (و توجه داشته باشید که ممکن است نباشید)، کلاس های ES2015/ES6 را ترجیح دهید. با این حال، توابع کوچک را به کلاس ها ترجیح دهید تا زمانی که متوجه شوید که به اشیاء بزرگتر و پیچیده تر نیاز دارید.

**Bad:**

```javascript
const Animal = function(age) {
  if (!(this instanceof Animal)) {
    throw new Error("Instantiate Animal with `new`");
  }

  this.age = age;
};

Animal.prototype.move = function move() {};

const Mammal = function(age, furColor) {
  if (!(this instanceof Mammal)) {
    throw new Error("Instantiate Mammal with `new`");
  }

  Animal.call(this, age);
  this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function liveBirth() {};

const Human = function(age, furColor, languageSpoken) {
  if (!(this instanceof Human)) {
    throw new Error("Instantiate Human with `new`");
  }

  Mammal.call(this, age, furColor);
  this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function speak() {};
```

**Good:**

```javascript
class Animal {
  constructor(age) {
    this.age = age;
  }

  move() {
    /* ... */
  }
}

class Mammal extends Animal {
  constructor(age, furColor) {
    super(age);
    this.furColor = furColor;
  }

  liveBirth() {
    /* ... */
  }
}

class Human extends Mammal {
  constructor(age, furColor, languageSpoken) {
    super(age, furColor);
    this.languageSpoken = languageSpoken;
  }

  speak() {
    /* ... */
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Use method chaining

### از روش زنجیره ای استفاده کنید

This pattern is very useful in JavaScript and you see it in many libraries such
as jQuery and Lodash. It allows your code to be expressive, and less verbose.
For that reason, I say, use method chaining and take a look at how clean your code
will be. In your class functions, simply return `this` at the end of every function,
and you can chain further class methods onto it.

این الگو در جاوا اسکریپت بسیار کاربردی است و آن را در بسیاری از کتابخانه ها مانند jQuery و Lodash مشاهده می کنید. این اجازه می دهد تا کد شما رسا، و کمتر پرمخاطب باشد. به همین دلیل، من می گویم، از روش زنجیره ای استفاده کنید و به پاک بودن کد خود نگاه کنید. در توابع کلاس خود، به سادگی «this» را در انتهای هر تابع برگردانید، و می توانید متدهای کلاس بیشتری را به آن زنجیره بزنید.

**Bad:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
  }

  setModel(model) {
    this.model = model;
  }

  setColor(color) {
    this.color = color;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

const car = new Car("Ford", "F-150", "red");
car.setColor("pink");
car.save();
```

**Good:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
    // NOTE: Returning this for chaining
    return this;
  }

  setModel(model) {
    this.model = model;
    // NOTE: Returning this for chaining
    return this;
  }

  setColor(color) {
    this.color = color;
    // NOTE: Returning this for chaining
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
    // NOTE: Returning this for chaining
    return this;
  }
}

const car = new Car("Ford", "F-150", "red").setColor("pink").save();
```

**[⬆ back to top](#table-of-contents)**

### Prefer composition over inheritance

### ترکیب را بر وراثت ترجیح دهید

As stated famously in [_Design Patterns_](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of
good reasons to use inheritance and lots of good reasons to use composition.
The main point for this maxim is that if your mind instinctively goes for
inheritance, try to think if composition could model your problem better. In some
cases it can.

همانطور که در _Design Patterns_ توسط باند چهار بیان شده است،
شما باید ترکیب را به ارث در جایی که می توانید ترجیح دهید. دلایل خوبی برای استفاده از وراثت و دلایل خوب زیادی برای استفاده از ترکیب وجود دارد. نکته اصلی برای این اصل این است که اگر ذهن شما به طور غریزی به سمت ارث می رود، سعی کنید فکر کنید که آیا ترکیب می تواند مشکل شما را بهتر مدل کند. در برخی موارد می تواند.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance
makes more sense than composition:

ممکن است از خود بپرسید که "چه زمانی باید از ارث استفاده کنم؟"
  این به مشکل شما بستگی دارد، اما این لیست مناسبی است از زمانی که وراثت بیشتر از ترکیب منطقی است:
  
  
1. Your inheritance represents an "is-a" relationship and not a "has-a"
   relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class.
   (Change the caloric expenditure of all animals when they move).
   
   1. وراثت شما نشان دهنده یک رابطه "is-a" است و نه "has-a"
    رابطه (انسان-> حیوان در مقابل کاربر-> جزئیات کاربر).
2. می توانید از کدهای کلاس های پایه مجددا استفاده کنید (انسان ها می توانند مانند همه حیوانات حرکت کنند).
3. می خواهید با تغییر یک کلاس پایه، تغییرات سراسری در کلاس های مشتق شده ایجاد کنید. (مصرف کالری همه حیوانات را هنگام حرکت تغییر دهید).

**Bad:**

```javascript
class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  // ...
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
class EmployeeTaxData extends Employee {
  constructor(ssn, salary) {
    super();
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}
```

**Good:**

```javascript
class EmployeeTaxData {
  constructor(ssn, salary) {
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}

class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  setTaxData(ssn, salary) {
    this.taxData = new EmployeeTaxData(ssn, salary);
  }
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## **SOLID**

### Single Responsibility Principle (SRP)

### اصل مسئولیت واحد (SRP)

As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify
a piece of it, it can be difficult to understand how that will affect other
dependent modules in your codebase.

همانطور که در Clean Code گفته شد، "هرگز نباید بیش از یک دلیل برای تغییر کلاس وجود داشته باشد". وسوسه انگیز است که یک کلاس را با کارایی زیاد جمع کنید، مانند زمانی که فقط می توانید یک چمدان را در پرواز خود ببرید. مشکل این است که کلاس شما از نظر مفهومی منسجم نخواهد بود و دلایل زیادی برای تغییر به آن می دهد. به حداقل رساندن تعداد دفعاتی که برای تغییر کلاس نیاز دارید مهم است.
این مهم است زیرا اگر عملکرد بیش از حد در یک کلاس وجود دارد و شما بخشی از آن را تغییر می‌دهید، درک اینکه چگونه بر دیگر ماژول‌های وابسته در پایگاه کد شما تأثیر می‌گذارد دشوار است.

**Bad:**

```javascript
class UserSettings {
  constructor(user) {
    this.user = user;
  }

  changeSettings(settings) {
    if (this.verifyCredentials()) {
      // ...
    }
  }

  verifyCredentials() {
    // ...
  }
}
```

**Good:**

```javascript
class UserAuth {
  constructor(user) {
    this.user = user;
  }

  verifyCredentials() {
    // ...
  }
}

class UserSettings {
  constructor(user) {
    this.user = user;
    this.auth = new UserAuth(user);
  }

  changeSettings(settings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Open/Closed Principle (OCP)

### اصل باز/بسته (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.

همانطور که برتراند مایر بیان کرد، "موجودات نرم افزاری (کلاس ها، ماژول ها، توابع و غیره) باید برای توسعه باز باشند، اما برای اصلاح بسته شوند." با این حال این به چه معناست؟ این اصل اساسا بیان می کند که باید به کاربران اجازه دهید تا بدون تغییر کد موجود، قابلیت های جدیدی را اضافه کنند.

**Bad:**

```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = "ajaxAdapter";
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = "nodeAdapter";
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    if (this.adapter.name === "ajaxAdapter") {
      return makeAjaxCall(url).then(response => {
        // transform response and return
      });
    } else if (this.adapter.name === "nodeAdapter") {
      return makeHttpCall(url).then(response => {
        // transform response and return
      });
    }
  }
}

function makeAjaxCall(url) {
  // request and return promise
}

function makeHttpCall(url) {
  // request and return promise
}
```

**Good:**

```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = "ajaxAdapter";
  }

  request(url) {
    // request and return promise
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = "nodeAdapter";
  }

  request(url) {
    // request and return promise
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    return this.adapter.request(url).then(response => {
      // transform response and return
    });
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Liskov Substitution Principle (LSP)

### اصل جایگزینی لیسکوف (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

این یک اصطلاح ترسناک برای یک مفهوم بسیار ساده است. به طور رسمی به این صورت تعریف می‌شود: «اگر S یک زیرگروه از T باشد، آنگاه اشیای نوع T ممکن است با اشیایی از نوع S جایگزین شوند (یعنی اشیاء نوع S ممکن است جایگزین اشیاء نوع T شوند) بدون تغییر هیچ یک از ویژگی‌های مطلوب آن برنامه. (صحت، کار انجام شده، و غیره)." این تعریف حتی ترسناک تر است.
بهترین توضیح برای این موضوع این است که اگر یک کلاس والد و یک کلاس فرزند دارید، کلاس پایه و کلاس فرزند را می توان به جای هم استفاده کرد بدون اینکه نتایج نادرستی دریافت کنید. این ممکن است هنوز گیج کننده باشد، بنابراین بیایید نگاهی به مثال کلاسیک مربع-مستطیل بیندازیم. از نظر ریاضی، مربع یک مستطیل است، اما اگر آن را با استفاده از رابطه "is-a" از طریق وراثت مدل کنید، به سرعت دچار مشکل می شوید.

**Bad:**

```javascript
class Rectangle {
  constructor() {
    this.width = 0;
    this.height = 0;
  }

  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width) {
    this.width = width;
    this.height = width;
  }

  setHeight(height) {
    this.width = height;
    this.height = height;
  }
}

function renderLargeRectangles(rectangles) {
  rectangles.forEach(rectangle => {
    rectangle.setWidth(4);
    rectangle.setHeight(5);
    const area = rectangle.getArea(); // BAD: Returns 25 for Square. Should be 20.
    rectangle.render(area);
  });
}

const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**Good:**

```javascript
class Shape {
  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor(length) {
    super();
    this.length = length;
  }

  getArea() {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes) {
  shapes.forEach(shape => {
    const area = shape.getArea();
    shape.render(area);
  });
}

const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
```

**[⬆ back to top](#table-of-contents)**

### Interface Segregation Principle (ISP)

### اصل جداسازی رابط (ISP)

JavaScript doesn't have interfaces so this principle doesn't apply as strictly
as others. However, it's important and relevant even with JavaScript's lack of
type system.

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use." Interfaces are implicit contracts in JavaScript because of
duck typing.

A good example to look at that demonstrates this principle in JavaScript is for
classes that require large settings objects. Not requiring clients to setup
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a
"fat interface".

جاوا اسکریپت رابط ندارد، بنابراین این اصل به سختی سایر اصول اعمال نمی شود. با این حال، حتی با عدم وجود سیستم نوع جاوا اسکریپت، مهم و مرتبط است.

ISP بیان می کند که "کلینت ها نباید مجبور شوند به واسط هایی که استفاده نمی کنند وابسته شوند." اینترفیس ها قراردادهای ضمنی در جاوا اسکریپت به دلیل تایپ اردک هستند.

یک مثال خوب که این اصل را در جاوا اسکریپت نشان می دهد برای کلاس هایی است که به اشیاء تنظیمات بزرگ نیاز دارند. عدم نیاز به مشتریان برای تنظیم مقادیر زیادی از گزینه ها مفید است، زیرا اکثر اوقات آنها به همه تنظیمات نیاز ندارند. اختیاری کردن آنها به جلوگیری از داشتن "رابط چربی" کمک می کند.

**Bad:**

```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.settings.animationModule.setup();
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName("body"),
  animationModule() {} // Most of the time, we won't need to animate when traversing.
  // ...
});
```

**Good:**

```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.options = settings.options;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.setupOptions();
  }

  setupOptions() {
    if (this.options.animationModule) {
      // ...
    }
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName("body"),
  options: {
    animationModule() {}
  }
});
```

**[⬆ back to top](#table-of-contents)**

### Dependency Inversion Principle (DIP)

### اصل وارونگی وابستگی (DIP)

This principle states two essential things:

1. High-level modules should not depend on low-level modules. Both should
   depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
   abstractions.

این اصل دو چیز اساسی را بیان می کند:

1. ماژول های سطح بالا نباید به ماژول های سطح پایین وابسته باشند. هر دو باید به انتزاعات بستگی داشته باشند.
2. انتزاع ها نباید به جزئیات بستگی داشته باشند. جزئیات باید به انتزاعات بستگی داشته باشد.


This can be hard to understand at first, but if you've worked with AngularJS,
you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.

درک این موضوع در ابتدا ممکن است سخت باشد، اما اگر با AngularJS کار کرده باشید، اجرای این اصل را در قالب Dependency Injection (DI) مشاهده کرده اید. در حالی که آنها مفاهیم یکسانی نیستند، DIP ماژول های سطح بالا را از دانستن جزئیات ماژول های سطح پایین خود و تنظیم آنها جلوگیری می کند. می تواند این کار را از طریق DI انجام دهد. یک مزیت بزرگ این است که جفت شدن بین ماژول ها را کاهش می دهد. کوپلینگ یک الگوی توسعه بسیار بد است، زیرا باعث می‌شود کد شما به‌سختی تغییر داده شود.

As stated previously, JavaScript doesn't have interfaces so the abstractions
that are depended upon are implicit contracts. That is to say, the methods
and properties that an object/class exposes to another object/class. In the
example below, the implicit contract is that any Request module for an
`InventoryTracker` will have a `requestItems` method.

همانطور که قبلاً گفته شد، جاوا اسکریپت واسط ندارد، بنابراین انتزاعاتی که به آنها وابسته هستند، قراردادهای ضمنی هستند. یعنی روش ها و ویژگی هایی که یک شی/کلاس در معرض شی/کلاس دیگر قرار می دهد. در مثال زیر، قرارداد ضمنی این است که هر ماژول درخواست برای «InventoryTracker» یک متد «requestItems» خواهد داشت.

**Bad:**

```javascript
class InventoryRequester {
  constructor() {
    this.REQ_METHODS = ["HTTP"];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryTracker {
  constructor(items) {
    this.items = items;

    // BAD: We have created a dependency on a specific request implementation.
    // We should just have requestItems depend on a request method: `request`
    this.requester = new InventoryRequester();
  }

  requestItems() {
    this.items.forEach(item => {
      this.requester.requestItem(item);
    });
  }
}

const inventoryTracker = new InventoryTracker(["apples", "bananas"]);
inventoryTracker.requestItems();
```

**Good:**

```javascript
class InventoryTracker {
  constructor(items, requester) {
    this.items = items;
    this.requester = requester;
  }

  requestItems() {
    this.items.forEach(item => {
      this.requester.requestItem(item);
    });
  }
}

class InventoryRequesterV1 {
  constructor() {
    this.REQ_METHODS = ["HTTP"];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryRequesterV2 {
  constructor() {
    this.REQ_METHODS = ["WS"];
  }

  requestItem(item) {
    // ...
  }
}

// By constructing our dependencies externally and injecting them, we can easily
// substitute our request module for a fancy new one that uses WebSockets.
const inventoryTracker = new InventoryTracker(
  ["apples", "bananas"],
  new InventoryRequesterV2()
);
inventoryTracker.requestItems();
```

**[⬆ back to top](#table-of-contents)**

## **Testing**

Testing is more important than shipping. If you have no tests or an
inadequate amount, then every time you ship code you won't be sure that you
didn't break anything. Deciding on what constitutes an adequate amount is up
to your team, but having 100% coverage (all statements and branches) is how
you achieve very high confidence and developer peace of mind. This means that
in addition to having a great testing framework, you also need to use a
[good coverage tool](https://gotwarlost.github.io/istanbul/).

آزمایش مهمتر از حمل و نقل است. اگر هیچ آزمایشی ندارید یا
مقدار ناکافی است، پس هر بار که کد ارسال می کنید، مطمئن نخواهید بود که چیزی را شکسته اید. تصمیم گیری در مورد اینکه چه چیزی مقدار کافی را تشکیل می دهد به تیم شما بستگی دارد، اما داشتن پوشش 100٪ (همه اظهارات و شعبه ها) چگونه به اعتماد بسیار بالا و آرامش خاطر توسعه دهنده دست می یابد. این بدان معناست که علاوه بر داشتن یک چارچوب تست عالی، باید از یک ابزار پوشش خوب نیز استفاده کنید

There's no excuse to not write tests. There are [plenty of good JS test frameworks](https://jstherightway.org/#testing-tools), so find one that your team prefers.
When you find one that works for your team, then aim to always write tests
for every new feature/module you introduce. If your preferred method is
Test Driven Development (TDD), that is great, but the main point is to just
make sure you are reaching your coverage goals before launching any feature,
or refactoring an existing one.

هیچ بهانه ای برای ننوشتن تست وجود ندارد. فریمورک‌های تست JS خوب زیادی وجود دارد، بنابراین یکی را پیدا کنید که تیم شما ترجیح می‌دهد.
وقتی یکی را پیدا کردید که برای تیم شما کار می کند، پس هدف خود را بنویسید که همیشه برای هر ویژگی/ماژول جدیدی که معرفی می کنید، تست بنویسید. اگر روش ترجیحی شما توسعه تست محور (TDD) است، عالی است، اما نکته اصلی این است که فقط مطمئن شوید که قبل از راه‌اندازی هر ویژگی یا بازسازی یک ویژگی موجود، به اهداف پوشش خود می‌رسید.

### Single concept per test

### مفهوم واحد در هر آزمون

**Bad:**

```javascript
import assert from "assert";

describe("MomentJS", () => {
  it("handles date boundaries", () => {
    let date;

    date = new MomentJS("1/1/2015");
    date.addDays(30);
    assert.equal("1/31/2015", date);

    date = new MomentJS("2/1/2016");
    date.addDays(28);
    assert.equal("02/29/2016", date);

    date = new MomentJS("2/1/2015");
    date.addDays(28);
    assert.equal("03/01/2015", date);
  });
});
```

**Good:**

```javascript
import assert from "assert";

describe("MomentJS", () => {
  it("handles 30-day months", () => {
    const date = new MomentJS("1/1/2015");
    date.addDays(30);
    assert.equal("1/31/2015", date);
  });

  it("handles leap year", () => {
    const date = new MomentJS("2/1/2016");
    date.addDays(28);
    assert.equal("02/29/2016", date);
  });

  it("handles non-leap year", () => {
    const date = new MomentJS("2/1/2015");
    date.addDays(28);
    assert.equal("03/01/2015", date);
  });
});
```

**[⬆ back to top](#table-of-contents)**

## **Concurrency**

## **همزمان**

### Use Promises, not callbacks

### از Promises استفاده کنید نه callback

Callbacks aren't clean, and they cause excessive amounts of nesting. With ES2015/ES6,
Promises are a built-in global type. Use them!

کالبک ها تمیز نیستند و باعث ایجاد مقدار زیادی تودرتو می شوند. با ES2015/ES6، Promises یک نوع جهانی داخلی است. از آنها استفاده کنید!
**Bad:**

```javascript
import { get } from "request";
import { writeFile } from "fs";

get(
  "https://en.wikipedia.org/wiki/Robert_Cecil_Martin",
  (requestErr, response, body) => {
    if (requestErr) {
      console.error(requestErr);
    } else {
      writeFile("article.html", body, writeErr => {
        if (writeErr) {
          console.error(writeErr);
        } else {
          console.log("File written");
        }
      });
    }
  }
);
```

**Good:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(body => {
    return writeFile("article.html", body);
  })
  .then(() => {
    console.log("File written");
  })
  .catch(err => {
    console.error(err);
  });
```

**[⬆ back to top](#table-of-contents)**

### Async/Await are even cleaner than Promises

### Async/Await حتی تمیزتر از Promises هستند

Promises are a very clean alternative to callbacks, but ES2017/ES8 brings async and await
which offer an even cleaner solution. All you need is a function that is prefixed
in an `async` keyword, and then you can write your logic imperatively without
a `then` chain of functions. Use this if you can take advantage of ES2017/ES8 features
today!

Promises جایگزین بسیار تمیزی برای تماس‌های برگشتی است، اما ES2017/ES8 همگام‌سازی و انتظار را به ارمغان می‌آورد که راه‌حلی حتی تمیزتر ارائه می‌دهد. تنها چیزی که نیاز دارید تابعی است که در یک کلمه کلیدی «ناهمگام» پیشوند باشد، و سپس می توانید منطق خود را به طور ضروری بدون زنجیره توابع «آنگاه» بنویسید. اگر امروز می توانید از ویژگی های ES2017/ES8 استفاده کنید، از این استفاده کنید!

**Bad:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(body => {
    return writeFile("article.html", body);
  })
  .then(() => {
    console.log("File written");
  })
  .catch(err => {
    console.error(err);
  });
```

**Good:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

async function getCleanCodeArticle() {
  try {
    const body = await get(
      "https://en.wikipedia.org/wiki/Robert_Cecil_Martin"
    );
    await writeFile("article.html", body);
    console.log("File written");
  } catch (err) {
    console.error(err);
  }
}

getCleanCodeArticle()
```

**[⬆ back to top](#table-of-contents)**

## **Error Handling**

## ** رسیدگی به خطا**

Thrown errors are a good thing! They mean the runtime has successfully
identified when something in your program has gone wrong and it's letting
you know by stopping function execution on the current stack, killing the
process (in Node), and notifying you in the console with a stack trace.

خطاهای پرتاب شده چیز خوبی است! آنها به این معنی هستند که زمان اجرا با موفقیت شناسایی شده است که مشکلی در برنامه شما اشتباه شده است و با متوقف کردن اجرای عملکرد در پشته فعلی، از بین بردن فرآیند (در Node) و اطلاع شما در کنسول با یک stack trace به شما اطلاع می دهد.

### Don't ignore caught errors

### خطاهای کشف شده را نادیده نگیرید

Doing nothing with a caught error doesn't give you the ability to ever fix
or react to said error. Logging the error to the console (`console.log`)
isn't much better as often times it can get lost in a sea of things printed
to the console. If you wrap any bit of code in a `try/catch` it means you
think an error may occur there and therefore you should have a plan,
or create a code path, for when it occurs.

انجام هیچ کاری با خطای کشف شده به شما این توانایی را نمی دهد که هرگز خطای گفته شده را برطرف کنید یا به آن واکنش نشان دهید. ثبت خطا در کنسول ('console.log') خیلی بهتر نیست زیرا اغلب اوقات ممکن است در دریایی از چیزهایی که روی کنسول چاپ شده گم شود. اگر هر بیت کدی را در یک «try/catch» بپیچید به این معنی است که فکر می‌کنید ممکن است خطایی در آنجا رخ دهد و بنابراین باید برای زمانی که رخ می‌دهد یک برنامه داشته باشید یا یک مسیر کد ایجاد کنید.

**Bad:**

```javascript
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
```

**Good:**

```javascript
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

### Don't ignore rejected promises

For the same reason you shouldn't ignore caught errors
from `try/catch`.

**Bad:**

```javascript
getdata()
  .then(data => {
    functionThatMightThrow(data);
  })
  .catch(error => {
    console.log(error);
  });
```

**Good:**

```javascript
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

**[⬆ back to top](#table-of-contents)**

## **Formatting**

## **قالب بندی**

Formatting is subjective. Like many rules herein, there is no hard and fast
rule that you must follow. The main point is DO NOT ARGUE over formatting.
There are [tons of tools](https://standardjs.com/rules.html) to automate this.
Use one! It's a waste of time and money for engineers to argue over formatting.

For things that don't fall under the purview of automatic formatting
(indentation, tabs vs. spaces, double vs. single quotes, etc.) look here
for some guidance.

قالب بندی ذهنی است. مانند بسیاری از قوانین در اینجا، هیچ قانون سخت و سریعی وجود ندارد که باید از آن پیروی کنید. نکته اصلی این است که بر سر قالب بندی بحث نکنید. هزاران ابزار برای خودکارسازی این کار وجود دارد. از یکی استفاده کن بحث در مورد قالب بندی برای مهندسان اتلاف وقت و پول است.
برای مواردی که در حیطه قالب بندی خودکار قرار نمی گیرند
(تورفتگی، برگه ها در مقابل فاصله، دو برابر در مقابل تک نقل قول ها، و غیره) اینجا را ببینید
برای راهنمایی
### Use consistent capitalization
### از حروف بزرگ استفاده کنید

JavaScript is untyped, so capitalization tells you a lot about your variables,
functions, etc. These rules are subjective, so your team can choose whatever
they want. The point is, no matter what you all choose, just be consistent.

جاوا اسکریپت بدون تایپ است، بنابراین حروف بزرگ به شما چیزهای زیادی در مورد متغیرها، توابع و غیره می گوید. این قوانین ذهنی هستند، بنابراین تیم شما می تواند هر چیزی را که می خواهد انتخاب کند. نکته این است که مهم نیست که همه شما چه چیزی را انتخاب می کنید، فقط ثابت قدم باشید.

**Bad:**

```javascript
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ["Back In Black", "Stairway to Heaven", "Hey Jude"];
const Artists = ["ACDC", "Led Zeppelin", "The Beatles"];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

**Good:**

```javascript
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ["Back In Black", "Stairway to Heaven", "Hey Jude"];
const ARTISTS = ["ACDC", "Led Zeppelin", "The Beatles"];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```

**[⬆ back to top](#table-of-contents)**

### Function callers and callees should be close

### تماس گیرندگان تابع و تماس گیرندگان باید نزدیک باشند

If a function calls another, keep those functions vertically close in the source
file. Ideally, keep the caller right above the callee. We tend to read code from
top-to-bottom, like a newspaper. Because of this, make your code read that way.

اگر تابع دیگری را فراخوانی کرد، آن توابع را به صورت عمودی در فایل منبع نزدیک نگه دارید. در حالت ایده آل، تماس گیرنده را درست بالای تماس گیرنده نگه دارید. ما تمایل داریم مانند یک روزنامه، کد را از بالا به پایین بخوانیم. به همین دلیل، کد خود را به این ترتیب بخوانید.

**Bad:**

```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  lookupPeers() {
    return db.lookup(this.employee, "peers");
  }

  lookupManager() {
    return db.lookup(this.employee, "manager");
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**Good:**

```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  lookupPeers() {
    return db.lookup(this.employee, "peers");
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  lookupManager() {
    return db.lookup(this.employee, "manager");
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**[⬆ back to top](#table-of-contents)**

## **Comments**

## **کامنتها**

### Only comment things that have business logic complexity.
### فقط چیزهایی را که دارای پیچیدگی منطق تجاری هستند کامنت دهید.

Comments are an apology, not a requirement. Good code _mostly_ documents itself.

کامنتها یک عذرخواهی است نه یک الزام. کد خوب _بیشتر_ خود سندی است برای خود.
**Bad:**

```javascript
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = (hash << 5) - hash + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

**Good:**

```javascript
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = (hash << 5) - hash + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Don't leave commented out code in your codebase

### کد کامنت شده را در پایگاه کد خود نگذارید

Version control exists for a reason. Leave old code in your history.

کنترل نسخه به دلایلی وجود دارد. کدهای قدیمی را در تاریخچه خود بگذارید.

**Bad:**

```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Good:**

```javascript
doStuff();
```

**[⬆ back to top](#table-of-contents)**

### Don't have journal comments

Remember, use version control! There's no need for dead code, commented code,
and especially journal comments. Use `git log` to get history!

**Bad:**

```javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
  return a + b;
}
```

**Good:**

```javascript
function combine(a, b) {
  return a + b;
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid positional markers

### از نشانگرهای موقعیتی خودداری کنید

They usually just add noise. Let the functions and variable names along with the
proper indentation and formatting give the visual structure to your code.

آنها معمولا فقط نویز اضافه می کنند. اجازه دهید توابع و نام متغیرها به همراه تورفتگی و قالب بندی مناسب ساختار بصری کد شما را ایجاد کنند.

**Bad:**

```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: "foo",
  nav: "bar"
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
};
```

**Good:**

```javascript
$scope.model = {
  menu: "foo",
  nav: "bar"
};

const actions = function() {
  // ...
};
```

**[⬆ back to top](#table-of-contents)**

## Translation

This is also available in other languages:

- ![am](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Armenia.png) **Armenian**: [hanumanum/clean-code-javascript/](https://github.com/hanumanum/clean-code-javascript)
- ![bd](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bangladesh.png) **Bangla(বাংলা)**: [InsomniacSabbir/clean-code-javascript/](https://github.com/InsomniacSabbir/clean-code-javascript/)
- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [fesnt/clean-code-javascript](https://github.com/fesnt/clean-code-javascript)
- ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Simplified Chinese**:
  - [alivebao/clean-code-js](https://github.com/alivebao/clean-code-js)
  - [beginor/clean-code-javascript](https://github.com/beginor/clean-code-javascript)
- ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Traditional Chinese**: [AllJointTW/clean-code-javascript](https://github.com/AllJointTW/clean-code-javascript)
- ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [GavBaros/clean-code-javascript-fr](https://github.com/GavBaros/clean-code-javascript-fr)
- ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [marcbruederlin/clean-code-javascript](https://github.com/marcbruederlin/clean-code-javascript)
- ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonesia**: [andirkh/clean-code-javascript/](https://github.com/andirkh/clean-code-javascript/)
- ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [frappacchio/clean-code-javascript/](https://github.com/frappacchio/clean-code-javascript/)
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/clean-code-javascript/](https://github.com/mitsuruog/clean-code-javascript/)
- ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [qkraudghgh/clean-code-javascript-ko](https://github.com/qkraudghgh/clean-code-javascript-ko)
- ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [greg-dev/clean-code-javascript-pl](https://github.com/greg-dev/clean-code-javascript-pl)
- ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**:
  - [BoryaMogila/clean-code-javascript-ru/](https://github.com/BoryaMogila/clean-code-javascript-ru/)
  - [maksugr/clean-code-javascript](https://github.com/maksugr/clean-code-javascript)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [tureey/clean-code-javascript](https://github.com/tureey/clean-code-javascript)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Spanish**: [andersontr15/clean-code-javascript](https://github.com/andersontr15/clean-code-javascript-es)
- ![rs](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Serbia.png) **Serbian**: [doskovicmilos/clean-code-javascript/](https://github.com/doskovicmilos/clean-code-javascript)
- ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [bsonmez/clean-code-javascript](https://github.com/bsonmez/clean-code-javascript/tree/turkish-translation)
- ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [mindfr1k/clean-code-javascript-ua](https://github.com/mindfr1k/clean-code-javascript-ua)
- ![vi](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [hienvd/clean-code-javascript/](https://github.com/hienvd/clean-code-javascript/)

**[⬆ back to top](#table-of-contents)**
