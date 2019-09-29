
ㅁStack
```javascript
var items = [];
var head = 0;

var size2=size();

function push(element) {
    items[head] = element;
    head++;
}

function pop() {
    return items[head--];
}

function peek() {
    return items[head];
}

function isEmpty() {
    if(size() == 0) return true;
    else return false;
}

function clear() {
    items = [];
}

function size() {
    return items.length;
}

function print(){
    return items.toString();
}
```