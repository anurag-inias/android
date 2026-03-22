# Activity - Basic setup

=== "Activity class"

    ```kotlin linenums="1"
    package com.example.playground

    import android.os.Bundle
    import android.util.Log
    import androidx.activity.enableEdgeToEdge
    import androidx.appcompat.app.AppCompatActivity

    class MainActivity : AppCompatActivity() {

      private var count = 1

      override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Log.v(TAG, "#onCreate")

        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        if (savedInstanceState != null) { // (1)
          count = savedInstanceState.getInt(COUNT_KEY)
        }
      }

      override fun onRestart() {
        super.onRestart()
        Log.v(TAG, "#onRestart")
      }

      override fun onStart() {
        super.onStart()
        Log.v(TAG, "#onStart")
      }

      override fun onRestoreInstanceState(savedInstanceState: Bundle) { // (2)
        super.onRestoreInstanceState(savedInstanceState)
        count = savedInstanceState.getInt(COUNT_KEY)
      }

      override fun onResume() {
        super.onResume()
        Log.v(TAG, "#onResume")
      }

      override fun onPause() {
        Log.v(TAG, "#onPause")
        super.onPause()
      }

      override fun onStop() {
        Log.v(TAG, "#onStop")
        super.onStop()
      }

      override fun onSaveInstanceState(outState: Bundle) { // (3)
        super.onSaveInstanceState(outState)
        outState.putInt(COUNT_KEY, count)
      }

      override fun onDestroy() {
        Log.v(TAG, "#onDestroy")
        super.onDestroy()
      }

      companion object {
        private const val TAG = "MainActivity"
        private const val COUNT_KEY = "COUNT"
      }
    }
    ```

    1. Restore the state if it exists
    2. Alternative: Dedicated restore method (called after `onStart`)
    3. Since Android 9+, it is now always called after `onStop`. <br> <br> Prior to Android 9 (API 28), it used to be called before `onStop`, but not guaranteed if before or after `onPause`. 

=== "Manifest"

    ```xml linenums="1" hl_lines="14-21"
    <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools">

      <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Playground">
        <activity
          android:exported="true"
          android:name=".MainActivity">
          <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
          </intent-filter>
        </activity>
      </application>

    </manifest>
    ```