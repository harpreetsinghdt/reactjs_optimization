# Reactjs Advanced Concepts (optimization)

## Virtual DOM

```
React checks for necessary DOM updates via a "Virtual DOM".
It creates and compares virtual DOM snapshots to find out which
parts of the rendered UI need to be updated.

-> How Eeact updates the Website UI
Step 1 - React creates the Component Tree starting from parent component (App component)
 to child (header, main) and grand child(counter, button, etc..)
Step 2 - React derives the actual html code that should be rendered from that component
tree and it then creates a Virtual Snapshot of the Target HTML Code from the component
tree  - still not reaching out to the real DOM instead it just creates a virtual representation that how real DOM should look like.
Step 3 - Compare New Virtual DOM Snapshot to Previous (old) Virtual DOM Snapshot.
Step 4- Identify and apply changes to the "Real DOM"
Therefor if the app is started there is no last (old) snapshot therefor react see everything change
then make all changes to real DOM. it means the entire the virtual DOM inserted into Real DOM with id="root"

and react repeats these steps everytime when something changes and
compare old virtual DOM and new virtual DOM and apply only those changes to real DOM.

```

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
useMemo() is beneficial to prevent the execution of normal function
in component unnecessary.
memo() is wrapped around component functions but useMemo() is
wrapped around normal functions that are executed in component
functions to prevent there execution.
useMemo() should only be used if normal function has complex
calculation that want to be prevent.
useMemo() accept first parameter an anonymous function( that normal
 function to perform complex calculations) and second parameter
 dependancy array. and only re-execute when dependency changes.

N.B dont overuse useMemo() to perform extra check which costs performance
```

```
The position of this component in the component tree.
React tracks state by component type & position (of that component) in the tree.
```

```
key value on component could be used to re-render the component when value passed to that key is changed i.e state value passed to child component so when state will update then child component re execute due to change in key value
<Counter key={chosenCount} initialCount={chosenCount} />
```

```
useEffect() Hook is also could be used to update the state value of child component while change is dependenacy value of hook which will cause the re-render of component due the new state value
but this task could be achieved by simply passing key value to child component in parent where pass the state value of parent to key for which we want to re-render the child.
```

## State Scheduling and Batching

```
React do not update the state immediately instead it schedule the update to next time means update will available on next render.
console.log(chosenCount); // won't work!

React also batch all state update in single function and effect only once in next render instead of multiple renders for each update of state within the same function.
setChosenCount(newCount);
setChosenCount((prevState) => prevState + 1);

function App() {
  const [chosenCount, setChosenCount] = useState(0);

  const handleSetCount = (newCount) => {
    setChosenCount(newCount);
    setChosenCount((prevState) => prevState + 1);
    console.log(chosenCount); // won't work!
  };

}
```

## Million JS

### https://million.dev/docs

```
Million Lint is a VSCode extension that speeds up your website!

Your React app is slow. Million Lint surfaces problematic code and automatically suggests ways to improve it.

Million Lint works with any React app (Next.js, Vite, Webpack, etc.) – get started in minutes!

Automatic Installation
```

```
npx million@latest
```
