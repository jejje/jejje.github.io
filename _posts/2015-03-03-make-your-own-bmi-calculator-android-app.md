---
id: 101
title: Make your own BMI Calculator Android App
date: 2015-03-03T11:11:52+00:00
author: JejjE
layout: post
guid: http://jejje.net/?p=101
permalink: /make-your-own-bmi-calculator-android-app/
dsq_thread_id:
  - "3842274686"
snap_MYURL:
  - ""
snapEdIT:
  - "1"
snapFB:
  - 's:225:"a:1:{i:0;a:8:{s:4:"doFB";s:1:"1";s:8:"postType";s:1:"A";s:10:"AttachPost";s:1:"2";s:10:"SNAPformat";s:23:"(%TITLE%) at %SITENAME%";s:9:"isAutoImg";s:1:"A";s:8:"imgToUse";s:0:"";s:9:"isAutoURL";s:1:"A";s:8:"urlToUse";s:0:"";}}";'
banner_image: /wp-content/uploads/2015/03/make_your_own_bmi_calculator_android_app.png
categories:
  - Android
tags:
  - android
  - android app
  - code
  - java
  - tutorial
---
The easiest way to learn the basics of Java and Android development is to dive head first into coding, of course you&#8217;ll need some basic understanding of Java, or programming in general. In this article I&#8217;m going to guide you through making a simple app which can calculate your Body Mass Index. In this tutorial we will use some elements to get you familiar with the absolute basics.
<!--more-->
  * <a title="Android refrence on TextView" href="http://developer.android.com/reference/android/widget/TextView.html" target="_blank" rel="nofollow">TextView</a>
  * <a title="Android refrence on EditText" href="http://developer.android.com/reference/android/widget/EditText.html" target="_blank" rel="nofollow">TextEdit</a>
  * <a title="Android refrence on Button" href="http://developer.android.com/reference/android/widget/Button.html" target="_blank" rel="nofollow">Button</a>
  * ButtonListener

This is a great practice for people who’ve just begun their Android or even Java coding. If you haven’t used <a title="Download Android Studio" href="http://developer.android.com/sdk/index.html" target="_blank" rel="nofollow">Android Studio, which is the IDE I’m using</a>, and I highly recommend it, and it&#8217;s pretty easy to get started with.

## The Strings of your Android Application

A good place to start is to set up the strings we&#8217;ll need in our app. When calculating BMI you will need two values from the user, their height and their weight. So we&#8217;re going to need two TextView strings, and one string for our button and of course we&#8217;ll need the name of the App &#8211; lets name it BMI Calculator.

<pre class="lang:xhtml decode:true" title="res/values/strings.xml"><resources>
    <string name="app_name">BMI Calculator</string>
    <string name="bmi_weight">Weight in KG:</string>
    <string name="bmi_height">Height in CM:</string>
    <string name="bmi_calc_button">Calculate BMI</string>
</resources></pre>

## Making your app beautiful, kind of

Lets get our layout design out of our way, it doesn’t have to be to complicated to fit our needs. We’ll just use a simple RelativeLayout, and put everything below each item. I know it’s not fancy, but hey &#8211; it’s functional!

<pre class="lang:xhtml decode:true " title="res/layout/activity_main.xml"><RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity"
    >

    <!-- The app name -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/app_name"
        android:id="@+id/textView"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:textSize="30sp" />
    <!-- Height in CM text -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/bmi_height"
        android:id="@+id/bmi_height"
        android:layout_below="@+id/textView"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:textSize="20sp" />
    <!-- Height in CM input -->
    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="number"
        android:ems="10"
        android:id="@+id/height_input"
        android:layout_below="@+id/bmi_height"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true" />
    <!-- Weight in KG text -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/bmi_weight"
        android:id="@+id/bmi_weight"
        android:layout_below="@+id/height_input"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:textSize="20sp" />
    <!-- Weight in KG input -->
    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="number"
        android:ems="10"
        android:id="@+id/weight_input"
        android:layout_below="@+id/bmi_weight"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true" />
    <!-- Calculate BMI Button -->
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/bmi_calc_button"
        android:id="@+id/bmi_calc_button"
        android:layout_below="@+id/weight_input"
        android:layout_centerHorizontal="true" />
    <!-- The TextView that will be updated with the Value -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:text="0"
        android:id="@+id/bmi_result"
        android:textSize="50sp"
        android:layout_below="@+id/bmi_calc_button"
        android:layout_centerHorizontal="true" />
