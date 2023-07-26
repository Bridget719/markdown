
``` js
{
  // "editor.formatOnSave": true,
  //代码保存时，自动执行ESlint格式化代码
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "eslint.autoFixOnSave": true,
    "source.fixAll.stylelint": true,
  },
  "stylelint.validate": [
    "css",
    "less",
    "postcss",
    "scss",
    "vue"
  ],
}
```