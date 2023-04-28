# How to import included layout resource file in an Activity
### XML resource layout file
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/background_miscellaneous"
    android:id="@+id/login"
    app:behavior_peekHeight= "@dimen/_20sdp"
    app:layout_behavior="@string/bottom_sheet_behavior"
    >


    <TextView
        android:id="@+id/textMiscellaneous"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:includeFontPadding="false"
        android:text="Login"
        android:textColor="@color/white"
        android:textSize="@dimen/_13sdp"
        />

    <LinearLayout
        android:id="@+id/layoutNoteColor"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="@dimen/_12sdp"
        android:gravity="center_vertical"
        android:orientation="vertical"
        >

        <EditText
            android:id="@+id/user_email"
            android:layout_width="242dp"
            android:layout_height="65dp"
            android:hint="xyz@gmail.com"
           />

        <EditText
            android:id="@+id/user_password"
            android:layout_width="239dp"
            android:layout_height="65dp"
            android:hint="password"
        />
        <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Button"
            android:backgroundTint="@color/yellow"
            />
    </LinearLayout>
</LinearLayout>
```
### Mainactivity xml resource file where The login layout resource file was included
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:background="@color/black"
    >

    <LinearLayout
        android:id="@+id/chat_layout"
        android:layout_width="match_parent"
        android:layout_height="@dimen/_390sdp"
        android:background="@drawable/background_miscellaneous"
        android:orientation="vertical"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.16000003"
        android:visibility="gone">

        <ListView
            android:id="@+id/messeges_list_view"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

        </ListView>

    </LinearLayout>

    <include
        android:id="@+id/login"
        layout="@layout/login"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="@dimen/_10sdp"
        android:layout_marginEnd="@dimen/_10sdp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.25" />

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/messege_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="30dp"
        android:layout_marginBottom="30dp"
        android:clickable="true"
        android:contentDescription="floating_button"
        android:focusable="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:srcCompat="@drawable/ic_messege"
        android:backgroundTint="@color/yellow"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```
### Java code in Activity
```
 View loginlayout = findViewById(R.id.login);
        Button button_login = (Button)loginlayout.findViewById(R.id.button);
        button_login.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getApplicationContext(), "login button clicked", Toast.LENGTH_LONG).show();
            }
        });
```
Here login is the name of the xml file example : ``` login.xml ```.  
This xml layout file was included in the main activity  
example :  The code below shows how to include a layout xml file into your main activity
```
<include
        android:id="@+id/login"
        layout="@layout/login"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="@dimen/_10sdp"
        android:layout_marginEnd="@dimen/_10sdp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.25" />
```
Now as you can see there are some ui components like 2 EditText fileds and a button. So now the question is how will you acess the ui components inside this layout view? The answer is simple ```Button button_login = (Button)loginlayout.findViewById(R.id.button);``` you just need to add the root layout on which the button is placed.
# How to Hide a view using Java in the backend in an android app using a button
### Java code to handle the hiding and showing of a view programatically using a button
```
        //now setting up an onclick listener for our floating button
        messege_button = (FloatingActionButton) findViewById(R.id.messege_button);
        messege_button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //Toast.makeText(getApplicationContext(), "Messege button clicked", Toast.LENGTH_LONG).show();
                if (loginlayout.getVisibility() == View.VISIBLE) {
                    // Its visible
                    loginlayout.setVisibility(View.GONE);
                    chatlayout.setVisibility(View.VISIBLE);
                } else {
                    // Either gone or invisible
                    loginlayout.setVisibility(View.VISIBLE);
                    chatlayout.setVisibility(View.GONE);
                }

            }
        });
```
### How to add animation when hiding or showing the view on a button click while using ```View.GONE or View.VISIBLE``` in the if else statement inside ```messege_button.setOnClickListener``` method 
```
        //now setting up an onclick listener for our floating button
        messege_button = (FloatingActionButton) findViewById(R.id.messege_button);
        messege_button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                //Toast.makeText(getApplicationContext(), "Messege button clicked", Toast.LENGTH_LONG).show();
                if (loginlayout.getVisibility() == View.VISIBLE) {
                    // Its visible
                    //loginlayout.setVisibility(View.GONE);
                    loginlayout.animate()
                            .translationY(view.getHeight())
                            .alpha(0.0f)
                            .setDuration(300)
                            .setListener(new AnimatorListenerAdapter() {
                                @Override
                                public void onAnimationEnd(Animator animation) {
                                    super.onAnimationEnd(animation);
                                    loginlayout.setVisibility(View.GONE);
                                }
                            });

                    //chatlayout.setVisibility(View.VISIBLE);
                    chatlayout.animate()
                            .translationY(view.getHeight())
                            .alpha(1.0f)
                            .setDuration(300)
                            .setListener(new AnimatorListenerAdapter() {
                                @Override
                                public void onAnimationEnd(Animator animation) {
                                    super.onAnimationEnd(animation);
                                    chatlayout.setVisibility(View.VISIBLE);
                                }
                            });
                } else {
                    // Either gone or invisible
                    //loginlayout.setVisibility(View.VISIBLE);
                    loginlayout.animate()
                            .translationY(view.getHeight())
                            .alpha(1.0f)
                            .setDuration(300)
                            .setListener(new AnimatorListenerAdapter() {
                                @Override
                                public void onAnimationEnd(Animator animation) {
                                    super.onAnimationEnd(animation);
                                    loginlayout.setVisibility(View.VISIBLE);
                                }
                            });

                    //chatlayout.setVisibility(View.GONE);
                    chatlayout.animate()
                            .translationY(view.getHeight())
                            .alpha(0.0f)
                            .setDuration(300)
                            .setListener(new AnimatorListenerAdapter() {
                                @Override
                                public void onAnimationEnd(Animator animation) {
                                    super.onAnimationEnd(animation);
                                    chatlayout.setVisibility(View.GONE);
                                }
                            });
                }

            }
        });
```