</RelativeLayout></pre>

This is how our Android app looks when rendered, as I said &#8211; it’s not the fanciest app you’ve seen but that is for another article, it’s functional and that’s the point of this tutorial. As you can see we have four TextViews, two number EditTexts and one Button, and we&#8217;ve made use of our previously made strings for easy editing.

[<img class="aligncenter wp-image-110" src="https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/bmi_calculator_layout.png?resize=480%2C853" alt="How our Android app will look" srcset="https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/bmi_calculator_layout.png?w=1080 1080w, https://i1.wp.com/jejje.net/wp-content/uploads/2015/03/bmi_calculator_layout.png?resize=169%2C300 169w, https://i2.wp.com/jejje.net/wp-content/uploads/2015/03/bmi_calculator_layout.png?resize=576%2C1024 576w" sizes="(max-width: 480px) 100vw, 480px" data-recalc-dims="1" />](https://i0.wp.com/jejje.net/wp-content/uploads/2015/03/bmi_calculator_layout.png)

## Finally some Java code

Finally we’re ready to begin with the actual Java coding for our application, are you excited? Good, you should be &#8211; coding is fun! We’ll begin by declaring some of our variables we’ll need, and then find the view items by their id.

<pre class="lang:java decode:true">// Find UI elements by ID and save to variable
EditText height = (EditText) findViewById(R.id.height_input);
EditText weight = (EditText) findViewById(R.id.weight_input);
TextView bmi_result = (TextView) findViewById(R.id.bmi_result);
Button button = (Button) findViewById(R.id.bmi_calc_button);
</pre>

Now we have setup our variables, and we will need to write a Listener for our button, since we only have one button to listen for we can keep it simple and stick everything in our main class. We do need to check for null values though, and we’re going to use Toast to tell the user that they need to enter the missing values.

## Make a send Toast method

To make it easy on us we will make a method in our main class below our **onCreate()** method, let’s call it **sendToast()**. Let’s begin with the sendToast() method, preferably this should be put into a separate helpers class but since this is a basic Android app, there is no need for that. First things first, we need context &#8211; well Toast needs context, so let’s define that first at the top of our class.

<pre class="lang:java decode:true">// Toast needs context
final Context context = this;</pre>

I’ve chosen to put this helper method at the bottom of our class, and it takes one String argument, which is the message we’re sending.

<pre class="lang:java decode:true">/***
 * This method will send the user a Toast
 * which is a small black popup that is 
 * only visible for a few seconds.
 * 
 * Our method takes one argument of a
 * String with the message.
 * 
 * @param msg
 */
public void sendToast(String msg)
{
    // Get the message from our method call
    CharSequence text = msg;
    int duration = Toast.LENGTH_SHORT;

    Toast toast = Toast.makeText(context, text, duration);
    toast.show();
}
</pre>

Looks neat right? When we’re coding we always need to be thinking and <a title="DRY - Don't Repeat Yourself" href="http://en.wikipedia.org/wiki/Don%27t_repeat_yourself" target="_blank" rel="nofollow">following the DRY principles</a>. As I mentioned above, we need to listen to the button click and then check for null values, or else our Android app will crash on launch &#8211; let’s do that now in our **onCreate()** method below our variables we set earlier.

<pre class="lang:java decode:true" title="Button Listener">// Listen for our click event
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

        // Check for null
        if (height.getText().toString().length() < 1)
        {
            sendToast("You must enter your height!");
            // Abort the onClick if null
            return;
        }
        if (weight.getText().toString().length() < 1)
        {
            sendToast("You must enter your weight, sorry!");
            // Abort the onClick if null
            return;
        }
        // Passed the null checks, let's do some math!

        /***
         * Android is funny this way, but you have
         * to convert it back and forth from integer/float
         * to strings, you'll get used to it. 😉
         */
        // Convert height from string to float
        float h = Float.valueOf(height.getText().toString());
        float w = Float.valueOf(weight.getText().toString());

        /***
         * Time for math!
         * BMI is calculated
         * (weigth in kg / (height in meter * height in meter)
         * But since we want the user to input in CM, we just
         * multiply it with 10 000 to get the correct value.
         */
        float BMI = w / (h * h) * 10000;

        // Set the bmi_result view item of the value of our BMI
        bmi_result.setText(String.valueOf(BMI));
    }
});</pre>

