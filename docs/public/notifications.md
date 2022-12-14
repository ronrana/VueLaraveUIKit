# Notifications

<hr>

We restyled the classic Bootstrap Alert and gave it a more attractive look.
We crafted a custom plugin inspired by [vue-notifyjs](https://github.com/cristijora/vue-notifyjs) which is simple yet effective.


## Usage
To use the notification plugin, import it from the components folder. Note that this is 
already done in `src/dashboard-plugin.js`
```js
import Notifications from './components/NotificationPlugin/index'
Vue.use(Notifications)
```

### Trigger notifications
```html
/*vue*/
<desc>
</desc>
<template>
<div class="places-buttons">
  <notifications></notifications>
  <div class="row d-flex justify-content-center">
    <p class="category">Click to view notifications</p>
  </div>
  <div class="row">
    <div class="col-lg-8 ml-auto mr-auto">
      <div class="row">
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('top','left')">Top Left</n-button>
        </div>
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('top','center')">Top Center</n-button>
        </div>
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('top','right')">Top Right</n-button>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-lg-8 ml-auto mr-auto">
      <div class="row">
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('bottom','left')">Bottom Left</n-button>
        </div>
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('bottom','center')">Bottom Center</n-button>
        </div>
        <div class="col-md-4">
          <n-button type="primary" block @click.native="notifyVue('bottom','right')">Bottom Right</n-button>
        </div>
      </div>
    </div>
  </div>

  </div>
</div>
</template>

<script>
  export default {
     data () {
      return {
        type: ['', 'info', 'success', 'warning', 'danger'],
        notifications: {
          topCenter: false
        }
      }
    },
    methods: {
      notifyVue (verticalAlign, horizontalAlign) {
        const color = Math.floor((Math.random() * 4) + 1)
        this.$notify(
          {
            message: 'Welcome to <b>Now Ui Dashboard Pro</b> - a beautiful freebie for every web developer',
            icon: 'fa fa-gift',
            horizontalAlign: horizontalAlign,
            verticalAlign: verticalAlign,
            type: this.type[color]
          })
      }
    }
  }
</script>
<style lang="scss">
</style>
```

**Note:** `<notifications></notifications>` can be declared only once anywhere in your app,
preferably in your root component so the notification component is alive inside any other components.

### Notification options
You can set notification options in 3 ways

1. Upon plugin initialization

```js
import Notify from 'vue-notifyjs'
Vue.use(Notify, {type: 'primary', timeout: 2000})
```
2. Dynamically via `setOptions` method

```js
this.$notifications.setOptions({
  type: 'primary', 
  timeout: 2000,
  horizontalAlign: 'right',
  verticalAlign: 'top'
})
```

3. When using `$notify`

```js
this.$notify({
  message: 'Welcome',
  type: 'success'
})
```

**Note:** Options sent through `this.$notify` will override default options and will have higher priority than default options.

### Props

### Notifications 

```js
transitionName: {
 type:String,
 default:'list'
},
transitionMode: {
 type:String,
 default:'in-out'
},
overlap: {
 type: Boolean,
 default: false
}
```

### Notification (passed through the object sent to $notify method)
```js
props: {
  message: String,
  title: String,
  icon: String,
  verticalAlign: {
    type: String,
    default: 'top' // top | bottom
  },
  horizontalAlign: {
    type: String,
    default: 'center' // right | center | left
  },
  type: {
    type: String,
    default: 'info' // info | warning | danger | success | primary
  },
  timeout: {
    type: Number,
    default: 5000
  },
  timestamp: {
    type: Date,
    default: () => new Date()
  },
  component: {  //is rendered instead of notification message
    type: [Object, Function]
  },
  showClose: {
      type: Boolean,
      default: true
  },
  closeOnClick: {
      type: Boolean,
      default: true
  },
  clickHandler: Function,
},
```
