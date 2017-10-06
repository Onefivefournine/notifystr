# Vue toaster notifications

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
import notifystr from 'notifystr';

/*
 you should provide an event bus for this component, 
 event bus is a new instance of vue
*/
export const EventBus = new Vue();

// register locally
let app = new Vue( {
	data(){
		return {
			EventBus		
		}
	},
	components:{
		notifystr
	}
} );

// register globally
Vue.component('notifystr',notifystr);

```

Place notifystr container anywhere on your page and provide an event bus to it.
NOTE: You should place it ONLY ONCE!

```html
<notifystr :event-bus="EventBus"></notifystr>
```

And then use EventBus anywhere to trigger toasts

```javascript
EventBus.$emit( toastType<string>, title<string> , message<string>)
```

There are 4 toastTypes available at the moment: `success`, `warning`, `danger` ,`info`.

Notifystr itself is extremely simple - so feel free to add custom types or other enhancements!