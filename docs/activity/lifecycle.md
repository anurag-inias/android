# Lifecycle

![](https://developer.android.com/guide/components/images/activity_lifecycle.png)

## Three ways Activities die:

=== "Low memory kill"
    
    **When:**

      : App is in background (`onStop` already happened) and system is low on memory

    **Lifecycle calls:**

      : `onStop -> Process killed`

    There is no goodbye kiss, just lights out.


=== "Configuration change"
    
    **When:**

      : Dark theme toggle, rotation, fold, unfold, language change

    **Lifecycle calls:**

      : `onPause -> onStop -> onDestroy -> (immediate) onCreate`


=== "Graceful exit"
    
    **When:**

      : 1. `finish()` called on the activity in code.
        2. Back button/gesture on child activity $(\text{Activity A} \rightarrow \text{Activity B} \rightarrow \text{back button})$.
        3. Back button/gesture on root activity in Android 11 or older.

        !!! note "Android 12 features and changes list"

            [Root launcher activities are no longer finished on Back press](https://developer.android.com/about/versions/12/behavior-changes-all#activity-lifecycle)

    **Lifecycle calls:**

      : `onPause -> onStop -> onDestroy`

    Activity is gone and system does **not** keep its state.













