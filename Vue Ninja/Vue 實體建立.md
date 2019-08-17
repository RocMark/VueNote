# Vue 實體建立

```html
  <div id="app">
    {{ name }}
  </div>
```

```js
  new Vue({
    el: '#app',
    data(){
      return {
        name: 'Mark'
      }
    }
  })
```