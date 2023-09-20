## 安裝 React & React-dom 類型定義文件

```
yarn add @types/react

yarn add @types/react-dom
```

## SFC 型別

React 的 type 文件中包含 SFC，可以避免我們重複定義 children、propTypes、contentTypes、defaultProps、displayName 的型別。

-   source code

```
node_modules/@types/react/index.d.ts
```

```
type SFC<P = {}> = StatelessComponent<P>;
interface StatelessComponent<P = {}> {
    (props: P & { children?: ReactNode }, context?: any): ReactElement<any> | null;
    propTypes?: ValidationMap<P>;
    contextTypes?: ValidationMap<any>;
    defaultProps?: Partial<P>;
    displayName?: string;
}
```

使用 SFC 進行無狀態 component 開發

```
import { SFC } from 'react'
import { MouseEvent } from 'react'
import * as React from 'react'
interface IProps {
  onClick (event: MouseEvent<HTMLDivElement>): void,
}
const Button: SFC<IProps> = ({onClick, children}) => {
  return (
    <div onClick={onClick}>
      { children }
    </div>
  )
}
export default Button
```

## 事件處理

React 提供 Event 對象的型別宣告

ClipboardEvent<T = Element> 剪贴板事件对象

DragEvent<T = Element> 拖拽事件对象

ChangeEvent<T = Element> Change 事件对象

KeyboardEvent<T = Element> 键盘事件对象

MouseEvent<T = Element> 鼠标事件对象

TouchEvent<T = Element> 触摸事件对象

WheelEvent<T = Element> 滚轮事件对象

AnimationEvent<T = Element> 动画事件对象

TransitionEvent<T = Element> 过渡事件对象

EX:

```
import { MouseEvent } from 'react'

interface IProps {

  onClick (event: MouseEvent<HTMLDivElement>): void,
}

```

MouseEvent Source Code:

```
node_modules/@types/react/index.d.ts
```

MouseEvent<T = Element> 繼承 SyntheticEvent<T>，並透過 T 接收一個 DOM 的型別，currentTarget 由 EventTarget & T 組成複合型別。

EventTarget Source Code:
`node_modules/typescript/lib/lib.dom.d.ts`

## 事件處理 function

EventHandler 型別別名，通過不同的 EventHandler進行宣告事件處理的型別
EventHandler Source Code :`node_modules/@types/react/index.d.ts`

```
    type EventHandler<E extends SyntheticEvent<any>> = { bivarianceHack(event: E): void }["bivarianceHack"];
    type ReactEventHandler<T = Element> = EventHandler<SyntheticEvent<T>>;
    type ClipboardEventHandler<T = Element> = EventHandler<ClipboardEvent<T>>;
    type DragEventHandler<T = Element> = EventHandler<DragEvent<T>>;
    type FocusEventHandler<T = Element> = EventHandler<FocusEvent<T>>;
    type FormEventHandler<T = Element> = EventHandler<FormEvent<T>>;
    type ChangeEventHandler<T = Element> = EventHandler<ChangeEvent<T>>;
    type KeyboardEventHandler<T = Element> = EventHandler<KeyboardEvent<T>>;
    type MouseEventHandler<T = Element> = EventHandler<MouseEvent<T>>;
    type TouchEventHandler<T = Element> = EventHandler<TouchEvent<T>>;
    type PointerEventHandler<T = Element> = EventHandler<PointerEvent<T>>;
    type UIEventHandler<T = Element> = EventHandler<UIEvent<T>>;
    type WheelEventHandler<T = Element> = EventHandler<WheelEvent<T>>;
    type AnimationEventHandler<T = Element> = EventHandler<AnimationEvent<T>>;
    type TransitionEventHandler<T = Element> = EventHandler<TransitionEvent<T>>;
```
EventHandler接收E作為處理function中的event對象型別。
bivarianceHack

....continue
https://juejin.cn/post/6844903684422254606?from=search-suggest