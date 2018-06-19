# filterMap
Polyfill (Array.prototype.filterMap) for filter and map in one trip through the target array.

### Why?
* Faster for large datasets than chaining filter and map (negligable for small ones...). Only goes through the target array once.
* Intuitive pattern is identical to Array.prototype.filter and Array.prototype.map, so use the same pattern when you have to do both instead of writing another one in Array.prototype.reduce.
* More declarative than making reduce do both tasks.

### Why Not?
* Commits a cardinal sin of extending native objects.
* It's not THAT much more efficient for small datasets.
* The people you work with probably won't like it.

### Signature:
```typescript
filterMap(filterCallback: (element: any, index?: number, origArray?: Array<T>) => boolean,
          mapCallback: (element: any, index?: number, origArray?: Array<T>) => Array<any>,
          thisArg?: any
): Array<any>;
```

### Example Usage:
```typescript
const testArray = [{id: 1, value: 'test 1'}, {id: 2, value: 'test 2'}, {id: 3, value: 'test 3'}];
const newArray = testArray.filterMap(
    (element) => element.id === 2,
    (element) => element.value
);
// newArray = ['test 2']
```

### Acknowledgements:
Adapted from MDN polyfills for [Array.prototype.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter#Polyfill) and [Array.prototype.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Polyfill).
