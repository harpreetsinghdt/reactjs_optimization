# Reactjs Advanced Concepts (optimization)

## memo() function

```
memo() compares prop values
if old prop value is equal to new prop value then component function will not execute.
it will execute only when prop value change or internal state changes.
memo only prevents function execution that are trigger by parent component not internal changes
```

### N.B. don't overuse memo()

```
Use it as high as in the component tree as possible
-> blocking a component execution there will also block all child component executions
```

```
Checking props with memo() costs performance
-> don't wrap it around all your components - it will just add a lot of unnecessary checks
```

```
Don't use it on components where props will change frequently
-> memo() would just perform a meaningless check in such cases (which costs performance)
```
