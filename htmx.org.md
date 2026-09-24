---
url: "https://htmx.org/docs/"
title: "</> htmx ~ Tài liệu"
---

# Tài liệu

**Mục lục**

- [giới thiệu](https://htmx.org/docs/#introduction)
- [cài đặt](https://htmx.org/docs/#installing)
- [ajax](https://htmx.org/docs/#ajax)
  - [trigger (bộ kích hoạt)](https://htmx.org/docs/#triggers)
    - [bộ điều chỉnh trigger](https://htmx.org/docs/#trigger-modifiers)
    - [bộ lọc trigger](https://htmx.org/docs/#trigger-filters)
    - [sự kiện đặc biệt](https://htmx.org/docs/#special-events)
    - [polling](https://htmx.org/docs/#polling)
    - [load polling](https://htmx.org/docs/#load_polling)
  - [chỉ báo (indicator)](https://htmx.org/docs/#indicators)
  - [target (đích)](https://htmx.org/docs/#targets)
  - [swapping (hoán đổi nội dung)](https://htmx.org/docs/#swapping)
  - [đồng bộ hóa](https://htmx.org/docs/#synchronization)
  - [hiệu ứng chuyển tiếp CSS](https://htmx.org/docs/#css_transitions)
  - [out of band swaps (hoán đổi ngoài luồng)](https://htmx.org/docs/#oob_swaps)
  - [lệnh swap từng phần từ server](https://htmx.org/docs/#partial_swaps)
  - [tham số](https://htmx.org/docs/#parameters)
  - [xác nhận](https://htmx.org/docs/#confirming)
- [kế thừa](https://htmx.org/docs/#inheritance)
- [boosting](https://htmx.org/docs/#boosting)
- [websockets & SSE](https://htmx.org/docs/#websockets-and-sse)
- [lịch sử (history)](https://htmx.org/docs/#history)
- [request & response](https://htmx.org/docs/#requests)
- [xác thực (validation)](https://htmx.org/docs/#validation)
- [hiệu ứng động (animation)](https://htmx.org/docs/#animations)
- [phần mở rộng (extensions)](https://htmx.org/docs/#extensions)
- [sự kiện & ghi log](https://htmx.org/docs/#events)
- [gỡ lỗi (debugging)](https://htmx.org/docs/#debugging)
- [scripting](https://htmx.org/docs/#scripting)
  - [thuộc tính hx-on](https://htmx.org/docs/#hx-on)
- [tích hợp bên thứ 3](https://htmx.org/docs/#3rd-party)
  - [Web Components](https://htmx.org/docs/#web-components)
- [caching](https://htmx.org/docs/#caching)
- [bảo mật](https://htmx.org/docs/#security)
- [cấu hình](https://htmx.org/docs/#config)

## [htmx trong một nốt nhạc](https://htmx.org/docs/\#introduction)

htmx là một thư viện cho phép bạn truy cập các tính năng trình duyệt hiện đại trực tiếp từ HTML, thay vì phải dùng
javascript.

Để hiểu htmx, trước tiên hãy xem qua một thẻ anchor (liên kết):

```html
<a href="/blog">Blog</a>
```

Thẻ anchor này báo cho trình duyệt biết:

> “Khi người dùng nhấp vào liên kết này, hãy gửi một yêu cầu HTTP GET đến ‘/blog’ và tải nội dung phản hồi
> vào cửa sổ trình duyệt”.

Với ý tưởng đó trong đầu, hãy xem đoạn HTML sau:

```html
<button hx-post="/clicked"
    hx-trigger="click"
    hx-target="#parent-div"
    hx-swap="outerHTML">
    Click Me!
</button>
```

Đoạn này báo cho htmx biết:

> “Khi người dùng nhấp vào nút này, hãy gửi một yêu cầu HTTP POST đến ‘/clicked’ và dùng nội dung từ phản hồi
> để thay thế phần tử có id `parent-div` trong DOM”

htmx mở rộng và khái quát hóa ý tưởng cốt lõi của HTML như một hypertext, mở ra nhiều khả năng hơn ngay
trong bản thân ngôn ngữ này:

- Giờ đây bất kỳ phần tử nào, không chỉ anchor và form, đều có thể gửi yêu cầu HTTP
- Giờ đây bất kỳ sự kiện nào, không chỉ click hay submit form, đều có thể kích hoạt yêu cầu
- Giờ đây bất kỳ [HTTP verb](https://en.wikipedia.org/wiki/HTTP_Verbs) nào, không chỉ `GET` và `POST`, đều có thể được sử dụng
- Giờ đây bất kỳ phần tử nào, không chỉ toàn bộ cửa sổ, đều có thể là đích cập nhật của yêu cầu

Lưu ý rằng khi dùng htmx, ở phía server bạn thường trả về _HTML_, chứ không phải _JSON_. Điều này giúp bạn vẫn nằm
trong [mô hình lập trình web nguyên bản](https://roy.gbiv.com/pubs/dissertation/rest_arch_style.htm),
sử dụng [Hypertext As The Engine Of Application State (HATEOAS)](https://en.wikipedia.org/wiki/HATEOAS)
mà không cần thực sự hiểu khái niệm đó.

Cũng đáng nói thêm là, nếu muốn, bạn có thể dùng tiền tố [`data-`](https://html.spec.whatwg.org/multipage/dom.html#attr-data-*) khi sử dụng htmx:

```html
<a data-hx-post="/click">Click Me!</a>
```

Nếu bạn đã hiểu các khái niệm về htmx và muốn xem những điểm “khác lạ” (quirks) của thư viện, hãy xem trang
[QUIRKS](https://htmx.org/quirks/).

## [Hướng dẫn di chuyển từ 1.x sang 2.x](https://htmx.org/docs/\#1-x-to-2-x-migration-guide)

[Phiên bản 1](https://v1.htmx.org/) của htmx vẫn được hỗ trợ và hỗ trợ IE11, nhưng phiên bản mới nhất của htmx là 2.x.

Nếu bạn đang chuyển sang htmx 2.x từ [htmx 1.x](https://v1.htmx.org/), vui lòng xem [hướng dẫn di chuyển htmx 1.x](https://htmx.org/migration-guide-htmx-1/).

Nếu bạn đang chuyển từ intercooler.js sang htmx, vui lòng xem [hướng dẫn di chuyển intercooler](https://htmx.org/migration-guide-intercooler/).

## [Cài đặt](https://htmx.org/docs/\#installing)

Htmx là một thư viện javascript hướng trình duyệt, không có phụ thuộc (dependency-free). Điều này có nghĩa là việc sử dụng nó đơn giản
như thêm một thẻ `<script>` vào phần head của tài liệu. Không cần hệ thống build để sử dụng nó.

### [Qua CDN (ví dụ: jsDelivr)](https://htmx.org/docs/\#via-a-cdn-e-g-jsdelivr)

Cách nhanh nhất để bắt đầu với htmx là tải nó qua CDN. Bạn chỉ cần thêm đoạn này vào
thẻ head và bắt đầu sử dụng:

```html
<script src="https://cdn.jsdelivr.net/npm/htmx.org@2.0.11/dist/htmx.min.js" integrity="sha384-2OatzQy1H+Zd/IIrjr1TcuDGqLXeHhbooAyJY1KdQMKnr4LZ22k31GBLdYKHmVjg" crossorigin="anonymous"></script>
```

Phiên bản chưa nén (unminified) cũng có sẵn:

```html
<script src="https://cdn.jsdelivr.net/npm/htmx.org@2.0.11/dist/htmx.js" integrity="sha384-gmJEF2eAKY4e+FDN+qtKIivWyb6ANwDB7JUdUybKgQspPKyEX/pIRZG/0uaRoW2C" crossorigin="anonymous"></script>
```

Cách dùng CDN tuy cực kỳ đơn giản, nhưng bạn cũng nên cân nhắc việc
[không dùng CDN trong môi trường production](https://blog.wesleyac.com/posts/why-not-javascript-cdn).

### [Tải một bản sao về máy](https://htmx.org/docs/\#download-a-copy)

Cách dễ tiếp theo để cài đặt htmx là chỉ cần sao chép nó vào dự án của bạn.

Tải `htmx.min.js` [từ jsDelivr](https://cdn.jsdelivr.net/npm/htmx.org@2.0.11/dist/htmx.min.js) và thêm vào thư mục phù hợp trong dự án của bạn,
rồi include nó ở nơi cần thiết bằng thẻ `<script>`:

```html
<script src="/path/to/htmx.min.js"></script>
```

### [npm](https://htmx.org/docs/\#npm)

Đối với các hệ thống build kiểu npm, bạn có thể cài htmx qua [npm](https://www.npmjs.com/):

```sh
npm install htmx.org@2.0.11
```

Sau khi cài đặt, bạn sẽ cần dùng công cụ phù hợp để sử dụng `node_modules/htmx.org/dist/htmx.js` (hoặc `.min.js`).
Ví dụ, bạn có thể đóng gói (bundle) htmx cùng với một số extension và mã nguồn riêng của dự án.

### [Webpack](https://htmx.org/docs/\#webpack)

Nếu bạn dùng webpack để quản lý javascript:

- Cài `htmx` qua trình quản lý gói yêu thích của bạn (như npm hoặc yarn)
- Thêm import vào `index.js`

```js
import 'htmx.org';
```

Nếu bạn muốn dùng biến toàn cục `htmx` (được khuyến nghị), bạn cần “bơm” nó vào phạm vi window:

- Tạo một file JS tùy chỉnh
- Import file này vào `index.js` (bên dưới import ở bước 2)

```js
import 'path/to/my_custom.js';
```

- Sau đó thêm đoạn code này vào file:

```js
window.htmx = require('htmx.org');
```

- Cuối cùng, build lại bundle của bạn

## [AJAX](https://htmx.org/docs/\#ajax)

Cốt lõi của htmx là một tập hợp các thuộc tính cho phép bạn gửi yêu cầu AJAX trực tiếp từ HTML:

| Thuộc tính | Mô tả |
| --- | --- |
| [hx-get](https://htmx.org/attributes/hx-get/) | Gửi yêu cầu `GET` đến URL đã cho |
| [hx-post](https://htmx.org/attributes/hx-post/) | Gửi yêu cầu `POST` đến URL đã cho |
| [hx-put](https://htmx.org/attributes/hx-put/) | Gửi yêu cầu `PUT` đến URL đã cho |
| [hx-patch](https://htmx.org/attributes/hx-patch/) | Gửi yêu cầu `PATCH` đến URL đã cho |
| [hx-delete](https://htmx.org/attributes/hx-delete/) | Gửi yêu cầu `DELETE` đến URL đã cho |

Mỗi thuộc tính trên nhận một URL để gửi yêu cầu AJAX đến. Phần tử sẽ gửi yêu cầu thuộc loại đã chỉ định
đến URL đã cho khi phần tử được [kích hoạt (trigger)](https://htmx.org/docs/#triggers):

```html
<button hx-put="/messages">
    Put To Messages
</button>
```

Đoạn này báo cho trình duyệt biết:

> Khi người dùng nhấp vào nút này, gửi yêu cầu PUT đến URL /messages và tải phản hồi vào nút bấm

### [Kích hoạt yêu cầu](https://htmx.org/docs/\#triggers)

Mặc định, yêu cầu AJAX được kích hoạt bởi sự kiện “tự nhiên” của phần tử:

- `input`, `textarea` & `select` được kích hoạt bởi sự kiện `change`
- `form` được kích hoạt bởi sự kiện `submit`
- mọi phần tử khác được kích hoạt bởi sự kiện `click`

Nếu muốn hành vi khác, bạn có thể dùng thuộc tính [hx-trigger](https://htmx.org/attributes/hx-trigger/)
để chỉ định sự kiện nào sẽ gây ra yêu cầu.

Đây là một `div` sẽ post đến `/mouse_entered` khi chuột di vào nó:

```html
<div hx-post="/mouse_entered" hx-trigger="mouseenter">
    [Here Mouse, Mouse!]
</div>
```

#### [Bộ điều chỉnh trigger](https://htmx.org/docs/\#trigger-modifiers)

Một trigger cũng có thể có thêm vài bộ điều chỉnh (modifier) làm thay đổi hành vi của nó. Ví dụ, nếu bạn muốn một yêu cầu
chỉ xảy ra một lần, bạn có thể dùng modifier `once` cho trigger:

```html
<div hx-post="/mouse_entered" hx-trigger="mouseenter once">
    [Here Mouse, Mouse!]
</div>
```

Các modifier khác bạn có thể dùng cho trigger là:

- `changed` – chỉ gửi yêu cầu nếu giá trị của phần tử đã thay đổi
- `delay:<khoảng thời gian>` – chờ khoảng thời gian đã cho (ví dụ `1s`) trước khi
gửi yêu cầu. Nếu sự kiện kích hoạt lại, bộ đếm sẽ được đặt lại.
- `throttle:<khoảng thời gian>` – chờ khoảng thời gian đã cho (ví dụ `1s`) trước khi
gửi yêu cầu. Khác với `delay`, nếu một sự kiện mới xảy ra trước khi hết thời gian giới hạn, sự kiện đó sẽ bị bỏ qua,
nên yêu cầu sẽ được kích hoạt vào cuối khoảng thời gian đó.
- `from:<CSS Selector>` – lắng nghe sự kiện trên một phần tử khác. Có thể dùng cho những thứ như phím tắt bàn phím. Lưu ý CSS selector này sẽ không được đánh giá lại nếu trang thay đổi.

Bạn có thể dùng các thuộc tính này để triển khai nhiều mẫu UX phổ biến, ví dụ [Active Search (tìm kiếm chủ động)](https://htmx.org/examples/active-search/):

```html
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup changed delay:500ms"
    hx-target="#search-results"
    placeholder="Search...">
<div id="search-results"></div>
```

Ô input này sẽ gửi yêu cầu 500 mili giây sau sự kiện keyup nếu input đã thay đổi, và chèn kết quả
vào `div` có id `search-results`.

Nhiều trigger có thể được chỉ định trong thuộc tính [hx-trigger](https://htmx.org/attributes/hx-trigger/), phân tách bằng dấu phẩy.

#### [Bộ lọc trigger](https://htmx.org/docs/\#trigger-filters)

Bạn cũng có thể áp dụng bộ lọc trigger bằng cách dùng dấu ngoặc vuông sau tên sự kiện, chứa một biểu thức javascript sẽ
được đánh giá. Nếu biểu thức trả về `true`, sự kiện sẽ được kích hoạt, ngược lại thì không.

Đây là ví dụ chỉ kích hoạt khi Control-Click vào phần tử

```html
<div hx-get="/clicked" hx-trigger="click[ctrlKey]">
    Control Click Me
</div>
```

Các thuộc tính như `ctrlKey` sẽ được phân giải dựa trên sự kiện kích hoạt trước, sau đó dựa trên phạm vi toàn cục. Ký hiệu
`this` sẽ được gán bằng phần tử hiện tại.

#### [Sự kiện đặc biệt](https://htmx.org/docs/\#special-events)

htmx cung cấp một vài sự kiện đặc biệt để dùng trong [hx-trigger](https://htmx.org/attributes/hx-trigger/):

- `load` – kích hoạt một lần khi phần tử được tải lần đầu
- `revealed` – kích hoạt một lần khi phần tử lần đầu cuộn vào trong viewport
- `intersect` – kích hoạt một lần khi phần tử lần đầu giao với viewport. Hỗ trợ thêm hai tùy chọn:

  - `root:<selector>` – một CSS selector của phần tử gốc để xét giao nhau
  - `threshold:<float>` – một số thực từ 0.0 đến 1.0, cho biết mức độ giao nhau cần để kích hoạt sự kiện

Bạn cũng có thể dùng sự kiện tùy chỉnh để kích hoạt yêu cầu nếu có trường hợp sử dụng nâng cao.

#### [Polling](https://htmx.org/docs/\#polling)

Nếu bạn muốn một phần tử polling (hỏi lặp lại) URL đã cho thay vì chờ sự kiện, bạn có thể dùng cú pháp `every`
với thuộc tính [`hx-trigger`](https://htmx.org/attributes/hx-trigger/):

```html
<div hx-get="/news" hx-trigger="every 2s"></div>
```

Đoạn này báo cho htmx biết:

> Cứ mỗi 2 giây, gửi một GET đến /news và tải phản hồi vào div

Nếu muốn dừng polling từ phía server, bạn có thể trả về mã phản hồi HTTP [`286`](https://en.wikipedia.org/wiki/86_(term))
và phần tử sẽ hủy việc polling.

#### [Load Polling](https://htmx.org/docs/\#load_polling)

Một kỹ thuật khác để đạt được polling trong htmx là “load polling”, trong đó một phần tử chỉ định
trigger `load` cùng với một khoảng delay, và tự thay thế chính nó bằng phản hồi:

```html
<div hx-get="/messages"
    hx-trigger="load delay:1s"
    hx-swap="outerHTML">
</div>
```

Nếu endpoint `/messages` liên tục trả về một div được thiết lập theo cách này, nó sẽ tiếp tục “polling” trở lại URL đó mỗi
giây.

Load polling có thể hữu ích trong các tình huống mà việc poll có một điểm kết thúc, tại đó việc polling chấm dứt, chẳng hạn
khi bạn hiển thị cho người dùng một [thanh tiến trình](https://htmx.org/examples/progress-bar/).

### [Chỉ báo yêu cầu (Request Indicators)](https://htmx.org/docs/\#indicators)

Khi một yêu cầu AJAX được gửi đi, thường nên cho người dùng biết là có điều gì đó đang xảy ra, vì trình duyệt
sẽ không cho họ bất kỳ phản hồi nào. Bạn có thể làm điều này trong htmx bằng cách dùng class `htmx-indicator`.

Class `htmx-indicator` được định nghĩa sao cho độ mờ (opacity) của bất kỳ phần tử nào có class này mặc định là 0, khiến nó vô hình
nhưng vẫn hiện diện trong DOM.

Khi htmx gửi một yêu cầu, nó sẽ gắn class `htmx-request` vào một phần tử (hoặc phần tử gửi yêu cầu, hoặc
phần tử khác, nếu được chỉ định). Class `htmx-request` sẽ khiến phần tử con có class `htmx-indicator`
chuyển sang độ mờ 1, hiển thị chỉ báo.

```html
<button hx-get="/click">
    Click Me!
    <img class="htmx-indicator" src="/spinner.gif" alt="Loading...">
</button>
```

Ở đây ta có một nút bấm. Khi nó được nhấp, class `htmx-request` sẽ được thêm vào nó, làm hiện ra phần tử
gif spinner. (Cá nhân người viết tài liệu gốc thích dùng [SVG spinner](http://samherbert.net/svg-loaders/) dạo gần đây.)

Trong khi class `htmx-indicator` dùng opacity để ẩn/hiện chỉ báo tiến trình, nếu bạn muốn dùng cơ chế khác
bạn có thể tự tạo một hiệu ứng chuyển tiếp CSS như sau:

```css
.htmx-indicator{
    display:none;
}
.htmx-request .htmx-indicator{
    display:inline;
}
.htmx-request.htmx-indicator{
    display:inline;
}
```

Nếu bạn muốn class `htmx-request` được thêm vào một phần tử khác, bạn có thể dùng thuộc tính [hx-indicator](https://htmx.org/attributes/hx-indicator/)
với một CSS selector để làm điều đó:

```html
<div>
    <button hx-get="/click" hx-indicator="#indicator">
        Click Me!
    </button>
    <img id="indicator" class="htmx-indicator" src="/spinner.gif" alt="Loading..."/>
</div>
```

Ở đây ta chỉ định rõ chỉ báo bằng id. Lưu ý rằng ta cũng có thể đặt class đó lên `div` cha
và vẫn có hiệu ứng tương tự.

Bạn cũng có thể thêm [thuộc tính `disabled`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled) vào
các phần tử trong suốt thời gian yêu cầu bằng cách dùng thuộc tính [hx-disabled-elt](https://htmx.org/attributes/hx-disabled-elt/).

### [Target (Đích)](https://htmx.org/docs/\#targets)

Nếu bạn muốn phản hồi được tải vào một phần tử khác thay vì phần tử đã gửi yêu cầu, bạn có thể
dùng thuộc tính [hx-target](https://htmx.org/attributes/hx-target/), nhận một CSS selector. Xem lại ví dụ Live Search của chúng ta:

```html
<input type="text" name="q"
    hx-get="/trigger_delay"
    hx-trigger="keyup delay:500ms changed"
    hx-target="#search-results"
    placeholder="Search...">
<div id="search-results"></div>
```

Bạn có thể thấy kết quả tìm kiếm sẽ được tải vào `div#search-results`, chứ không phải vào
thẻ input.

#### [CSS Selector mở rộng](https://htmx.org/docs/\#extended-css-selectors)

`hx-target`, và hầu hết các thuộc tính nhận CSS selector, hỗ trợ cú pháp CSS “mở rộng”:

- Bạn có thể dùng từ khóa `this`, cho biết phần tử mà thuộc tính `hx-target` nằm trên đó chính là đích
- Cú pháp `closest <CSS selector>` sẽ tìm phần tử tổ tiên [gần nhất](https://developer.mozilla.org/docs/Web/API/Element/closest)
hoặc chính nó, khớp với CSS selector đã cho.
(ví dụ `closest tr` sẽ nhắm đến hàng bảng gần nhất với phần tử)
- Cú pháp `next <CSS selector>` sẽ tìm phần tử tiếp theo trong DOM khớp với CSS selector đã cho.
- Cú pháp `previous <CSS selector>` sẽ tìm phần tử trước đó trong DOM khớp với CSS selector đã cho.
- `find <CSS selector>` sẽ tìm phần tử con hậu duệ đầu tiên khớp với CSS selector đã cho.
(ví dụ `find tr` sẽ nhắm đến hàng con hậu duệ đầu tiên của phần tử)

Ngoài ra, một CSS selector có thể được bao trong ký tự `<` và `/>`, mô phỏng theo cú pháp
[query literal](https://hyperscript.org/expressions/query-reference/) của hyperscript.

Các đích tương đối như thế này rất hữu ích để tạo giao diện người dùng linh hoạt mà không cần rải
nhiều thuộc tính `id` khắp DOM.

### [Swapping (Hoán đổi nội dung)](https://htmx.org/docs/\#swapping)

htmx cung cấp một vài cách khác nhau để hoán đổi HTML trả về vào trong DOM. Mặc định, nội dung sẽ thay thế
`innerHTML` của phần tử đích. Bạn có thể thay đổi điều này bằng cách dùng thuộc tính [hx-swap](https://htmx.org/attributes/hx-swap/)
với bất kỳ giá trị nào sau đây:

| Tên | Mô tả |
| --- | --- |
| `innerHTML` | mặc định, đặt nội dung bên trong phần tử đích |
| `outerHTML` | thay thế toàn bộ phần tử đích bằng nội dung trả về |
| `afterbegin` | chèn nội dung trước phần tử con đầu tiên bên trong đích |
| `beforebegin` | chèn nội dung trước đích, trong phần tử cha của đích |
| `beforeend` | thêm nội dung sau phần tử con cuối cùng bên trong đích |
| `afterend` | thêm nội dung sau đích, trong phần tử cha của đích |
| `delete` | xóa phần tử đích bất kể phản hồi là gì |
| `none` | không thêm nội dung từ phản hồi ( [Out of Band Swaps](https://htmx.org/docs/#oob_swaps) và [Response Headers](https://htmx.org/docs/#response-headers) vẫn được xử lý) |

#### [Morph Swap](https://htmx.org/docs/\#morphing)

Ngoài các cơ chế swap tiêu chuẩn ở trên, htmx còn hỗ trợ swap kiểu _morphing_, thông qua extension. Morph swap
cố gắng _hợp nhất_ nội dung mới vào DOM hiện có, thay vì chỉ đơn giản thay thế nó. Chúng thường làm tốt hơn việc
giữ lại trạng thái như focus, trạng thái video, v.v. bằng cách biến đổi các node hiện có tại chỗ trong quá trình swap, với
cái giá là tốn CPU hơn.

Các extension sau đây có sẵn cho kiểu swap morph:

- [Idiomorph](https://htmx.org/extensions/idiomorph) – Một thuật toán morph do đội ngũ phát triển htmx tạo ra.
- [Morphdom Swap](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/morphdom-swap/README.md) – Dựa trên [morphdom](https://github.com/patrick-steele-idem/morphdom),
thư viện morph DOM nguyên bản.
- [Alpine-morph](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/alpine-morph/README.md) – Dựa trên plugin [alpine morph](https://alpinejs.dev/plugins/morph), phối hợp
tốt với alpine.js

#### [View Transitions](https://htmx.org/docs/\#view-transitions)

[View Transitions API](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) mới, còn đang thử nghiệm,
cho phép nhà phát triển tạo hiệu ứng chuyển động giữa các trạng thái DOM khác nhau. API này vẫn đang được phát triển tích cực
và chưa có sẵn trên mọi trình duyệt, nhưng htmx cung cấp cách làm việc với API mới này, tự động dùng cơ chế
không-transition nếu API không khả dụng trên trình duyệt đó.

Bạn có thể thử nghiệm API mới này theo các cách sau:

- Đặt biến cấu hình `htmx.config.globalViewTransitions` thành `true` để dùng transition cho mọi swap
- Dùng tùy chọn `transition:true` trong thuộc tính `hx-swap`
- Nếu một swap phần tử sẽ được chuyển tiếp do một trong hai cấu hình trên, bạn có thể bắt sự kiện
`htmx:beforeTransition` và gọi `preventDefault()` để hủy chuyển tiếp.

View Transition có thể được cấu hình bằng CSS, như mô tả trong [tài liệu Chrome về tính năng này](https://developer.chrome.com/docs/web-platform/view-transitions/#simple-customization).

Bạn có thể xem ví dụ view transition trên trang [Ví dụ hiệu ứng động](https://htmx.org/examples/animations#view-transitions).

#### [Tùy chọn Swap](https://htmx.org/docs/\#swap-options)

Thuộc tính [hx-swap](https://htmx.org/attributes/hx-swap/) hỗ trợ nhiều tùy chọn để tinh chỉnh hành vi swap của htmx. Ví dụ,
mặc định htmx sẽ swap tiêu đề của thẻ title tìm thấy ở bất kỳ đâu trong nội dung mới. Bạn có thể tắt hành vi này
bằng cách đặt modifier `ignoreTitle` thành true:

```html
    <button hx-post="/like" hx-swap="outerHTML ignoreTitle:true">Like</button>
```

Các modifier có sẵn trên `hx-swap` là:

| Tùy chọn | Mô tả |
| --- | --- |
| `transition` | `true` hoặc `false`, có dùng View Transition API cho swap này hay không |
| `swap` | Độ trễ swap cần dùng (ví dụ `100ms`) giữa lúc nội dung cũ bị xóa và nội dung mới được chèn vào |
| `settle` | Độ trễ settle cần dùng (ví dụ `100ms`) giữa lúc nội dung mới được chèn và lúc nó được “ổn định” |
| `ignoreTitle` | Nếu đặt `true`, tiêu đề bất kỳ tìm thấy trong nội dung mới sẽ bị bỏ qua và không cập nhật tiêu đề tài liệu |
| `scroll` | `top` hoặc `bottom`, sẽ cuộn phần tử đích tới đỉnh hoặc đáy của nó |
| `show` | `top` hoặc `bottom`, sẽ cuộn để đỉnh hoặc đáy của phần tử đích lọt vào tầm nhìn |

Tất cả modifier của swap xuất hiện sau khi kiểu swap được chỉ định, phân tách bằng dấu hai chấm.

Xem tài liệu [hx-swap](https://htmx.org/attributes/hx-swap/) để biết thêm chi tiết về các tùy chọn này.

### [Đồng bộ hóa](https://htmx.org/docs/\#synchronization)

Thường thì bạn muốn phối hợp các yêu cầu giữa hai phần tử. Ví dụ, bạn có thể muốn yêu cầu từ một phần tử
thay thế yêu cầu của phần tử khác, hoặc chờ cho đến khi yêu cầu của phần tử kia hoàn tất.

htmx cung cấp thuộc tính [`hx-sync`](https://htmx.org/attributes/hx-sync/) để giúp bạn làm điều này.

Hãy xem một tình huống tranh chấp (race condition) giữa việc submit form và yêu cầu xác thực của một input riêng lẻ trong đoạn HTML này:

```html
<form hx-post="/store">
    <input id="title" name="title" type="text"
        hx-post="/validate"
        hx-trigger="change">
    <button type="submit">Submit</button>
</form>
```

Nếu không dùng `hx-sync`, việc điền input rồi submit form ngay lập tức sẽ kích hoạt hai yêu cầu song song đến
`/validate` và `/store`.

Dùng `hx-sync="closest form:abort"` trên input sẽ theo dõi các yêu cầu trên form và hủy yêu cầu của input nếu
có yêu cầu form đang tồn tại hoặc bắt đầu trong khi yêu cầu của input đang chạy:

```html
<form hx-post="/store">
    <input id="title" name="title" type="text"
        hx-post="/validate"
        hx-trigger="change"
        hx-sync="closest form:abort">
    <button type="submit">Submit</button>
</form>
```

Điều này giải quyết việc đồng bộ hóa giữa hai phần tử theo cách khai báo (declarative).

htmx cũng hỗ trợ cách hủy yêu cầu theo lập trình: bạn có thể gửi sự kiện `htmx:abort` đến một phần tử để
hủy mọi yêu cầu đang chạy:

```html
<button id="request-button" hx-post="/example">
    Issue Request
</button>
<button onclick="htmx.trigger('#request-button', 'htmx:abort')">
    Cancel Request
</button>
```

Có thể tìm thêm ví dụ và chi tiết trên [trang thuộc tính `hx-sync`.](https://htmx.org/attributes/hx-sync/)

### [Hiệu ứng chuyển tiếp CSS](https://htmx.org/docs/\#css_transitions)

htmx giúp bạn dễ dàng dùng [CSS Transition](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions) mà không cần
javascript. Hãy xem đoạn nội dung HTML này:

```html
<div id="div1">Original Content</div>
```

Hãy tưởng tượng nội dung này được htmx thay thế qua một yêu cầu ajax bằng nội dung mới sau:

```html
<div id="div1" class="red">New Content</div>
```

Lưu ý hai điều:

- div có id _giống nhau_ trong nội dung gốc và nội dung mới
- class `red` đã được thêm vào nội dung mới

Với tình huống này, ta có thể viết một CSS transition từ trạng thái cũ sang trạng thái mới:

```css
.red {
    color: red;
    transition: all ease-in 1s ;
}
```

Khi htmx swap nội dung mới này vào, nó sẽ làm theo cách để CSS transition được áp dụng cho nội dung mới,
mang lại cho bạn một hiệu ứng chuyển tiếp mượt mà, đẹp mắt sang trạng thái mới.

Vậy, tóm lại, tất cả những gì bạn cần làm để dùng CSS transition cho một phần tử là giữ `id` của nó ổn định qua các yêu cầu!

Bạn có thể xem [Ví dụ hiệu ứng động](https://htmx.org/examples/animations/) để biết thêm chi tiết và bản demo trực tiếp.

#### [Chi tiết](https://htmx.org/docs/\#details)

Để hiểu CSS transition thực sự hoạt động thế nào trong htmx, bạn cần hiểu mô hình swap & settle bên dưới mà htmx sử dụng.

Khi nội dung mới được nhận từ server, trước khi nội dung được swap vào, nội dung hiện có
trên trang được kiểm tra để tìm các phần tử khớp theo thuộc tính `id`. Nếu tìm thấy khớp
cho một phần tử trong nội dung mới, các thuộc tính của nội dung cũ sẽ được sao chép
sang phần tử mới trước khi diễn ra swap. Nội dung mới sau đó được swap vào, nhưng với các
giá trị thuộc tính _cũ_. Cuối cùng, các giá trị thuộc tính mới được swap vào, sau một độ trễ “settle”
(mặc định 20ms). Nghe hơi điên rồ, nhưng chính điều này cho phép CSS transition hoạt động mà không cần bất kỳ javascript nào
từ phía nhà phát triển.

### [Out of Band Swaps (Hoán đổi ngoài luồng)](https://htmx.org/docs/\#oob_swaps)

Nếu bạn muốn swap nội dung từ phản hồi trực tiếp vào DOM bằng thuộc tính `id`, bạn có thể dùng
thuộc tính [hx-swap-oob](https://htmx.org/attributes/hx-swap-oob/) trong HTML của _phản hồi_:

```html
<div id="message" hx-swap-oob="true">Swap me directly!</div>
Additional Content
```

Trong phản hồi này, `div#message` sẽ được swap trực tiếp vào phần tử DOM khớp với nó, trong khi nội dung
bổ sung sẽ được swap vào đích theo cách thông thường.

Bạn có thể dùng kỹ thuật này để “ăn theo” các cập nhật trên các yêu cầu khác.

#### [Vấn đề với bảng (Troublesome Tables)](https://htmx.org/docs/\#troublesome-tables)

Các phần tử bảng có thể gây rắc rối khi kết hợp với out of band swap, vì theo đặc tả HTML, nhiều phần tử
không thể tự đứng riêng trong DOM (ví dụ `<tr>` hay `<td>`).

Để tránh vấn đề này, bạn có thể dùng thẻ `template` để bọc các phần tử này:

```html
<template>
  <tr id="message" hx-swap-oob="true"><td>Joe</td><td>Smith</td></tr>
</template>
```

#### [Lệnh Swap từng phần từ Server (Server-Sent Partial Swap Commands)](https://htmx.org/docs/\#partial_swaps)

Đối với các phản hồi phức tạp hơn cần cập nhật nhiều phần của trang, htmx hỗ trợ
[`<hx-partial>`](https://htmx.org/attributes/hx-partial/) — một định dạng lệnh swap do server gửi. Server
bọc nội dung trong thẻ `<hx-partial hx-target="...">`; htmx đọc các chỉ dẫn nhắm đích,
thực hiện swap, rồi loại bỏ hoàn toàn phần bọc đó. Không có gì từ bản thân thẻ này
xuất hiện trong trang.

```html
<div>Updated main content</div>

<hx-partial hx-target="#cart-count">3</hx-partial>
<hx-partial hx-target="#cart-total">$29.97</hx-partial>
```

Giống như `hx-swap-oob`, partial được thực thi **trước** swap chính, và các đích được xác định
tương đối theo phần tử kích hoạt, dùng đầy đủ bộ từ vựng của [CSS selector mở rộng](https://htmx.org/docs/#extended-css-selectors)
(`closest`, `find`, `next`, `previous`, v.v.).

Xem [tài liệu `hx-partial`](https://htmx.org/attributes/hx-partial/) để biết đầy đủ chi tiết.

#### [Chọn nội dung để Swap](https://htmx.org/docs/\#selecting-content-to-swap)

Nếu bạn muốn chọn một phần của HTML phản hồi để swap vào đích, bạn có thể dùng thuộc tính [hx-select](https://htmx.org/attributes/hx-select/),
nhận một CSS selector và chọn các phần tử khớp từ phản hồi.

Bạn cũng có thể chọn ra các phần nội dung cho một swap ngoài luồng bằng thuộc tính [hx-select-oob](https://htmx.org/attributes/hx-select-oob/),
nhận danh sách các id phần tử để chọn ra và swap.

#### [Giữ nguyên nội dung trong lúc Swap](https://htmx.org/docs/\#preserving-content-during-a-swap)

Nếu có nội dung mà bạn muốn giữ nguyên qua các lần swap (ví dụ một trình phát video mà bạn muốn tiếp tục phát
ngay cả khi có swap xảy ra), bạn có thể dùng thuộc tính [hx-preserve](https://htmx.org/attributes/hx-preserve/)
trên các phần tử bạn muốn giữ nguyên.

### [Tham số](https://htmx.org/docs/\#parameters)

Mặc định, một phần tử gây ra yêu cầu sẽ gửi kèm giá trị của nó, nếu có. Nếu phần tử là một form, nó
sẽ gửi kèm giá trị của tất cả input bên trong nó.

Cũng như với form HTML thông thường, thuộc tính `name` của input được dùng làm tên tham số trong yêu cầu mà htmx gửi.

Ngoài ra, nếu phần tử gây ra một yêu cầu không phải `GET`, giá trị của tất cả input thuộc form liên quan sẽ
được gửi kèm (thường là form bao quanh gần nhất, nhưng có thể khác nếu dùng ví dụ `<button form="associated-form">`).

Nếu bạn muốn gửi kèm giá trị của các phần tử khác, bạn có thể dùng thuộc tính [hx-include](https://htmx.org/attributes/hx-include/)
với một CSS selector cho tất cả các phần tử mà bạn muốn gửi kèm giá trị trong yêu cầu.

Nếu bạn muốn lọc bớt một số tham số, bạn có thể dùng thuộc tính [hx-params](https://htmx.org/attributes/hx-params/).

Cuối cùng, nếu bạn muốn thay đổi tham số theo lập trình, bạn có thể dùng sự kiện [htmx:configRequest](https://htmx.org/events/#htmx:configRequest).

#### [Tải file lên (File Upload)](https://htmx.org/docs/\#files)

Nếu bạn muốn tải file lên qua yêu cầu htmx, bạn có thể đặt thuộc tính [hx-encoding](https://htmx.org/attributes/hx-encoding/) thành
`multipart/form-data`. Điều này sẽ dùng một đối tượng `FormData` để gửi yêu cầu, đảm bảo file được gửi kèm
đúng cách trong yêu cầu.

Lưu ý rằng tùy vào công nghệ phía server của bạn, bạn có thể phải xử lý các yêu cầu có kiểu nội dung body này
theo cách rất khác.

Lưu ý rằng htmx phát ra sự kiện `htmx:xhr:progress` định kỳ dựa trên sự kiện `progress` tiêu chuẩn trong khi tải lên,
mà bạn có thể móc vào để hiển thị tiến trình tải lên.

Xem [phần ví dụ](https://htmx.org/examples/) để biết thêm các mẫu form nâng cao, bao gồm [thanh tiến trình](https://htmx.org/examples/file-upload/) và [xử lý lỗi](https://htmx.org/examples/file-upload-input/).

#### [Giá trị bổ sung](https://htmx.org/docs/\#extra-values)

Bạn có thể thêm giá trị bổ sung vào một yêu cầu bằng thuộc tính [hx-vals](https://htmx.org/attributes/hx-vals/) (cặp tên-biểu thức theo định dạng JSON) và
thuộc tính [hx-vars](https://htmx.org/attributes/hx-vars/) (cặp tên-biểu thức phân tách bằng dấu phẩy, được tính toán động).

### [Xác nhận yêu cầu](https://htmx.org/docs/\#confirming)

Thường thì bạn sẽ muốn xác nhận một hành động trước khi gửi yêu cầu. htmx hỗ trợ thuộc tính [`hx-confirm`](https://htmx.org/attributes/hx-confirm/),
cho phép bạn xác nhận một hành động bằng một hộp thoại javascript đơn giản:

```html
<button hx-delete="/account" hx-confirm="Are you sure you wish to delete your account?">
    Delete My Account
</button>
```

Dùng sự kiện, bạn có thể triển khai các hộp thoại xác nhận phức tạp hơn. [Ví dụ confirm](https://htmx.org/examples/confirm/)
cho thấy cách dùng thư viện [sweetalert2](https://sweetalert2.github.io/) để xác nhận các hành động htmx.

#### [Xác nhận yêu cầu bằng sự kiện](https://htmx.org/docs/\#confirming-requests-using-events)

Một cách khác để xác nhận là qua [sự kiện `htmx:confirm`](https://htmx.org/events/#htmx:confirm). Sự kiện
này được kích hoạt trên _mọi_ trigger của một yêu cầu (không chỉ trên các phần tử có thuộc tính `hx-confirm`) và có thể được dùng
để triển khai xác nhận bất đồng bộ cho yêu cầu.

Đây là ví dụ dùng [sweet alert](https://sweetalert.js.org/guides/) trên bất kỳ phần tử nào có thuộc tính `confirm-with-sweet-alert='true'`:

```javascript
document.body.addEventListener('htmx:confirm', function(evt) {
  if (evt.target.matches("[confirm-with-sweet-alert='true']")) {
    evt.preventDefault();
    swal({
      title: "Are you sure?",
      text: "Are you sure you are sure?",
      icon: "warning",
      buttons: true,
      dangerMode: true,
    }).then((confirmed) => {
      if (confirmed) {
        evt.detail.issueRequest();
      }
    });
  }
});
```

## [Kế thừa thuộc tính](https://htmx.org/docs/\#inheritance)

Hầu hết các thuộc tính trong htmx được kế thừa: chúng áp dụng cho phần tử chứa chúng cũng như mọi phần tử con. Điều này
cho phép bạn “đẩy” thuộc tính lên trên trong DOM để tránh lặp code. Hãy xem đoạn htmx sau:

```html
<button hx-delete="/account" hx-confirm="Are you sure?">
    Delete My Account
</button>
<button hx-put="/account" hx-confirm="Are you sure?">
    Update My Account
</button>
```

Ở đây ta có thuộc tính `hx-confirm` bị lặp lại. Ta có thể đẩy thuộc tính này lên phần tử cha:

```html
<div hx-confirm="Are you sure?">
    <button hx-delete="/account">
        Delete My Account
    </button>
    <button hx-put="/account">
        Update My Account
    </button>
</div>
```

Thuộc tính `hx-confirm` này giờ sẽ áp dụng cho tất cả phần tử dùng htmx bên trong nó.

Đôi khi bạn muốn hủy sự kế thừa này. Hãy tưởng tượng nếu ta có một nút hủy trong nhóm này, nhưng không muốn nó
phải xác nhận. Ta có thể thêm chỉ dẫn `unset` như sau:

```html
<div hx-confirm="Are you sure?">
    <button hx-delete="/account">
        Delete My Account
    </button>
    <button hx-put="/account">
        Update My Account
    </button>
    <button hx-confirm="unset" hx-get="/">
        Cancel
    </button>
</div>
```

Hai nút phía trên khi đó sẽ hiển thị hộp thoại xác nhận, còn nút hủy phía dưới thì không.

Sự kế thừa có thể được tắt theo từng phần tử và từng thuộc tính riêng lẻ, dùng thuộc tính
[`hx-disinherit`](https://htmx.org/attributes/hx-disinherit/).

Nếu bạn muốn tắt hoàn toàn sự kế thừa thuộc tính, bạn có thể đặt biến cấu hình `htmx.config.disableInheritance`
thành `true`. Điều này sẽ tắt kế thừa như mặc định, và cho phép bạn chỉ định kế thừa một cách rõ ràng
bằng thuộc tính [`hx-inherit`](https://htmx.org/attributes/hx-inherit/).

## [Boosting](https://htmx.org/docs/\#boosting)

Htmx hỗ trợ “boosting” (tăng cường) các thẻ anchor và form HTML thông thường bằng thuộc tính [hx-boost](https://htmx.org/attributes/hx-boost/). Thuộc tính
này sẽ chuyển đổi tất cả thẻ anchor và form thành yêu cầu AJAX, mặc định nhắm vào phần body của trang.

Đây là một ví dụ:

```html
<div hx-boost="true">
    <a href="/blog">Blog</a>
</div>
```

Thẻ anchor trong div này sẽ gửi yêu cầu AJAX `GET` đến `/blog` và swap phản hồi vào thẻ `body`.

### [Tăng cường tiệm tiến (Progressive Enhancement)](https://htmx.org/docs/\#progressive_enhancement)

Một đặc điểm của `hx-boost` là nó suy giảm nhẹ nhàng (degrade gracefully) nếu javascript không được bật: các liên kết và form vẫn tiếp
tục hoạt động, chỉ là chúng không dùng yêu cầu ajax nữa. Đây được gọi là
[Tăng cường tiệm tiến (Progressive Enhancement)](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement), và nó cho phép
một lượng người dùng rộng hơn có thể sử dụng chức năng của trang web bạn.

Các mẫu htmx khác cũng có thể được điều chỉnh để đạt được tăng cường tiệm tiến, nhưng chúng sẽ đòi hỏi cân nhắc kỹ hơn.

Hãy xét ví dụ [active search](https://htmx.org/examples/active-search/). Như hiện tại, nó sẽ không suy giảm nhẹ nhàng:
người không bật javascript sẽ không thể dùng tính năng này. Điều này được làm vậy vì mục đích đơn giản,
để giữ ví dụ càng ngắn gọn càng tốt.

Tuy nhiên, bạn có thể bọc input được tăng cường bởi htmx trong một phần tử form:

```html
<form action="/search" method="POST">
    <input class="form-control" type="search"
        name="search" placeholder="Begin typing to search users..."
        hx-post="/search"
        hx-trigger="keyup changed delay:500ms, search"
        hx-target="#search-results"
        hx-indicator=".htmx-indicator">
</form>
```

Với thiết lập này, các client có bật javascript vẫn có trải nghiệm active-search tốt, còn các client không
bật javascript vẫn có thể nhấn phím enter để tìm kiếm. Thậm chí tốt hơn, bạn có thể thêm cả một nút “Search”.
Khi đó bạn sẽ cần cập nhật form với `hx-post` phản ánh thuộc tính `action`, hoặc có thể dùng `hx-boost`
trên đó.

Bạn sẽ cần kiểm tra phía server header `HX-Request` để phân biệt giữa yêu cầu do htmx điều khiển và
yêu cầu thông thường, nhằm xác định chính xác nên render gì cho client.

Các mẫu khác cũng có thể được điều chỉnh tương tự để đạt được yêu cầu tăng cường tiệm tiến cho ứng dụng của bạn.

Như bạn thấy, điều này đòi hỏi cân nhắc và công sức nhiều hơn. Nó cũng loại bỏ hoàn toàn một số chức năng.
Những đánh đổi này phải do chính bạn, nhà phát triển, quyết định, dựa trên mục tiêu và đối tượng người dùng của dự án.

[Khả năng tiếp cận (Accessibility)](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/What_is_accessibility) là một khái niệm
liên quan chặt chẽ đến tăng cường tiệm tiến. Sử dụng các kỹ thuật tăng cường tiệm tiến như `hx-boost` sẽ giúp
ứng dụng htmx của bạn dễ tiếp cận hơn với nhiều người dùng.

Các ứng dụng dựa trên htmx rất giống với các ứng dụng web thông thường không dùng AJAX, vì htmx hướng đến HTML.

Do đó, các khuyến nghị về khả năng tiếp cận HTML thông thường vẫn áp dụng. Ví dụ:

- Sử dụng HTML ngữ nghĩa (semantic HTML) càng nhiều càng tốt (tức là dùng đúng thẻ cho đúng mục đích)
- Đảm bảo trạng thái focus hiển thị rõ ràng
- Gắn nhãn văn bản (label) cho tất cả các trường form
- Tối đa hóa khả năng đọc của ứng dụng bằng font chữ, độ tương phản phù hợp, v.v.

## [Web Sockets & SSE](https://htmx.org/docs/\#websockets-and-sse)

Web Sockets và Server Sent Events (SSE) được hỗ trợ qua extension. Vui lòng xem
trang [SSE extension](https://htmx.org/extensions/sse) và [WebSocket extension](https://htmx.org/extensions/ws)
để tìm hiểu thêm.

## [Hỗ trợ lịch sử (History Support)](https://htmx.org/docs/\#history)

Htmx cung cấp một cơ chế đơn giản để tương tác với [History API của trình duyệt](https://developer.mozilla.org/en-US/docs/Web/API/History_API):

Nếu bạn muốn một phần tử đẩy URL yêu cầu của nó vào thanh điều hướng trình duyệt và thêm trạng thái hiện tại của trang
vào lịch sử trình duyệt, hãy thêm thuộc tính [hx-push-url](https://htmx.org/attributes/hx-push-url/):

```html
<a hx-get="/blog" hx-push-url="true">Blog</a>
```

Khi người dùng nhấp vào liên kết này, htmx sẽ chụp lại (snapshot) DOM hiện tại và lưu trữ nó trước khi gửi yêu cầu đến /blog.
Sau đó nó thực hiện swap và đẩy một vị trí mới vào ngăn xếp lịch sử.

Khi người dùng nhấn nút back, htmx sẽ lấy lại nội dung cũ từ bộ nhớ lưu trữ và swap nó trở lại vào đích,
mô phỏng việc “quay lại” trạng thái trước đó. Nếu vị trí không được tìm thấy trong cache, htmx sẽ gửi một yêu cầu
ajax đến URL đã cho, với header `HX-History-Restore-Request` được đặt thành true, và mong đợi nhận lại HTML cần thiết
cho toàn bộ trang. Bạn nên luôn đặt `htmx.config.historyRestoreAsHxRequest` thành false để ngăn header `HX-Request`,
nhờ đó có thể an toàn dùng để trả về các phần (partial). Ngoài ra, nếu biến cấu hình `htmx.config.refreshOnHistoryMiss`
được đặt thành true, nó sẽ thực hiện một lần refresh trình duyệt hoàn toàn.

**LƯU Ý:** Nếu bạn đẩy một URL vào lịch sử, bạn **bắt buộc** phải có khả năng điều hướng đến URL đó và nhận về một trang đầy đủ!
Người dùng có thể copy và dán URL đó vào email, hoặc tab mới. Ngoài ra, htmx sẽ cần toàn bộ trang khi khôi phục
lịch sử nếu trang đó không có trong cache lịch sử.

### [Chỉ định phần tử chụp lịch sử](https://htmx.org/docs/\#specifying-history-snapshot-element)

Mặc định, htmx sẽ dùng `body` để chụp và khôi phục snapshot lịch sử. Đây thường là lựa chọn đúng, nhưng
nếu bạn muốn dùng một phần tử hẹp hơn để chụp, bạn có thể dùng thuộc tính [hx-history-elt](https://htmx.org/attributes/hx-history-elt/)
để chỉ định một phần tử khác.

Cẩn thận: phần tử này cần phải có mặt trên mọi trang, nếu không việc khôi phục từ lịch sử sẽ không hoạt động đáng tin cậy.

### [Hoàn tác biến đổi DOM do thư viện bên thứ 3 gây ra](https://htmx.org/docs/\#undoing-dom-mutations-by-3rd-party-libraries)

Nếu bạn đang dùng một thư viện bên thứ 3 và muốn dùng tính năng lịch sử của htmx, bạn sẽ cần dọn dẹp DOM trước khi
snapshot được chụp. Hãy xét thư viện [Tom Select](https://tom-select.js.org/), giúp các phần tử select trở thành
trải nghiệm người dùng phong phú hơn nhiều. Hãy thiết lập TomSelect để biến bất kỳ phần tử input nào có class
`.tomselect` thành một select element phong phú.

Đầu tiên ta cần khởi tạo các phần tử có class đó trong nội dung mới:

```javascript
htmx.onLoad(function (target) {
    // find all elements in the new content that should be
    // an editor and init w/ TomSelect
    var editors = target.querySelectorAll(".tomselect")
            .forEach(elt => new TomSelect(elt))
});
```

Điều này sẽ tạo một selector phong phú cho tất cả các phần tử input có class `.tomselect`. Tuy nhiên, nó biến đổi
DOM và ta không muốn biến đổi đó được lưu vào cache lịch sử, vì TomSelect sẽ được khởi tạo lại khi nội dung
lịch sử được tải trở lại màn hình.

Để xử lý điều này, ta cần bắt sự kiện `htmx:beforeHistorySave` và dọn sạch các biến đổi của TomSelect bằng cách gọi
`destroy()` trên chúng:

```javascript
htmx.on('htmx:beforeHistorySave', function() {
    // find all TomSelect elements
    document.querySelectorAll('.tomSelect')
            .forEach(elt => elt.tomselect.destroy()) // and call destroy() on them
})
```

Điều này sẽ đưa DOM trở lại HTML gốc, nhờ đó cho phép chụp một snapshot sạch.

### [Tắt chụp snapshot lịch sử](https://htmx.org/docs/\#disabling-history-snapshots)

Việc chụp snapshot lịch sử có thể bị tắt cho một URL bằng cách đặt thuộc tính [hx-history](https://htmx.org/attributes/hx-history/) thành `false`
trên bất kỳ phần tử nào trong tài liệu hiện tại, hoặc bất kỳ đoạn html nào được htmx tải vào tài liệu hiện tại. Điều này có thể được dùng
để ngăn dữ liệu nhạy cảm đi vào cache `localStorage`, điều có thể quan trọng đối với các máy tính dùng chung / công cộng.
Việc điều hướng lịch sử vẫn hoạt động như mong đợi, nhưng khi khôi phục, URL sẽ được yêu cầu từ server thay vì
từ cache lịch sử cục bộ.

## [Request & Response](https://htmx.org/docs/\#requests)

Htmx mong đợi các phản hồi cho những yêu cầu AJAX mà nó gửi phải là HTML, thường là các đoạn HTML (fragment) (dù một tài liệu
HTML đầy đủ, kết hợp với thẻ [hx-select](https://htmx.org/attributes/hx-select/), cũng có thể hữu ích). Htmx sau đó sẽ swap
HTML trả về vào tài liệu tại đích đã chỉ định, với chiến lược swap đã chỉ định.

Đôi khi bạn có thể muốn không làm gì trong lúc swap, nhưng vẫn muốn kích hoạt một sự kiện phía client ([xem bên dưới](https://htmx.org/docs/#response-headers)).

Trong trường hợp này, mặc định, bạn có thể trả về mã phản hồi `204 - No Content`, và htmx sẽ bỏ qua nội dung
của phản hồi.

Trong trường hợp server trả về phản hồi lỗi (ví dụ 404 hoặc 501), htmx sẽ kích hoạt sự kiện [`htmx:responseError`](https://htmx.org/events/#htmx:responseError),
mà bạn có thể xử lý.

Trong trường hợp lỗi kết nối, sự kiện [`htmx:sendError`](https://htmx.org/events/#htmx:sendError) sẽ được kích hoạt.

### [Cấu hình xử lý phản hồi](https://htmx.org/docs/\#response-handling)

Bạn có thể cấu hình hành vi trên của htmx bằng cách thay đổi hoặc thay thế mảng `htmx.config.responseHandling`. Đối
tượng này là một tập hợp các đối tượng JavaScript được định nghĩa như sau:

```js
    responseHandling: [\
        {code:"204", swap: false},   // 204 - No Content by default does nothing, but is not an error\
        {code:"[23]..", swap: true}, // 200 & 300 responses are non-errors and are swapped\
        {code:"[45]..", swap: false, error:true}, // 400 & 500 responses are not swapped and are errors\
        {code:"...", swap: false}    // catch all for any other response code\
    ]
```

Khi htmx nhận một phản hồi, nó sẽ lặp qua mảng `htmx.config.responseHandling` theo thứ tự và kiểm tra xem thuộc tính
`code` của đối tượng, khi được coi như một Biểu thức Chính quy (Regular Expression), có khớp với phản hồi hiện tại không. Nếu một mục
khớp với mã phản hồi hiện tại, nó sẽ được dùng để xác định phản hồi có được xử lý và xử lý như thế nào.

Các trường có sẵn để cấu hình xử lý phản hồi trên các mục của mảng này là:

- `code` – một Chuỗi biểu diễn một biểu thức chính quy sẽ được kiểm tra với mã phản hồi.
- `swap` – `true` nếu phản hồi nên được swap vào DOM, `false` nếu không
- `error` – `true` nếu htmx nên coi phản hồi này là lỗi
- `ignoreTitle` – `true` nếu htmx nên bỏ qua các thẻ title trong phản hồi
- `select` – một CSS selector dùng để chọn nội dung từ phản hồi
- `target` – một CSS selector chỉ định đích thay thế cho phản hồi
- `swapOverride` – một cơ chế swap thay thế cho phản hồi

#### [Ví dụ cấu hình xử lý phản hồi](https://htmx.org/docs/\#response-handling-examples)

Để minh họa cách dùng cấu hình này, hãy xét tình huống khi một framework phía server trả về phản hồi
[`422 - Unprocessable Entity`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422) khi xảy ra lỗi xác thực. Mặc định, htmx sẽ bỏ qua phản hồi này,
vì nó khớp với Biểu thức Chính quy `[45]..`.

Dùng cơ chế [cấu hình meta](https://htmx.org/docs/#configuration-options) để cấu hình responseHandling, ta có thể thêm cấu hình
sau:

```html
<!--
  * 204 No Content by default does nothing, but is not an error
  * 2xx, 3xx and 422 responses are non-errors and are swapped
  * 4xx & 5xx responses are not swapped and are errors
  * all other responses are swapped using "..." as a catch-all
-->
<meta
	name="htmx-config"
	content='{
        "responseHandling":[\
            {"code":"204", "swap": false},\
            {"code":"[23]..", "swap": true},\
            {"code":"422", "swap": true},\
            {"code":"[45]..", "swap": false, "error":true},\
            {"code":"...", "swap": true}\
        ]
    }'
/>
```

Nếu bạn muốn swap mọi thứ, bất kể mã phản hồi HTTP là gì, bạn có thể dùng cấu hình này:

```html
<meta name="htmx-config" content='{"responseHandling": [{"code":".*", "swap": true}]}' /> <!--all responses are swapped-->
```

Cuối cùng, cũng đáng cân nhắc dùng extension [Response Targets](https://htmx.org/extensions/response-targets),
cho phép bạn cấu hình hành vi của mã phản hồi một cách khai báo thông qua thuộc tính.

### [CORS](https://htmx.org/docs/\#cors)

Khi dùng htmx trong ngữ cảnh cross-origin (khác nguồn gốc), nhớ cấu hình web server của bạn để thiết lập header
Access-Control để các header của htmx được nhìn thấy phía client.

- [Access-Control-Allow-Headers (cho request header)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)
- [Access-Control-Expose-Headers (cho response header)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)

[Xem tất cả request header và response header mà htmx triển khai.](https://htmx.org/reference/#request_headers)

### [Request Header](https://htmx.org/docs/\#request-headers)

htmx thêm vào yêu cầu một số header hữu ích:

| Header | Mô tả |
| --- | --- |
| `HX-Boosted` | cho biết yêu cầu này thông qua một phần tử dùng [hx-boost](https://htmx.org/attributes/hx-boost/) |
| `HX-Current-URL` | URL hiện tại của trình duyệt |
| `HX-History-Restore-Request` | “true” nếu yêu cầu này dùng để khôi phục lịch sử sau khi không tìm thấy trong cache lịch sử cục bộ |
| `HX-Prompt` | phản hồi của người dùng cho một [hx-prompt](https://htmx.org/attributes/hx-prompt/) |
| `HX-Request` | luôn là “true” trừ trên các yêu cầu khôi phục lịch sử nếu `htmx.config.historyRestoreAsHxRequest` bị tắt |
| `HX-Target` | `id` của phần tử đích nếu có |
| `HX-Trigger-Name` | `name` của phần tử kích hoạt nếu có |
| `HX-Trigger` | `id` của phần tử kích hoạt nếu có |

### [Response Header](https://htmx.org/docs/\#response-headers)

htmx hỗ trợ một số response header đặc thù của htmx:

- [`HX-Location`](https://htmx.org/headers/hx-location/) – cho phép bạn thực hiện redirect phía client mà không cần tải lại toàn bộ trang
- [`HX-Push-Url`](https://htmx.org/headers/hx-push-url/) – đẩy một url mới vào ngăn xếp lịch sử
- [`HX-Redirect`](https://htmx.org/headers/hx-redirect/) – có thể dùng để redirect phía client đến vị trí mới
- `HX-Refresh` – nếu đặt thành “true” thì phía client sẽ thực hiện refresh toàn bộ trang
- [`HX-Replace-Url`](https://htmx.org/headers/hx-replace-url/) – thay thế URL hiện tại trên thanh địa chỉ
- `HX-Reswap` – cho phép bạn chỉ định cách phản hồi sẽ được swap. Xem [hx-swap](https://htmx.org/attributes/hx-swap/) để biết các giá trị khả dụng
- `HX-Retarget` – một CSS selector cập nhật đích của việc cập nhật nội dung sang một phần tử khác trên trang
- `HX-Reselect` – một CSS selector cho phép bạn chọn phần nào của phản hồi được dùng để swap vào. Ghi đè một [`hx-select`](https://htmx.org/attributes/hx-select/) sẵn có trên phần tử kích hoạt
- [`HX-Trigger`](https://htmx.org/headers/hx-trigger/) – cho phép bạn kích hoạt sự kiện phía client
- [`HX-Trigger-After-Settle`](https://htmx.org/headers/hx-trigger/) – cho phép bạn kích hoạt sự kiện phía client sau bước settle
- [`HX-Trigger-After-Swap`](https://htmx.org/headers/hx-trigger/) – cho phép bạn kích hoạt sự kiện phía client sau bước swap

Để biết thêm về các header `HX-Trigger`, xem [Response Header `HX-Trigger`](https://htmx.org/headers/hx-trigger/).

Việc submit form qua htmx có lợi ích là không còn cần đến [mẫu Post/Redirect/Get](https://en.wikipedia.org/wiki/Post/Redirect/Get).
Sau khi xử lý thành công một yêu cầu POST trên server, bạn không cần trả về [HTTP 302 (Redirect)](https://en.wikipedia.org/wiki/HTTP_302). Bạn có thể trực tiếp trả về đoạn HTML mới.

Ngoài ra, các response header ở trên không được cung cấp cho htmx để xử lý với các mã phản hồi 3xx Redirect như [HTTP 302 (Redirect)](https://en.wikipedia.org/wiki/HTTP_302). Thay vào đó, trình duyệt sẽ tự chặn việc chuyển hướng nội bộ và trả về các header cùng phản hồi từ URL được chuyển hướng đến. Khi có thể, hãy dùng các mã phản hồi thay thế như 200 để cho phép trả về các response header này.

### [Thứ tự các bước thực hiện yêu cầu](https://htmx.org/docs/\#request-operations)

Thứ tự các bước thực hiện trong một yêu cầu htmx là:

- Phần tử được kích hoạt và bắt đầu một yêu cầu
  - Các giá trị được thu thập cho yêu cầu
  - Class `htmx-request` được gắn vào các phần tử phù hợp
  - Yêu cầu sau đó được gửi bất đồng bộ qua AJAX
    - Khi nhận được phản hồi, phần tử đích được gắn class `htmx-swapping`
    - Một độ trễ swap tùy chọn được áp dụng (xem thuộc tính [hx-swap](https://htmx.org/attributes/hx-swap/))
    - Việc swap nội dung thực sự được thực hiện
      - class `htmx-swapping` bị gỡ khỏi đích
      - class `htmx-added` được thêm vào mỗi phần nội dung mới
      - class `htmx-settling` được gắn vào đích
      - Một độ trễ settle được thực hiện (mặc định: 20ms)
      - DOM được “ổn định” (settle)
      - class `htmx-settling` bị gỡ khỏi đích
      - class `htmx-added` bị gỡ khỏi mỗi phần nội dung mới

Bạn có thể dùng các class `htmx-swapping` và `htmx-settling` để tạo
[hiệu ứng chuyển tiếp CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions) giữa các trang.

## [Xác thực (Validation)](https://htmx.org/docs/\#validation)

Htmx tích hợp với [HTML5 Validation API](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
và sẽ không gửi yêu cầu cho một form nếu một input có thể xác thực bị không hợp lệ. Điều này đúng cho cả yêu cầu AJAX lẫn
gửi qua WebSocket.

Htmx kích hoạt các sự kiện xung quanh việc xác thực mà bạn có thể dùng để móc vào xác thực tùy chỉnh và xử lý lỗi:

- `htmx:validation:validate` – được gọi trước khi phương thức `checkValidity()` của phần tử được gọi. Có thể dùng để thêm
logic xác thực tùy chỉnh
- `htmx:validation:failed` – được gọi khi `checkValidity()` trả về false, cho biết input không hợp lệ
- `htmx:validation:halted` – được gọi khi một yêu cầu không được gửi do lỗi xác thực. Các lỗi cụ thể có thể tìm thấy
trong đối tượng `event.detail.errors`

Các phần tử không phải form mặc định không xác thực trước khi gửi yêu cầu, nhưng bạn có thể bật xác thực bằng cách đặt
thuộc tính [`hx-validate`](https://htmx.org/attributes/hx-validate/) thành “true”.

Việc submit form thông thường của trình duyệt tự động cảnh báo người dùng về bất kỳ lỗi xác thực nào và tự động focus vào input không hợp lệ đầu tiên. Vì lý do tương thích ngược, mặc định htmx không báo cáo việc xác thực cho người dùng, và bạn nên luôn bật tùy chọn này bằng cách đặt `htmx.config.reportValidityOfForms` thành `true` để khôi phục hành vi mặc định của trình duyệt.

### [Ví dụ xác thực](https://htmx.org/docs/\#validation-example)

Đây là ví dụ về một input dùng thuộc tính [`hx-on`](https://htmx.org/attributes/hx-on) để bắt
sự kiện `htmx:validation:validate` và yêu cầu input phải có giá trị `foo`:

```html
<form id="example-form" hx-post="/test">
    <input name="example"
           onkeyup="this.setCustomValidity('') // reset the validation on keyup"
           hx-on:htmx:validation:validate="if(this.value != 'foo') {
                    this.setCustomValidity('Please enter the value foo') // set the validation error
                    htmx.find('#example-form').reportValidity()          // report the issue
                }">
</form>
```

Lưu ý rằng mọi xác thực phía client đều phải được làm lại ở phía server, vì chúng luôn có thể bị bỏ qua (bypass).

## [Hiệu ứng động (Animations)](https://htmx.org/docs/\#animations)

Htmx cho phép bạn dùng [CSS transition](https://htmx.org/docs/#css_transitions)
trong nhiều tình huống chỉ với HTML và CSS.

Vui lòng xem [Hướng dẫn hiệu ứng động](https://htmx.org/examples/animations/) để biết thêm chi tiết về các tùy chọn có sẵn.

## [Phần mở rộng (Extensions)](https://htmx.org/docs/\#extensions)

htmx cung cấp cơ chế [extension](https://htmx.org/extensions) cho phép bạn tùy chỉnh hành vi của thư viện.
Extension [được định nghĩa bằng javascript](https://htmx.org/extensions/building) rồi được bật thông qua
thuộc tính [`hx-ext`](https://htmx.org/attributes/hx-ext/).

### [Extension cốt lõi](https://htmx.org/docs/\#core-extensions)

htmx hỗ trợ một vài extension “cốt lõi”, được đội ngũ phát triển htmx hỗ trợ:

- [head-support](https://htmx.org/extensions/head-support) – hỗ trợ hợp nhất thông tin thẻ head (style, v.v.) trong các yêu cầu htmx
- [htmx-1-compat](https://htmx.org/extensions/htmx-1-compat) – khôi phục các mặc định & chức năng của htmx 1
- [idiomorph](https://htmx.org/extensions/idiomorph) – hỗ trợ chiến lược swap `morph` dùng idiomorph
- [preload](https://htmx.org/extensions/preload) – cho phép bạn tải trước nội dung để có hiệu năng tốt hơn
- [response-targets](https://htmx.org/extensions/response-targets) – cho phép bạn nhắm đích phần tử dựa trên mã phản hồi HTTP (ví dụ `404`)
- [sse](https://htmx.org/extensions/sse) – hỗ trợ [Server Sent Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
- [ws](https://htmx.org/extensions/ws) – hỗ trợ [Web Sockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)

Bạn có thể xem tất cả extension có sẵn trên trang [Extensions](https://htmx.org/extensions).

### [Cài đặt Extension](https://htmx.org/docs/\#installing-extensions)

Cách nhanh nhất để cài đặt các extension htmx do người khác tạo ra là tải chúng qua CDN. Nhớ luôn include thư viện htmx cốt lõi trước các extension và [bật extension](https://htmx.org/docs/#enabling-extensions). Ví dụ, nếu bạn muốn dùng extension [response-targets](https://htmx.org/extensions/response-targets), bạn có thể thêm đoạn này vào thẻ head:

```html
<head>
    <script src="https://cdn.jsdelivr.net/npm/htmx.org@2.0.11/dist/htmx.min.js" integrity="sha384-2OatzQy1H+Zd/IIrjr1TcuDGqLXeHhbooAyJY1KdQMKnr4LZ22k31GBLdYKHmVjg" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/htmx-ext-response-targets@2.0.4" integrity="sha384-T41oglUPvXLGBVyRdZsVRxNWnOOqCynaPubjUVjxhsjFTKrFJGEMm3/0KGmNQ+Pg" crossorigin="anonymous"></script>
</head>
<body hx-ext="extension-name">
    ...
```

Phiên bản chưa nén cũng có sẵn tại `https://cdn.jsdelivr.net/npm/htmx-ext-extension-name/dist/extension-name.js` (thay `extension-name` bằng tên extension).

Dù cách dùng CDN đơn giản, bạn cũng nên cân nhắc [không dùng CDN trong production](https://blog.wesleyac.com/posts/why-not-javascript-cdn). Cách dễ tiếp theo để cài extension htmx là chỉ cần sao chép chúng vào dự án của bạn. Tải extension từ `https://cdn.jsdelivr.net/npm/htmx-ext-extension-name` (thay `extension-name` bằng tên extension) ví dụ, https://cdn.jsdelivr.net/npm/htmx-ext-response-targets. Sau đó thêm nó vào thư mục phù hợp trong dự án và include nó khi cần bằng thẻ `<script>`.

Đối với các hệ thống build kiểu npm, bạn có thể cài extension htmx qua [npm](https://www.npmjs.com/) (thay `extension-name` bằng tên extension):

```sh
npm install htmx-ext-extension-name
```

Sau khi cài đặt, bạn sẽ cần dùng công cụ phù hợp để đóng gói `node_modules/htmx-ext-extension-name/dist/extension-name.js` (hoặc `.min.js`). Ví dụ, bạn có thể đóng gói extension cùng với htmx core từ `node_modules/htmx.org/dist/htmx.js` và mã nguồn riêng của dự án.

Nếu bạn dùng bundler để quản lý javascript (ví dụ Webpack, Rollup):

- Cài `htmx.org` và `htmx-ext-extension-name` qua npm (thay `extension-name` bằng tên extension)
- Import cả hai gói vào `index.js`

```js
import `htmx.org`;
import `htmx-ext-extension-name`; // replace `extension-name` with the name of the extension
```

Lưu ý: [Idiomorph](https://htmx.org/extensions/idiomorph) không tuân theo quy ước đặt tên của các extension htmx. Hãy dùng `idiomorph` thay vì `htmx-ext-idiomorph`. Ví dụ, `https://cdn.jsdelivr.net/npm/idiomorph` hoặc `npm install idiomorph`.

Lưu ý: Các extension cộng đồng được host bên ngoài repository này có thể có hướng dẫn cài đặt khác. Vui lòng kiểm tra repository tương ứng để biết hướng dẫn thiết lập.

### [Bật Extension](https://htmx.org/docs/\#enabling-extensions)

Để bật một extension, thêm thuộc tính `hx-ext="extension-name"` vào `<body>` hoặc một phần tử HTML khác (thay `extension-name` bằng tên extension). Extension sẽ được áp dụng cho tất cả phần tử con.

Ví dụ sau cho thấy cách bật extension [response-targets](https://htmx.org/extensions/response-targets), cho phép bạn chỉ định các phần tử đích khác nhau để swap dựa trên mã phản hồi HTTP.

```html
<body hx-ext="response-targets">
    ...
    <button hx-post="/register" hx-target="#response-div" hx-target-404="#not-found">
        Register!
    </button>
    <div id="response-div"></div>
    <div id="not-found"></div>
    ...
</body>
```

### [Tạo Extension](https://htmx.org/docs/\#creating-extensions)

Nếu bạn muốn tạo extension riêng cho htmx, vui lòng [xem tài liệu về extension](https://htmx.org/extensions/building).

## [Sự kiện & Ghi log](https://htmx.org/docs/\#events)

Htmx có một [cơ chế sự kiện](https://htmx.org/reference/#events) phong phú, đồng thời đóng vai trò như hệ thống ghi log.

Nếu bạn muốn đăng ký lắng nghe một sự kiện htmx nào đó, bạn có thể dùng

```js
document.body.addEventListener('htmx:load', function(evt) {
    myJavascriptLib.init(evt.detail.elt);
});
```

hoặc, nếu muốn, bạn có thể dùng hàm hỗ trợ sau của htmx:

```javascript
htmx.on("htmx:load", function(evt) {
    myJavascriptLib.init(evt.detail.elt);
});
```

Sự kiện `htmx:load` được kích hoạt mỗi khi một phần tử được htmx tải vào DOM, và về cơ bản tương đương
với sự kiện `load` thông thường.

Một số cách dùng phổ biến của sự kiện htmx là:

### [Khởi tạo thư viện bên thứ 3 bằng sự kiện](https://htmx.org/docs/\#init_3rd_party_with_events)

Việc dùng sự kiện `htmx:load` để khởi tạo nội dung phổ biến đến mức htmx cung cấp một hàm hỗ trợ:

```javascript
htmx.onLoad(function(target) {
    myJavascriptLib.init(target);
});
```

Điều này làm điều tương tự như ví dụ đầu tiên, nhưng gọn gàng hơn một chút.

### [Cấu hình yêu cầu bằng sự kiện](https://htmx.org/docs/\#config_request_with_events)

Bạn có thể xử lý sự kiện [`htmx:configRequest`](https://htmx.org/events/#htmx:configRequest) để thay đổi một yêu cầu AJAX trước khi nó được gửi đi:

```javascript
document.body.addEventListener('htmx:configRequest', function(evt) {
    evt.detail.parameters['auth_token'] = getAuthToken(); // add a new parameter into the request
    evt.detail.headers['Authentication-Token'] = getAuthToken(); // add a new header into the request
});
```

Ở đây ta thêm một tham số và một header vào yêu cầu trước khi nó được gửi.

### [Thay đổi hành vi Swap bằng sự kiện](https://htmx.org/docs/\#modifying_swapping_behavior_with_events)

Bạn có thể xử lý sự kiện [`htmx:beforeSwap`](https://htmx.org/events/#htmx:beforeSwap) để thay đổi hành vi swap của htmx:

```javascript
document.body.addEventListener('htmx:beforeSwap', function(evt) {
    if(evt.detail.xhr.status === 404){
        // alert the user when a 404 occurs (maybe use a nicer mechanism than alert())
        alert("Error: Could Not Find Resource");
    } else if(evt.detail.xhr.status === 422){
        // allow 422 responses to swap as we are using this as a signal that
        // a form was submitted with bad data and want to rerender with the
        // errors
        //
        // set isError to false to avoid error logging in console
        evt.detail.shouldSwap = true;
        evt.detail.isError = false;
    } else if(evt.detail.xhr.status === 418){
        // if the response code 418 (I'm a teapot) is returned, retarget the
        // content of the response to the element with the id `teapot`
        evt.detail.shouldSwap = true;
        evt.detail.target = htmx.find("#teapot");
    }
});
```

Ở đây ta xử lý một số [mã phản hồi lỗi cấp 400](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses)
mà bình thường sẽ không được swap trong htmx.

### [Đặt tên sự kiện](https://htmx.org/docs/\#event_naming)

Lưu ý rằng mọi sự kiện đều được phát ra với hai tên khác nhau

- Camel Case
- Kebab Case

Vậy nên, ví dụ, bạn có thể lắng nghe `htmx:afterSwap` hoặc `htmx:after-swap`. Điều này giúp tương tác dễ dàng
với các thư viện khác. Ví dụ, [Alpine.js](https://github.com/alpinejs/alpine/) yêu cầu kebab case.

### [Ghi log (Logging)](https://htmx.org/docs/\#logging)

Nếu bạn đặt một logger tại `htmx.logger`, mọi sự kiện sẽ được ghi log. Điều này rất hữu ích để gỡ lỗi:

```javascript
htmx.logger = function(elt, event, data) {
    if(console) {
        console.log(event, elt, data);
    }
}
```

## [Gỡ lỗi (Debugging)](https://htmx.org/docs/\#debugging)

Lập trình khai báo (declarative) và hướng sự kiện với htmx (hay bất kỳ ngôn ngữ khai báo nào khác) có thể là một hoạt động
tuyệt vời và rất năng suất, nhưng một nhược điểm so với các cách tiếp cận mệnh lệnh (imperative) là việc gỡ lỗi có thể khó khăn hơn.

Ví dụ, việc tìm hiểu vì sao điều gì đó _không_ xảy ra có thể khó nếu bạn không biết các mẹo.

Vậy, đây là các mẹo:

Công cụ gỡ lỗi đầu tiên bạn có thể dùng là phương thức `htmx.logAll()`. Nó sẽ ghi log mọi sự kiện mà htmx kích hoạt và
cho phép bạn thấy chính xác thư viện đang làm gì.

```javascript
htmx.logAll();
```

Tất nhiên, điều đó sẽ không cho bạn biết vì sao htmx _không_ làm điều gì đó. Bạn cũng có thể không biết phần tử DOM
đang phát ra những sự kiện _nào_ để dùng làm trigger. Để giải quyết điều này, bạn có thể dùng phương thức
[`monitorEvents()`](https://developers.google.com/web/updates/2015/05/quickly-monitor-events-from-the-console-panel) có sẵn trong
console trình duyệt:

```javascript
monitorEvents(htmx.find("#theElement"));
```

Điều này sẽ in ra mọi sự kiện xảy ra trên phần tử có id `theElement` ra console, và cho phép bạn
thấy chính xác điều gì đang diễn ra với nó.

Lưu ý rằng điều này _chỉ_ hoạt động từ console, bạn không thể nhúng nó vào một thẻ script trên trang.

Cuối cùng, nếu bất đắc dĩ, bạn có thể muốn tự gỡ lỗi `htmx.js` bằng cách tải phiên bản chưa nén. Nó khoảng
2500 dòng javascript, nên không phải là một lượng code không thể vượt qua. Bạn có lẽ sẽ muốn đặt breakpoint
trong các phương thức `issueAjaxRequest()` và `handleAjaxResponse()` để xem chuyện gì đang xảy ra.

Và luôn thoải mái ghé qua [Discord](https://htmx.org/discord) nếu bạn cần trợ giúp.

### [Tạo Demo](https://htmx.org/docs/\#creating-demos)

Đôi khi, để minh họa một lỗi hoặc làm rõ cách dùng, sẽ tốt nếu có thể dùng một trang chia sẻ đoạn javascript
như [jsfiddle](https://jsfiddle.net/). Để việc tạo demo dễ dàng hơn, htmx host một script demo
sẽ cài đặt:

- htmx
- hyperscript
- một thư viện giả lập request (mock)

Chỉ cần thêm thẻ script sau vào demo/fiddle/bất cứ đâu của bạn:

```html
<script src="https://demo.htmx.org"></script>
```

Trợ giúp này cho phép bạn thêm phản hồi giả bằng cách thêm thẻ `template` với thuộc tính `url` để chỉ ra URL nào.
Phản hồi cho url đó sẽ là innerHTML của template, giúp dễ dàng xây dựng phản hồi giả. Bạn có thể
thêm độ trễ cho phản hồi bằng thuộc tính `delay`, là một số nguyên chỉ số mili giây cần trễ

Bạn có thể nhúng các biểu thức đơn giản trong template bằng cú pháp `${}`.

Lưu ý rằng điều này chỉ nên dùng cho demo và không đảm bảo hoạt động trong thời gian dài
vì nó sẽ luôn lấy phiên bản mới nhất của htmx và hyperscript!

#### [Ví dụ Demo](https://htmx.org/docs/\#demo-example)

Đây là một ví dụ về đoạn code này hoạt động:

```html
<!-- load demo environment -->
<script src="https://demo.htmx.org"></script>

<!-- post to /foo -->
<button hx-post="/foo" hx-target="#result">
    Count Up
</button>
<output id="result"></output>

<!-- respond to /foo with some dynamic content in a template tag -->
<script>
    globalInt = 0;
</script>
<template url="/foo" delay="500"> <!-- note the url and delay attributes -->
    ${globalInt++}
</template>
```

## [Scripting](https://htmx.org/docs/\#scripting)

Trong khi htmx khuyến khích cách tiếp cận hypermedia để xây dựng ứng dụng web, nó cũng cung cấp nhiều tùy chọn cho scripting phía client. Scripting nằm trong mô tả kiến trúc web kiểu REST, xem: [Code-On-Demand](https://roy.gbiv.com/pubs/dissertation/rest_arch_style.htm#sec_5_1_7). Trong khả năng cho phép, chúng tôi khuyến nghị cách tiếp cận [thân thiện với hypermedia](https://htmx.org/essays/hypermedia-friendly-scripting) khi viết script cho ứng dụng web của bạn:

- [Tôn trọng HATEOAS](https://htmx.org/essays/hypermedia-friendly-scripting#prime_directive)
- [Dùng sự kiện để giao tiếp giữa các component](https://htmx.org/essays/hypermedia-friendly-scripting#events)
- [Dùng “island” để tách biệt các component không phải hypermedia khỏi phần còn lại của ứng dụng](https://htmx.org/essays/hypermedia-friendly-scripting#islands)
- [Cân nhắc scripting nội tuyến (inline)](https://htmx.org/essays/hypermedia-friendly-scripting#inline)

Điểm tích hợp chính giữa htmx và các giải pháp scripting là các [sự kiện](https://htmx.org/docs/#events) mà htmx gửi ra và có thể
phản hồi lại. Xem ví dụ SortableJS trong phần [Javascript bên thứ 3](https://htmx.org/docs/#3rd-party) để có một mẫu tốt cho việc
tích hợp một thư viện JavaScript với htmx thông qua sự kiện.

Các giải pháp scripting phối hợp tốt với htmx bao gồm:

- [VanillaJS](http://vanilla-js.com/) – Chỉ đơn giản dùng khả năng có sẵn của JavaScript để gắn các trình xử lý sự kiện
phản hồi các sự kiện mà htmx phát ra có thể hoạt động rất tốt cho scripting. Đây là cách tiếp cận cực kỳ nhẹ và ngày càng
phổ biến.
- [AlpineJS](https://alpinejs.dev/) – Alpine.js cung cấp một bộ công cụ phong phú để tạo các script front-end tinh vi,
bao gồm hỗ trợ lập trình phản ứng (reactive), trong khi vẫn cực kỳ nhẹ. Alpine khuyến khích cách tiếp cận “scripting nội tuyến”
mà chúng tôi cảm thấy phối hợp tốt với htmx.
- [jQuery](https://jquery.com/) – Dù đã có tuổi đời và tiếng tăm ở một số nơi, jQuery phối hợp rất tốt với htmx, đặc biệt
trong các codebase cũ vốn đã dùng nhiều jQuery.
- [hyperscript](https://hyperscript.org/) – Hyperscript là một ngôn ngữ scripting front-end thử nghiệm, được tạo bởi cùng
đội ngũ đã tạo ra htmx. Nó được thiết kế để nhúng tốt vào HTML và vừa phản hồi vừa tạo ra sự kiện, và phối hợp rất tốt
với htmx.

Chúng tôi có hẳn một chương mang tên [“Client-Side Scripting”](https://hypermedia.systems/client-side-scripting/) trong
[cuốn sách của chúng tôi](https://hypermedia.systems/), xem xét cách tích hợp scripting vào ứng dụng dựa trên htmx của bạn.

### [Liên kết đến: the-hx-on-attributes](https://htmx.org/docs/\#the-hx-on-attributes)[Thuộc tính `hx-on*`](https://htmx.org/docs/\#hx-on)

HTML cho phép nhúng script nội tuyến qua [thuộc tính `onevent`](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers#using_onevent_properties),
như `onClick`:

```html
<button onclick="alert('You clicked me!')">
    Click Me!
</button>
```

Tính năng này cho phép logic scripting được đặt cùng vị trí với các phần tử HTML mà logic đó áp dụng, mang lại
[Locality of Behaviour (LoB) – Tính cục bộ của hành vi](https://htmx.org/essays/locality-of-behaviour) tốt. Đáng tiếc, HTML chỉ cho phép các thuộc tính `on*` cho một số lượng
[sự kiện DOM cụ thể](https://www.w3schools.com/tags/ref_eventattributes.asp) cố định (ví dụ `onclick`) và
không cung cấp cơ chế tổng quát để phản hồi các sự kiện tùy ý trên phần tử.

Để giải quyết hạn chế này, htmx cung cấp các thuộc tính [`hx-on*`](https://htmx.org/attributes/hx-on). Các thuộc tính này cho phép
bạn phản hồi bất kỳ sự kiện nào theo cách vẫn giữ được LoB như các thuộc tính `on*` chuẩn.

Nếu ta muốn phản hồi sự kiện `click` bằng thuộc tính `hx-on`, ta sẽ viết như sau:

```html
<button hx-on:click="alert('You clicked me!')">
    Click Me!
</button>
```

Vậy, cú pháp là chuỗi `hx-on`, theo sau bởi dấu hai chấm (hoặc dấu gạch ngang), rồi đến tên sự kiện.

Đối với sự kiện `click`, tất nhiên, chúng tôi khuyến nghị vẫn dùng thuộc tính `onclick` chuẩn. Tuy nhiên, hãy xét một
nút bấm dùng htmx muốn thêm một tham số vào yêu cầu bằng sự kiện `htmx:config-request`. Điều này sẽ không
thể làm được bằng thuộc tính `on*` chuẩn, nhưng có thể làm được bằng thuộc tính `hx-on:htmx:config-request`:

```html
<button hx-post="/example"
        hx-on:htmx:config-request="event.detail.parameters.example = 'Hello Scripting!'">
    Post Me!
</button>
```

Ở đây tham số `example` được thêm vào yêu cầu `POST` trước khi nó được gửi đi, với giá trị ‘Hello Scripting!’.

Một trường hợp sử dụng khác là [đặt lại dữ liệu người dùng nhập](https://htmx.org/examples/reset-user-input/) khi yêu cầu thành công, dùng sự kiện `afterRequest`,
tránh việc phải dùng thứ như out of band swap.

Các thuộc tính `hx-on*` là một cơ chế rất đơn giản cho scripting nhúng tổng quát. Nó _không_ phải là thứ thay thế cho các
giải pháp scripting front-end phát triển đầy đủ hơn như AlpineJS hay hyperscript. Tuy nhiên, nó có thể bổ sung cho cách tiếp cận
scripting dựa trên VanillaJS trong ứng dụng dùng htmx của bạn.

Lưu ý rằng thuộc tính HTML _không phân biệt chữ hoa/thường_. Điều này có nghĩa là, đáng tiếc, các sự kiện dựa vào
viết hoa/camel case sẽ không thể được phản hồi. Nếu bạn cần hỗ trợ sự kiện camel case, chúng tôi khuyến nghị dùng một
giải pháp scripting đầy đủ chức năng hơn như AlpineJS hay hyperscript. Chính vì lý do này mà htmx phát ra mọi sự kiện của nó
ở cả dạng camelCase lẫn kebab-case.

### [Javascript bên thứ 3](https://htmx.org/docs/\#3rd-party)

Htmx tích hợp khá tốt với các thư viện bên thứ 3. Nếu thư viện đó phát ra sự kiện trên DOM, bạn có thể dùng các sự kiện đó để
kích hoạt yêu cầu từ htmx.

Một ví dụ tốt cho điều này là [demo SortableJS](https://htmx.org/examples/sortable/):

```html
<form class="sortable" hx-post="/items" hx-trigger="end">
    <div class="htmx-indicator">Updating...</div>
    <div><input type='hidden' name='item' value='1'/>Item 1</div>
    <div><input type='hidden' name='item' value='2'/>Item 2</div>
    <div><input type='hidden' name='item' value='2'/>Item 3</div>
</form>
```

Với Sortable, cũng như hầu hết các thư viện javascript khác, bạn cần khởi tạo nội dung vào một thời điểm nào đó.

Trong jquery bạn có thể làm như sau:

```javascript
$(document).ready(function() {
    var sortables = document.body.querySelectorAll(".sortable");
    for (var i = 0; i < sortables.length; i++) {
        var sortable = sortables[i];
        new Sortable(sortable, {
            animation: 150,
            ghostClass: 'blue-background-class'
        });
    }
});
```

Trong htmx, bạn sẽ dùng hàm `htmx.onLoad` thay thế, và bạn sẽ chỉ chọn từ nội dung mới được tải,
thay vì toàn bộ tài liệu:

```js
htmx.onLoad(function(content) {
    var sortables = content.querySelectorAll(".sortable");
    for (var i = 0; i < sortables.length; i++) {
        var sortable = sortables[i];
        new Sortable(sortable, {
            animation: 150,
            ghostClass: 'blue-background-class'
        });
    }
})
```

Điều này sẽ đảm bảo rằng khi nội dung mới được htmx thêm vào DOM, các phần tử sortable được khởi tạo đúng cách.

Nếu javascript thêm nội dung có thuộc tính htmx vào DOM, bạn cần đảm bảo nội dung này
được khởi tạo bằng hàm `htmx.process()`.

Ví dụ, nếu bạn lấy một số dữ liệu và đặt vào một div bằng API `fetch`, và HTML đó có
thuộc tính htmx trong nó, bạn sẽ cần thêm lệnh gọi `htmx.process()` như sau:

```js
let myDiv = document.getElementById('my-div')
fetch('http://example.com/movies.json')
    .then(response => response.text())
    .then(data => { myDiv.innerHTML = data; htmx.process(myDiv); } );
```

Một số thư viện bên thứ 3 tạo nội dung từ phần tử template HTML. Ví dụ, Alpine JS dùng thuộc tính
`x-if` trên template để thêm nội dung có điều kiện. Các template như vậy ban đầu không nằm trong DOM và,
nếu chúng chứa thuộc tính htmx, sẽ cần gọi `htmx.process()` sau khi được tải. Ví dụ sau
dùng hàm `$watch` của Alpine để theo dõi thay đổi giá trị sẽ kích hoạt nội dung có điều kiện:

```html
<div x-data="{show_new: false}"
    x-init="$watch('show_new', value => {
        if (show_new) {
            htmx.process(document.querySelector('#new_content'))
        }
    })">
    <button @click = "show_new = !show_new">Toggle New Content</button>
    <template x-if="show_new">
        <div id="new_content">
            <a hx-get="/server/newstuff" href="#">New Clickable</a>
        </div>
    </template>
</div>
```

#### [Web Components](https://htmx.org/docs/\#web-components)

Vui lòng xem trang [Ví dụ Web Components](https://htmx.org/examples/web-components/) để có ví dụ về cách tích hợp htmx
với web component.

## [Caching](https://htmx.org/docs/\#caching)

htmx hoạt động sẵn với các cơ chế [HTTP caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
tiêu chuẩn, không cần thiết lập thêm.

Nếu server của bạn thêm header phản hồi HTTP
[`Last-Modified`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified)
vào phản hồi cho một URL nhất định, trình duyệt sẽ tự động thêm header yêu cầu HTTP
[`If-Modified-Since`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since)
vào các yêu cầu tiếp theo đến cùng URL đó. Hãy lưu ý rằng nếu
server của bạn có thể render nội dung khác nhau cho cùng một URL tùy vào một số
header khác, bạn cần dùng header phản hồi HTTP [`Vary`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#vary).
Ví dụ, nếu server của bạn render toàn bộ HTML khi header
`HX-Request` bị thiếu hoặc là `false`, và render một đoạn (fragment) của HTML đó
khi `HX-Request: true`, bạn cần thêm `Vary: HX-Request`. Điều đó khiến cache được đánh khóa dựa trên
tổ hợp giữa URL phản hồi và header yêu cầu `HX-Request` — chứ không chỉ dựa trên URL phản hồi.
Luôn tắt `htmx.config.historyRestoreAsHxRequest` để các yêu cầu trang đầy đủ khi khôi phục lịch sử không bị cache cùng
với các phản hồi đoạn (fragment).

Nếu bạn không thể (hoặc không muốn) dùng header `Vary`, bạn có thể thay thế bằng cách đặt tham số cấu hình
`getCacheBusterParam` thành `true`. Nếu biến cấu hình này được đặt, htmx sẽ thêm một tham số chống cache (cache-busting)
vào các yêu cầu `GET` mà nó gửi, giúp ngăn trình duyệt cache các phản hồi dựa trên htmx và không dựa trên htmx
vào cùng một slot cache.

htmx cũng hoạt động với [`ETag`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag)
như mong đợi. Hãy lưu ý rằng nếu server của bạn có thể render nội dung khác nhau cho cùng một
URL (ví dụ, tùy thuộc vào giá trị của header `HX-Request`), server cần
tạo `ETag` khác nhau cho từng loại nội dung.

## [Bảo mật](https://htmx.org/docs/\#security)

htmx cho phép bạn định nghĩa logic trực tiếp trong DOM của bạn. Điều này có một số lợi thế, lớn nhất là
[Locality of Behavior (Tính cục bộ của hành vi)](https://htmx.org/essays/locality-of-behaviour/), giúp hệ thống của bạn dễ hiểu và
dễ bảo trì hơn.

Tuy nhiên, một mối lo với cách tiếp cận này là bảo mật: vì htmx làm tăng khả năng biểu đạt của HTML, nếu một
người dùng ác ý có thể chèn HTML vào ứng dụng của bạn, họ có thể lợi dụng khả năng biểu đạt này của htmx cho các
mục đích xấu.

### [Quy tắc 1: Escape mọi nội dung người dùng](https://htmx.org/docs/\#rule-1-escape-all-user-content)

Quy tắc đầu tiên của phát triển web dựa trên HTML luôn là: _không tin tưởng dữ liệu đầu vào từ người dùng_. Bạn nên escape mọi
nội dung bên thứ 3, không đáng tin cậy được chèn vào trang web của bạn. Điều này để ngăn ngừa, trong số các vấn đề khác,
[tấn công XSS](https://en.wikipedia.org/wiki/Cross-site_scripting).

Có rất nhiều tài liệu về XSS và cách phòng chống trên [trang OWASP](https://owasp.org/www-community/attacks/xss/) tuyệt vời,
bao gồm [Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html).

Tin tốt là đây là một chủ đề rất cũ và được hiểu rõ, và phần lớn các ngôn ngữ template phía server đều
hỗ trợ [tự động escape](https://docs.djangoproject.com/en/4.2/ref/templates/language/#automatic-html-escaping) nội dung
để ngăn chính vấn đề này.

Dù vậy, đôi khi người ta chọn cách chèn HTML nguy hiểm hơn, thường qua một cơ chế kiểu `raw()`
nào đó trong ngôn ngữ template của họ. Điều này có thể được làm vì lý do chính đáng, nhưng nếu nội dung được chèn vào
đến từ bên thứ 3 thì nó _phải_ được làm sạch, bao gồm việc loại bỏ các thuộc tính bắt đầu bằng `hx-` và `data-hx`, cũng như
các thẻ `<script>` nội tuyến, v.v.

Nếu bạn chèn HTML thô và tự làm việc escape, một cách làm tốt nhất là dùng danh sách _cho phép (whitelist)_ các thuộc tính và
thẻ mà bạn cho phép, thay vì danh sách _cấm (blacklist)_ những thứ bạn không cho phép.

### [Công cụ bảo mật của htmx](https://htmx.org/docs/\#htmx-security-tools)

Tất nhiên, lỗi vẫn có thể xảy ra và nhà phát triển không hoàn hảo, nên tốt nhất là có cách tiếp cận nhiều lớp cho bảo mật
của ứng dụng web, và htmx cũng cung cấp các công cụ để giúp bảo mật ứng dụng của bạn.

Hãy cùng xem qua chúng.

#### [`hx-disable`](https://htmx.org/docs/\#hx-disable)

Công cụ đầu tiên htmx cung cấp để giúp bảo mật thêm cho ứng dụng của bạn là thuộc tính [`hx-disable`](https://htmx.org/attributes/hx-disable).
Thuộc tính này sẽ ngăn việc xử lý mọi thuộc tính htmx trên một phần tử nhất định, và trên mọi phần tử bên trong
nó. Vậy nên, ví dụ, nếu bạn đang chèn nội dung HTML thô vào một template (một lần nữa, điều này không được khuyến nghị!) thì bạn
có thể đặt một div bao quanh nội dung đó với thuộc tính `hx-disable`:

```html
<div hx-disable>
    <%= raw(user_content) %>
</div>
```

Và htmx sẽ không xử lý bất kỳ thuộc tính hoặc tính năng liên quan đến htmx nào tìm thấy trong nội dung đó. Thuộc tính này không thể
bị vô hiệu hóa bằng cách chèn thêm nội dung: nếu một thuộc tính `hx-disable` được tìm thấy ở bất kỳ đâu trong hệ thống cha
của một phần tử, nó sẽ không được htmx xử lý.

#### [`hx-history`](https://htmx.org/docs/\#hx-history)

Một cân nhắc bảo mật khác là cache lịch sử của htmx. Bạn có thể có những trang chứa dữ liệu nhạy cảm mà bạn không
muốn lưu vào cache `localStorage` của người dùng. Bạn có thể bỏ qua một trang nhất định khỏi cache lịch sử bằng cách thêm
thuộc tính [`hx-history`](https://htmx.org/attributes/hx-history) ở bất kỳ đâu trên trang, và đặt giá trị của nó là `false`.

#### [Tùy chọn cấu hình](https://htmx.org/docs/\#configuration-options)

htmx cũng cung cấp các tùy chọn cấu hình liên quan đến bảo mật:

- `htmx.config.selfRequestsOnly` – nếu đặt thành `true`, chỉ các yêu cầu đến cùng domain với tài liệu hiện tại mới được cho phép
- `htmx.config.allowScriptTags` – htmx sẽ xử lý các thẻ `<script>` tìm thấy trong nội dung mới mà nó tải. Nếu bạn muốn tắt
hành vi này bạn có thể đặt biến cấu hình này thành `false`
- `htmx.config.historyCacheSize` – có thể đặt thành `0` để tránh lưu bất kỳ HTML nào vào cache `localStorage`
- `htmx.config.allowEval` – có thể đặt thành `false` để tắt mọi tính năng của htmx dựa vào eval:

  - bộ lọc sự kiện (event filter)
  - thuộc tính `hx-on:`
  - `hx-vals` với tiền tố `js:`
  - `hx-headers` với tiền tố `js:`

Lưu ý rằng mọi tính năng bị loại bỏ khi tắt `eval()` đều có thể được triển khai lại bằng javascript tùy chỉnh của riêng bạn và
mô hình sự kiện của htmx.

#### [Sự kiện](https://htmx.org/docs/\#events-1)

Nếu bạn muốn cho phép yêu cầu đến một số domain ngoài host hiện tại, nhưng không muốn mở hoàn toàn, bạn có thể
dùng sự kiện `htmx:validateUrl`. Sự kiện này sẽ có URL yêu cầu trong `detail.url`, cũng như
một thuộc tính `sameHost`.

Bạn có thể kiểm tra các giá trị này và, nếu yêu cầu không hợp lệ, gọi `preventDefault()` trên sự kiện để ngăn
yêu cầu được gửi đi.

```javascript
document.body.addEventListener('htmx:validateUrl', function (evt) {
  // only allow requests to the current server as well as myserver.com
  if (!evt.detail.sameHost && evt.detail.url.hostname !== "myserver.com") {
    evt.preventDefault();
  }
});
```

### [Tùy chọn CSP](https://htmx.org/docs/\#csp-options)

Trình duyệt cũng cung cấp các công cụ để bảo mật thêm cho ứng dụng web của bạn. Công cụ mạnh nhất có sẵn là
[Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP). Dùng CSP bạn có thể báo cho
trình duyệt, ví dụ, không gửi yêu cầu đến các host khác nguồn gốc (non-origin), không đánh giá các thẻ script nội tuyến, v.v.

Đây là một ví dụ CSP trong thẻ `meta`:

```html
    <meta http-equiv="Content-Security-Policy" content="default-src 'self';">
```

Điều này báo cho trình duyệt “Chỉ cho phép kết nối đến domain gốc (nguồn)”. Điều này sẽ trùng lặp với
`htmx.config.selfRequestsOnly`, nhưng cách tiếp cận nhiều lớp cho bảo mật là hợp lý, và thực tế, là lý tưởng, khi xử lý
bảo mật ứng dụng.

Một cuộc thảo luận đầy đủ về CSP nằm ngoài phạm vi tài liệu này, nhưng [bài viết trên MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) là điểm khởi đầu tốt
để khám phá chủ đề này.

### [Phòng chống CSRF](https://htmx.org/docs/\#csrf-prevention)

Việc gán và kiểm tra token CSRF thường là trách nhiệm của backend, nhưng `htmx` có thể hỗ trợ tự động trả về token CSRF cùng với mỗi yêu cầu bằng thuộc tính `hx-headers`. Thuộc tính này cần được thêm vào phần tử gửi yêu cầu hoặc một trong các phần tử tổ tiên của nó. Điều này khiến các phần tử `html` và `body` trở thành phương tiện toàn cục hiệu quả để thêm token CSRF vào header yêu cầu `HTTP`, như minh họa dưới đây.

Lưu ý: `hx-boost` không cập nhật thẻ `<html>` hay `<body>`; nếu dùng tính năng này với `hx-boost`, hãy đảm bảo bao gồm token CSRF trên một phần tử _sẽ_ được thay thế. Nhiều framework web hỗ trợ tự động chèn token CSRF dưới dạng một input ẩn trong form HTML. Điều này được khuyến khích bất cứ khi nào có thể.

```html
<html lang="en" hx-headers='{"X-CSRF-TOKEN": "CSRF_TOKEN_INSERTED_HERE"}'>
    :
</html>
```

```html
    <body hx-headers='{"X-CSRF-TOKEN": "CSRF_TOKEN_INSERTED_HERE"}'>
        :
    </body>
```

Các phần tử trên thường là duy nhất trong một tài liệu HTML và nên dễ tìm thấy trong template.

## [Cấu hình htmx](https://htmx.org/docs/\#config)

Htmx có một số tùy chọn cấu hình có thể truy cập theo lập trình hoặc khai báo. Chúng được
liệt kê dưới đây:

| Biến cấu hình | Thông tin |
| --- | --- |
| `htmx.config.historyEnabled` | mặc định `true`, thực sự chỉ hữu ích cho việc kiểm thử |
| `htmx.config.historyCacheSize` | mặc định 10 |
| `htmx.config.refreshOnHistoryMiss` | mặc định `false`, nếu đặt `true` htmx sẽ thực hiện refresh toàn trang khi không tìm thấy trong lịch sử, thay vì dùng yêu cầu AJAX |
| `htmx.config.defaultSwapStyle` | mặc định `innerHTML` |
| `htmx.config.defaultSwapDelay` | mặc định 0 |
| `htmx.config.defaultSettleDelay` | mặc định 20 |
| `htmx.config.includeIndicatorStyles` | mặc định `true` (quyết định style chỉ báo có được tải hay không) |
| `htmx.config.indicatorClass` | mặc định `htmx-indicator` |
| `htmx.config.requestClass` | mặc định `htmx-request` |
| `htmx.config.addedClass` | mặc định `htmx-added` |
| `htmx.config.settlingClass` | mặc định `htmx-settling` |
| `htmx.config.swappingClass` | mặc định `htmx-swapping` |
| `htmx.config.allowEval` | mặc định `true`, có thể dùng để tắt việc htmx dùng eval cho một số tính năng (ví dụ bộ lọc trigger) |
| `htmx.config.allowScriptTags` | mặc định `true`, quyết định htmx có xử lý thẻ script tìm thấy trong nội dung mới hay không |
| `htmx.config.inlineScriptNonce` | mặc định `''`, nghĩa là sẽ không có nonce nào được thêm vào script nội tuyến |
| `htmx.config.attributesToSettle` | mặc định `["class", "style", "width", "height"]`, các thuộc tính cần settle trong giai đoạn settling |
| `htmx.config.inlineStyleNonce` | mặc định `''`, nghĩa là sẽ không có nonce nào được thêm vào style nội tuyến |
| `htmx.config.useTemplateFragments` | mặc định `false`, thẻ HTML template dùng để phân tích nội dung từ server (không tương thích với IE11!) |
| `htmx.config.wsReconnectDelay` | mặc định `full-jitter` |
| `htmx.config.wsBinaryType` | mặc định `blob`, [kiểu dữ liệu nhị phân](https://developer.mozilla.org/docs/Web/API/WebSocket/binaryType) được nhận qua kết nối WebSocket |
| `htmx.config.disableSelector` | mặc định `[hx-disable], [data-hx-disable]`, htmx sẽ không xử lý các phần tử có thuộc tính này hoặc một phần tử cha có thuộc tính này |
| `htmx.config.withCredentials` | mặc định `false`, cho phép yêu cầu Access-Control cross-site dùng thông tin xác thực như cookie, header authorization hoặc chứng chỉ TLS client |
| `htmx.config.timeout` | mặc định 0, số mili giây một yêu cầu có thể chạy trước khi tự động bị chấm dứt |
| `htmx.config.scrollBehavior` | mặc định ‘instant’, hành vi cuộn khi dùng modifier [show](https://htmx.org/attributes/hx-swap/#scrolling-scroll-show) với `hx-swap`. Các giá trị cho phép là `instant` (cuộn diễn ra tức thì trong một bước), `smooth` (cuộn sẽ có hiệu ứng mượt) và `auto` (hành vi cuộn được xác định bởi giá trị tính toán của [scroll-behavior](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior)). |
| `htmx.config.defaultFocusScroll` | phần tử được focus có nên được cuộn vào tầm nhìn hay không, mặc định false và có thể ghi đè bằng modifier swap [focus-scroll](https://htmx.org/attributes/hx-swap/#focus-scroll). |
| `htmx.config.getCacheBusterParam` | mặc định false, nếu đặt true htmx sẽ thêm phần tử đích vào yêu cầu `GET` theo định dạng `org.htmx.cache-buster=targetElementId` |
| `htmx.config.globalViewTransitions` | nếu đặt thành `true`, htmx sẽ dùng API [View Transition](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API) khi swap nội dung mới vào. |
| `htmx.config.methodsThatUseUrlParams` | mặc định `["get", "delete"]`, htmx sẽ định dạng yêu cầu với các phương thức này bằng cách mã hóa tham số vào URL, không phải trong request body |
| `htmx.config.selfRequestsOnly` | mặc định `true`, có chỉ cho phép yêu cầu AJAX đến cùng domain với tài liệu hiện tại hay không |
| `htmx.config.ignoreTitle` | mặc định `false`, nếu đặt `true` htmx sẽ không cập nhật tiêu đề tài liệu khi tìm thấy thẻ `title` trong nội dung mới |
| `htmx.config.disableInheritance` | tắt kế thừa thuộc tính trong htmx, sau đó có thể ghi đè bằng thuộc tính [`hx-inherit`](https://htmx.org/attributes/hx-inherit/) |
| `htmx.config.scrollIntoViewOnBoost` | mặc định `true`, đích của một phần tử boost có được cuộn vào viewport hay không. Nếu `hx-target` bị bỏ qua trên một phần tử boost, đích mặc định là `body`, khiến trang cuộn lên đầu. |
| `htmx.config.triggerSpecsCache` | mặc định `null`, cache để lưu các đặc tả trigger đã được đánh giá, cải thiện hiệu năng phân tích với chi phí dùng nhiều bộ nhớ hơn. Bạn có thể định nghĩa một object đơn giản để dùng cache không bao giờ xóa, hoặc tự triển khai hệ thống riêng dùng [proxy object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Proxy) |
| `htmx.config.responseHandling` | hành vi [Xử lý phản hồi](https://htmx.org/docs/#response-handling) mặc định cho các mã trạng thái phản hồi có thể được cấu hình ở đây thành swap hoặc error |
| `htmx.config.allowNestedOobSwaps` | mặc định `true`, có xử lý OOB swap trên các phần tử lồng trong phần tử phản hồi chính hay không. Xem [Nested OOB Swaps](https://htmx.org/attributes/hx-swap-oob/#nested-oob-swaps). |
| `htmx.config.historyRestoreAsHxRequest` | mặc định `true`, có coi các yêu cầu tải lại toàn trang do cache miss lịch sử là một “HX-Request” bằng cách trả về header phản hồi này hay không. Điều này nên luôn bị tắt khi dùng header HX-Request để tùy chọn trả về phản hồi từng phần |
| `htmx.config.reportValidityOfForms` | mặc định `false`, có báo cáo lỗi xác thực form cho người dùng và focus vào input không hợp lệ đầu tiên, giống như submit form nguyên bản, hay không (htmx 4 sẽ xác thực form mặc định; xem `hx-validate`) |

Bạn có thể đặt chúng trực tiếp trong javascript, hoặc dùng thẻ `meta`:

```html
<meta name="htmx-config" content='{"defaultSwapStyle":"outerHTML"}'>
```

## [Kết luận](https://htmx.org/docs/\#conclusion)

Và thế là xong!

Chúc bạn vui vẻ với htmx! Bạn có thể làm được [khá nhiều thứ](https://htmx.org/examples/) mà không cần viết nhiều code!
