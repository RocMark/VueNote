#27 Slots
> http://t.cn/RdVOQvc

* 必看
> https://www.jianshu.com/p/a0a83029a217

# Slots 用途
父組件準備好內容，分發給子組件安排的結構
* 父組件只負責內容，但不負責擺放的位置
* 子組件負責擺放位置，但不理會內容是什麼。

# 簡介
> 簡易實作 http://t.cn/RdVFJ0G
* 子元件 設定放置位置
<slot name="slot-content" 
      :item="val" 
      v-for="val in list"></slot>
從 list 撈出單一個項目，並將 該項目存入 item 中

* 父元件 利用 template 指定 slot 要插入的內容

* scope 其實就是 <slot> 標籤的屬性集合
<c-content>
  <!-- scope="可取任意字符串" -->
  <template scope="props" slot="slot-content">
    <h1>{{ props.item.title }}</h1>
    <p>{{ props.item.content }}</p>
  </template>
</c-content>

# Slot 基本介紹
由父層 傳遞 HTML Template 至子元件
* 沒有具名(Named Slots)的內容在，匹配不到時會被捨棄
```js
  // 父層 先 import 該子元件
  components: {
    'HelloWorld': HelloWorld,
  }

  <HelloWorld>
    <h2>父層自加的內容</h2>
    <h2 slot="slot1">{{ title }}</h2>
    <h2 slot="slot2">Slot2</h2>
  </HelloWorld>
  // 動態資料 寫於 init slot屬性的元件
  data(){ title: 'new Title'}


  // 子層 於 template 中加入 <slot></slot>
  <div>
    可多個內容 給予名稱，位置自行選擇

    <slot>父元件沒有要分發的內容時才顯示<slot>

    <slot name="slot1"></slot>
    <h1>原本的內容</h1>
    slot 功能像錨點，將父層自加的內容插入該位置
    <slot name="slot2"></slot>
  </div>
```

# Slots 實際應用 範例
* 子元件定義固定內容 & Style
由父元件傳入 客制化的區塊
```html
  <!-- 子元件 Form Component -->
  <form>
    <div id="form-header">
      <slot name="form-header"></slot>
    </div>
    <div id="form-fields">
      <slot name="form-fields"></slot>
    </div>
    <div id="form-controls">
      <slot name="form-controls"></slot>
    </div>
    <div id="useful-links">
      <ul>
        <li>
          <a href="#">Link 1</a>
          <a href="#">Link 2</a>
          <a href="#">Link 3</a>
          <a href="#">Link 4</a>
        </li>
      </ul>
    </div>
  </form>
```
* 父元件內容
```html
  <form-compo>
    <div slot="form-header">
      <h3>Title Form</h3>
      <p>Info for Diamond Member</p>
    </div>
    <div slot="form-fields">
      <input type="text" placeholder="name" required>
      <input type="password" placeholder="password" required>
    </div>
    <div slot="form-controls">
      <button @click="submitEvt" type="submit" >Submit</button>
    </div>
  </form-compo>
```

# Scoped Slots
用於資料傳遞，使用方式類似元件 Props Down

屬性名可自行取
id="item.id" {{ props.id }} 即可取用

<slot text="想傳遞的資料"></slot>

* scope="props" 中的 props 用來保存資料的變數
即 帶出 text 的值
{{ props.text }}

```html
  <div id="app">
    <app-layout>
      <app-footer>
        <!-- props 將 想傳遞的資料保存 -->
        <template scope="props">
          <!-- 利用 template 渲染 props保存的資料 -->
          <span>{{ props.text }}</span>
        </template>
      </app-footer>
    </app-layout>
  </div>
```
```js
  Vue.component('app-layout', {
    template: `
      <div class="layout">
        <slot></slot>
      </div>`
  });

  Vue.component('app-footer', {
    template: `
      <div>
        <slot text="想傳遞的資料">
        </slot>
      </div>`
  });

  // Root 要放最下面
  var vm = new Vue({
    el: '#app'
  });
```

# Scoped Slots 常用於 List 範例
* 利用 props 從 根元素(父) 傳給子 list

* 利用 子元素中的 :text="" 保存 item.text
切記要使用 v-bind:id="item.id"

* 回到上層 template scope="props" 儲存 item.text
取出 並將其渲染

```html
  <div id="app">
    <list :items="items">
      <template slot="item" scope="props">
        <li>{{ props.id }} + {{ props.text }}</li>
      </template>
    </list>
  </div>
```
```js
  Vue.component('list', {
    props: ['items'],
    template: `
      <ul>
        <slot name="item"
          v-for="item in items"
          :text="item.text" :id="item.id">
        </slot>
      </ul>
    `
  });

  var vm = new Vue({
    el: '#app',
    data: {
      items: [
        { id: 1, text: '項目 a' },
        { id: 2, text: '項目 b' },
        { id: 3, text: '項目 c' }
      ]
    }
  });
```