---
title: "Programmatically create Ripple Drawable"
layout: post

categories: post
tags:
---

It comes in handy many times, from customising colors to set Ripple Drawables dynamically based on content.

```java
public static Drawable getAdaptiveRippleDrawable(int normalColor, int pressedColor) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
        return new RippleDrawable(ColorStateList.valueOf(pressedColor),
                null, getRippleMask(normalColor));
    } else { 
        return getStateListDrawable(normalColor, pressedColor);
    } 
} 
 
private static Drawable getRippleMask(int color) {
    float[] outerRadii = new float[8];
    Arrays.fill(outerRadii, 3);// 3 is radius of final ripple, instead of 3 you can give required final radius
 
    RoundRectShape r = new RoundRectShape(outerRadii, null, null);
 
    ShapeDrawable shapeDrawable = new ShapeDrawable(r);
    shapeDrawable.getPaint().setColor(color);
 
    return shapeDrawable;
} 
 
public static StateListDrawable getStateListDrawable(int normalColor, int pressedColor) {
    StateListDrawable states = new StateListDrawable();
    states.addState(new int[]{android.R.attr.state_pressed}, new ColorDrawable(pressedColor));
    states.addState(new int[]{android.R.attr.state_focused}, new ColorDrawable(pressedColor));
    states.addState(new int[]{android.R.attr.state_activated}, new ColorDrawable(pressedColor));
    states.addState(new int[]{}, new ColorDrawable(normalColor));
    return states;
} 
```

you can get the drawable and apply to any view using view.setBackgroundDrawable()

```java
Drawable drawable = getPressedColorRippleDrawable(normalColor, pressedColor);
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
    view.setBackground(drawable);
} else {
    view.setBackgroundDrawable(drawable);
}
```

for lollipop+ devices you will get ripple else it will change the color of view
