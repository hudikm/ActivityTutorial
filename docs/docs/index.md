    # Welcome to MkDocs

For full documentation visit [mkdocs.org][1].
[1]: http://mkdocs.org

[Material Design][2]
  [2]: https://squidfunk.github.io/mkdocs-material/
## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


<!--//home//martin//PycharmProjects//PatchCreator//out.patch' -->
<!--tgen file='/home/martin/AndroidStudioProjects/ActivityTutorial/out.patch' lang=java prefix="Krok č. " tabs t_new="Nové" t_old="Pred úpravou" -->

## Návrh GUI
> Cvičenie : Úlohou cvičenia je vytvoriť aplikáciu kuchárska kniha, ktorá bude pozostávať z dvoch obrazoviek. Prvá, hlavná obrazovka, bude obsahovať zoznam receptov a druhá bude zobrazovať detail o recepte. Na aplikáciu su kladené tieto požiadavky:
> 
> Aplikacia použije dynamický layoutu a to konkrétne Recyclerview. Tento prvok bude zobrazovať zoznam receptov.Obrazovky uživatelského rozhrania budú tvorené z dvoch fragmentov: ListFagment, DetailFragment.

<!--tgen step=1.0 lang=xml tabs=false  -->
####Krok č. 1.0 Zmena layoutu [:link:](https://github.com/hudikm/ActivityTutorial/commit/3e48d42a0c12214f66927fd6389c6defdcdce34d/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/3e48d42a0c12214f66927fd6389c6defdcdce34d/app/src/main/res/layout/activity_main.xml) app/src/main/res/layout/activity_main.xml**
     

``` xml  hl_lines="2 6 10 13 15"
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

</LinearLayout>

```


<!--end-->

Pridaméme komponenty tak ako sú znáorné na obrázku č.1

<!--tgen step=1.1 lang=xml -->
####Krok č. 1.1 Pridané nové UI komponenty [:link:](https://github.com/hudikm/ActivityTutorial/commit/7e19050b70ccdcc1a4f91b07ec0b515292ace762/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/7e19050b70ccdcc1a4f91b07ec0b515292ace762/app/src/main/res/layout/activity_main.xml) app/src/main/res/layout/activity_main.xml**
                          

``` xml tab="Nové" hl_lines="4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

    <CheckBox
        android:id="@+id/checkBox2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="CheckBox" />

    <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button" />

    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="textPersonName"
        android:text="Name" />

    <Button
        android:id="@+id/button2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Search" />

</LinearLayout>

```

``` xml tab="Pred úpravou" 
        android:layout_height="wrap_content"
        android:text="Hello World!" />

</LinearLayout>

```

<!--end-->

<!--tgen step=1.2-2.1 -->
####Krok č. 1.2 Zmena textu v prvku TextView [:link:](https://github.com/hudikm/ActivityTutorial/commit/5987353de8cdd1d8e300850b2d8a05c801569cee/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/5987353de8cdd1d8e300850b2d8a05c801569cee/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
           

``` java tab="Nové" hl_lines="4 5 11 12 17 18 19 20 21 22 23"
package sk.uniza.activitytutorial;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                textView.setText("Ahoj Svet");
            }
        });
    }
}

```

``` java tab="Pred úpravou" 
package sk.uniza.activitytutorial;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}

```
####Krok č. 1.3 Doplnenie funkcie SaveInstanceState & RestoreInstanceState [:link:](https://github.com/hudikm/ActivityTutorial/commit/80a602c9fb1158a4a809179b62e13f0f63bc6917/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/80a602c9fb1158a4a809179b62e13f0f63bc6917/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
 
 > import android.os.Bundle;

``` java tab="Nové" hl_lines="4"
import android.view.View;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

```

``` java tab="Pred úpravou" 
import android.view.View;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

```
           
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5 6 7 8 9 10 11 12 13 14"
            }
        });
    }

    @Override
    public void onSaveInstanceState(@NonNull Bundle outState) {
        super.onSaveInstanceState(outState);

    }

    @Override
    protected void onRestoreInstanceState(@NonNull Bundle savedInstanceState) {
        super.onRestoreInstanceState(savedInstanceState);
    }
}

