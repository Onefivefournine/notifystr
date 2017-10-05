# Vue multiple tags select

### Installation

```
npm i -s selectr-tags
```

#### Or...

```
yarn add selectr-tags
```

#### Or...

```
git clone https://github.com/Onefivefournine/selectr-tags.git
```

### Usage

Import and register component with event emitter
```javascript

import {notifystr,ee} from 'notifystr';

// locally
let app = new Vue( {
	components:{
		notifystr
	}
} );

// globally
Vue.component('notifystr',notifystr);

```

Place notifystr container anywhere on your page
NOTE: You should place it ONLY ONCE!

```html
<notifystr></notifystr>
```

And then use event emitter anywhere to trigger toasts

```javascript
ee.$emit( toastType<string>, title<string> , message<string>)
```

There are 4 toastTypes available at the moment: `success`, `warning`, `danger` ,`info`.

Notifystr itself is extremely simple - so feel free to add custom types or other enhancements!