# Lifecycle

![](https://developer.android.com/guide/components/images/activity_lifecycle.png)

## onCreate

  - must be implemented.
  - perform basic application startup logic that happens once in the entire life of the activity.
  - e.g. bind data ot lists, instantiate class-scope varibales, associate activity with a `ViewModel`.

## onStart

  - completes quickly and activity does not remain in this state for long.

## onResume

  - can be called multiple times as the app loses focus and then regains it (e.g. user receiving phone call).

## onPause

  - activity is no longer in the foreground, but may still be visible.
  - is very brief and does not have enough time for any save operations.

## onStop

  - release or adjust resources that are not needed while the app is not visible. e.g. pause animations or switch location from fine-grained to coarse-grained.
  - can use this to perform relatively CPU-intensive shutdown operation. e.g. save information to a database.

  When in `STOPPED`, activity object is kept in memory, but not attached to the window manager.

## onSaveInstanceState

Since Android 9 (API 28), it is always called after `onStop`.

Prior to that, it could be either:

  : 1. `onPause -> onSaveInstanceState -> onStop`.
    2. `onSaveInstanceState -> onPause -> onStop`.

`outState` has a strict total size limit of 1MB across the entire app, so effectively much smaller for a single activity.

---

## Three ways Activities die

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













