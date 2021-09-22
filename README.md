# MyReminder
 Remider Confused Program

#### `style.xml`
```xml
//type 1
<item name="android:statusBarColor" tools:targetApi="l">@android:color/white</item>
<item name="android:fitsSystemWindows">false</item>

//type 2
<item name="android:navigationBarColor">@color/black</item>
<item name="android:windowLightNavigationBar" tools:targetApi="27">true</item>
```
```java
int decore = -1;
//type 1
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
    //enable this tho maker icon status bar become black
    decore += View.SYSTEM_UI_FLAG_LIGHT_STATUS_BAR;
}

//type 2
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
    //enable this tho maker icon Navigation bar become black
    decore +=  View.SYSTEM_UI_FLAG_LIGHT_NAVIGATION_BAR;
}

getWindow().getDecorView().setSystemUiVisibility(decore);
```
#
#### View Height
```java
LinearLayout content = findViewById(R.id.content);
LinearLayout.LayoutParams layoutParams;
//Width Height
layoutParams = new LinearLayout.LayoutParams(
        ViewGroup.LayoutParams.MATCH_PARENT,
        GblFunction.getValueInDP(getApplicationContext(), 100)
);
```
[GblFunction.java](https://github.com/gzeinnumer/ImmersiveBestConfig/blob/master/README.md#gblfunction)
#
#### Set View Padding
```java
LinearLayout parent = findViewById(R.id.parent);
parent.setPadding(0, 0, 0, 0);
```
#
#### Height actionBarSize
```xml
android:layout_marginTop="?attr/actionBarSize"
```
#
#### Remove WORD
```java
String str = "Select * FROM table1 WHERaE 1";
String strTemp = str.toUpperCase();
String toRemove = "WHERE";
int x = strTemp.indexOf(toRemove);
if (x != -1) str = str.substring(0,x) + str.substring(x+toRemove.length(),str.length());
Log.d(TAG, "onCreate_: " + str);
```
#
#### `GblVariable.myDB`
```java
public class GblVariabel {
    private static final String TAG = "GblVariabel";

    public static SQLiteDatabase myDb = null;

    public static void initDb(Context context) {
        DatabaseHelperOLD dbHelper = null;
        try {
            dbHelper = new DatabaseHelperOLD(context);k
            if (dbHelper.checkDatabase()) {
                GblVariabel.myDb = dbHelper.openDataBase();
            } else {
                Log.e(TAG, "initDb:  database kosong");
            }
        } catch (Throwable throwable) {
            throwable.printStackTrace();
            Log.e(TAG, "initDb: " + throwable.getMessage());
        }
    }
}
```
[DatabaseHelper](https://github.com/gzeinnumer/MyReminder/blob/master/files/DatabaseHelper.java)
& [DatabaseHelper Old Style](https://github.com/gzeinnumer/MyReminder/blob/master/files/DatabaseHelperOLD.java)
#
#### External android 10 Spesial Permit
```xml
<application
    android:requestLegacyExternalStorage="true">

</application>
```
#
#### Get Color
```java
ColorStateList color = ContextCompat.getColorStateList(this, R.color.white);
Color color = Color.parseColor("#F2F5F8");
int color = 0xFFCC5500;
```
#
#### Resource
```java
String string = getApplicationContext().getString(R.string.app_name);
int color = getResources().getColor(R.color.colorPrimary);
int color1 = ContextCompat.getColor(getApplicationContext(), R.color.colorPrimary);
```
#
#### Get Drawable
```java
final int sdk = android.os.Build.VERSION.SDK_INT;
if(sdk < android.os.Build.VERSION_CODES.JELLY_BEAN) {
    layout.setBackgroundDrawable(ContextCompat.getDrawable(context, R.drawable.ready) );
} else {
    layout.setBackground(ContextCompat.getDrawable(context, R.drawable.ready));
}
```
#
#### TextInputLayout Hint Color
```xml
<com.google.android.material.textfield.TextInputLayout
    android:textColorHint="@color/colorPrimary">

    <com.google.android.material.textfield.TextInputEditText />
</com.google.android.material.textfield.TextInputLayout>
```
#
#### TextInputLayout Password Toggle
```xml
<com.google.android.material.textfield.TextInputLayout
    app:endIconMode="password_toggle">

    <com.google.android.material.textfield.TextInputEditText/>
</com.google.android.material.textfield.TextInputLayout>
```
#
#### Timer CountDown
```java
//30 second 29 Second 28 Second ...... 1 Second
new CountDownTimer(30000, 1000) {

    public void onTick(long millisUntilFinished) {
        int progress = (int) millisUntilFinished / 1000;
    }

    public void onFinish() {
    }
}.start();
```
#
#### adjustResize & screenOrientation
```xml
<activity
    android:name=".MainActivity"
    android:screenOrientation="portrait"
    android:windowSoftInputMode="adjustResize" />
```
#
#### AS
```java
((Module_1_ComponentProvider) getApplication()).getModule_1_Component().inject(this);
```
#
#### Remove All Space
```java
String s = "CREATE TABLE             table1 (" +
        "id INTEGER            PRIMARY KEY AUTOINCREMENT, "+
        "name TEXT, " +
        "rating REAL, " +
        "descr TEXT, " +
        "flag_active INTEGER, " +
        "created_at TEXT)";

s=s.replaceAll("\\s+"," ");
String[] parts = s.split(" ");
Log.d(TAG, "onCreate_: "+parts[2]);
```
#
#### `getSupportFragmentManager()`
```java
Activity activity = MainActivity.this;
FragmentTransaction transaction = ((FragmentActivity) activity).getSupportFragmentManager().beginTransaction();

Class class = activity.getClass();
new Intent(requireContext(), class)
```
#
#### Kotlin simple get set
```kotlin
var TOKEN: String
    get() = prefs.getString(KEY_TOKEN,default)
    set(value) = prefs.edit().putString(KEY_TOKEN, value).apply()
```
#
#### Shape
```xml
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <corners android:Radius="50dp" />

    <solid android:color="@color/background" />

</shape>
```
#
#### TextView Color Default
```xml
android:textColor="@android:color/tab_indicator_text"

//or

#808080
```
#
#### Remove new
```java
public class ValidatorValue {

    @SuppressLint("StaticFieldLeak") static volatile ValidatorValue singleton = null;

    public static ValidatorValue get() {
        if (singleton == null) {
            synchronized (ValidatorValue.class) {
                if (singleton == null) {
                    if (ValidatorValue.context == null) {
                        throw new IllegalStateException("context == null");
                    }
                    singleton = new ValidatorValue(ValidatorValue.context).build();
                }
            }
        }
        return singleton;
    }

    static Context context;

    public ValidatorValue(Context context) {
        this.context = context;
    }

    public ValidatorValue build() {
        return this;
    }
}
```
```java
ValidatorValue.with(getApplicationContext()).build();
```
#
#### TimeFormat 12/24
```java
boolean isSystem24Hour = DateFormat.is24HourFormat(getApplicationContext());
int clockFormat;
if (isSystem24Hour){
    clockFormat = TimeFormat.CLOCK_24H;
} else {
    clockFormat = TimeFormat.CLOCK_12H;
}
```
#
#### Split String
```java
String currentString = "Fruit: they taste good";
String[] separated = currentString.split(":");
separated[0]; // this will contain "Fruit"
separated[1]; // this will contain " they taste good"
```
#
#### Last Dot . Checked
```java
if (holder.number.getText().length() > 0 && holder.number.getText().toString().endsWith(".")){
    holder.numberP.setError("Format salah");
    isDone = false;
    break;
}
```
#
#### RecyclerView Big Cached
```java
binding.rvData.setItemViewCacheSize(100);
```
#
#### RecyclerView Divider
```java
binding.rv.addItemDecoration(new DividerItemDecoration(this, DividerItemDecoration.VERTICAL));
```
#
#### RecyclerView Keep Value On Model And Show
```java
public class DummyAdapter extends RecyclerView.Adapter<DummyAdapter.ViewHolder> {

    ...

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
        holder.binding.tvName.setText(items.get(position).itemcode);
        if (items.get(position).qty != null && items.get(position).qty.length() > 0){
            holder.binding.edQty.setText(items.get(position).qty);
        }else {
            holder.binding.edQty.setText("");
        }
    }

    @Override
    public void onViewRecycled(@NonNull ViewHolder holder) {
        super.onViewRecycled(holder);
        int index = holder.getAdapterPosition();
        if (index >= 0) {
            items.get(index).qty = holder.binding.edQty.getText().toString();
        }
    }
}
```
#
#### EditText Attribute
```java
holder.numberP.setSuffixText("%");
holder.numberP.setHint("Percentace");
holder.number.setFilters(new InputFilter[]{new InputFilter.LengthFilter(3)});
holder.number.setInputType(InputType.TYPE_CLASS_NUMBER);
holder.number.setKeyListener(DigitsKeyListener.getInstance("123456789"));
```
#
#### Disable 0 First
```java
//maven { url "https://jitpack.io" }
//implementation 'com.github.gzeinnumer:MyLibSimpleTextWatcher:1.0.1'

editTexts.addTextChangedListener(new SimpleTextWatcher(s -> {
    if (s.length() > 0 && s.toString().charAt(0) == '0') {
        final String newText = s.toString().substring(1);
        editTexts.setText(newText);
        editTexts.setSelection(newText.length());
    }
}));
```
#
#### Disable Space First
```java
//maven { url "https://jitpack.io" }
//implementation 'com.github.gzeinnumer:MyLibSimpleTextWatcher:1.0.1'

editTexts.addTextChangedListener(new SimpleTextWatcher(s -> {
    if (s.length() > 0 && s.toString().charAt(0) == ' ') {
        final String newText = s.toString().substring(1);
        editTexts.setText(newText);
        editTexts.setSelection(newText.length());
    } else {
        srVM.setValue(s.toString());
    }
}));
```
#
#### Intent to GMaps
```java
Uri gmmIntentUri = Uri.parse("http://maps.google.com/maps?saddr="+Olatitude+","+Olongitude+"&daddr="+Dlatitude+","+Dlongitude+"");
Intent mapIntent = new Intent(Intent.ACTION_VIEW, gmmIntentUri);
mapIntent.setPackage("com.google.android.apps.maps");
startActivity(mapIntent);
```
#
#### Read JSON From Assets
```java
//readFile(MainActivity.this, "raw/my_json.json");
public static String readFile(Activity activity, String fileName) {
    BufferedReader reader;
    StringBuilder content = new StringBuilder();
    try {
        reader = new BufferedReader(new InputStreamReader(activity.getAssets().open(fileName), "UTF-8"));
        String line;
        while ((line = reader.readLine()) != null) {
            content.append(line.trim());
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
    return content.toString();
}
```
#
#### Read Image From Assets
```java
try {
    // get input stream
    InputStream ims = getAssets().open("avatar.jpg");
    // load image as Drawable
    Drawable d = Drawable.createFromStream(ims, null);
    // set image to ImageView
    mImage.setImageDrawable(d);
  ims .close();
}
catch(IOException ex)
{
    return;
}
```
#
#### setBackgroundResource programatically
```java
bindingItem.tvStatus.setText("Open");
bindingItem.tvStatus.setBackgroundResource(R.drawable.shape_green);
```
#
#### ShapeTextView
```xml
<TextView
    android:background="@drawable/shape_green"
    android:paddingStart="5dp"
    android:paddingEnd="5dp"
    android:text="Open"
    android:textColor="@android:color/white" />
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <corners android:radius="5dp" />
    <solid android:color="@color/green_500" />
</shape>
```
#
#### Copy All Record Table
```
insert into api_response
select * from buang_api_response a
where not EXISTS (select 1 from api_response b where a.id=b.id);
```
#
#### Koltin Configuration

![](https://github.com/gzeinnumer/MyReminder/blob/master/preview/example1.jpg)
#
#### Http Save Log
```java
HttpLoggingInterceptor logging = new HttpLoggingInterceptor(new Logger() {
  @Override public void log(String message) {
    Timber.tag("OkHttp").d(message);
  }
});
```
#
#### Set Drawable
```java
myImgView.setImageDrawable(getResources().getDrawable(R.drawable.ic_arrow_down));
myImgView.setImageDrawable(ContextCompat.getDrawable(context, R.drawable.ic_arrow_down));
```
#
#### Get Date Range
```java
Calendar mCalendar = Calendar.getInstance();
//int remainingDay = mCalendar.getActualMaximum(Calendar.DAY_OF_MONTH) - mCalendar.get(Calendar.DAY_OF_MONTH) + 1;
int remainingDay = 7;
ArrayList<String> allDays = new ArrayList<String>();
SimpleDateFormat mFormat = new SimpleDateFormat("YYYY-MM-dd");
for(int i = 0; i < remainingDay; i++){
    // Add day to list
    allDays.add(mFormat.format(mCalendar.getTime()));
    // Move pref day
    mCalendar.add(Calendar.DAY_OF_MONTH, -1);
    // Move next day
    //mCalendar.add(Calendar.DAY_OF_MONTH, 1);
}

Log.d(getClass().getSimpleName(), "on_Create: "+allDays.toString());
```
#
#### Create Random Code
```java
public int createRandomCode(int codeLength) {
    char[] chars = "1234567890".toCharArray();
    StringBuilder sb = new StringBuilder();
    Random random = new SecureRandom();
    for (int i = 0; i < codeLength; i++) {
        char c = chars[random.nextInt(chars.length)];
        sb.append(c);
    }
    return Integer.parseInt(sb.toString());
}
```
#
#### Object ToJson - Json ToObject
```java
Log.d(getClass().getSimpleName(), "onCre_ate: "+read.get(i).toJson());

public String toJson() {
    return new GsonBuilder().create().toJson(this, Table1.class);
}

//with json indent
@Override
public String toString() {
    return new GsonBuilder().setPrettyPrinting().create().toJson(this, S_Maintenace_Header.class);
}
```
```java
Gson gson = new Gson();
Log.d(getClass().getSimpleName(), "onCre_ate: "+gson.toJson(read.get(i)));
```
```java
String json = string_json;
List<Object> lstObject = gson.fromJson(json_ string, Object.class);
```
#
#### Object ToJson - Json ToObject
```java
@POST("api/save")
Flowable<Response<BaseResponseKao>> sendTraveling2(@Body Trans_H trans_h);
```
```java
String request = gson.toJson(data);
apiService.sendData(data)
    .subscribe(new Consumer<Response<BaseResponseKao>>() {
        @Override
        public void accept(Response<BaseResponseKao> response) throws Exception {
            Toast.makeText(this, "_"+response.body().getMessage(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+response.code(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+response.headers(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+response.raw().request().url(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+response.raw().request().method(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+response.raw().request().headers(), Toast.LENGTH_SHORT).show();
            Toast.makeText(this, "_"+bodyToString(response.raw().request().body()), Toast.LENGTH_SHORT).show();
        }
    }, throwable -> {

    });
```
```java
private String bodyToString(final RequestBody request) {
    try {
        final RequestBody copy = request;
        final Buffer buffer = new Buffer();
        if (copy != null)
            copy.writeTo(buffer);
        else
            return "";
        return buffer.readUtf8();
    } catch (final IOException e) {
        return "did not work";
    }
}
```
```java
//implementation 'com.squareup.retrofit2:retrofit:2.8.1'

public String requestToString(Response response) {
    String msg = "";

    msg+="\nCode : "+ response.code();
    msg+="\nMethod : "+response.raw().request().method();
    msg+="\nURL : "+response.raw().request().url();
    //msg+="\nHeaders :\n "+response.headers().toString();
    //msg+="\nToken :\n "+response.raw().request().headers();
    msg+="\nResponse :\n"+response.body().toString();
    msg+="\n\nRequest :\n "+bodyToString(response.raw().request().body());

    return msg;
}
```
#
#### CI3 CI4 CodeIgnither

- CI3
```php
$sql = "select * from users order by id desc;";
$query = $this->db->query($sql);
return $query->result_array();
//echo $d['id'];;
```

- CI4
```php
$query = "SELECT * FROM product;";
$db = \Config\Database::connect();
$data = $db->query($query);

// return json_encode($data->getResult());
// return json_encode($query->getResultArray());
// return json_encode($query->getRow());
return $this->respond($data->getResult());
```
#
#### CompositeDisposable RXJava
```java

private final CompositeDisposable compositeDisposable = new CompositeDisposable();
compositeDisposable.add(
    apiService.registerDeview()..
);
```
#
#### SD_SO_MAIN 
```
search on google `leveling query id parent_id mysql`.
```
#
#### Base64 String
```
import org.apache.commons.codec.binary.Base64;

Strig str = "gzeinnumer";

// Encode data on your side using BASE64
byte[] bytesEncoded = Base64.encodeBase64(str.getBytes());
Log.d(TAG,"encoded value is " + new String(bytesEncoded));

// Decode data on other side, by processing encoded data
byte[] valueDecoded = Base64.decodeBase64(bytesEncoded);
Log.d(TAG,"Decoded value is " + new String(valueDecoded));
```

[Recomended](https://stackoverflow.com/questions/20215744/how-to-create-a-mysql-hierarchical-recursive-query)

#
#### Flutter Update
```
flutter channel master
flutter upgrade
```
#
#### CI4 Redirect
```php
return redirect()->to('url'); 
return redirect()->route('named_route');
```
#
#### Flutter Row Center
```dart
Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: []
)
```
#
#### Flutter List
```dart
List<T> datas = List<T>.empty(growable: true);
json['datas'].forEach((v) {
    datas.add(create(v));
});
```
#
#### Flutter Items Generator
```dart
final List<MyModel>? product_desc;

List<Widget> get items => itemGenerator(product_desc!);

List<Widget> itemGenerator(List<MyModel> data){
    List<Widget> d = List<Widget>.empty(growable: true);
    for(var i=0; i<data.length; i++){
      d.add(Text(data[i].description.toString()));
    }
    return d;
}
```
```dart
List<String> list = ['one', 'two', 'three', 'four'];
List<Widget> widgets = list.map((name) => new Text(name)).toList();
```
```dart
var list = ["one", "two", "three", "four"];

child: Column(
    mainAxisAlignment: MainAxisAlignment.center,
    children: <Widget>[
        for(var item in list ) Text(item)
    ],
),
```
```
https://stackoverflow.com/questions/50441168/iterating-through-a-list-to-render-multiple-widgets-in-flutter
```
#
#### Flutter Generate From Current Value
```dart
String get freeDeliveryString => freeDelivery(subTotal);

String freeDelivery(subTotal){
    if(subTotal >= 30){
        return "You have FREE Delivery";
    } else{
        double missing = 30.0-subTotal;
        return "Add \$${missing.toStringAsFixed(2)} for FREE Delivery";
    }
}
```
#
#### Flutter Generate Widget Array
```dart
var list = ["one", "two", "three", "four"];

@override
Widget build(BuildContext context) {
    return new MaterialApp(
        home: new Scaffold(
            appBar: new AppBar(
                title: new Text('List Test'),
            ),
            body: new Center(
                child: new Column( // Or Row or whatever :),
                children: createChildrenTexts(),
            ),
        ),
    );
}

List<Text> createChildrenTexts() {
    /// Method 1
    List<Text> childrenTexts = List<Text>();
    for (String name in list) {
        childrenTexts.add(new Text(name, style: new TextStyle(color: Colors.red),));
    }
    return childrenTexts;

    /// Method 2
    return list.map((text) => Text(text, style: TextStyle(color: Colors.blue),)).toList();
}
```
#
#### Flutter ListView.builder
```dart
Container(
  child: ListView.builder(
    shrinkWrap: true,
    itemCount: items.length,
    itemBuilder: (BuildContext context, int index){
      return Container(
        child: Text(
          items[index]['property']
        ),
      );
    },
  ),
);
```
#
#### Flutter Statusbar Color

Update Flutter 2.0 (Recommended):
```dart
AppBar(
    backwardsCompatibility: true,
    systemOverlayStyle: SystemUiOverlayStyle(statusBarColor: Colors.white),
)
```
Only Android (more flexibility):
```dart
SystemChrome.setSystemUIOverlayStyle(SystemUiOverlayStyle(
    systemNavigationBarColor: Colors.blue, // navigation bar color
    statusBarColor: Colors.pink, // status bar color
));
```
Both iOS and Android:
```dart
AppBar(
    backgroundColor: Colors.red, // status bar color
    brightness: Brightness.light, // status bar brightness
)
```
#
#### Flutter StatusBarColor NavigationColor Recomended
```dart
SystemChrome.setSystemUIOverlayStyle(SystemUiOverlayStyle(
    statusBarColor: Colors.white,
    statusBarBrightness: Brightness.dark,
    systemNavigationBarColor: Colors.white,
    systemNavigationBarIconBrightness: Brightness.dark
));
```
```dart
AppBar(
    backwardsCompatibility: true,
    systemOverlayStyle: SystemUiOverlayStyle(
        statusBarColor: Colors.white,
        statusBarBrightness: Brightness.dark,
        systemNavigationBarColor: Colors.white,
        systemNavigationBarIconBrightness: Brightness.dark,
    ),
)
```
#
#### Flutter DebugBanner
```dart
MaterialApp(
  debugShowCheckedModeBanner: false,
)
```
#
#### nestedScrollingEnabled NestedScrollView RecyclerView
```xml
<androidx.core.widget.NestedScrollView
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerView"
        android:layout_width="match_parent"
        android:nestedScrollingEnabled="false"
        android:layout_height="wrap_content"
        android:padding="4dp" />

</androidx.core.widget.NestedScrollView>
```
```java
recyclerView.setNestedScrollingEnabled(false);
```
#
#### Check Service Is Running
```java
private boolean isMyServiceRunning(Class<?> serviceClass) {
    ActivityManager manager = (ActivityManager) getSystemService(Context.ACTIVITY_SERVICE);
    for (ActivityManager.RunningServiceInfo service : manager.getRunningServices(Integer.MAX_VALUE)) {
        if (serviceClass.getName().equals(service.service.getClassName())) {
            return true;
        }
    }
    return false;
}

//in function
if (!isMyServiceRunning(EmployeeVisitService.class)) {
    startService(new Intent(this, EmployeeVisitService.class));
} else {
    Log.d(TAG, "service Employee sudah ada ");
}
```
#
#### FLutter Divider
```dart
const Divider(
    height: 20,
    thickness: 5,
    indent: 20,
    endIndent: 20,
)
```
#
#### Android Issue Core:1.7
```dart
configurations.all {
    resolutionStrategy {
        force 'androidx.core:core-ktx:1.6.0'
    }
}
```
#
#### Dynamic RecyclerView Scroll On Focused Ediitext
```xml
<activity
    android:name=".ui.scoring.subMenu.pertanyaan.PertanyaanActivity"
    android:screenOrientation="portrait"
    android:windowSoftInputMode="adjustResize" />
```
```java
holder.freetext.setOnFocusChangeListener((view, b) -> {
    if (b){
        InputMethodManager imm = (InputMethodManager) context.getSystemService(Context.INPUT_METHOD_SERVICE);
        imm.toggleSoftInput(InputMethodManager.SHOW_FORCED, 0);
    }
});
```
```xml
<com.google.android.material.textfield.TextInputLayout
    android:id="@+id/freetext_p"
    style="@style/MyTextInputLayoutOutlinedBoxNext"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="8dp"
    android:hint="Notes"
    android:visibility="gone"
    tools:visibility="visible">

    <com.google.android.material.textfield.TextInputEditText
        android:id="@+id/freetext"
        style="@style/MyTextInputEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:focusableInTouchMode="true"
        android:maxLength="200" />

</com.google.android.material.textfield.TextInputLayout>
```
```java
binding.rvData.setAdapter(adapterLevel1);
binding.rvData.setHasFixedSize(true);
binding.rvData.setLayoutManager(new LinearLayoutManager(getApplicationContext()));
binding.rvData.setItemViewCacheSize(100);
```
```xml
<!--<androidx.core.widget.NestedScrollView-->
<!--    android:layout_width="match_parent"-->
<!--    android:layout_height="wrap_content">-->

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rv_data"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:nestedScrollingEnabled="false" />
<!--</androidx.core.widget.NestedScrollView>-->
```
#
#### Flutter Dialog Disable Outside
```dart
showDialog(
  barrierDismissible: false,
  builder: ...
);
```
#
#### FLutter CallBack
```dart
final Function()? onPositivePressed;
final ValueChanged<String>? onChanged;
```
#
#### Flutter Container Radius
```dart
Container(
    width: match_parent,
    decoration : BoxDecoration(
        color: Colors.white,
        borderRadius: new BorderRadius.circular(def_margin)
    ),
    margin: const EdgeInsets.all(def_margin),
    child: PaddingAll(
        child: Column(
            children: [
                ...
            ],
        ),
    ),
),
```

---

```
Copyright 2021 M. Fadli Zein
```