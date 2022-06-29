# How to use ReactDOM.createPortal()?

https://stackoverflow.com/questions/46393642/how-to-use-reactdom-createportal-in-react-16
https://reactjs.org/docs/portals.html

## 应用场景

`portal` 的典型用例是当父组件有 overflow: hidden 或 z-index 样式时，但你需要子组件能够在视觉上“跳出”其容器。例如，对话框、悬浮卡以及提示框. 同时， `portals` are a way to render React children outside the main DOM hierarchy of the parent component _without losing the react context_.

## 如何使用

### 方法 1

预定义的 HTML 挂载点 —— 使用 React Portal 时，你需要提前定义一个 HTML DOM 元素作为 Portal 组件的挂载。

```html
<body>
  <noscript>You need to enable JavaScript to run this app.</noscript>
  <div id="overlays"></div>
  <div id="root"></div>
  <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
</body>
```

定义组件来使用预定义的 DOM 节点 => `ReactDOM.createPortal()`

```javascript
import React, { Fragment } from 'react';
import ReactDOM from 'react-dom';

import classes from './Modal.module.css';

const Backdrop = (props) => {
  const { showModal, setShowModal } = props;
  return (
    <div
      className={classes.backdrop}
      onClick={() => setShowModal(!showModal)}
    ></div>
  );
};

const ModalOverlay = (props) => {
  return (
    <div className={classes.modal}>
      <div className={classes.content}>{props.children}</div>
    </div>
  );
};

export const Modal = (props) => {
  const { showModal, setShowModal } = props;

  const portalElement = document.getElementById('overlays');

  return (
    <Fragment>
      {ReactDOM.createPortal(
        <Backdrop showModal={showModal} setShowModal={setShowModal} />,
        portalElement
      )}
      {ReactDOM.createPortal(
        <ModalOverlay>{props.children}</ModalOverlay>,
        portalElement
      )}
    </Fragment>
  );
};
```

### 方法 2

```javascript
node = document.createElement('div');
document.body.appendChild(node);
ReactDOM.render(<Modal {...props} />, node);
```

Let's say we are creating a modal view, we can create a wrapper for the same

```javascript
import React, { useEffect } from 'react';
import ReactDOM from 'react-dom';
import Modal from './Modal';
let node = null;
const ModalWrapper = (props) => {
  useEffect(() => {
    node && ReactDOM.render(<Modal {...props} />, node);
  });
  useEffect(() => {
    node = document.createElement('div');
    document.body.appendChild(node);
    ReactDOM.render(<Modal {...props} />, node);
  }, []);
  return <script />;
};
```
