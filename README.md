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
#### NOTE: ```alpha = 0.0f``` means the pixels of a view is transparent and ```alpha = 1.0f``` means the pixels of a view is opaque
# How to Use RecyclerView in an app
### Step 1 : initialize the Base UI of a recyclerView (activity_main.xml file)
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
        android:layout_height="@dimen/_490sdp"
        android:background="@drawable/chat_dialog_bg"
        android:orientation="vertical"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.16000003"
        android:visibility="gone">

        <TextView
            android:id="@+id/customer_support"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center"
            android:includeFontPadding="false"
            android:text="@string/customer_support"
            android:textColor="@color/white"
            android:textSize="@dimen/_13sdp"
            />

        <androidx.recyclerview.widget.RecyclerView
            android:id="@+id/recylerView_chat_options"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingTop="@dimen/_20sdp"
        >
        </androidx.recyclerview.widget.RecyclerView>


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
In activity.xml file declare RecyclerView base UI 
```
        <androidx.recyclerview.widget.RecyclerView
            android:id="@+id/recylerView_chat_options"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingTop="@dimen/_20sdp"
        >
```
### Step 2 : Create a RecyclerView item holder layout view in (custome_list_item.xml)
This is a View that holds the RecyclerView items inside a cart within a recyclerView
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/mainLayout"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="@dimen/_5sdp">

    <!--add this blurrkit after adding dependencies in gradle file
     implementation 'io.alterac.blurkit:blurkit:1.1.0'

     <io.alterac.blurkit.BlurLayout
        android:id="@+id/blurLayout"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/cardView" />

     -->

    <androidx.cardview.widget.CardView
        android:id="@+id/cardView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="7dp"
        app:cardBackgroundColor="@android:color/transparent"
        app:cardElevation="0dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        >

        <!--add this app:cardElevation="0dp" inside cardView widget-->

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/chat_bg"
            >

            <ImageView
                android:id="@+id/imageView"
                android:layout_width="@dimen/_50sdp"
                android:layout_height="@dimen/_25sdp"
                android:layout_marginStart="@dimen/_10sdp"
                android:layout_marginTop="@dimen/_10sdp"
                android:layout_marginBottom="@dimen/_10sdp"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:srcCompat="@drawable/bullet"
                android:paddingBottom="@dimen/_10sdp"/>

            <TextView
                android:id="@+id/chat_option_text"
                android:layout_width="300dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="20dp"
                android:layout_marginTop="10dp"
                android:text="Folder_name"
                android:textColor="#F8F6F6"
                android:textSize="@dimen/_14sdp"
                android:textStyle="bold"
                app:layout_constraintStart_toEndOf="@+id/imageView"
                app:layout_constraintTop_toTopOf="parent" />

            <TextView
                android:id="@+id/folder_detail_row_card_view_layout"
                android:layout_width="2dp"
                android:layout_height="2dp"
                android:layout_marginStart="20dp"
                android:layout_marginTop="10dp"
                android:text="note_id"
                android:textColor="#F8F6F6"
                android:textSize="25sp"
                android:textStyle="bold"
                android:alpha="0"
                app:layout_constraintStart_toEndOf="@+id/imageView"
                app:layout_constraintTop_toTopOf="parent" />

            <TextView
                android:id="@+id/folder_id_row"
                android:layout_width="2dp"
                android:layout_height="2dp"
                android:layout_marginStart="20dp"
                android:layout_marginTop="20dp"
                android:layout_marginBottom="20dp"
                android:alpha="0"
                android:padding="12dp"
                android:text="1"
                android:textColor="#FFFEFE"
                android:textSize="40sp"
                android:textStyle="bold"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>

</androidx.constraintlayout.widget.ConstraintLayout>
```
### Step 3 : Create a MyViewHolder java class for RecyclerView (MyViewHolder.java)
This will initialize all the UI elements inside The RecyclerView for example TextView , Buttons etc...
```
package com.example.client_app;

import android.view.View;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

