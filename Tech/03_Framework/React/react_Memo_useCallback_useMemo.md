# React.memo(), React.useCallback(), React.useMemo()

## React.memo() 和 React.callback()

由于 React 的 Re-evaluation 机制，会使得每次只要 props，state 或者 context 发生变化都会重新执行组件，这样会造成浪费，通过使用 React.Memo 可以避免不必要的计算

只需要在导出函数组建的时候将函数组建传入 React.Memo() 即可。

但是 React.Memo 判断是否发生变化是基于 JavaScript 的基础元素，如果是对象（函数，数组等），此时需要用到另外一个比较是否发生变化的 React.callback(). React.callback() 用来封装对象元素，从而不会再次创建这个对象，当函数被再次执行的时候在 Re-evaluation 阶段。

## React.useMemo() 和 React.callback()

React.useMemo() 用于保存复杂计算后的结果，减少不必要的重复计算从而提升性能。

> `useMemo(() => computation(a, b), [a, b])` is the hook that lets you memoize expensive computations. Given the same `[a, b]` dependencies, once memoized, the hook is going to return the memoized value without invoking computation`(a, b)`.

`React.useMemo()` 和 `React.useCallback()`的区别
React.useMemo() 用于保存复杂计算后的结果, React.callback()用来保存函数的引用，来区分两次是不是同一个函数。

> `useCallback(() => {...}, [prop])` returns the same function instance as long as prop dependency is the same.

[How to Memoize with React.useMemo()](https://dmitripavlutin.com/react-usememo-hook/)
