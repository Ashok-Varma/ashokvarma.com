---
title: "Find number of lines in TextView"
layout: post

categories: post
tags:
---

There are different ways to find no of lines in a textview.

## First method :

```java
int lineCnt = textView.getLineCount();
```

Simple but might lead to errors. Because this can be only used in when the view is rendered (i.e after your textview onDraw is called).
So you can use this if you are calling this method after your view is created.

## Second Method :

```java
textview.setText("placeHolder");
textview.post(new Runnable() {
    @Override
    public void run() {
        int lineCnt = textview.getLineCount();
        // Perform any actions you want based on the line count here.
    }
});
```

This is similar to first method but as we are calling in post runnable the call happens after view is created. So no errors.

What if i want to find out no of lines before a textview is created ??  Is there a way ?
Yes, there is a way

## Third Method :

```java
Rect bounds = new Rect();
Paint paint = new Paint();
paint.setTextSize(currentSize);
paint.getTextBounds(testString, 0, testString.length(), bounds);

int width = (int) Math.ceil( bounds.width());
int noOfLines = (int) Math.ceil(width/textview.getWidth());
```

This is used when you need no of lines before textview is created. We never used Textview in above code except for the width (Which can be found even before TextView onDraw method). So it works perfect in most of the cases. But might not be accurate because in real textView you might be using padding etc.. which we are not specifying here. Adding all those to our paint object makes code more complex. Use third only if you disparately need the textView lines before it’s creation.

So, Out of all three the second method should be opted for most of the cases.

## Usage :

### 1) Auto Adjust Text size based on of lines in textView

This can be used to set text size based on text length. (i.e You have a textview with only one line and you are displaying text larger than the view can hold, then textview will truncate the text, Instead you can check no of lines  and auto adjust textsize based on it). Take care that if your text is too long the text size will be reduced too low user might not able to see text. Check all use cases before you plan to you this.