Not many lines of code and you’ve made a simple Android app that gets input from the user and then updates the textview from zero to the users BMI. I know that this app needs a lot of refinement, for example if the user enters zero as height or weight the result will be NaN _(Not a Number)_ and more checking is needed, but for this short tutorial it&#8217;s overkill. Just below here is our full code of our **MainActivity.java** &#8211; everything put together.

<pre class="lang:java decode:true" title="MainActivity.java">package net.jejje.java.bmicalculatortutorial;

import android.content.Context;
import android.support.v7.app.ActionBarActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;


public class MainActivity extends ActionBarActivity {

    // Toast needs context
    final Context context = this;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Find UI elements by ID and save to variable
        final EditText height = (EditText) findViewById(R.id.height_input);
        final EditText weight = (EditText) findViewById(R.id.weight_input);
        final TextView bmi_result = (TextView) findViewById(R.id.bmi_result);
        Button button = (Button) findViewById(R.id.bmi_calc_button);

        // Listen for our click event
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                // Check for null
                if (height.getText().toString().length() < 1)
                {
                    sendToast("You must enter your height!");
                    // Abort the onClick if null
                    return;
                }
                if (weight.getText().toString().length() < 1)
                {
                    sendToast("You must enter your weight, sorry!");
                    // Abort the onClick if null
                    return;
                }
                // Passed the null checks, let's do some math!

                /***
                 * Android is funny this way, but you have
                 * to convert it back and forth from integer/float
                 * to strings, you'll get used to it. 😉
                 */
                // Convert height from string to float
                float h = Float.valueOf(height.getText().toString());
                float w = Float.valueOf(weight.getText().toString());

                /***
                 * Time for math!
                 * BMI is calculated
                 * (weigth in kg / (height in meter * height in meter)
                 * But since we want the user to input in CM, we just
                 * multiply it with 10 000 to get the correct value.
                 */
                float BMI = w / (h * h) * 10000;

                // Set the bmi_result view item of the value of our BMI
                bmi_result.setText(String.valueOf(BMI));
            }
        });


    }

    /***
     * This method will send the user a Toast
     * which is a small black popup that is
     * only visible for a few seconds.
     *
     * Our method takes one argument of a
     * String with the message.
     *
     * @param msg
     */
    public void sendToast(String msg)
    {
        // Get the message from our method call
        CharSequence text = msg;
        int duration = Toast.LENGTH_SHORT;

        Toast toast = Toast.makeText(context, text, duration);
        toast.show();
    }

}</pre>

If you&#8217;re not a Copy and paste kind of guy or gal, you can find the code for this Tutorial at my GitHub page, <a href="https://github.com/jejje/android-bmi-calculator-tutorial" target="_blank" rel="nofollow">BMI Calculator Tutorial at GitHub</a>.

<div style="font-size:0px;height:0px;line-height:0px;margin:0;padding:0;clear:both">
</div>