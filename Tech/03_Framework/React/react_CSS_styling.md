# React 中常用的几种 CSS 方法

## 传统的 CSS 文件 和 inline-style

## Styled Components

https://styled-components.com/

- Based on JavaScript text template literal syntax
- Supporting passing props among React components
- In CSS lines, `&` refers to the componet itself => `&:pesudo select`

Example:

```javascript
// to define a styled element
const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${(props) => (props.invalid ? 'red' : '#ccc')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid ${(props) => (props.invalid ? 'red' : '#ccc')};
    background-color: ${(props) => (props.invalid ? 'salmon' : 'transparent')};
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }
`;

// to use props to setup differen stylings
<FormControl invalid={!isValid}>
  <label>Course Goal</label>
  <input type="text" onChange={goalInputChangeHandler} />
</FormControl>;
```

## CSS Module 方法

Only support to the project allows to use it. It works in React project.

- rename css files like: `CSSFile.module.css`
- in components,

```javascript
import classes from './Button.module.css';
```

https://create-react-app.dev/docs/adding-a-css-modules-stylesheet
