# JavaScript对象

## 概述

在本课程中，我们将介绍、定义和使用对象。

## 目标

+ 在JavaScript中创建对象
+ 访问对象中的值
+ 向对象添加键值对
+ 从对象中删除键值对

## 介绍

当我们遇到一个不认识的单词时，通常会查阅词典。词典本质上是一个单词列表；在每个单词下面是一个或多个定义。如果我们知道要查找的单词，我们只需在词典中查找它，并获取所有相关信息。

再举一个例子，想象一个日程安排。日程安排中有一系列日期，每个日期都有一系列时间；在每个时间点，都安排有一个事件（或者没有）。日程安排为我们提供了一种将事件与发生时间关联起来的方式。如果我们查找特定的时间，我们会看到那时会发生什么事情。

在编程中，像词典这样的结构被称为“关联数据结构”：它们包含键（在我们的词典类比中是单词）和值（在我们的词典类比中是定义）的对。

在JavaScript中，最基本的关联数据结构称为**对象**。这意味着在对象中，您可以通过其**键**查找其**值**，就像在词典中一样。事实上，您可能会听到一些人将对象称为“字典”。我们将其称为“对象”，因为它们是JavaScript的`Object`的实例。

## 创建对象

您可以通过两种不同的方式创建对象，使用文字语法和使用`Object` _构造函数_。**构造函数**恰如其名：它用于构造对象（在这种情况下，是`Object`对象）。确保在控制台中跟随操作。

文字语法：

```js
var meals = {};
```

花括号（`{}`）就是一个对象！您刚刚创建了第一个对象！

对象构造函数：

```js
var meals = new Object();
```

您刚刚又创建了另一个对象！

您还可以在创建对象时使用键值对初始化对象：

```js
var meals = { breakfast: "燕麦粥" };

// 或者，等效地

var meals = new Object({ breakfast: 'oatmeal' })
```

在这种情况下，`breakfast`是键，`"燕麦粥"`是值。

**注意，JavaScript对象中的所有键都是字符串。**这意味着即使您可以创建一个对象 `{1: '是最孤独的数字'}`，在这里，键`1`会变成字符串`'1'`。值可以是任何类型。

**还要注意**，键必须是唯一的。如果您初始化了以下对象

``` javascript
var meals = {
  breakfast: '鸡蛋',
  breakfast: '培根'
}
```

然后检查`meals`的值，您会看到

``` javascript
{ breakfast: '培根' }
```

只有最后一对使用`breakfast`作为键的键值对被保存！但值不必是唯一的：

``` javascript
var meals = {
  breakfast: '鳄梨',
  lunch: '鳄梨',
  dinner: '鳄梨'
}
```

我们可能想考虑丰富我们的饮食，但除此之外，上面的对象按预期工作。

类似地，如果您有一个变量 `const firstMeal = 'breakfast'` 并尝试创建一个对象 `var meals = { firstMeal: 'oatmeal' }`，`meals`对象的键将是`'firstMeal'`，而不是`'breakfast'`。

**顶级提示**：ES 6 提供了一种使用变量作为对象键的方法 — 您必须用方括号(`[]`)将键括起来。使用上面的示例，您可以编写 `var meals = { [firstMeal]: 'oatmeal' }` 然后 `meals` 将是 `{ breakfast: 'oatmeal' }`。很酷，对吧？

我们可以使用点表示法访问对象中的值

``` javascript
meals.breakfast // 'oatmeal'
```

或方括号表示法

``` javascript
meals['breakfast'] // 'oatmeal'
```

请注意，当我们使用点语法时，我们_不需要_将键用引号括起来，并且键必须能够被视为字符串。方括号语法要求如果我们直接引用键，则必须使用引号，但它也为我们提供了额外的灵活性 — 我们也可以这样做

``` javascript
meals[firstMeal] // 'oatmeal'
```

使用变量 `firstMeal`（等于字符串 `'breakfast'`）。如果我们尝试使用点表示法与我们的 `firstMeal` 变量呢？

```javascript
meals.firstMeal //undefined
```

当我们使用点表示法时，键始终被视为字面上提供的字符串。如果我们想要访问（或删除）属于变量键的值，则_必须_使用方括号表示法。

## 向对象添加内容

初始化对象时，如果我们知道键和值的名称，我们可以使用点语法添加新的键值对：

``` javascript
meals.snack = 'yogurt';
```

看到那个点 `.` 吗？对于对象来说，它具有特殊的含义 — 它告诉JavaScript我们将要访问紧随其后的_字符串_（在本例中为`'snack'`）作为属性。因此，在此我们将值 `'yogurt'` 分配给对象中键为 `'snack'` 的键。我们可以像以前一样访问这个新值：

``` javascript
meals

.snack // 'yogurt'
meals['snack'] // 'yogurt'
meals.lunch // 'burrito'
```

我们还可以使用方括号表示法添加键值对：

``` javascript
meals['second breakfast'] = 'bagel'
```

这在上面的示例中非常方便，因为我们的键不是一个简单的字符串。我们也可以使用变量作为键：

``` javascript
var sweetMeal = 'dessert'

meals[sweetMeal] = 'cake';

meals.dessert // 'cake'
meals[sweetMeal] // 'cake'
```

