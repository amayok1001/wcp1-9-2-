# wcp1-10

## Webページ作り
    - :visited
        一度訪問済みの<a>タグに関する設定

## ハンバーガーメニュー
    スマホ用のmenuボタン
    CSSとtrasitionでメニューづくり。
    実際は、JSなどが必要（というか、あったほうが動きがでていいってこと？）

### HTML
<header>
  <div id="nav-drawer">
      <input id="nav-input" type="checkbox" class="nav-unshown">
      <label id="nav-open" for="nav-input"><span></span></label>
      <label class="nav-unshown" id="nav-close" for="nav-input"></label>
      <div id="nav-content">ここに中身を入れる</div>
  </div>
</header>

#### input
    - <input id="nav-input" type="checkbox" class="nav-unshown">
        チェックボックス。常に表示
#### label
    - ラベル1: <label id="nav-open" for="nav-input"><span></span></label>
        チェックボックスのラベル。ここでハンバーガーアイコンを表示("nav-open")
        タップによりinputにチェックを入れる役割をする
    - ラベル2: <label class="nav-unshown" id="nav-close" for="nav-input"></label>
        はじめは非表示。
#### div
    - <div id="nav-content">ここに中身を入れる</div>
        表示される中身

### CSS
header {
  padding:10px;
  background: skyblue;
}

#nav-drawer {
  position: relative;
}

/*チェックボックス等は非表示に*/
.nav-unshown {
  display:none;
}

/*アイコンのスペース*/
#nav-open {
  display: inline-block;
  width: 30px;
  height: 22px;
  vertical-align: middle;
}

/*ハンバーガーアイコンをCSSだけで表現*/
#nav-open span, #nav-open span:before, #nav-open span:after {
  position: absolute;
  height: 3px;/*線の太さ*/
  width: 25px;/*長さ*/
  border-radius: 3px;
  background: #555;
  display: block;
  content: '';
  cursor: pointer;
}
#nav-open span:before {
  bottom: -8px;
}
#nav-open span:after {
  bottom: -16px;
}

/*閉じる用の薄黒カバー*/
#nav-close {
  display: none;/*はじめは隠しておく*/
  position: fixed;
  z-index: 99;
  top: 0;/*全体に広がるように*/
  left: 0;
  width: 100%;
  height: 100%;
  background: black;
  opacity: 0;
  transition: .3s ease-in-out;
}

/*中身*/
#nav-content {
  overflow: auto;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;/*最前面に*/
  width: 90%;/*右側に隙間を作る（閉じるカバーを表示）*/
  max-width: 330px;/*最大幅（調整してください）*/
  height: 100%;
  background: #fff;/*背景色*/
  transition: .3s ease-in-out;/*滑らかに表示*/
  -webkit-transform: translateX(-105%);
  transform: translateX(-105%);/*左に隠しておく*/
}

/*チェックが入ったらもろもろ表示*/
#nav-input:checked ~ #nav-close {
  display: block;/*カバーを表示*/
  opacity: .5;
}

#nav-input:checked ~ #nav-content {
  -webkit-transform: translateX(0%);
  transform: translateX(0%);/*中身を表示（右へスライド）*/
  box-shadow: 6px 0 25px rgba(0,0,0,.15);
}
