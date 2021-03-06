# Spinner

## Introduction
A Spinner is a control/widget, used to display the multiple options to the user from which the user can select only one option. It is like a drop down menu with multiple values from which the end user can select only one value.
In the default state, a spinner shows its currently selected value. Touching the spinner displays a dropdown menu with all other available values, from which a user can select a new one or in complicated sentense, we can say, When it is inactive, it displays a single value. When activated, it displays (drops down) a list of values, from which the user may select one. When the user selects a new value, the control reverts to its inactive state, displaying the selected value.It is often used in the design of graphical user interface.

## History
In 2009,in version 2.0-2.1, level 5-7, Enclair, some of the Android Applications were improved and some new were added to Android,In that, in Adroid App Widgets,further in Control Widgets spinner was used, at that time, the level of user interface was updated. 

## Methods and Attributes
This is how spinner is wrapped to work

Spinner
public class Spinner 
extends AbsSpinner implements DialogInterface.OnClickListener


    java.lang.Object
    
    ↳	android.view.View
   
 	   ↳	android.view.ViewGroup
      
 	 	   ↳	android.widget.AdapterView<android.widget.SpinnerAdapter>
         
 	 	 	   ↳	android.widget.AbsSpinner
            
 	 	 	 	   ↳	android.widget.Spinner

 ### Methods used to implement spinner
(Major inherited methods)
- From class android.widget.AbsSpinner
- From class android.widget.AdapterView
- From class android.view.ViewGroup
- From class android.view.View
- From class java.lang.Object
- From interface android.view.ViewParent
- From interface android.view.ViewManager
- From interface android.graphics.drawable.Drawable.Callback
- From interface android.view.KeyEvent.Callback
- From interface android.view.accessibility.AccessibilityEventSource
- From interface android.content.DialogInterface.OnClickListener

Some other methods used:-
- onDetachedFromWindow()
- onLayout(boolean changed, int l, int t, int r, int b)
- onMeasure(int widthMeasureSpec, int heightMeasureSpec)

### Attributes used to implement spinner
( Major Inherited XML attributes)
-From class android.widget.AbsSpinner
-From class android.view.ViewGroup
-From class android.view.View

Some other attributes:-
- android:dropDownHorizontalOffset
- android:dropDownSelector
- android:dropDownVerticalOffset
- android:dropDownWidth
- android:gravity
- android:popupBackground
- android:prompt
- android:spinnerMode

For more infomation on Methods and Attributes [FollowThisLink]https://developer.android.com/reference/android/widget/Spinner


## How spinner works
This explains the functionality of spinner, how it works:
Providing the spinner with choices:-The choices can come from any source, but should be provided or added through spinnerAdapter such as ArrayAdapter, if the choices are available in Array and CursorAdapter, if the choices are available from database query or we can use string Array defined in string resource file , if the choices are pre-determined.

Suppling the Array to spinner:- we can supply the array to spinner using ArrayAdapter( ArrayAdapter helps to show a ArrayList of objects into view items loaded into the list view container),For this, First we need to create the ArrayAdapter from string Array, then we need to decide how the selected item should appear in the spinner control, and the simple_spinner_item is the default layout, then in next step we need to call setDropDownViewResource() to specify the layout for drop down list, when it shows the avilable choices, then at last apply the adapter to the spinner.

Responding to user selections:-when the item is selected from drop down menu, it implements "AdpterView.OnItemSelectedListener" interface , which has two call back methods onItemSelected() and onNothingSelected(). 

## The Code
We will create an android application that consists of a simple spinner that allows selecting an item from a drop down list. We will display static data in the spinner. Selecting an item from spinner would display a toast message.
This example has two spinners(spinner1 and spinner2), one has a list of flowers and other has a list of colours.

spinner1:- In spinner 1, the values are provided in string array in a resource file "string.xml" and implementing it in MainActivity.java using a java class "CustomOnItemSelectedListener.java" 

Spinner2:- In this case, list and function both are included in  MainActivity.java
The one used for spinner2 is more preferable.