public class MyViewHolder extends RecyclerView.ViewHolder {

    TextView chat_option_text;

    public MyViewHolder(@NonNull View itemView) {
        super(itemView);
        chat_option_text = itemView.findViewById(R.id.chat_option_text);
    }
}

```
### Step 4 : Create an adapter for the RecyclerView example (MyAdapter.java)
This Adapter java files handles functions like setting up onclickListener on items of the RecyclerView ,  
Pulling data from the database and showing it on the recyclerView etc ...
```
package com.example.client_app;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class MyAdapter extends RecyclerView.Adapter<MyViewHolder> {

    Context context;
    List<String> chat_options_data_list;

    public MyAdapter(Context context, List<String> chat_options_data) {
        this.context = context;
        this.chat_options_data_list = chat_options_data;
    }

    @NonNull
    @Override
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(context).inflate(R.layout.custome_list_item, parent, false);
        return new MyViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder, int position) {
        holder.chat_option_text.setText(chat_options_data_list.get(position));

    }

    @Override
    public int getItemCount() {
        return chat_options_data_list.size();
    }
}

```
### Step 5 : Setting up RecyclerView in MainActivity.java
```
package com.example.client_app;

import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;


import android.animation.Animator;
import android.animation.AnimatorListenerAdapter;
import android.content.Context;
import android.os.Bundle;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;

import android.widget.Button;
import android.widget.EditText;

import android.widget.LinearLayout;
import android.widget.Toast;

import com.google.android.material.floatingactionbutton.FloatingActionButton;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    private FloatingActionButton messege_button;

    //setting up chat option recyclerView
    private RecyclerView recylerView_chat_options;
    private RecyclerView.LayoutManager layoutManager;
    private RecyclerView.Adapter adapter;
    //model object for our list data


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //initializing and handeling login view xml here
        //this login view xml was included here into this activity main xml file
        View loginlayout = findViewById(R.id.login);
        Button button_login = (Button)loginlayout.findViewById(R.id.button);
        button_login.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getApplicationContext(), "login button clicked", Toast.LENGTH_LONG).show();
            }
        });

        //initializing the chatlayout
        View chatlayout = findViewById(R.id.chat_layout);

        //now setting up an onclick listener for our floating button
        /*
        * This button will hide the login view when clicked and show us the chat view and vice a versa
        * */
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

        //chatView RECYCLER VIEW
        /*
        * Initializing the chat's recyclerView where all the chat options will be shown
        * */
        recylerView_chat_options = findViewById(R.id.recylerView_chat_options);
        
        //data to be fed in the recycler view
        /*
        * usually we would feed the data to the recyler view either through apis of a website or a database like SQLite
        * */
        List<String> item = new ArrayList<>();
        item.add("Login related issues");

        recylerView_chat_options.setLayoutManager(new LinearLayoutManager(MainActivity.this));
        //setting up the adapter to the recyclerView and feeding the data to be shown in the recyclerView through a List of Strings
        MyAdapter recyclerViewAdapter = new MyAdapter(this, item);
        recylerView_chat_options.setAdapter(recyclerViewAdapter);
    }

    }

```
Notice these lines are the one that handles the recyclerView
```
//chatView RECYCLER VIEW
        /*
        * Initializing the chat's recyclerView where all the chat options will be shown
        * */
        recylerView_chat_options = findViewById(R.id.recylerView_chat_options);
        //data to be fed in the recycler view
        /*
        * usually we would feed the data to the recyler view either through apis of a website or a database like SQLite
        * */
        List<String> item = new ArrayList<>();
        item.add("Login related issues");

        recylerView_chat_options.setLayoutManager(new LinearLayoutManager(MainActivity.this));
        //setting up the adapter to the recyclerView and feeding the data to be shown in the recyclerView through a List of Strings
        MyAdapter recyclerViewAdapter = new MyAdapter(this, item);
        recylerView_chat_options.setAdapter(recyclerViewAdapter);
```