> **注意：**在JavaScript中，当我们命名变量和函数时，我们使用'camelCase'命名约定。也就是说 - 如果一个变量或函数使用单词命名，那么该单词以小写字母开头。如果使用多个单词，则第一个单词后的每个单词都以大写字母开头。 `sweetMeal` 就是一个例子。我们稍后会看到更多示例。请记住，测试通常也会期望使用这种约定！

不要让上面的更改看起来像我们只能添加新东西一样，我们可以通过使用键来更新现有的键值对：

``` javascript
meals.breakfast = '麦片'
```

请注意，上面突出显示的所有更改都是_破坏性_的。这意味着如果我们将这些更改应用于通过将对象传递给函数来的对象，则_原始对象_将更改。让我们来试试：

``` javascript
function destructivelyUpdateObjectWithKeyAndValue(obj, key, value) {
  obj[key] = value

  return obj
}

const recipe = { eggs: 3 }

destructivelyUpdateObjectWithKeyAndValue(recipe, 'flour', '3 cups')
// 返回 { eggs: 3, flour: '3 cups' }

// 但也：

recipe // { eggs: 3, flour: '3 cups' }
```

嗯，但如果这不是我们想要做的呢？如果我们想要创建一个_新的_对象，其中包含旧对象和新属性呢？

## `Object.assign()`

我们可以使用 `Object.assign()` 创建一个新对象，并从现有对象中传递属性。第一个值是要修改的目标对象。之后的所有值都可以是任意数量的对象。然后它将它们从左到右复制到目标对象上（因此，如果两个对象共享一个键，则最右边的对象的该键的值将获胜）。让我们来试试：

``` javascript
Object.assign({}, { foo: 'bar' })
// { foo: 'bar' }

Object.assign({ eggs: 3 }, { flour: '1 cup' })
// { eggs: 3, flour: '1 cup' }

Object.assign({ eggs: 3 }, { chocolate: '1 cup', flour: '2 cups' }, { flour: '1/2 cup' })
// { eggs: 3, chocolate: '1 cup', flour: '1/2 cup' }
```

`Object.assign` 的强大之处在于它允许我们以不破坏的方式重写上面的更新函数：

``` javascript
function updateObjectWithKeyAndValue(obj, key, value) {
 
  return Object.assign({}, obj, { [key]: value })
}
  // it's important that we merge everything into
  // a new object such as the empty {}. 
	// Otherwise, the object obj will be modified. 
	// Test what happens if this line was written as:
	// return Object.assign(obj, { [key]: value })
	
const recipe = { eggs: 3 }

updateObjectWithKeyAndValue(recipe, 'chocolate', '1 cup')
// 返回 `{ eggs: 3, chocolate: '1 cup' }`

recipe // { eggs: 3 }
```

不错（而且不仅仅因为有巧克力）！我们可以使我们的更新函数更加简洁：

``` javascript
function updateObjectWithObject(targetObject, updatesObject) {
  return Object.assign({}, targetObject, updatesObject)
}
```

## 删除键值对

假设现在只有下午5点，我们改变了对晚餐的想法，所以我们想要删除晚餐的键值对：

```js
var meals = { breakfast: "燕麦粥", lunch: "火鸡三明治", dinner: "牛排和土豆" };

// `delete` 运算符如果成功删除则返回 `true`，否则返回 `false`
delete meals.dinner; // true

meals;
// 返回 { breakfast: "燕麦粥", lunch: "火鸡三明治" }
```

## 更改值

假设我们实际上早餐吃的是燕麦粥和香蕉，我们想要更新 `breakfast` 键存储的值：

```js
var meals = {
  breakfast: "燕麦粥",
  lunch: "火鸡三明治",
  dinner: "牛排和土豆"
};
meals.breakfast = ["燕麦粥", "香蕉"];

meals;
// {
//   breakfast: ["燕麦粥", "香蕉"],
//   lunch: "火鸡三明治",
//   dinner: "牛排和土豆"
//  }
```

同样，我们可以使用 `Object.assign` 非破坏性地（保留原始对象）更改值：

``` javascript
var meals = {
  breakfast: "燕麦粥",
  lunch: "火鸡三明治",
  dinner: "牛排和土豆"
};


Object.assign({}, meals, { breakfast: ['燕麦粥', '香蕉'] })
// 返回 {
//   breakfast: ["燕麦粥", "香蕉"],
//   lunch: "火鸡三明治",
//   dinner: "牛排和土豆"
//  }


meals
// 仍然是 {
//   breakfast: "燕麦粥",
//   lunch: "火鸡三明治",
//   dinner: "牛排和土豆"
// };


```

## 说明

1. 打开 `objects.js`

2. 将一个对象分配给变量 `playlist`，并使用键值对初始化对象 — 键将是艺术家名称，值将是歌曲标题。（这给我们的 `playlist` 带来了什么限制？）

3. 创建一个名为 `updatePlaylist` 的函数，接受三个参数：playlist（一个对象）、艺术家名称（一个字符串）和歌曲标题。函数的主体应将歌曲和艺术家作为键值对添加到播放列表对象中。函数应返回整个播放列表。

4. 创建一个名为 `removeFromPlaylist` 的函数，接受两个参数（播放列表对象和艺术家名称）。函数的主体应从播放列表中删除键值对，并返回更新后的播放列表。