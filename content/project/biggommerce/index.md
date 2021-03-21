---
title: BigGommerce
subtitle: A BigCommerce API Helper for Go
date: 2021-03-07T19:09:41.277Z
summary: This is a library for consuming the Big Commerce API in go. Handles
  things like auth and \[un]marshalling to hopefully make things easier.
draft: false
featured: true
external_link: /project/biggommerce/
links:
  - url: https://github.com/dan-collins/biggommerce
    name: BigGommerce on Github
    icon_pack: fab
    icon: github
  - url: https://pkg.go.dev/github.com/dan-collins/biggommerce
    name: BigCommerce on pkg.go.dev
image:
  filename: logo80.png
  focal_point: Smart
  preview_only: true
  alt_text: Gopher reading a bigcommerce.com book.
---
If you want to interact with the BigCommerce rest API in a golang project, this library should help you out. The plan is to eventually build it out for all endpoints/resources but for now most of the [orders](https://developer.bigcommerce.com/api-reference/store-management/orders/) endpoint is addressed.