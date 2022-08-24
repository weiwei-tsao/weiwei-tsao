# React.memo(), React.useCallback(), React.useMemo()

## React.memo() 和 React.callback()

由于 React 的 Re-evaluation 机制，会使得每次只要 props，state 或者 context 发生变化都会重新执行/渲染组件，这样会造成浪费，通过使用 `React.memo()` 可以避免不必要的计算.只需要在导出函数组建的时候将函数组建传入 `React.memo()` 即可。

- 当组件被 `React.memo()` 封装后，后再次渲染组件时，如果 `props` ，`state` 或者 `context` 的值跟 上一次的一样，React 会使用上次渲染的结果，而不是每次都进行渲染。
- React.memo() 进行的是 shallow 比较，如果需要自定义比较的函数，可以使用其第二个参数，从而来判断每次渲染是否和上一次一样。 `React.memo(Component, [areEqual(prevProps, nextProps)])`

```javascript
function moviePropsAreEqual(prevMovie, nextMovie) {
  return (
    prevMovie.title === nextMovie.title &&
    prevMovie.releaseDate === nextMovie.releaseDate
  );
}
const MemoizedMovie2 = React.memo(Movie, moviePropsAreEqual);
```

那应该在什么时候使用 `React.memo()`：函数组件会被经常渲染，然后 `props` 或者 `state` 并不经常变化的情况下，常见的情况是 parent 组件 渲染引起 child 组件被迫渲染。此时，可以使用 `React.memo()`来减少性能开销. 更多 -> [`React.memo()`](https://dmitripavlutin.com/use-react-memo-wisely/)

但是 `React.memo` 判断是否发生变化是基于 JavaScript 的基础元素，如果是对象（函数，数组等），此时需要用到另外一个比较是否发生变化的 React.callback(). React.callback() 用来封装对象元素，从而不会再次创建这个对象，当函数被再次执行的时候在 Re-evaluation 阶段。

## React.useMemo() 和 React.callback()

React.useMemo() 用于保存复杂计算后的结果，减少不必要的重复计算从而提升性能。

> `useMemo(() => computation(a, b), [a, b])` is the hook that lets you memoize expensive computations. Given the same `[a, b]` dependencies, once memoized, the hook is going to return the memoized value without invoking computation`(a, b)`.

`React.useMemo()` 和 `React.useCallback()`的区别
React.useMemo() 用于保存复杂计算后的结果, React.callback()用来保存函数的引用，来区分两次是不是同一个函数。

> `useCallback(() => {...}, [prop])` returns the same function instance as long as prop dependency is the same.

[How to Memoize with React.useMemo()](https://dmitripavlutin.com/react-usememo-hook/)

## React.useCallback() and React.useEffect()

搭配使用 `useCallback` 来处理 获取数据的情况，防止获取数据的方法需要外部依赖，又不会导致在使用 `useEffect` 的时候无限循环

```javascript
const fetchMoivesHandler = React.useCallback(async () => {
  try {
    setIsLoading(true);
    setError(null);

    const resp = await fetch('https://swapi.dev/api/films/');
    if (!resp.ok) {
      throw new Error('Something went wrong!');
    }

    const data = await resp.json();

    const transformedMoives = data.results.map((moive) => {
      return {
        id: moive.episode_id,
        title: moive.title,
        openingText: moive.opening_crawl,
        releaseDate: moive.release_date,
      };
    });
    setMoives(transformedMoives);
  } catch (error) {
    setError(error.message);
  }

  setIsLoading(false);
}, []);

React.useEffect(() => {
  fetchMoivesHandler();
}, [fetchMoivesHandler]);
```
