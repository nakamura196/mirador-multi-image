# Mirador Multi Image

## Overview

This is a memo on how to use Scroll View in Mirador 3.

The example here is based on ["鹿児嶋征討記之内　高瀬口河通ノ戦争野津公聯隊旗を取返ス図 (Owned by the National Diet Library)"](https://dl.ndl.go.jp/info:ndljp/pid/1301543).

![](https://storage.googleapis.com/zenn-user-upload/e9a74e739cd3-20240706.png)

This IIIF manifest is composed of three canvases (images), which are usually displayed one at a time in Single mode.

![](https://storage.googleapis.com/zenn-user-upload/12b9b8d4138b-20240706.png)

The goal is to display these three images connected together.

## Demo

You can try it out here:

https://nakamura196.github.io/mirador-multi-image/

The IIIF manifest file is a modified version of the one published by the National Diet Library:

- Before the change:

<https://dl.ndl.go.jp/api/iiif/1301543/manifest.json>

- After the change:

<https://nakamura196.github.io/mirador-multi-image/manifest.json>

The modification, while not directly related to the purpose of this article about Scroll View, involves adding `"viewingDirection": "right-to-left"` so that images are displayed from right to left.

## Mirador Configuration

In Mirador 2, Scroll View was available without any setup, but it seems to be disabled by default in Mirador 3.

<https://projectmirador.org/embed/?iiif-content=https://nakamura196.github.io/mirador-multi-image/manifest.json>

![](https://storage.googleapis.com/zenn-user-upload/c8b786565a72-20240706.png)

Thus, the initial configuration of Mirador 3 is modified as follows:

https://github.com/nakamura196/mirador-multi-image/blob/main/docs/index.html

```js
const config = {
  id: "mirador",
  windows: [
    {
      manifestId: "./manifest.json",
    },
  ],
  language: "ja",
  window: {
    sideBarOpenByDefault: true,
    defaultSideBarPanel: "info",
    defaultView: "scroll",
    views: [{ key: "single" }, { key: "gallery" }, { key: "scroll" }],
  },
};

Mirador.viewer(config);
```

The key point is `views: [{ key: "single" }, { key: "gallery" }, { key: "scroll" }]`. This addition allows Scroll View to appear as an option, as shown below.

![](https://storage.googleapis.com/zenn-user-upload/1d805cdf64d8-20240706.png)
