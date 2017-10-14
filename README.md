# Vue toaster notifications

### Requirements
Module bundler(webpack/rollup)
Vuejs 2.0+
Babel transpiler
any SCSS compiler (inside module bundler is preferred)

### Installation

```
npm i -s notifystr
```

#### Or...

```
yarn add notifystr
```

#### Or...

```
git clone https://github.com/Onefivefournine/notifystr.git
```

### Usage
```javascript
// Import and register component
import Vue from 'vue';
import notifystr from 'notifystr';

// register globally
Vue.component(notifystr);

// or register locally in Vue instance
const vm = new Vue({
    components:{
        notifystr
    }
})

```

Place notifystr container anywhere on your page.
NOTE: You should place it ONLY ONCE!

```html
<notifystr></notifystr>
```

And then use instance methods anywhere to trigger toasts

```javascript
this.$notifystr[toastType<string>](title<string> , message<string>, durationInMs<number>)

// for example
this.$notifystr.success('Title','Message',1500)
```

There are 4 toastTypes available at the moment: `success`, `warning`, `danger` ,`info`.

Notifystr itself is extremely simple - so feel free to add custom types or other enhancements!