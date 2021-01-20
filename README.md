# The useLayOutEffect Hook
This hook has the same syntax as the `useEffect` hook but most of the time you will not use this hook and the `useEffect` hook will be more than enough for most of the cases

#### The syntax
```js
useLayoutEffect(cbFunction, [dependencies])
```

Example
```js
useLayoutEffect(()=> {
  //...do some side effects
  //BUT do this before browser painting the UI
})
```

#### useEffect vs useLayoutEffect
**useLayoutEffect**: runs *`synchronously`* after the DOM mutations but before the browser paints the screen
**useEffect**: runs *`asynchronously`* after the DOM mutaions and after painting the screen.

The steps when running **useEffect**:
1. The user performs an action.
2. React updates the state.
3. React perform updates on the DOM.
4. Browser paints DOM changes to the browser screen.
    - In this stage the User can see the changes he made.
5. The useEffect function will run.
    - So the function passed to useEffect will be fired only after the DOM changes are painted to the screen, this way it can't block the browser painiting process.

The steps when running **useLayoutEffect**:
1. The user performs an action.
2. React updates the state.
3. React perform updates on the DOM.
4. **React runs useLayoutEffect** before the painting.
5. Browser paints DOM changes to the browser screen.

#### Code Example
React hooks will always be fired based on their [order](https://reactjs.org/docs/hooks-rules.html#explanation).
so if we have multiple useEffect it will run the first one then the second and so on.

```js
useEffect(()=> {
  console.log("First");
});

useEffect(()=> {
  console.log("Second");
});
```

but in case that we had useLayoutEffect with useEffect then watch what will happen with this one

```js
useEffect(()=> {
  console.log("First");
});

//this will show up first 
//even it came last in the order
useLayoutEffect(()=> {
  console.log("Second");
});
```

Most of the time you don't need to use useLayoutEffect unless you are doing heavy dom mutations, scroll, styles, and animations, but always start with useEffect and then if you saw some flickering or some weird animation behaviour then try useLayoutEffect.

---

#### React hooks flow diagram
This diagram shows you React hook flow and which one fires before the other. ([original repo](https://github.com/donavon/hook-flow))

https://raw.githubusercontent.com/donavon/hook-flow/master/hook-flow.png

![](https://i.imgur.com/RcuMh1H.png)

---

#### Resources
I recommend going through these resources and examples
- [useEffect vs useLayoutEffect](https://kentcdodds.com/blog/useeffect-vs-uselayouteffect), Kent Dodds
- [When to useLayoutEffect Instead of useEffect](https://daveceddia.com/useeffect-vs-uselayouteffect/), Dave Ceddia
- [React Docs](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)

---
