## Factory Pattern

With this pattern, we use factory functions to create objs. A factory fn creates an obj without using the `new` keyword.

### Example

```js
const createUser = ({ firstName, lastName, email }) => ({
  firstName,
  lastName,
  email,
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
});
```

We pass certain values to the factory function to create an obj. Then, we can create new propierties, like `fullName`, that will be added to the obj.

Now, we can use the factory function to create new users:

```js
const user1 = createUser({
  firstName: "John",
  lastName: "Doe",
  email: "john@doe.com",
});

const user2 = createUser({
  firstName: "Jane",
  lastName: "Doe",
  email: "jane@doe.com",
});
```

### Pros

- Useful when creating multiple smaller objs with similar properties
- A factory fn can be made to return custom objs easily

### Cons

- Often more memory efficient to create new instances
