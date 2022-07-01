# Retrieving keys for the React components

React has its quirks. The `key` property React asks to set for the components, rendered within an iteration of any kind, are [amongst them](https://reactjs.org/docs/lists-and-keys.html).

```javascript
{
    users.map(user => (
        <Card
            key={user.someUniqueProperty}
            user={user}
        />
    ));
}
```

The habit of setting it with a unique value will save you many moments of sheer amusement. React can do interesting and even nasty things with the markup and event listeners of the components rendered in a cycle without keys.

Usually, when each data piece has a unique property, this is a clear no-brainer.

But, sometimes, you have to use the pieces of data with no IDs to map through to render React components. Practice shows that there are different approaches to make the things done.

```javascript
{
    users.map(user => (
        <Card
            key={calculateHashOfTheObject(user)}
            user={user}
        />
    ));
}
```

This one looks like an overhead to me. The function has to keep all hashes for each object to avoid recalculations of them on each render. And usually, developers add an external dependency to solve the task.

If there is no id on data, you may add them still using the same indexes.

```javascript
const Cards = users => {
    const [preparedUsers] = useState(
        users.map((user, i) => ({
            ...user,
            id: i
        }))
    );

    return preparedUsers.map(user => (
        <Card key={user.id} user={user} />
    ));
};
```

It works because the index set as ID only once, and won't be updated with each next render. Any other operations with the list and following re-renders won't affect id somehow.