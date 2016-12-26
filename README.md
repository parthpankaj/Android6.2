# Android6.2
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:background="#5f5951"
    android:orientation="horizontal" >

    <fragment
        android:id="@+id/listFragment"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_marginBottom="?android:attr/actionBarSize"
        android:layout_marginTop="?android:attr/actionBarSize"
        android:layout_weight="1" >
    </fragment>

    <FrameLayout
        android:id="@+id/detailFragment"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="2" >
    </FrameLayout>

</LinearLayout>
----------------------------
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#ffffff"
    android:gravity="center"
    android:orientation="vertical" >

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="8"
        android:gravity="left|center_vertical"
        android:text="Layout1"
        android:textColor="#000000" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="8"
        android:gravity="left|center_vertical"
        android:text="Layout2"
        android:textColor="#000000" />

    <Button
        android:id="@+id/button3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="8"
        android:gravity="left|center_vertical"
        android:text="Layout3"
        android:textColor="#000000" />

    <Button
        android:id="@+id/button4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="8"
        android:gravity="left|center_vertical"
        android:text="Layout4"
        android:textColor="#000000" />

</LinearLayout>
-----------------
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/darker_gray"
    android:gravity="center_horizontal|center_vertical"
    android:orientation="vertical" >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Layout 1"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:textSize="30dip"
        android:textColor="#000000" />

</LinearLayout>
----------
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/darker_gray"
    android:gravity="center_horizontal|center_vertical"
    android:orientation="vertical" >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Layout 2"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:textSize="30dip"
        android:textColor="#000000" />

</LinearLayout>
------------
package com.example.pankaj.fragment62;

import android.app.Activity;
import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.os.Bundle;

public class MainActivity extends Activity implements
        ListFragment.OnItemSelectedListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
// TODO Auto-generated method stub
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onRssItemSelected(String link) {
// TODO Auto-generated method stub
        FragmentManager fragmentManager = getFragmentManager();
        FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();

        Layout1 layout1; //Fragment 1
        Layout2 layout2; //Fragment 2

        if (link.equals("layout1")) {
            layout1 = new Layout1();
            fragmentTransaction.replace(R.id.detailFragment, layout1);
            fragmentTransaction.commit();
        } else if (link.equals("layout2")) {
            layout2 = new Layout2();
            fragmentTransaction.replace(R.id.detailFragment, layout2);
            fragmentTransaction.commit();
        }
    }
}
-----
package com.example.pankaj.fragment62;

import android.app.Activity;
import android.app.Fragment;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;

public class ListFragment extends Fragment {

    private OnItemSelectedListener listener;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.list_fragment, container, false);

        Button button = (Button) view.findViewById(R.id.button1);
        Button button1 = (Button) view.findViewById(R.id.button2);
        Button button2 = (Button) view.findViewById(R.id.button3);
        Button button3 = (Button) view.findViewById(R.id.button4);

        button.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                updateDetail("layout1");
            }
        });

        button1.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                updateDetail("layout2");
            }
        });

        button2.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                updateDetail("layout3");
            }
        });

        button3.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                updateDetail("layout4");
            }
        });

        return view;
    }

    public interface OnItemSelectedListener {
        public void onRssItemSelected(String link);
    }

    @Override
    public void onAttach(Activity activity) {
        super.onAttach(activity);
        if (activity instanceof OnItemSelectedListener) {
            listener = (OnItemSelectedListener) activity;
        } else {
            throw new ClassCastException(activity.toString() + " must implemenet MyListFragment.OnItemSelectedListener");
        }
    }

    // May also be triggered from the Activity
    public void updateDetail(String s) {
        listener.onRssItemSelected(s);
    }
}
