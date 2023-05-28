Plain objects are unordered data structures and everything is stored in **key value pairs**. For example, like this object literal:
```JS
let instructor = {
  firstName: 'Kelly',
  isInstructor: true,
  favoriteNumber: [1, 2, 3, 4],
}
```
the object is stored in a variable called instructor. We've got three key value pairs. An object key will always be type of `string`, but the value can be of any type. It could be any of the primitives such as `string`, `boolean`, `number` or an [[Object Reference|object reference]].