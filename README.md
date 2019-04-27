# Lab4
实验四_扩展的Activity

## Main:
![](/Screenshot/Main1.png)
![](/Screenshot/Main2.png)

## In-line preferences 
### CheckBoxPreference:
![](/Screenshot/Main1.png)

## Dialog-based preferences:
### EditTextPreference:
![](/Screenshot/Edit_text_preference.png)
### ListPreference:
![](/Screenshot/List_preference.png)

## Launch preferences 
### PreferenceScreen: 跳转到另一个PreferenceScreen
![](/Screenshot/Screen_preference.png)
### PreferenceScreen: 启动一个网页
![](/Screenshot/Intent_preference.png)

## Preference attributes
### CheckBox: 父选项 
### CheckBox: 子选项，当父选项勾选时呈现
![](/Screenshot/Checkbox_preference.png)

## 代码：
### Main.java：
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //加载Fragment
        FragmentManager fragmentManager=getFragmentManager();
        //开启一个新事务
        FragmentTransaction transaction=fragmentManager.beginTransaction();
        Preference preference=new Preference();
        transaction.add(R.id.pre,preference);
        transaction.commit();
    }
}

### Main.xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/pre"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

</android.support.constraint.ConstraintLayout>

### Preference.java:
public class Preference extends PreferenceFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //从xml文件中加载选项
        addPreferencesFromResource(R.xml.preference);
    }
}

### Preference.xml
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_height="match_parent"
    android:layout_width="match_parent">
    <PreferenceCategory android:title="In-line preferences">
        <CheckBoxPreference
            android:key="checkbox_preference"
            android:summary="This a checkbox"
            android:title="Checkbox preference"/>
    </PreferenceCategory>
    
    <PreferenceCategory android:title="Dialog-based preferences">
        <EditTextPreference
            android:dialogTitle="Enter your favorite animal"
            android:title="Edit text preference"
            android:key="edit_text_preference"
            android:summary="An example that uses an edit text dialog"/>
        <ListPreference
            android:entries="@array/options"
            android:entryValues="@array/options"
            android:dialogTitle="Choose one"
            android:summary="An example that use a list dialog"
            android:title="List preference"
            android:key="list_preference"/>
    </PreferenceCategory>
    
    <PreferenceCategory android:title="Launch preferences">
        <PreferenceScreen
            android:key="screen_preference"
            android:summary="Shows another screen of preferences"
            android:title="Screen preference">
            <CheckBoxPreference
                android:key="next_screen_checkbox_preference"
                android:summary="Preference that is on the next screen but same hierarchy"
                android:title="Toggle preference"/>
        </PreferenceScreen>
        <PreferenceScreen
            android:summary="Launches an Activity from an intent"
            android:title="Intent preference">
            <intent
                android:action="android.intent.action.VIEW"
                android:data="https://www.baidu.com"/>
        </PreferenceScreen>
    </PreferenceCategory>
    
    <!--设置项关联，选中父选项时，子选项才显示。使用dependency属性-->
    <PreferenceCategory android:title="Preference attributes">
        <CheckBoxPreference
            android:key="parent_checkbox_preference"
            android:summary="This is visually parent"
            android:title="Parent checkbox preference" />
        <!-- 子类的可见类型是由样式属性定义的 -->
        <CheckBoxPreference
            android:dependency="parent_checkbox_preference"
            android:key="child_checkbox_preference"
            android:summary="This is visually a child"
            android:title="Child checkbox preference" />
    </PreferenceCategory>
</PreferenceScreen>
