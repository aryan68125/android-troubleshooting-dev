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
