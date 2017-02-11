# Template string

Enfin une syntaxe pour éviter ces horribles concaténations de chaines de caractères ! Cette synxtaxe se nomme également **_string interpolaton_**.

Dès lors que vous utilisez des _backticks_ \` pour définir votre chaine, toutes les expressions contenues dans `${}` sera remplacé par sa valeur.

```js
const name = "Eric";
const welcome = `Salut ${name}, Good Morniiiiiiiiiiiing!`;

console.log(welcome);

// Works well with multi-line strings
const message = `
  # Title

  This is a multi line string as markdown.
  It's pretty nice.
`;
console.log(message);
```

Les expressions sont également interpolées.

```js
let interpol = `00${1 * 7}`,my name is `${bond()}`
``