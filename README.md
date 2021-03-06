# React.js wrapper for StPageFlip
Simple React.js wrapper for StPageFlip library, for creating realistic and beautiful page turning effect

![](video.gif)

### Features of StPageFlip
* Works with simple images on canvas and complex HTML blocks
* Has simple API and flexible configuration
* Compatible with mobile devices
* Supports landscape and portrait screen mode
* Supports soft and hard page types (only in HTML mode) 
* No dependencies

Live Demo with source code: https://nodlik.github.io/react-pageflip/

Docs and examples to StPageFlip: https://nodlik.github.io/StPageFlip/

### Installation
You can install the latest version using npm:

```npm install react-pageflip```

### Basic Usage

```jsx
import HTMLFlipBook from "react-pageflip";

function MyBook(props) {
  return (
    <HTMLFlipBook width={300} height={500}>
      <div className="demoPage">Page 1</div>
      <div className="demoPage">Page 2</div>
      <div className="demoPage">Page 3</div>
      <div className="demoPage">Page 4</div>
    </HTMLFlipBook>
  );
}
```

### Advanced Usage

You can define pages as a component, but in this case you should use ```React.forwardRef``` method. Like this:
```jsx
const Page = React.forwardRef((props, ref) => {
  return (
    <div className="demoPage" ref={ref}> /* ref required */
      <h1>Page Header</h1>
      <p>{props.children}</p>
      <p>Page number: {props.number}</p>
    </div>
  );
});

function MyBook(props) {
  return (
    <HTMLFlipBook width={300} height={500}>
      <Page number="1">Page text</Page>
      <Page number="2">Page text</Page>
      <Page number="3">Page text</Page>
      <Page number="4">Page text</Page>
    </HTMLFlipBook>
  );
}
```

### Props

To set configuration use these props:

* ```width: number``` - required
* ```height: number``` - required
* ```size: ("fixed", "stretch")``` - default: ```"fixed"``` Whether the book will be stretched under the parent element or not
* ```minWidth, maxWidth, minHeight, maxHeight: number``` You must set threshold values ​​with size: ```"stretch"```
* ```drawShadow: bool``` - default: ```true``` Draw shadows or not when page flipping
* ```flippingTime: number``` (milliseconds) - default: ```1000``` Flipping animation time
* ```usePortrait: bool``` - default: ```true``` Enable switching to portrait mode
* ```startZIndex: number``` - default: ```0``` Initial value to z-index
* ```autoSize: bool``` - default: ```true``` If this value is true, the parent element will be equal to the size of the book
* ```maxShadowOpacity: number [0..1]``` - default: ```1``` Shadow intensity (1: max intensity, 0: hidden shadows)
* ```showCover: boolean``` - default: ```false``` If this value is true, the first and the last pages will be marked as hard and will be shown in single page mode 
* ```mobileScrollSupport: boolean``` - default: ```true``` disable content scrolling when touching a book on mobile devices
### Events
You can use the following events:
```jsx
...
class DemoBook extends React.Component {
    onFlip(data) {
        console.log('Current page: ' + data);
    }

    render() {
        return (
            <HTMLFlipBook
             /* props */
             onFlip={(e) => this.onFlip(e.data)}
            >
            /* ... pages */
            </HTMLFlipBook>
        )
    }
}
```
**Available events:**
* ```onFlip: number``` - triggered by page turning
* ```onChangeOrientation: ("portrait", "landscape")``` - triggered when page orientation changes
* ```onChangeState: ("user_fold", "fold_corner", "flipping", "read")``` - triggered when the state of the book changes

Event object has two fields: ```data: number | string``` and ```object: PageFlip```

### Methods

To use methods, you need to get a ```PageFlip``` object. This can be done using ```ref``` and ```getPageFlip(): PageFlip``` method
```jsx
  render() {
    return (
        <HTMLFlipBook
            ...
            ref={(component) => (this.pageFlip = component)}
            ...
        >
            /* ... pages */
        </HTMLFlipBook>
    )
  }
```
For example - flipping to the next page:
```js
this.pageFlip.getPageFlip().flipNext();
```
**Available methods:**

| Method name | Parameters | Return type | Description|
| ----------- | ---------- | ----------- | ---------- |
| `getPageCount` | ` ` | `number` | Get number of all pages |
| `getCurrentPageIndex` | ` ` | `number` | Get the current page number (starts at 0) |
| `turnToPage` | `pageNum: number` | `void` | Turn to the specified page number (without animation)
| `turnToNextPage` | ` ` | `void` | Turn to the next page (without animation)
| `turnToPrevPage` | ` ` | `void` | Turn to the previous page (without animation)
| `flipNext` | `corner: ['top', 'bottom']` | `void` | Turn to the next page (with animation)
| `flipPrev` | `corner: ['top', 'bottom']` | `void`  | Turn to the previous page (with animation)
| `flip` | `pageNum: number, corner: ['top', 'bottom']` | `void` | Turn to the specified page (with animation)
| `loadFromImages` | `images: ['path-to-image1.jpg', ...]` | `void` | Load page from images
| `loadFromHtml` | `items: NodeListOf, HTMLElement[]` | `void` | Load page from html elements
| `updateFromHtml` | `items: NodeListOf, HTMLElement[]` | `void` | Update page from html elements
| `updateFromImages` | `images: ['path-to-image1.jpg', ...]` | `void` | Update page from images
| `destroy` | ` ` | `void` | Destructor. Removes Parent HTML Element and all event handlers


### Contacts
Oleg,

<oleg.litovski9@gmail.com>

https://github.com/Nodlik/react-pageflip
