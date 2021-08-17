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

---

```
Copyright 2021 M. Fadli Zein
```