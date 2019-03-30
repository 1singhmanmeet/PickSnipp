# PickSnipp
This is just a collection of small code snippet for android programmers. I am creating this collection because i know being a android developer you know there are things you just have to find and write next time probably you find something here. 

#### Note: For now i am adding the snippets. Anyone can contribute.

## TextView with Marquee 
```
<TextView
    android:text="START | lunch 20.00 | Dinner 60.00 | Travel 60.00 | Doctor 5000.00 | lunch 20.00 | Dinner 60.00 | Travel 60.00 | Doctor 5000.00 | END"
    android:id="@+id/MarqueeText" 
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" 
    android:singleLine="true"
    android:ellipsize="marquee" 
    android:marqueeRepeatLimit="marquee_forever"
    android:scrollHorizontally="true" 
    android:paddingLeft="15dip" 
    android:paddingRight="15dip" 
    android:focusable="true" 
    android:focusableInTouchMode="true" 
    android:freezesText="true">
```
##### textView.setSelected(true) needs to be set in code behind for this to work.
