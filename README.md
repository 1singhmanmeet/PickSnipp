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
#### To set the bullets to TextView just create a List of String and pass it to the above method and set the result of function to the TextView.

## Insert bitmap in local storage in android 10 and above

``` 
fun saveImageInQ(bitmap: Bitmap): Uri {
        val filename = "IMG_${System.currentTimeMillis()}.jpg"
        var fos: OutputStream? = null
        var imageUri: Uri? = null
        val contentValues = ContentValues().apply {
            put(MediaStore.MediaColumns.DISPLAY_NAME, filename)
            put(MediaStore.MediaColumns.MIME_TYPE, "image/jpg")
            put(MediaStore.MediaColumns.RELATIVE_PATH, Environment.DIRECTORY_PICTURES)
            put(MediaStore.Images.Media.IS_PENDING, 1)
        }

        //use application context to get contentResolver
        val contentResolver = application.contentResolver

        contentResolver.also { resolver ->
            imageUri = resolver.insert(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, contentValues)
            fos = imageUri?.let { resolver.openOutputStream(it) }
        }

        fos?.use { bitmap.compress(Bitmap.CompressFormat.JPEG, 70, it) }

        contentValues.clear()
        contentValues.put(MediaStore.Images.Media.IS_PENDING, 0)
        contentResolver.update(imageUri!!, contentValues, null, null)

        return imageUri!!
    }
```
## Using Coroutine worker in WorkManager Android
#### Dependencies

```
    
    // for regular java
    implementation "androidx.work:work-runtime:2.4.0"

    // Kotlin + coroutines
    implementation "androidx.work:work-runtime-ktx:2.4.0"
```

#### Example

```

class MyWork(context: Context, params: WorkerParameters) :
        CoroutineWorker(context, params) {override suspend fun doWork(): Result = withContext(Dispatchers.IO) {return try {
            // Do something
            Result.success()
        } catch (error: Throwable) {
            Result.failure()
        }
    }
}

```
## Using ActivityResultsContracts API
#### Dependencies

```
    implementation 'androidx.activity:activity-ktx:1.2.0-alpha07'
    implementation 'androidx.fragment:fragment-ktx:1.3.0-alpha07
```

```
    val sampleLauncher =registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
        
        }
    val intent=Intent()
    sampleLauncher.launch(sampleLauncher)
```

## Using Imaghe Croping After onActivityResult() is depericated
#### Dependencies https://github.com/TakuSemba/CropMe

```

    implementation 'com.github.takusemba:cropme:2.0.5'

```
## Library compatibale with ActivityResultContacts
https://github.com/CanHub/Android-Image-Cropper
