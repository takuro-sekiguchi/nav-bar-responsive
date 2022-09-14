# レスポンシブ対応のナビゲーションバー

[デモサイトはこちら](https://taku-web3.com/project/nav-bar/index.html)

## ■改めて学んだこと
- navの基本的な書き方
- @media screenの書き方
- 要素を縦に均等に並べる方法
- 要素を画面外から登場させる方法
- toggleを使わずにスタイルをつけたり外したりする方法



### navのflexの書き方
```css
nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  min-height: 8vh;
  background-color: #364e8b;
}
```
navの中をさらにflexにすることでli要素を横並びにする。
```css
.nav-links {
  display: flex;
  justify-content: space-around;
  width: 40%;
  transition: all 0.5s ease-in-out;
}
```

### ハンバーガーメニューの作り方
```html
 <div class="burger">
  <div class="line1"></div>
  <div class="line2"></div>
  <div class="line3"></div>
 </div>
```
widthとheightを決めてmarginをつければハンバーガーになる。
```css
.burger div {
  width: 25px;
  height: 3px;
  background-color: white;
  margin: 5px;
}
```

rotateとtranslateの調節が少し難しい。
複数列挙したtransformの変形は「右から順番に」適用されるので、書く順番によって見た目が変わる。
```css
.toggle .line1 {
  transform: rotate(-45deg) translate(-5px, 6px);
  transition: all 0.5s ease-in-out;
}
.toggle .line2 {
  opacity: 0;
}
.toggle .line3 {
  transform: rotate(405deg) translate(-5px, -6px);
  transition: all 0.5s ease-in-out;
}
```


### @media screenの書き方
```css
@media screen and (max-width: 1024px) {
}

@media screen and (max-width: 768px) {
  /* 画面が横にずれるのを防ぐ */
  body {
      overflow-x: hidden;
    }
}
```


### 要素を縦に均等に並べる方法
```css
 .nav-links {
    position: fixed;
    right: 0;
    height: 92vh;
    top: 8vh;
    background-color: #364e8b;
    flex-direction: column;
    align-items: center;
    width: 50%;
    transform: translateX(100%);
  }
```


### 要素を画面外から登場させる方法
```css
@keyframes navLinksFade {
  0% {
    opacity: 0;
    transform: translateX(100px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
```

```js
link.style.animation = `navLinksFade 0.5s ease forwards ${index / 4 + 0.3}s`
// forwardsをつけるとアニメーションが終了した状態が維持される
```


### toggleを使わずにスタイルをつけたり外したりする方法
2回目からはハンバーガーメニューのアニメーションが機能しなくなるバグを修正する方法
```js
navLinks.forEach((link, index) => {
  //もしスタイルがついてる場合は空にする。
  if(link.style.animation) {
    link.style.animation = "";
  }else {
    //インデックス番号を使って、アニメーションの遅延時間を決めている。
    link.style.animation = `navLinksFade 0.5s ease forwards ${index / 4 + 0.3}s`
  }
});
```