```

``` java tab="Pred úpravou" 
            }
        });
    }
}

```
####Krok č. 1.4 Uloženie textu z prvku TextView [:link:](https://github.com/hudikm/ActivityTutorial/commit/7a65fda966d26861ec5bbd9f87802b1de69d2312/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/7a65fda966d26861ec5bbd9f87802b1de69d2312/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
 
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4"
    @Override
    public void onSaveInstanceState(@NonNull Bundle outState) {
        super.onSaveInstanceState(outState);
        outState.putCharSequence("textView", textView.getText());
    }

    @Override

```
 
``` java tab="Pred úpravou" hl_lines="4"
    @Override
    public void onSaveInstanceState(@NonNull Bundle outState) {
        super.onSaveInstanceState(outState);

    }

    @Override

```
####Krok č. 1.5 Obnovenie uložených dat [:link:](https://github.com/hudikm/ActivityTutorial/commit/b78ea8825cbfbbeea97b02857f3d811d2b1a2d36/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/b78ea8825cbfbbeea97b02857f3d811d2b1a2d36/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
  
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5"
    @Override
    protected void onRestoreInstanceState(@NonNull Bundle savedInstanceState) {
        super.onRestoreInstanceState(savedInstanceState);
        CharSequence charSequence = savedInstanceState.getCharSequence("textView", "Default");
        textView.setText(charSequence);
    }
}

```

``` java tab="Pred úpravou" 
    @Override
    protected void onRestoreInstanceState(@NonNull Bundle savedInstanceState) {
        super.onRestoreInstanceState(savedInstanceState);
    }
}

```
####Krok č. 1.6 Nájdenie inštancie prvku Checkbox [:link:](https://github.com/hudikm/ActivityTutorial/commit/4bc6a6a7866962cac2d30edfb19ebd9c2af9107c/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/4bc6a6a7866962cac2d30edfb19ebd9c2af9107c/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
 
 > package sk.uniza.activitytutorial;

``` java tab="Nové" hl_lines="3"
import android.os.Bundle;
import android.view.View;
import android.widget.CheckBox;
import android.widget.TextView;

import androidx.annotation.NonNull;

```

``` java tab="Pred úpravou" 
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import androidx.annotation.NonNull;

```
  
 > import androidx.appcompat.app.AppCompatActivity;

``` java tab="Nové" hl_lines="4 11"
public class MainActivity extends AppCompatActivity {

    private TextView textView;
    private CheckBox checkBox;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        checkBox = findViewById(R.id.checkBox2);
        findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

```

``` java tab="Pred úpravou" 
public class MainActivity extends AppCompatActivity {

    private TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

```
  
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5"
        CharSequence charSequence = savedInstanceState.getCharSequence("textView", "Default");
        textView.setText(charSequence);
    }


}

```

``` java tab="Pred úpravou" 
        CharSequence charSequence = savedInstanceState.getCharSequence("textView", "Default");
        textView.setText(charSequence);
    }
}

```
####Krok č. 1.7 Trvalé uloženie hodnoty CheckBoxu [:link:](https://github.com/hudikm/ActivityTutorial/commit/7cb24a85215b76132931462e3724694f0e13239a/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/7cb24a85215b76132931462e3724694f0e13239a/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
     
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5 6 7 8"
        textView.setText(charSequence);
    }

    @Override
    protected void onPause() {
        super.onPause();
        getPreferences(MODE_PRIVATE).edit().putBoolean("CheckBox", checkBox.isChecked()).commit();
    }
}

```
 
``` java tab="Pred úpravou" hl_lines="4"
        textView.setText(charSequence);
    }


}

```
####Krok č. 1.8 Obnovenie uloženych nastavení [:link:](https://github.com/hudikm/ActivityTutorial/commit/b0e4686344af0068245773b05def1cb2212b712f/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/b0e4686344af0068245773b05def1cb2212b712f/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
    
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5 6 7"
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        checkBox = findViewById(R.id.checkBox2);

        boolean aBoolean = getPreferences(MODE_PRIVATE).getBoolean("CheckBox", false);
        checkBox.setChecked(aBoolean);

        findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

```

