This is under development and poorly documented. Use at your own risk.

## Usage
```html
<snackbarqueue :defaultProps="snackbarDefaults"/>
<button @click="showSnack()">SNACK ME!</button>
```

```js
const snackbarDefaults = {timeout: 5000};

let count = 1;
function showSnack(){
    window.snackbar.showSnack("Snack #" + count);
    count++;
}

function showSnackFast(){
    window.snackbar.showSnack("Snack #" + count, {timeout: 500});
    count++;
}
```
