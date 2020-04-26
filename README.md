# expression_rules_builder

## Options

```html
<div id="expressions-container"></div>
<div id="rules-container"></div>
```

```js
var erb = ExpressionRulesBuilder({
  expressionsContainer: "#expressions-container",
  rulesContainer: "#rules-container",
  fields: [
    {
      name: "fieldName",
      type: "list",
      values: [
        ["Label", "value"],
        ["Label", "value"],
        ["Label", "value"],
      ],
    },
    {
      name: "fieldName2",
      type: "text",
    },
  ],
  expressions: [
    {
      name: "rule1",
      text: "Lorem ipsum dolor sit {fieldName}, consectetur adipiscing elit.",
    },
    {
      name: "rule2",
      text: "Donec {fieldName} ullamcorper. Duis consequat {fieldName2}",
    },
  ],
  rules: [
    {
      expression: "rule2",
      fields: { fieldName: "example", fieldName2: "example2" },
    },
  ],
});

var values = erb.getRules();
// values => [{ rule: "rule2", values: { fieldName: "example", fieldName2: "example2" } }]

erb.beforeAddExpression(function (expressionName) {
  if (confirm("Are you sure?") == false) {
    console.log(`Stopped by user!`);
    return false; // return false to stop action
  }
});

erb.afterAddExpression(function (expressionName) {
  console.log(`Expression ${expressionName} added`);
});

erb.beforeRemoveRule(function (expressionName) {
  if (confirm("Are you sure?") == false) {
    console.log(`Stopped by user!`);
    return false; // return false to stop action
  }
});

erb.afterRemoveRule(function (expressionName) {
  console.log(`Rule ${expressionName} removed`);
});
```

## Behavior

Ao selecionar um item na lista de regras, ele marcará o item com a classe "selected", possibilitando que você desabilite, oculte ou altere o estilo das regras selecionadas.

## Commands

Para gerar o pacote de distribuição em /dist

```bash
yarn run build
```

Para iniciar o servidor de DEV e testar o exemplo (index.html) em http://localhost:9000/

```bash
yarn run dev
```
