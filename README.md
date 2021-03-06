<img src="assets/magellan_icon_web_hi_res_512.png" width="200" align="right" hspace="20" />

# Magellan

The simplest navigation library for Android.


## Main Features

 - Navigation is as simple as calling `goTo(screen)`
 - You get **full control** of the backstack
 - Transitions are automaticaly handled for you
 
## Download

Add the dependencies you need in your `build.gradle`:

### Core library

```gradle
compile 'com.wealthfront:magellan:0.1.4'
```
### With optional add-ons

```gradle
def magellanVersion = '0.1.4'
compile 'com.wealthfront:magellan:' + magellanVersion
compile 'com.wealthfront:magellan-rx:' + magellanVersion
```

## Getting started

### Minimal implementation in your main activity

In your single `MainActivity.java`:

```java
  static Navigator navigator = Navigator.with(new HomeScreen()).build();

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main_activity);
    
    navigator.onCreate(this, savedInstanceState);
  }
  
  @Override
  public void onBackPressed() {
    if (!navigator.handleBack()) {
      super.onBackPressed();
    }
  }
  
  @Override
  protected void onDestroy() {
    navigator.onDestroy(this);
    super.onDestroy();
  }

```

In your `main_activity.xml`:

```xml
<com.wealthfront.magellan.ScreenContainer
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@id/magellan_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    /> 
```

### Minimal Screen implementation

`Screen` example `HomeScreen.java`:

```java
public class HomeScreen extends Screen<HomeView> {
  @Override
  protected HomeView createView(Context context) {
    return new HomeView(context);
  }
}
```

Associated `ScreenView` in `HomeView.java`:

```java
public class HomeView extends BaseScreenView<HomeScreen> {
  public InviteView(Context context) {
    super(context);
    inflate(getContext(), R.layout.home, this);
  }
}
``` 

## License

```
Copyright 2017 Wealthfront, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
