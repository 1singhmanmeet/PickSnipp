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


## Creating Bullets for TextView

Check the class below:

```
public class BulletListBuilder {

    private static final String SPACE = " ";
    private static final String BULLET_SYMBOL = "&#8226";
    private static final String EOL = System.getProperty("line.separator");
    private static final String TAB = "\t";

    private BulletListBuilder() {

    }

    public static String getBulletList(String header, String []items) {
        StringBuilder listBuilder = new StringBuilder();
        if (header != null && !header.isEmpty()) {
            listBuilder.append(header + EOL + EOL);
        }
        if (items != null && items.length != 0) {
            for (String item : items) {
                Spanned formattedItem = Html.fromHtml(BULLET_SYMBOL + SPACE + item);
                listBuilder.append(TAB + formattedItem + EOL);
            }
        }
        return listBuilder.toString();
    }

}

```
##### To set the bullets to TextView just create a List of String and pass it to the above method and set the result of function to the TextView.
