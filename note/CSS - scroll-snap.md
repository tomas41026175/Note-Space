# scroll-snap 提升滾動順暢、定位與優化使用者體驗
當遇上多個項目或圖片在同個區塊需做上下/左右滑動效果，scroll-snap這個屬性就是讓滑動時可以定位在單個項目(圖片)上，不需要使用者手動滑動置中，也不會因為滑動速度太快以致略過。

## 使用方式
要設定scroll snap，需要分別在容器與項目做設定。

- 作用在父容器上
  - scroll-snap-type: 容器裡的吸附方向 | 是否強制吸附
  - none　預設值，滾動時不會做吸附，也就是平時使用的滾動情況。
  - x　吸附水平的定位點。
  - y　 吸附垂直的平定位點。
  - block　 吸附和塊狀元素排列方向同個滾動方向的定位点。預設情況下是垂直軸。
  - inline　 吸附和同列元素排列方向同個滾動方向的定位点 。預設情況下是水平軸。
  - both　XY軸都吸附。
  - mandatory　強制吸附。
  - proximity　不強制吸附，如容器高度(或寬度)太小以致無法呈現完整一個項目，則不會導致強制跳過。
  - scroll-snap-stop: 是否允许滾動容器忽略吸附位置。
  - normal　可以忽略吸附位置，預設值。
  - always　不能忽略吸附位置。且必須定位到第一个元素的位置。
  - scroll-padding: number，吸附點會受容器的padding影響做推移。

- 作用在父容器上
    - scroll-snap-align: 滾動捕獲的對齊位置
    - none　預設值。不定義位置。
    - start　起始位置對齊，垂直滾動，對齊子項目上緣。
    - end　结束位置對齊，垂直滾動，對齊子項目下緣。
    - center　居中對齊。子元素中心和滾動容器中心一致。

- Reference
  - https://yukihiew.com/css-scroll-snap/
  - 完整滑動屬性scroll snap
    - https://www.gushiciku.cn/pl/grR1/zh-tw
  - https://www.zhangxinxu.com/wordpress/2018/11/know-css-scroll-snap/
  - https://pjchender.dev/css/css-scroll-snap/