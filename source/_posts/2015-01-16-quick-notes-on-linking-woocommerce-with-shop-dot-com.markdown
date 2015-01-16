---
layout: post
title: "Quick Notes on Linking Woocommerce with Shop.com"
date: 2015-01-16 17:36:27 +0800
comments: true
categories: SOHO, WooCommerce, Shop.com
published: false
---

So I've been busy with mutiple cases since the start of 2015, and just want to leave a quick note on what I'm currently working on.

## Enter Shop.com

They are just another direct sale company

## Option Simple-And-Easy: Store Exporter Delux

They create costum order fields, and export! That simple!! They even got
an url for cron jobs to call!!!! Wow

### Cost: USD $20

## Option Hardwork: Do-It-My-Self

I've been bigging through Wordpress and Woocommerce for a bit this afternoon, this are what I gathered.

* Both of this systems stores most informations in key-value pair
* Items are found in \_posts and \_postmeta
* Orders are found in \_woocommerce_order_items and
  \_woocommerce_order_itemmata
* wc_add_order_item_meta()adds attributes to order_itemmata
* now I just need to construct the sql to fetch all the stuff I need.

