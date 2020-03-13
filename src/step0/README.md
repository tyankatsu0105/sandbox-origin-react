jsxではXML構文をjsに変換するので、HTMLのように書ける
```jsx
const element = <h1 title="foo">Hello</h1>
```

Reactでは、createElementのときにこういう構造になる
```jsx
const element = React.createElement(
  "h1",
  { title: "foo" },
  "Hello"
)
```

擬似的にelementを使ってプロパティで表現する
```js
const element = {
  type: 'h1',
  props: {
    title: 'foo',
    children: 'Hello'
  }
}
```

最終的にDOMをappendしたいcontainerを指定する
```js
const container = document.getElementById('app');

const node = document.createElement(element.type)
node['title'] = element.props.title

const text = document.createTextNode('');
text['nodeValue'] = element.props.children;

node.appendChild(text);
container.appendChild(node);
```

nodeを作る
タグはtypeからh1とする
attributeはpropsのtitleを使う
```js
const node = document.createElement(element.type)
node['title'] = element.props.title
```

innerTextじゃなくてtextNodeを作るようにすると、確実にtextタイプのnodeが作れるのでcreateTextNodeを使う
nodeValue、この場合はtextNodeのvalueをpropsのchildrenとする
```js
const text = document.createTextNode('');
text['nodeValue'] = element.props.children;
```

appendして終わり
```js
node.appendChild(text);
container.appendChild(node);
```