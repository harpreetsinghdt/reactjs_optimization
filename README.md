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

## useCallback() Hook

```
useCallback Hook is usefull to create cache for function in
component to prevent re-rendering unnecessary
while parent component re-render
otherwise if not use useCallback after re-rendering
function will created new function in memory with new memory address
and will treated as new value which will invoke the child component to re-rendered as value change
but it is the same function but only memory address pointer changed.
I hope you understand what i mean
```

## useMemo() Hook

```
useMemo() is beneficial to prevent the execution of normal function in component unnecessary.
memo() is wrapped around component functions but useMemo() is wrapped around normal functions that are executed in component functions to prevent there execution.
useMemo() should only be used if normal function has complex calculation that want to be prevent.
useMemo() accept first parameter an anonymous function( that normal function to perform complex calculations) and second parameter dependancy array. and only re-execute when dependency changes.
N.B dont overuse useMemo() to perform extra check which costs performance
```
