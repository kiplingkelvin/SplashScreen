# How to create a Splash screen

##### Well, actually, it's easy. The ingredients are:

* An Activity for the Splash Screen (without the layout file)
* Your Manifest: to declare you Splash Screen as the Launcher
* One drawable(logo) file to customize the splash screen a little

 *The splash view has to be ready immediately, even before you can inflate a layout file in your splash activity.*


# Api's Used

For making our splash screen more attractive and more real, I used two animation api's to ehnhance the look. The api's are [com.daimajia.androidanimations:library](https://github.com/daimajia/AnimationEasingFunctions) and [com.airbnb.android:lottie](https://github.com/airbnb/lottie-android). So, lets get started on adding the dependencies.

## The recipe:

## Step 1 (Adding dependencies)
### Android Animations Library
#### Gradle
```groovy
dependencies {
        implementation 'com.daimajia.androidanimations:library:2.3@aar'
}
```
#### Maven

```xml
<dependency>
    <groupId>com.android.support</groupId>
    <artifactId>support-compat</artifactId>
    <version>25.1.1</version>
</dependency>
<dependency>
    <groupId>com.daimajia.androidanimation</groupId>
    <artifactId>library</artifactId>
    <version>2.3</version>
</dependency>
<dependency>
    <groupId>com.daimajia.easing</groupId>
    <artifactId>library</artifactId>
    <version>2.0</version>
</dependency>
```
### Android Lottie
#### Gradle
Gradle is the only supported build configuration, so just add the dependency to your project `build.gradle` file:

```groovy
dependencies {
  implementation 'com.airbnb.android:lottie:$lottieVersion'
}
```
The latest Lottie version is:
![lottieVersion](https://maven-badges.herokuapp.com/maven-central/com.airbnb.android/lottie/badge.svg)

Lottie 2.8.0 and above only supports projects that have been migrated to [androidx](https://developer.android.com/jetpack/androidx/). For more information, read Google's [migration guide](https://developer.android.com/jetpack/androidx/migrate).

## Step 2

###### Create your Splash Screen Activity

```java
public class SplashActivity extends Activity {
    //This is the time it will take for the splash screen to be displayed
    private static int SPLASH_TIME_OUT = 3000;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash);

        //This is where we change our app name font to blacklist font
        Typeface typeface = ResourcesCompat.getFont(this, R.font.blacklist);

        TextView appname= findViewById(R.id.appname);
        appname.setTypeface(typeface);

         // We use the Yoyo to make our app logo to bounce app and down.
        //There is a lot of Attension Techniques styles
        // example Flash, Pulse, RubberBand, Shake, Swing, Wobble, Bounce, Tada, StandUp, Wave.
        // Your can change the techniques to fit your liking.
        YoYo.with(Techniques.Bounce)
                .duration(7000)
                .playOn(findViewById(R.id.logo));

        //This is where we make our app name fade in as it moves up
        // There are other Fade Techniques too
        //example FadeIn, FadeInUp, FadeInDown, FadeInLeft, FadeInRight
        //FadeOut, FadeOutDown, FadeOutLeft, FadeOutRight, FadeOutUp
        YoYo.with(Techniques.FadeInUp)
                .duration(5000)
                .playOn(findViewById(R.id.appname));

        new Handler().postDelayed(new Runnable() {

            /*
             * Showing splash screen with a timer. This will be useful when you
             * want to show case your app logo / company
             */

            @Override
            public void run() {
                // This method will be executed once the timer is over
                // Start your app main activity
                startActivity(new Intent(SplashActivity.this,WelcomeActivity.class));
                finish();
            }
        }, SPLASH_TIME_OUT);
    }
}

```

activity_splash.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/colorPrimary"
    tools:context=".SplashActivity">

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ImageView
            android:id="@+id/logo"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true"
            android:src="@drawable/paw"/>

        <TextView
            android:layout_marginTop="10dp"
            android:textColor="#fff"
            android:textSize="35sp"
            android:id="@+id/appname"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_below="@id/logo"
            android:text="@string/app_name"
            android:layout_centerHorizontal="true"/>


        <com.airbnb.lottie.LottieAnimationView
            android:id="@+id/animation_view"
            android:layout_width="80dp"
            android:layout_height="80dp"
            app:lottie_fileName="splash.json"
            app:lottie_loop="true"
            app:lottie_autoPlay="true"
            android:layout_gravity="center"
            android:layout_alignParentBottom="true"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="20dp"/>

    </RelativeLayout>

</androidx.constraintlayout.widget.ConstraintLayout>

```

and your Manifest should look something like this

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.marichtech.splashscreen">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme"
        tools:ignore="GoogleAppIndexingWarning">
        <activity android:name=".SplashActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".MainActivity"/>
    </application>

</manifest>
```


That is it. You can clone the project using Android Studio and have fun.
Dont forget to follow me for more projects.

