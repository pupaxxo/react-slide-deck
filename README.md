> A simple react component for swipe, tabs, carousel, one page scroll ...,
with animation hooks. works on PC and touch devices

---


## `npm i react-slide-deck --save`

---

# [Demo](http://output.jsbin.com/hexada)
also open on touch device, see the swipe effect

--

#### Usage:

```js
import Deck from 'react-slide-deck';

class Demo extends Component {
  constructor(props) {
    super(props);
    this.state = {
      current: 0,
      horizontal: true,
      swipe: true,
      loop: true,
      factor: 0.4,
      dura: 1400
    };
  }
  change(event) {
    let target = event.target;
    let index = Array.prototype.indexOf.call(target.parentElement.children, target);

    this.setState({
      current: index
    });
  }
  render() {
    return (
      <div className='carousel'>

        <Deck {...this.state}>
          <Deck.Slide> slide 1 </Deck.Slide>
          <Deck.Slide> slide 2 </Deck.Slide>
          <Deck.Slide>
            <div className='item'>slide 3</div>
          </Deck.Slide>
          <Deck.Slide> slide 4 </Deck.Slide>
        </Deck>

        <ul className={styles.indicators} onClick={::this.change}>
          <li>1</li>
          <li>2</li>
          <li>3</li>
          <li>4</li>
        </ul>
      </div>
    );
  }
}

```

---

```js
<Deck
  horizontal|vertical // direction for the slides
  swipe // can scroll(mousewheel) or not; on touch devices, it is touch event
  factor // swipe distance used to determine whether to swipe forward or abort.
         // if (swipeDistance / width(or height for vertical)) > factor, then will switch to next slide, otherwise return to the current slide.
  loop //  scroll down on the last Deck.Slide => transition to the first Deck.Slide. only work when `scroll` is set
  dura // duration for slide transition, optional. default is 1400ms
  >
  <Deck.Slide> content </Deck.Slide>
  <Deck.Slide> content2 </Deck.Slide>
</Deck>
```

---
#### animation hooks
`Deck.Slide`
- `.slide--current` // current slide
- `.slide--before` // slides before current slide
- `.slide--after` // slides after current slide
- `.slide--prev` // the previous slide

use these classes hook to do css animations, for example:
```css
.item {
  transition: all 1s ease;
}
.slide--current .item {
  transform: translateX(200px);
}
// when switch to the 3rd slide, the `.item` will be animated
```

---

#### Note.

- it doesn't provide the slide indicators(usually for slides navigation), because it's hard to meet all needs.

- if you need slide indicators, do what you want, just provide the `current` slide index to `<Deck current={current}>`, it will take care of the transition
