## 在 HTML 中，`;` 主要用于以下两种情况：

- **表示属性值的结束**

在 HTML 中，属性值可以是任何 JavaScript 表达式，包括函数调用和简单表达式。如果表达式的结果是对象，那么需要添加`;` 来表示表达式的结束。

以下是一些使用`;` 表示属性值结束的示例：

HTML

```
<input type="button" onclick="alert('Hello, world!');">
<a href="https://example.com" onclick="window.location.href = 'https://google.com';">跳转到 Google</a>
<img src="image.jpg" onclick="document.getElementById('div1').style.display = 'block';">
```

在这些示例中，属性值都是 JavaScript 表达式，包括函数调用。在这些情况下，需要添加`;`。如果我们将表达式中的`;` 去掉，那么表达式的结果将是对象，而不是字符串。因此，当属性被触发时，将会出错。

- **表示语句的结束**

在 JavaScript 中，`;` 用于表示语句的结束。在 HTML 中，如果使用 JavaScript 代码，那么也需要使用`;` 来表示语句的结束。

以下是一些使用`;` 表示语句结束的示例：

HTML

```
<script>
  alert('Hello, world!');
</script>
```

在这种情况下，`;` 用于表示 JavaScript 代码块的结束。如果我们将`;` 去掉，那么 JavaScript 代码将无法正确执行。

总而言之，在 HTML 中，`;` 主要用于表示属性值的结束和语句的结束。如果我们不确定是否需要使用`;`，那么可以参考 HTML 标准或浏览器的文档。