These two spinners are same but they are added and implemented in little bit different ways



 **MainActivity.java**
 ```
 package com.example.n01204447.spinner;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Spinner;
import java.util.ArrayList;
import java.util.List;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.ArrayAdapter;
import android.widget.Toast;


public class MainActivity extends AppCompatActivity {

    private Spinner spinner1, spinner2;
    private Button btnSubmit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        addItemsOnSpinner2();
        addListenerOnButton();
        addListenerOnSpinnerItemSelection();
    }

    //in this function we are making a 2nd spinner and adding a content to it
    public void addItemsOnSpinner2() {

        spinner2 = (Spinner) findViewById(R.id.spinner2);

        List<String> list = new ArrayList<String>();

        list.add("Red");
        list.add("Blue");
        list.add("Yellow");
        list.add("Pink");
        list.add("Orange");
        list.add("white");

        ArrayAdapter<String> dataAdapter = new ArrayAdapter<String>(this, //create an  ArrayAdapter using the string array and a default spinner layout
                android.R.layout.simple_spinner_item, list);
        dataAdapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item); //specify the layout to use when the list of choices appears
        spinner2.setAdapter(dataAdapter);  // apply the adapter to the spinner

    }

    //this is for implementation of spinner
    public void addListenerOnSpinnerItemSelection() {
        spinner1 = (Spinner) findViewById(R.id.spinner1);
        spinner1.setOnItemSelectedListener(new CustomOnItemSelectedListener());

    }


    // get the selected dropdown list value
    //In this we added listener to three control items
    //when we click on button it should show what the user has selected

    public void addListenerOnButton() {

        spinner1 = (Spinner) findViewById(R.id.spinner1);
        spinner2 = (Spinner) findViewById(R.id.spinner2);
        btnSubmit = (Button) findViewById(R.id.btnSubmit);

        btnSubmit.setOnClickListener (new OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this,
                        "OnClickListener: "
                               + "\nSpinner 1 : " + String.valueOf(spinner1.getSelectedItem()) +
                                "\nSpinner 2 : " + String.valueOf(spinner2.getSelectedItem()),
                        Toast.LENGTH_SHORT).show();

            }


        });
    }


}

 ```
 
 **activity_main.xml**
 ```
 <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    // this spinner1
    <Spinner

        android:id="@+id/spinner1"
        android:layout_width="match_parent"
        android:layout_height="67dp"
        android:entries="@array/flower_arrays"
        android:prompt ="@string/flower_prompt" />

    // this spinner2
    <Spinner

        android:id="@+id/spinner2"
        android:layout_width="match_parent"
        android:layout_height="69dp" />

    //Submit button
    <Button

        android:id="@+id/btnSubmit"
        android:layout_width="128dp"
        android:layout_height="82dp"
        android:text="Submit" />

</LinearLayout>
 ```
 **String.xml** has a array list of flower names
 ```
 <resources>

    <string name="app_name">spinner</string>

        <string name="flower_prompt">choose a flower</string>

        <string-array name="flower_arrays">

            <item>Rose</item>
            <item>Lily</item>
            <item>Sun Flower</item>
            <item>Tulip</item>
            <item>Daffodil</item>
            <item>Daisy</item>

        </string-array>

</resources>

```
**CustomOnItemSelectedListener.java** 
```
package com.example.n01204447.spinner;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemSelectedListener;
import android.widget.Toast;

public class CustomOnItemSelectedListener implements OnItemSelectedListener {

    //when item is selected
    public void onItemSelected(AdapterView<?> parent, View view, int pos,long id) {

        //showing selected spinner item
        Toast.makeText(parent.getContext(),
                "OnItemSelectedListener : " + parent.getItemAtPosition(pos).toString(),    //retrieving an item from spinner
                Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onNothingSelected(AdapterView<?> arg0) {
        // interface callback
        //don't do anything stay there
    }

}
```
# Output

![firstscreen](https://user-images.githubusercontent.com/43186746/49681816-32ca3e00-fa76-11e8-84a5-5b7e472f21d5.PNG)![spinner1dropdown](https://user-images.githubusercontent.com/43186746/49681819-3958b580-fa76-11e8-8221-96bfbb135ab2.PNG)

![spinner2dropdown](https://user-images.githubusercontent.com/43186746/49681823-3e1d6980-fa76-11e8-82da-53dec5325ee6.PNG)![displayingresult](https://user-images.githubusercontent.com/43186746/49681826-42498700-fa76-11e8-902c-232eb3949971.PNG)



## The reference

https://www.javatpoint.com

https://developer.android.com

https://www.tutorialspoint.com