``` java tab="Pred úpravou" 
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        checkBox = findViewById(R.id.checkBox2);
        findViewById(R.id.button).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

```
####Krok č. 2.0 Pridaná nová aktivita [:link:](https://github.com/hudikm/ActivityTutorial/commit/d07a3c241327466c2b698362ea57b023476eff76/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/d07a3c241327466c2b698362ea57b023476eff76/app/src/main/AndroidManifest.xml) app/src/main/AndroidManifest.xml**
 

``` java tab="Nové" hl_lines="4"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".Main2Activity"></activity>
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

```

``` java tab="Pred úpravou" 
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

```

>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/d07a3c241327466c2b698362ea57b023476eff76/app/src/main/java/sk/uniza/activitytutorial/Main2Activity.java) app/src/main/java/sk/uniza/activitytutorial/Main2Activity.java**
              

``` java tab="Nové" hl_lines="1 2 3 4 5 6 7 8 9 10 11 12 13 14"
package sk.uniza.activitytutorial;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;

public class Main2Activity extends AppCompatActivity {
    //    Nová aktivyta, pretože ľščťžýá
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
    }
}

```


>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/d07a3c241327466c2b698362ea57b023476eff76/app/src/main/res/layout/activity_main2.xml) app/src/main/res/layout/activity_main2.xml**
        

``` java tab="Nové" hl_lines="1 2 3 4 5 6 7 8"
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Main2Activity">

</androidx.constraintlayout.widget.ConstraintLayout>

```

####Krok č. 2.1 Implicitný intent: Ako zavolať prehliadač? [:link:](https://github.com/hudikm/ActivityTutorial/commit/637cd32291d540b8e655170b673649457783ddd4/)
>  **[🖹](https://github.com/hudikm/ActivityTutorial/blob/637cd32291d540b8e655170b673649457783ddd4/app/src/main/java/sk/uniza/activitytutorial/MainActivity.java) app/src/main/java/sk/uniza/activitytutorial/MainActivity.java**
   

``` java tab="Nové" hl_lines="3 4 8"
package sk.uniza.activitytutorial;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.TextView;

import androidx.annotation.NonNull;

```

``` java tab="Pred úpravou" 
package sk.uniza.activitytutorial;

import android.os.Bundle;
import android.view.View;
import android.widget.CheckBox;
import android.widget.TextView;

import androidx.annotation.NonNull;

```
 
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="3"
    private TextView textView;
    private CheckBox checkBox;
    private EditText searchTxt;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

```

``` java tab="Pred úpravou" 
    private TextView textView;
    private CheckBox checkBox;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

```
 
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4"
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        checkBox = findViewById(R.id.checkBox2);
        searchTxt = findViewById(R.id.editText);
        boolean aBoolean = getPreferences(MODE_PRIVATE).getBoolean("CheckBox", false);
        checkBox.setChecked(aBoolean);


```
 
``` java tab="Pred úpravou" hl_lines="4"
        setContentView(R.layout.activity_main);
        textView = findViewById(R.id.textView);
        checkBox = findViewById(R.id.checkBox2);

        boolean aBoolean = getPreferences(MODE_PRIVATE).getBoolean("CheckBox", false);
        checkBox.setChecked(aBoolean);


```
          
 > public class MainActivity extends AppCompatActivity {

``` java tab="Nové" hl_lines="4 5 6 7 8 9 10 11 12 13"
                textView.setText("Ahoj Svet");
            }
        });
        // Search button
        findViewById(R.id.button2).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Uri uri = Uri.parse("http://www.google.com/#q=" +
                        searchTxt.getText().toString());
                Intent intent = new Intent(Intent.ACTION_VIEW, uri);
                startActivity(intent);
            }
        });
    }

    @Override

```

``` java tab="Pred úpravou" 
                textView.setText("Ahoj Svet");
            }
        });
    }

    @Override

```

<!--end-->









