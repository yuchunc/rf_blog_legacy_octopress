---
layout: post
title: "Quick Notes on Linking Woocommerce with Shop.com"
date: 2015-01-16 17:36:27 +0800
comments: true
categories: SOHO, WooCommerce, Shop.com
---

####Disclaimer I have 0 experience with php, so yeah...

So I've been busy with mutiple cases since the start of 2015, and just want to leave a quick note on what I'm currently working on.

## Enter Shop.com

They are just another direct sale company, whose philosophy I completely disagree with.

## Option Simple-And-Easy: Store Exporter Delux

They create costum order fields, and export! That simple!! They even got
an url for cron jobs to call!!!! Wow

### Cost: USD $20

## Wordpress and function.php

Being a wordpress newb and all, I wasted good amount of time trying to write code in respective locations. eg, header.php for getting
RID, display RID in form, etc.

But it was all so much simpler when you follow the WooCommerce conventions, and do some RTFM. \*Sad Face\*

So in each WP theme you installed, contains a function.php, where all the WP/WC hooks and filters live. **Hook
performs functions, filter alters display**. [WC Hook/Filter Reference](http://docs.woothemes.com/document/hooks/)

Great!! One file to *RULE THEM ALL*

So this is what I finally come up with.

Get RID:

    function set_rid() {
      // echo $_GET["RID"];
      setcookie ("RID", $_GET["RID"]);
      // echo $_COOKIE["RID"];
    }
    add_action('init', 'set_rid');

Add RID Field on Checkout:
<pre><code>
add_action( 'woocommerce_after_order_notes', 'my_custom_checkout_field' );

function my_custom_checkout_field( $checkout ) {
  if( isset($_COOKIE["RID"]) ) {
    $RID = $_COOKIE['RID'];
    woocommerce_form_field( 'RID', array(
      'type'          => 'text',
      'class'         => array('my-field-class form-row-wide'),
      'label'         => __('美安Shop.com 編號'),
      'default' => $RID,
    ), $checkout->get_value( 'RID' ));
  }
}
</code></pre>

Updates the order meta with RID
<pre><code>
add_action( 'woocommerce_checkout_update_order_meta',
  'rid_checkout_field_update_order_meta' );

function rid_checkout_field_update_order_meta( $order_id ) {
  if ( ! empty( $_POST['RID'] ) ) {
    update_post_meta( $order_id, 'RID', sanitize_text_field( $_POST['RID'] ) );
  }
}
</code></pre>

That is it!! = )

Now just use Store Exporter to fish out the data, and you are set!!



## <del>Option Hardwork: Do-It-My-Self</del>
### F*** This...
### too damn annoying constructing sql string for getting key-value pair.

<del>I've been bigging through Wordpress and Woocommerce for a bit this afternoon, this are what I gathered.</del>

* <del>Both of this systems stores most informations in key-value pair</del>
* <del>Items are found in \_posts and \_postmeta</del>
* <del>Orders are found in \_woocommerce_order_items and \_woocommerce_order_itemmata</del>
* <del>wc_add_order_item_meta()adds attributes to order_itemmata</del>
* <del>now I just need to construct the sql to fetch all the stuff I need.</del>

