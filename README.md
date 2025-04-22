
# Android-Doc



Basic level

## ✅ **What is Android, and How Does it Work?**

---

### 📱 **What is Android?**

**Android** is an **open-source** operating system developed by **Google**, primarily designed for **mobile devices** such as smartphones, tablets, smart TVs, and even wearables.  

- It is based on the **Linux kernel**.  
- Written mainly in **Java, Kotlin, and C++**.  
- Android powers **billions of devices** around the world.  
- It supports a huge ecosystem of **apps via Google Play Store**.

---

### 🧠 **How Android Works (Architecture Overview)**

Android is structured in **layers**, where each layer interacts with the one above or below it:

#### 1. **Linux Kernel (Bottom Layer)**  
- Acts as a bridge between hardware and software.  
- Handles **low-level device operations**: memory management, security, drivers, etc.  

#### 2. **Hardware Abstraction Layer (HAL)**  
- Acts as an interface between the hardware and the higher Android system.  
- Converts function calls from higher layers to hardware-specific commands.

#### 3. **Android Runtime (ART)**  
- Replaces the older Dalvik VM.  
- Converts bytecode to native instructions using **Ahead-of-Time (AOT)** and **Just-in-Time (JIT)** compilation.  
- Handles garbage collection and app execution.  

#### 4. **Native Libraries (C/C++)**  
- Includes core libraries like SQLite (database), WebKit (browser engine), OpenGL (graphics), etc.  
- These are used internally or via NDK (Native Development Kit).  

#### 5. **Java/Kotlin Libraries & Framework**  
- Provide essential APIs (Activity Manager, View System, Location, etc.)  
- Android app developers use these via Java or Kotlin.  

#### 6. **Application Framework**  
- High-level services that developers use, like:  
  - Activity Manager  
  - Notification Manager  
  - Resource Manager  
  - Content Providers  

#### 7. **Applications (Top Layer)**  
- These are the actual apps: Gmail, WhatsApp, Camera, etc.  
- Installed apps interact with the OS using SDK & APIs provided in the framework.

---


## What are the four main components of an Android application?

The **four main components** of an Android application are:

---

### 🔹 1. **Activity**

- Represents a **single screen with a user interface (UI)**.
- It’s where users **interact** with your app.
- Each activity goes through a **lifecycle** (e.g., `onCreate()`, `onPause()`).

📌 **Example:** Login screen, Home screen, Settings screen.

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```

---

### 🔹 2. **Service**

- A component that runs in the **background**, without a UI.
- Used for long-running operations (e.g., playing music, downloading files).
- Can be **foreground, background**, or **bound** service.

📌 **Example:** Music playing app service.

```kotlin
class MyService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // Do background work
        return START_STICKY
    }
}
```

---

### 🔹 3. **Broadcast Receiver**

- Listens for **system-wide broadcast events** (e.g., battery low, airplane mode).
- Apps can also **send custom broadcasts**.
- It doesn’t display a UI, but can **trigger notifications** or start other components.

📌 **Example:** Listening for device boot.

```kotlin
class BootReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if (intent.action == Intent.ACTION_BOOT_COMPLETED) {
            // Start some service or task
        }
    }
}
```

---

### 🔹 4. **Content Provider**

- Manages **data sharing** between applications.
- Provides a **standard interface to query or modify** data.
- Typically used with **SQLite**, but can work with any data source.

📌 **Example:** Accessing contacts, media files, etc.

```kotlin
val cursor = contentResolver.query(
    ContactsContract.Contacts.CONTENT_URI,
    null, null, null, null
)
```

---

### 🧩 Summary Table

| Component         | Purpose                          | Has UI? |
|------------------|----------------------------------|---------|
| **Activity**      | Represents a screen              | ✅ Yes  |
| **Service**       | Background processing            | ❌ No   |
| **BroadcastReceiver** | Listens/responds to system events | ❌ No   |
| **ContentProvider**   | Shares app data with others       | ❌ No   |

---

Here are detailed answers to your questions:

---

### **1. What are the main folders in an Android project, and what is their purpose?**

An Android project follows a specific directory structure. Here are the main folders and their purposes:

1. **`src/main/java`**:
   - Contains the Java or Kotlin source code for your app, including Activities, ViewModels, Adapters, and other logical components.
   - Organized by package structure.

2. **`src/main/res`**:
   - Contains all the app's resources, such as layouts, images, strings, colors, and styles.
   - Subfolders are structured based on resource types (e.g., `drawable`, `layout`, `values`).

3. **`src/main/AndroidManifest.xml`**:
   - A configuration file that defines app components (Activities, Services, Broadcast Receivers), app permissions, app metadata, themes, and more.

4. **`build/`**:
   - Contains generated files during the build process. You typically do not modify anything in this folder.

5. **`gradle/`**:
   - Contains Gradle wrapper files, which help manage the build system for the project.

6. **`libs/`**:
   - Used to store external library `.jar` or `.aar` files that are included in your project.

7. **`src/test/`**:
   - Contains unit tests written in JUnit for testing app logic.

8. **`src/androidTest/`**:
   - Contains instrumented tests for testing app behavior on an Android device or emulator.

9. **`.idea/` and `.gradle/`**:
   - Internal configuration files and settings for Android Studio and Gradle.

---

### **2. What is the `res` folder used for in an Android project?**

The **`res` (resources)** folder is used to store all non-code assets of the Android application. These assets are organized into subfolders based on their types:

1. **`res/drawable`**:
   - Stores XML drawable files and images (PNG, JPEG, etc.) used in the app.

2. **`res/layout`**:
   - Contains XML files that define the layout of UI components for Activities and Fragments.

3. **`res/values`**:
   - Holds XML files for storing key-value pairs such as strings (`strings.xml`), colors (`colors.xml`), dimensions (`dimens.xml`), and styles/themes (`styles.xml`).

4. **`res/mipmap`**:
   - Contains app launcher icons in various densities (e.g., `mdpi`, `hdpi`, `xhdpi`).

5. **`res/raw`**:
   - Stores raw assets such as audio files, video files, or other binary files that you want to access as-is.

6. **`res/menu`**:
   - Contains XML files that define app menus (e.g., options menu or context menu).

---

### **3. What is the purpose of the `build.gradle` file?**

The `build.gradle` file is the configuration file for the Gradle build system in Android projects. It exists in two levels: **project-level** and **module-level**.

1. **Project-Level `build.gradle`**:
   - Configures build settings for the entire project.
   - Specifies the Gradle plugin version and repositories for dependencies.
   - Example:
     ```groovy
     buildscript {
         repositories {
             google()
             mavenCentral()
         }
         dependencies {
             classpath 'com.android.tools.build:gradle:7.3.1'
         }
     }
     ```

2. **Module-Level `build.gradle`**:
   - Configures settings for a specific app module.
   - Specifies dependencies, SDK versions, build types, and more.
   - Example:
     ```groovy
     android {
         compileSdkVersion 33
         defaultConfig {
             applicationId "com.example.myapp"
             minSdkVersion 21
             targetSdkVersion 33
             versionCode 1
             versionName "1.0"
         }
     }
     dependencies {
         implementation 'androidx.core:core-ktx:1.9.0'
         implementation 'androidx.appcompat:appcompat:1.5.1'
     }
     ```

---

### **4. What is the difference between `res/drawable`, `res/mipmap`, and `res/raw` folders?**

| **Folder**    | **Purpose**                                                                                     | **Typical Contents**                                                                 |
|---------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| **`drawable`**| Stores images and drawable resources used in your app's UI.                                      | PNGs, JPEGs, vector drawables, XML shapes, and selectors.                          |
| **`mipmap`**  | Specifically for app launcher icons of various densities.                                        | Launcher icons (`ic_launcher`) for different device resolutions (`mdpi`, `hdpi`).  |
| **`raw`**     | Holds raw (unprocessed) files that you want to access programmatically without modification.      | Audio files (MP3, WAV), video files, or JSON configurations.                       |

#### **Key Differences:**
- **Purpose**: Use `drawable` for UI assets, `mipmap` for launcher icons, and `raw` for unprocessed files.
- **Launcher Icons**: The Android system prefers `mipmap` for launcher icons because it optimizes them for different screen densities.

---

### **5. How do you add an image or icon to an Android project?**

#### **Steps to Add an Image/Icon:**

1. **Add the Image to the `drawable` Folder**:
   - Save your image as `.png`, `.jpg`, or `.webp`.
   - Copy the image file into the `res/drawable` folder or its variant (`drawable-mdpi`, `drawable-hdpi`, etc.).

2. **Add an Icon to the `mipmap` Folder** (for launcher icons):
   - Use the **Image Asset Studio** in Android Studio:
     - Right-click the `res` folder > **New** > **Image Asset**.
     - Choose the type (e.g., Launcher Icon) and provide the source image.
     - Android Studio will generate launcher icons in various resolutions (`mipmap-mdpi`, `mipmap-hdpi`, etc.).

3. **Use the Image/Icon in Your Code or XML Layout**:
   - In XML Layout:
     ```xml
     <ImageView
         android:layout_width="wrap_content"
         android:layout_height="wrap_content"
         android:src="@drawable/your_image" />
     ```
   - In Kotlin/Java:
     ```kotlin
     imageView.setImageResource(R.drawable.your_image)
     ```

4. **For `raw` Files (e.g., Audio/Video)**:
   - Place the file in the `res/raw` folder.
   - Access it programmatically:
     ```kotlin
     val inputStream = resources.openRawResource(R.raw.your_raw_file)
     ```

#### **Tips:**
- Use vector drawables (`res/drawable`) for scalable and resolution-independent images.
- Convert high-resolution images to `.webp` format for better performance and reduced size.

---


### What is an Activity in Android?
In Android, an **Activity** is a **single, focused screen** that the user interacts with. Think of it like a window or a page in an app. Each Activity represents a **UI** (user interface) where users can do something—like view a list, fill out a form, or play a video.

### Key Points:
- It’s a **core component** of Android apps.
- An app can have **multiple activities** (like LoginActivity, MainActivity, SettingsActivity, etc.).
- Activities are managed in a **back stack**, which allows users to navigate back through the app’s history.

### Example:
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main); // sets the layout for this activity
    }
}
```

### Activity Lifecycle:
Activities go through a lifecycle with methods like:
- `onCreate()`: Called when the activity is first created.
- `onStart()`: Called when the activity becomes visible.
- `onResume()`: Called when the activity starts interacting with the user.Sure! Here are one-line definitions for each:
- `onPause()`: Called when the activity is partially visible but no longer in the foreground (e.g., another activity is in front, but this one is still visible in the background).  
- `onStop()`: Called when the activity is completely hidden and no longer visible to the user.  
- `onDestroy()`: Called before the activity is destroyed, allowing final cleanup of resources.
  
- `onPause()`, `onStop()`, `onDestroy()`: Called when the activity is going into the background or being destroyed.
  
---
Want a quick visual of the lifecycle or how multiple activities interact?


Absolutely! Here's a **quick visual** of the **Android Activity Lifecycle** and how activities interact:

---

### 🌱 **Activity Lifecycle Diagram**
```plaintext
         +-----------------------------+
         |         onCreate()          |
         +-------------+---------------+
                       |
                       v
               +---------------+
               |   onStart()   |
               +---------------+
                       |
                       v
              +----------------+
              |   onResume()   |  <--- Activity is now in the foreground
              +----------------+
                       |
     User navigates away (e.g., new activity starts)
                       |
                       v
               +---------------+
               |   onPause()   |
               +---------------+
                       |
      Activity no longer visible (completely obscured)
                       |
                       v
               +--------------+
               |   onStop()   |
               +--------------+
                       |
     Activity is finishing or system is killing it
                       |
                       v
              +----------------+
              |  onDestroy()   |
              +----------------+
```

---

### 🔁 **Multiple Activities Interaction Example**

Imagine you have two activities: `MainActivity` and `DetailsActivity`.

#### Flow:
1. User opens app → `MainActivity` goes through `onCreate()` → `onStart()` → `onResume()`.
2. User taps on an item → `DetailsActivity` starts:
   - `MainActivity`: `onPause()` → `onStop()`  
   - `DetailsActivity`: `onCreate()` → `onStart()` → `onResume()`
3. User presses back:
   - `DetailsActivity`: `onPause()` → `onStop()` → `onDestroy()`  
   - `MainActivity`: `onRestart()` → `onStart()` → `onResume()`

---

### What is the difference between an Activity and a Fragment?

Great question! **Activity** and **Fragment** are both essential components in Android development, but they serve different purposes. Here's a clear breakdown:

---

### 🧱 **Activity vs Fragment**

| Feature         | **Activity**                                | **Fragment**                                       |
|-----------------|---------------------------------------------|----------------------------------------------------|
| **Definition**  | A screen with a UI that the user interacts with | A reusable portion of the UI inside an activity     |
| **Lifecycle**   | Independent lifecycle                       | Lifecycle is **dependent** on the host Activity     |
| **Usage**       | Typically used as a full screen / container | Used for modular UI (e.g., tabs, dynamic UIs)       |
| **Navigation**  | Navigated using Intents                    | Replaced/added using FragmentManager                |
| **UI Handling** | Directly handles UI                        | Needs to be attached to an Activity for UI          |
| **Reusability** | Less reusable                              | Highly reusable in multiple activities             |
| **Back Stack**  | Managed by Android system                  | Managed manually using FragmentManager              |

---

### What is an Intent, and how do you use it to navigate between activities?

An **Intent** in Android is a **messaging object** used to request an action from another component—like starting an Activity, sending data, or starting a service.

---

### 🧭 **What is an Intent?**

- It's a way to **communicate between components**.
- Most commonly used to **navigate between activities** or to **send data** from one activity to another.

---

### 📦 Types of Intents:
1. **Explicit Intent**: Specifies the exact component (e.g., `SecondActivity.class`).
2. **Implicit Intent**: Declares a general action to be performed (e.g., "view a web page").

---

### 🚀 **Navigating Between Activities (Explicit Intent)**

#### **Example**: Going from `MainActivity` to `SecondActivity`

```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivity(intent);
```

---

### 📨 **Passing Data Between Activities**

```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
intent.putExtra("username", "JohnDoe");
startActivity(intent);
```

#### In `SecondActivity`:
```java
String username = getIntent().getStringExtra("username");
```

---

### 🔙 Go Back to Previous Activity

- Just use the **Back button**, or call:
```java
finish(); // This closes the current activity and returns to the previous one
```

---


### What is the purpose of the AndroidManifest.xml file?

The **`AndroidManifest.xml`** file is like the **blueprint** of your Android app. It tells the Android system everything it needs to know about your app **before it runs**.

---

### 🧾 **Purpose of `AndroidManifest.xml`:**

1. **Declare components**  
   - All **Activities**, **Services**, **BroadcastReceivers**, and **ContentProviders** must be declared here.
   ```xml
   <activity android:name=".MainActivity" />
   ```

2. **Request permissions**  
   - If your app needs access to the internet, camera, storage, etc.
   ```xml
   <uses-permission android:name="android.permission.INTERNET" />
   ```

3. **Define app metadata**  
   - Like app name, icon, theme, minimum SDK version, etc.
   ```xml
   <application
       android:icon="@mipmap/ic_launcher"
       android:label="@string/app_name">
   ```

4. **Set the launcher activity**  
   - The entry point when the app starts.
   ```xml
   <intent-filter>
       <action android:name="android.intent.action.MAIN" />
       <category android:name="android.intent.category.LAUNCHER" />
   </intent-filter>
   ```

5. **Declare hardware and software features**
   - E.g., touchscreen, camera, sensors, etc.


The `AndroidManifest.xml` acts as a **bridge between your app and the Android OS**, ensuring the system knows **what your app needs**, **what it contains**, and **how to launch it**.


---
### What is the role of Gradle in an Android project?

Great question! **Gradle** is the **build system** used in Android development. It’s like the behind-the-scenes **automation engine** that compiles your code, packages it into APKs, manages dependencies, and more.

---

### ⚙️ **Role of Gradle in Android Projects:**

1. **Build Automation**  
   - Compiles your Java/Kotlin code.
   - Merges resources (XML, images, etc.).
   - Generates APKs or AABs for different build variants (like `debug` and `release`).

2. **Dependency Management**  
   - Automatically downloads and includes libraries from repositories like Maven or JCenter.
   ```groovy
   implementation 'com.squareup.retrofit2:retrofit:2.9.0'
   ```

3. **Build Variants and Flavors**  
   - You can define different versions of your app (e.g., free vs paid, dev vs prod).
   ```groovy
   buildTypes {
       debug {
           // debug-specific config
       }
       release {
           minifyEnabled true
           proguardFiles getDefaultProguardFile('proguard-android-optimize.txt')
       }
   }
   ```

4. **Custom Tasks & Scripts**  
   - You can write custom Gradle tasks to automate stuff like versioning, code generation, signing, etc.

5. **Integration with Android Studio**  
   - Android Studio uses Gradle under the hood, so when you click **Run**, it’s Gradle doing the actual work.

---

### 📁 Key Gradle Files in Android:
- `build.gradle (Project-level)` – Configures global settings, repositories, plugin versions.
- `build.gradle (App/module-level)` – Configures the app itself: dependencies, build types, SDK versions, etc.
- `gradle-wrapper.properties` – Defines the version of Gradle to use.

---
**Gradle = The engine that builds, packages, and manages everything in your Android project.**

---

### How do you run an Android application on a real device?
Running your Android app on a **real device** is super useful for testing performance and hardware-related features. Here’s a step-by-step guide to get it up and running:

---

### 📲 **Steps to Run Your App on a Real Android Device:**

#### ✅ **1. Enable Developer Options on the Device**
- Go to **Settings** > **About phone**.
- Tap **Build number** 7 times until you see *"You are now a developer!"*.

#### ✅ **2. Enable USB Debugging**
- Go to **Settings** > **System** > **Developer options**.
- Turn on **USB Debugging**.

#### ✅ **3. Connect Device via USB**
- Plug your phone into your computer using a USB cable.
- Select **“File Transfer” (MTP)** or **“USB Debugging”** mode when prompted on your device.

#### ✅ **4. Authorize the Connection**
- You’ll see a prompt on your phone:  
  > *Allow USB debugging?*  
  Tap **Allow**.

#### ✅ **5. Run from Android Studio**
- Open your project in **Android Studio**.
- Click the **Run (▶️) button**.
- In the **device chooser**, select your connected device.

---

### 🧪 Tip:
If your device doesn’t show up:
- Make sure **USB drivers** are installed (especially on Windows).
- Try `adb devices` in terminal to check if it's detected.

---

### 🔁 Optional: Wireless Debugging (Android 11+)
You can also connect your device **wirelessly** via Wi-Fi using ADB over network.

---
### What is an XML layout file in Android?

An **XML layout file** in Android defines the **user interface (UI)** of an app screen using **XML (eXtensible Markup Language)**. It's how you describe **what the screen should look like** — buttons, text, images, and how they are arranged.

---

### 🧾 **What is it used for?**
- Describes the **structure and appearance** of the UI.
- Used by Activities and Fragments to **inflate (load)** the UI.
- Makes it easy to **separate design from code**.

---

### 🔧 **Basic Example: `activity_main.xml`**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/helloText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />

    <Button
        android:id="@+id/myButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click me" />

</LinearLayout>
```

---

### 🔁 How it's used in code:
In your `Activity`:
```java
setContentView(R.layout.activity_main); // Loads the XML layout
```

You can then access UI elements like:
```java
Button myButton = findViewById(R.id.myButton);
```

---

An XML layout file is where you **design the screen** — what users see and interact with — using a clean, declarative format.

---

### What are the different types of layouts available in Android?

In Android, **layouts** are containers that define **how UI elements (Views)** are arranged on the screen. Android provides several built-in layout types to suit different design needs.

---

### 🧱 **Common Types of Layouts in Android:**

| Layout Type          | Description |
|----------------------|-------------|
| **LinearLayout**     | Arranges children in a **single row or column** (vertically or horizontally). |
| **RelativeLayout**   | Positions children **relative to each other or to the parent**. |
| **ConstraintLayout** | A powerful and flexible layout that allows you to create **complex UIs with flat view hierarchies** using constraints. |
| **FrameLayout**      | Displays a **single child** view or **stacks views** on top of each other. Great for fragments or overlays. |
| **TableLayout**      | Arranges children into **rows and columns**, like a table. |
| **GridLayout**       | Places views in a **grid-like structure** (rows + columns), more flexible than TableLayout. |
| **CoordinatorLayout**| A super-powered FrameLayout for implementing **material design interactions** like collapsing toolbars and floating action buttons. |
| **ScrollView**       | A layout that provides **scrolling** for its content (vertically). |

---
- Prefer **ConstraintLayout** for complex UIs — it avoids deep nesting and improves performance.
- Use **ScrollView** when content might not fit the screen.
- Avoid deeply nested layouts for better performance.

---

### Want a visual diagram of each layout or help choosing the best one for your screen design?


Here are answers to your Android-related questions:

---

### 1. **What is the difference between LinearLayout and RelativeLayout?**

| **Feature**       | **LinearLayout**                                  | **RelativeLayout**                                |
|-------------------|--------------------------------------------------|-------------------------------------------------|
| **Definition**    | Arranges child views in **a single row or column** (vertical or horizontal). | Positions child views **relative to each other** or **to the parent container**. |
| **Usage**         | Simple layouts with a clear sequence of elements. | More flexible for complex layouts.             |
| **Performance**   | Faster as it is simpler to compute.              | Slightly slower due to measuring relative positions. |
| **Example**       | Displaying a list of items in a vertical or horizontal order. | Aligning elements like a button below a TextView. |

---

### 2. **How do you display a simple TextView and Button in an Android app?**

**`activity_main.xml`** (UI Layout):
```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />
</LinearLayout>
```

**`MainActivity.java`**:
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main); // Load the XML layout
    }
}
```

---

### 3. **What is the purpose of `findViewById()`?**

- **Definition**: `findViewById()` is used to **retrieve a reference to a UI element** (like a `TextView`, `Button`, etc.) defined in an XML layout file.
- **Purpose**: It allows you to interact with the UI element in Java/Kotlin code (e.g., set text, handle clicks).
- **Example**:
    ```java
    TextView textView = findViewById(R.id.textView);
    textView.setText("New Text");
    ```

---

### 4. **How do you handle button clicks in Android?**

You can handle button clicks in two common ways:

#### ** Using an `OnClickListener`:**
```java
Button button = findViewById(R.id.button);
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // Handle button click
        Toast.makeText(MainActivity.this, "Button clicked!", Toast.LENGTH_SHORT).show();
    }
});
```

#### ** Using `onClick` Attribute in XML:**
**XML**:
```xml
<Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="handleButtonClick"
    android:text="Click Me" />
```

**Java**:
```java
public void handleButtonClick(View view) {
    Toast.makeText(this, "Button clicked!", Toast.LENGTH_SHORT).show();
}
```

---

###  **What is a RecyclerView, and how is it different from ListView?**

| **Feature**         | **RecyclerView**                                   | **ListView**                                      |
|---------------------|---------------------------------------------------|-------------------------------------------------|
| **Definition**      | A flexible and efficient version of ListView.     | A simpler component for displaying a list of items. |
| **Performance**     | Reuses views via the **ViewHolder pattern** for better performance. | Less efficient as it does not reuse views properly. |
| **Flexibility**     | Highly customizable with support for grids, staggered layouts, etc. | Limited to simple vertical lists.               |
| **Animation**       | Supports item animations out of the box.          | Requires additional coding for animations.      |
| **Adapter**         | Uses `RecyclerView.Adapter`.                      | Uses `ArrayAdapter` or similar.                 |

---

###  **How do you change the theme or color scheme of an Android app?**

#### **Steps to Change Theme/Colors:**
1. **Edit `res/values/themes.xml`:**
   ```xml
   <style name="Theme.MyApp" parent="Theme.Material3.DayNight">
       <item name="colorPrimary">@color/primary</item>
       <item name="colorPrimaryVariant">@color/primary_variant</item>
       <item name="colorSecondary">@color/secondary</item>
   </style>
   ```
   - Replace colors with your custom ones in `res/values/colors.xml`.

2. **Apply the Theme in `AndroidManifest.xml`:**
   ```xml
   <application
       android:theme="@style/Theme.MyApp">
   ```

3. **Use `AppCompat`/Material Design Components** to respect the theme.

---

###  **What is an explicit intent vs. an implicit intent?**

| **Type**        | **Explicit Intent**                              | **Implicit Intent**                              |
|------------------|-------------------------------------------------|-------------------------------------------------|
| **Definition**   | Specifies the exact component (Activity/Service) to be opened. | Declares an action or task to be handled by any matching app. |
| **Use Case**     | Navigation within your app, e.g., opening another activity. | Opening external apps, e.g., opening a web page. |
| **Example**      | ```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivity(intent); 
``` | ```java
Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("https://www.example.com"));
startActivity(intent);
``` |

---

### 8. **How do you pass data between activities using Intent?**

#### **Passing Data:**
**In `MainActivity`:**
```java
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
intent.putExtra("username", "JohnDoe");
startActivity(intent);
```

#### **Receiving Data:**
**In `SecondActivity`:**
```java
String username = getIntent().getStringExtra("username");
```

---

### **What is the back stack in Android?**

- The **back stack** is a **stack data structure** used to manage the order of activities in an Android app.
- **Purpose**: It allows users to navigate through activities using the **Back button**.
- When an activity is started, it is **pushed onto the stack**. When the Back button is pressed, the current activity is **popped off the stack**, and the previous activity is resumed.

#### **Example:**
1. Open `Activity A` → `Activity B` → `Activity C`.
2. Back button pressed → `Activity C` is removed, and `Activity B` is displayed.

--- 


###  **How do you open a new activity using an Intent?**

To open a new activity, you use an **explicit intent** to specify the target activity.

#### Example:
```java
Intent intent = new Intent(CurrentActivity.this, NewActivity.class);
startActivity(intent);
```

- **`CurrentActivity.this`**: The context of the current activity.
- **`NewActivity.class`**: The activity you want to open.

---

###  **What is the purpose of `startActivityForResult()`?**

- **Purpose**: `startActivityForResult()` is used to **start another activity** and then **receive a result back** from that activity.
- **Use Case**: Commonly used for scenarios like picking an image from the gallery, taking a photo, or getting user input.

#### Example:
**In Caller Activity**:
```java
Intent intent = new Intent(CurrentActivity.this, NewActivity.class);
startActivityForResult(intent, 1); // 1 is the request code
```

**In Called Activity**:
```java
Intent resultIntent = new Intent();
resultIntent.putExtra("data_key", "Result Data");
setResult(Activity.RESULT_OK, resultIntent);
finish(); // Finish the activity and return the result
```

**Handling the Result in Caller Activity**:
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == 1 && resultCode == Activity.RESULT_OK) {
        String result = data.getStringExtra("data_key");
        // Use the result
    }
}
```

---

###  **What are SharedPreferences in Android?**

**SharedPreferences** is a lightweight storage option for storing **key-value pairs**. It is primarily used for **storing small amounts of data**, such as user preferences, settings, or flags.

#### Features:
- Stores **primitive data types**: `String`, `int`, `float`, `boolean`, `long`.
- Data persists even after the app is closed.

---

###  **How do you store and retrieve a simple key-value pair using SharedPreferences?**

#### Storing Data:
```java
SharedPreferences sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE);
SharedPreferences.Editor editor = sharedPreferences.edit();
editor.putString("username", "JohnDoe"); // Key: "username", Value: "JohnDoe"
editor.apply(); // Save changes
```

#### Retrieving Data:
```java
SharedPreferences sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE);
String username = sharedPreferences.getString("username", "DefaultName"); // DefaultName if key doesn't exist
```

---

###  **What is the difference between Internal Storage and External Storage in Android?**

| **Feature**          | **Internal Storage**                               | **External Storage**                              |
|-----------------------|---------------------------------------------------|-------------------------------------------------|
| **Definition**        | Storage space that is **private** to the app.     | Storage space that is **accessible** by other apps and users. |
| **Accessibility**     | Data is not accessible by other apps.             | Data can be accessed by other apps (with permissions). |
| **Security**          | More secure; files are app-private.               | Less secure as it can be accessed openly.       |
| **Use Case**          | Storing sensitive or app-only data.               | Sharing files like images, videos, or documents. |
| **Example Path**      | `/data/data/<app_package>/files/`                 | `/storage/emulated/0/` or `/sdcard/`            |

---

###  **How does SQLite work in Android?**

- **SQLite** is a lightweight, embedded, relational database engine included in Android.
- It allows you to perform SQL operations (like `INSERT`, `UPDATE`, `DELETE`, `SELECT`) to manage structured data.

#### Steps to Use SQLite:
1. **Create a Database**:
   ```java
   SQLiteDatabase db = openOrCreateDatabase("MyDatabase", Context.MODE_PRIVATE, null);
   db.execSQL("CREATE TABLE IF NOT EXISTS Users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER);");
   ```

2. **Insert Data**:
   ```java
   db.execSQL("INSERT INTO Users (name, age) VALUES ('John', 30);");
   ```

3. **Retrieve Data**:
   ```java
   Cursor cursor = db.rawQuery("SELECT * FROM Users", null);
   if (cursor.moveToFirst()) {
       do {
           int id = cursor.getInt(0);
           String name = cursor.getString(1);
           int age = cursor.getInt(2);
       } while (cursor.moveToNext());
   }
   cursor.close();
   ```

---

###  **What is the Room database, and why is it recommended over SQLite?**

**Room** is a **Jetpack library** that provides an abstraction layer over SQLite for easier database access and management.

#### Advantages of Room Over SQLite:
1. **Compile-Time Verification**: SQL queries are verified at compile time, reducing runtime errors.
2. **Boilerplate Reduction**: Automatically handles table creation, updates, and common database operations.
3. **Integration with LiveData and Coroutines**: Supports modern Android architecture patterns.
4. **Migration Support**: Provides simpler tools for database versioning and migration.

#### Example Usage:
1. **Define an Entity**:
   ```java
   @Entity
   public class User {
       @PrimaryKey(autoGenerate = true)
       public int id;
       public String name;
       public int age;
   }
   ```

2. **Create a DAO (Data Access Object)**:
   ```java
   @Dao
   public interface UserDao {
       @Insert
       void insert(User user);

       @Query("SELECT * FROM User")
       List<User> getAllUsers();
   }
   ```

3. **Build the Database**:
   ```java
   @Database(entities = {User.class}, version = 1)
   public abstract class AppDatabase extends RoomDatabase {
       public abstract UserDao userDao();
   }

   AppDatabase db = Room.databaseBuilder(getApplicationContext(),
           AppDatabase.class, "MyDatabase").build();
   ```

Room is recommended for its ease of use, safety features, and integration with modern Android practices.

--- 

5. Networking
###  **What is an API, and how do you call an API in Android?**

- **API (Application Programming Interface)**: A set of rules and protocols that allow two software components to communicate with each other. For example, a weather app can use an API to fetch weather data from a server.
- **Calling an API in Android**:
  1. Use a library like **Retrofit** or **OkHttp** for network requests.
  2. Configure the API endpoint and HTTP methods (GET, POST, etc.).
  3. Parse the server's response (usually in JSON format) and display it in the app.

**Example using Retrofit:**
```java
public interface ApiService {
    @GET("users/{id}")
    Call<User> getUser(@Path("id") int userId);
}

// Create Retrofit instance
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build();

// Call the API
ApiService apiService = retrofit.create(ApiService.class);
apiService.getUser(1).enqueue(new Callback<User>() {
    @Override
    public void onResponse(Call<User> call, Response<User> response) {
        if (response.isSuccessful()) {
            User user = response.body();
        }
    }

    @Override
    public void onFailure(Call<User> call, Throwable t) {
        t.printStackTrace();
    }
});
```

---

###  **What is Retrofit, and why is it commonly used for network calls?**

- **Retrofit**: A type-safe HTTP client for Android and Java, developed by Square. It simplifies API calls by abstracting HTTP requests and responses.
- **Why Retrofit?**
  1. **Ease of Use**: Simplifies making HTTP calls, such as GET, POST, PUT, etc.
  2. **Automatic Parsing**: Converts JSON responses into Java/Kotlin objects using converters (e.g., Gson, Moshi).
  3. **Error Handling**: Provides built-in mechanisms to handle API errors.
  4. **Scalability**: Easily supports complex APIs with query parameters, headers, and request bodies.

---

###  **How do you make an HTTP request in Android?**

There are several ways to make an HTTP request in Android:

#### **1. Using OkHttp:**
```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
    .url("https://api.example.com/data")
    .build();

client.newCall(request).enqueue(new Callback() {
    @Override
    public void onResponse(Call call, Response response) throws IOException {
        if (response.isSuccessful()) {
            String responseData = response.body().string();
        }
    }

    @Override
    public void onFailure(Call call, IOException e) {
        e.printStackTrace();
    }
});
```

#### ** Using HttpURLConnection (Native Approach):**
```java
URL url = new URL("https://api.example.com/data");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("GET");

InputStream inputStream = connection.getInputStream();
BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
StringBuilder result = new StringBuilder();
String line;
while ((line = reader.readLine()) != null) {
    result.append(line);
}
reader.close();
```

---

###  **What is the purpose of JSON in API communication?**

- **JSON (JavaScript Object Notation)**: A lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate.
- **Purpose in API Communication**:
  1. **Data Serialization**: JSON is used to send and receive structured data (e.g., user details, lists) between the client (Android app) and server.
  2. **Interoperability**: JSON is language-independent, making it widely used across different platforms.
  3. **Readable Format**: Easy to debug and understand during development.

**Example JSON Response:**
```json
{
    "id": 1,
    "name": "John Doe",
    "email": "john.doe@example.com"
}
```

---

### **What is OkHttp, and how does it help in networking?**

- **OkHttp**: A powerful HTTP client for Android and Java, developed by Square.
- **How it Helps in Networking**:
  1. **Efficient Connection Management**: Supports connection pooling, reducing network latency.
  2. **Interceptors**: Allows adding, modifying, or logging requests and responses.
  3. **Asynchronous Requests**: Supports both synchronous and asynchronous HTTP calls.
  4. **Caching**: Provides a built-in caching mechanism for offline support.
  5. **HTTP/2 Support**: Reduces network overhead and improves performance.

**Example with Interceptor:**
```java
OkHttpClient client = new OkHttpClient.Builder()
    .addInterceptor(chain -> {
        Request request = chain.request();
        Response response = chain.proceed(request);
        return response;
    })
    .build();
```

---

Let me know if you need further examples or explanations for these topics!



6. Multithreading

### 1. **What is a thread in Android?**
A thread in Android is a lightweight sub-process that executes code independently. The Android runtime starts with a single main thread, commonly called the **UI thread**, which manages all user interface (UI) rendering and input events. You can create additional threads to perform tasks in parallel, such as downloading data, processing files, or interacting with databases, so the main thread remains free to handle UI updates.

Threads are part of Java's concurrency model, and Android inherits this functionality. However, managing threads properly is crucial to avoid issues like thread starvation, race conditions, or deadlocks.

---

### 2. **What is the difference between a UI thread and a background thread?**

| **Aspect**          | **UI Thread**                                                | **Background Thread**                                      |
|----------------------|-------------------------------------------------------------|-----------------------------------------------------------|
| **Purpose**          | Handles UI rendering and user interactions.                 | Performs heavy or long-running tasks.                     |
| **Examples**         | Button clicks, screen updates, animations.                  | Network requests, database queries, file I/O.             |
| **Performance**      | Must remain responsive to avoid ANR errors.                 | Operates independently of the UI to avoid blocking it.     |
| **Interaction**      | Directly interacts with UI elements.                        | Cannot directly update UI; must use mechanisms like `Handler` or `LiveData`. |
| **Lifecycle Awareness** | Automatically tied to the app's lifecycle.                 | Requires manual management and cleanup.                   |

---

### 3. **Why should network operations not be performed on the main thread?**
Network operations are inherently slow and unpredictable due to factors like latency, bandwidth, or server response times. Performing these operations on the main thread can cause:
1. **UI Freezing**: The app becomes unresponsive while waiting for the network call to complete.
2. **Application Not Responding (ANR)**: If the operation takes longer than 5 seconds, Android triggers an ANR, leading to a poor user experience and potential app crashes.
3. **Bad User Experience**: Users expect snappy and responsive apps, so blocking the UI thread with network calls violates this expectation.

Instead, network operations should be executed on a background thread using tools like `AsyncTask`, `Thread`, or modern approaches like **Kotlin Coroutines** or **WorkManager**.

---

### 4. **What is an AsyncTask, and why is it discouraged?**
#### **AsyncTask**:
- An `AsyncTask` is a class provided by Android to perform background operations and publish results on the UI thread without directly managing threads.
- It simplifies threading by providing methods like `doInBackground()` for background tasks and `onPostExecute()` for updating the UI.

#### **Why is it discouraged?**
1. **Memory Leaks**: AsyncTask holds a reference to the enclosing class (like an Activity). If the task continues running after the Activity is destroyed, it can cause memory leaks.
2. **Lifecycle Mismatch**: It doesn’t handle the lifecycle of Activities or Fragments well, leading to crashes if the Activity is destroyed while the task is running.
3. **Limited Thread Pool**: AsyncTasks use a fixed thread pool by default, which can cause bottlenecks if too many tasks are executed simultaneously.
4. **Deprecated**: AsyncTask is officially deprecated as of Android 11 (API level 30) in favor of more modern and efficient solutions like Kotlin Coroutines.

---

### 5. **What are Kotlin Coroutines, and how do they improve background tasks?**
#### **Kotlin Coroutines**:
- Kotlin Coroutines are a modern concurrency framework designed to simplify asynchronous programming. They enable developers to write asynchronous code in a sequential, readable style.
- Coroutines run on a lightweight, cooperative threading model, allowing you to launch thousands of background tasks without the overhead of traditional threads.

#### **How They Improve Background Tasks**:
1. **Structured Concurrency**: Coroutines ensure that tasks are tied to a specific scope, such as a `ViewModel` or `Lifecycle`, so they are automatically canceled when the scope is destroyed.
2. **Simplified Syntax**: Using `suspend` functions, developers can write asynchronous code that looks and behaves like synchronous code.
3. **Thread Management**: Coroutines handle thread switching seamlessly using dispatchers like:
   - `Dispatchers.Main`: For UI tasks.
   - `Dispatchers.IO`: For intensive I/O operations like network requests or database queries.
   - `Dispatchers.Default`: For CPU-intensive tasks.
4. **Efficiency**: Coroutines are lightweight, enabling thousands of them to run concurrently without causing performance issues.
5. **Lifecycle Awareness**: Coroutines integrate with Android's lifecycle-aware components, ensuring tasks are canceled when no longer needed.

#### **Example**:
Here is an example of using Kotlin Coroutines for a network request:
```kotlin
import kotlinx.coroutines.*

fun fetchData() {
    // Start a coroutine on the Main thread (UI thread)
    CoroutineScope(Dispatchers.Main).launch {
        try {
            // Switch to a background thread for the network call
            val result = withContext(Dispatchers.IO) {
                performNetworkRequest()
            }
            // Back on the UI thread to update the UI
            updateUI(result)
        } catch (e: Exception) {
            showError(e.message)
        }
    }
}

suspend fun performNetworkRequest(): String {
    // Simulate a network call
    delay(2000)
    return "Network Response"
}
```

---



7. Jetpack Components
---

### **1. What is ViewModel, and why is it used?**

#### **What is ViewModel?**
The **ViewModel** is a class provided by Android Jetpack's Architecture Components. It is designed to store and manage UI-related data in a way that survives configuration changes (e.g., screen rotations). This avoids the need to reload data when the screen is recreated.

#### **Why is it used?**
1. **Data Persistence Across Configuration Changes**: When an Activity or Fragment is recreated (e.g., during a screen rotation), the ViewModel retains its data, preventing unnecessary data reloads or loss.
2. **Lifecycle Awareness**: The ViewModel is tied to the lifecycle of its owner (e.g., Activity or Fragment) and is automatically cleared when the lifecycle is permanently destroyed.
3. **Separation of Concerns**: It separates UI logic from business logic, promoting a clean architecture where the ViewModel handles data processing and exposes it to the UI.
4. **Optimization**: Avoids unnecessary calls to data sources like databases or APIs by caching the data for the UI.

#### **Example Usage**:
1. **Defining a ViewModel**:
```kotlin
class MyViewModel : ViewModel() {
    val userName = MutableLiveData<String>()
    
    fun setUserName(name: String) {
        userName.value = name
    }
}
```

2. **Using it in an Activity**:
```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var viewModel: MyViewModel
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // Initializing ViewModel
        viewModel = ViewModelProvider(this).get(MyViewModel::class.java)
        
        // Observing LiveData
        viewModel.userName.observe(this) { name ->
            // Update UI with the new name
            textView.text = name
        }
        
        // Setting data in ViewModel
        viewModel.setUserName("John Doe")
    }
}
```

---

### **2. What is LiveData, and how does it work?**

#### **What is LiveData?**
LiveData is a lifecycle-aware, observable data holder provided by Android Jetpack. It is designed to store and notify UI components of data changes while respecting their lifecycle states.

#### **How does it work?**
1. **Lifecycle Awareness**: LiveData ensures that updates are delivered only to active observers (those in the STARTED or RESUMED lifecycle states).
2. **Observer Pattern**: Observers (like Activities or Fragments) subscribe to LiveData and are notified whenever the data changes.
3. **Automatic Cleanup**: Observers are automatically removed when their lifecycle owner (Activity/Fragment) is destroyed.

#### **Example Workflow**:
1. **Define LiveData in ViewModel**:
```kotlin
class MyViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> get() = _data

    fun updateData(newData: String) {
        _data.value = newData
    }
}
```

2. **Observe LiveData in the UI Layer**:
```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var viewModel: MyViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize ViewModel
        viewModel = ViewModelProvider(this).get(MyViewModel::class.java)

        // Observe LiveData
        viewModel.data.observe(this) { updatedData ->
            // Update UI
            textView.text = updatedData
        }

        // Update LiveData
        viewModel.updateData("Hello, LiveData!")
    }
}
```

---

### **3. What is Navigation Component, and how does it simplify navigation?**

#### **What is Navigation Component?**
The Navigation Component is part of Android Jetpack and provides a framework for managing app navigation. It supports navigation between fragments, activities, and deep linking.

#### **How does it simplify navigation?**
1. **Centralized Navigation**: Navigation is defined in a single XML file (`nav_graph.xml`), providing a clear and visual overview of all navigation paths.
2. **Type-Safe Arguments**: Allows you to pass data between destinations in a type-safe manner using `SafeArgs`.
3. **Automatic Back Stack Management**: Automatically handles the back stack, reducing the need to manually write fragment transactions.
4. **Deep Linking Support**: Makes it easier to handle deep links that navigate users to specific destinations within the app.

#### **Example**:
1. **Define Navigation Graph** (`nav_graph.xml`):
```xml
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    app:startDestination="@id/homeFragment">

    <fragment
        android:id="@+id/homeFragment"
        android:name="com.example.HomeFragment">
        <action
            android:id="@+id/action_home_to_detail"
            app:destination="@id/detailFragment" />
    </fragment>

    <fragment
        android:id="@+id/detailFragment"
        android:name="com.example.DetailFragment" />
</navigation>
```

2. **Navigate Between Fragments**:
```kotlin
findNavController().navigate(R.id.action_home_to_detail)
```

---

### **4. What is WorkManager, and when should it be used?**

#### **What is WorkManager?**
WorkManager is a Jetpack library for scheduling and managing deferrable, asynchronous tasks. It ensures the execution of tasks even if the app is closed, the device restarts, or the app is killed by the system.

#### **When should it be used?**
1. **Deferrable Tasks**: Tasks that don't need to execute immediately, such as sending logs, syncing data, or uploading files.
2. **Guaranteed Execution**: When tasks must be completed regardless of app state or system conditions.
3. **Flexible Constraints**: When tasks need to run under specific conditions, such as network availability or device charging.

#### **Example**:
1. **Define a Worker**:
```kotlin
class MyWorker(context: Context, params: WorkerParameters) : Worker(context, params) {
    override fun doWork(): Result {
        // Perform background task
        return Result.success()
    }
}
```

2. **Schedule Work**:
```kotlin
val workRequest = OneTimeWorkRequestBuilder<MyWorker>().build()
WorkManager.getInstance(context).enqueue(workRequest)
```

---

### **5. What is the difference between DataBinding and ViewBinding?**

| **Aspect**             | **DataBinding**                                         | **ViewBinding**                                      |
|-------------------------|--------------------------------------------------------|-----------------------------------------------------|
| **Purpose**             | Binds XML layouts to data directly, enabling two-way binding. | Simplifies binding views to layout files.           |
| **Complexity**          | More complex and powerful; requires additional setup.  | Simpler and faster to implement.                   |
| **Two-Way Binding**     | Supports two-way data binding using `@={}` syntax.     | Does not support two-way data binding.             |
| **Generated Classes**   | Generates binding classes with data-binding logic.     | Generates classes for accessing views directly.     |
| **Use Case**            | Preferred for complex UIs with direct data binding to layouts. | Preferred for straightforward view binding.         |

#### **Example of ViewBinding**:
1. **Enable ViewBinding in `build.gradle`**:
```gradle
android {
    viewBinding {
        enabled = true
    }
}
```

2. **Access Views**:
```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
        
        // Access views
        binding.textView.text = "Hello, ViewBinding!"
    }
}
```

#### **Example of DataBinding**:
1. **Enable DataBinding in `build.gradle`**:
```gradle
android {
    dataBinding {
        enabled = true
    }
}
```

2. **Bind Data**:
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android">
    <data>
        <variable
            name="viewModel"
            type="com.example.MyViewModel" />
    </data>
    <TextView
        android:text="@{viewModel.userName}" />
</layout>
```

---




8. Firebase & Notifications
---

### **1. What is Firebase, and how can it be used in an Android app?**

#### **What is Firebase?**
Firebase is a comprehensive platform developed by Google for building mobile and web applications. It provides a suite of backend services and tools, allowing developers to focus on creating apps without worrying about server management, database setup, or infrastructure.

#### **Key Features of Firebase:**
1. **Authentication**: Simplifies user authentication using email/password, phone numbers, or third-party providers like Google, Facebook, etc.
2. **Realtime Database**: A NoSQL cloud database that syncs data across clients in real-time.
3. **Cloud Firestore**: A flexible and scalable NoSQL database for modern apps.
4. **Cloud Messaging (FCM)**: For sending push notifications to devices.
5. **Hosting**: For deploying web apps.
6. **Crashlytics**: Real-time crash reporting and analytics.
7. **Analytics**: Provides insights into app usage and user behavior.
8. **Remote Config**: Dynamically change app behavior and appearance without publishing updates.

#### **How can it be used in an Android app?**
Firebase can be used to:
1. Enable easy user authentication.
2. Provide real-time data synchronization for chat apps, live feeds, etc.
3. Send push notifications (e.g., promotional offers, updates).
4. Monitor app performance and crashes.
5. Store files like images, videos, or documents using Cloud Storage.

#### **Steps to Add Firebase to an Android App:**
1. **Set up a Firebase Project**:
   - Go to the [Firebase Console](https://console.firebase.google.com).
   - Create a new project and register your Android app by entering its package name.
   
2. **Add the Firebase SDK**:
   - Download the `google-services.json` file from the Firebase Console.
   - Place it in the `app/` directory of your Android project.
   
3. **Add Dependencies**:
   - Update the `build.gradle` files:
     ```groovy
     // In the project-level build.gradle
     dependencies {
         classpath 'com.google.gms:google-services:4.3.15'
     }

     // In the app-level build.gradle
     dependencies {
         implementation platform('com.google.firebase:firebase-bom:32.1.1') // Firebase BOM
         implementation 'com.google.firebase:firebase-analytics' // Example service
     }
     apply plugin: 'com.google.gms.google-services'
     ```

4. **Initialize Firebase**:
   Firebase is initialized automatically when you add the `google-services.json` file and apply the Google Services plugin.

---

### **2. How do you integrate Firebase Authentication into an Android app?**

#### **What is Firebase Authentication?**
Firebase Authentication offers a secure way to authenticate users in your app using various methods like:
- Email and Password
- Phone Authentication
- Third-party providers (Google, Facebook, Twitter, etc.)
- Anonymous Login

#### **Steps to Integrate Firebase Authentication:**
1. **Set Up Firebase Authentication**:
   - In the Firebase Console, go to the "Authentication" section and enable the desired sign-in methods (e.g., Email/Password, Google, etc.).

2. **Add Authentication Dependencies**:
   Add the Firebase Authentication library in your `build.gradle` file:
   ```groovy
   implementation 'com.google.firebase:firebase-auth'
   ```

3. **Authenticate a User**:
   - **Email/Password Authentication**:
     ```kotlin
     val auth = FirebaseAuth.getInstance()

     // Sign up a new user
     auth.createUserWithEmailAndPassword(email, password)
         .addOnCompleteListener { task ->
             if (task.isSuccessful) {
                 val user = auth.currentUser
                 Log.d("Auth", "User created: ${user?.email}")
             } else {
                 Log.e("Auth", "Error: ${task.exception?.message}")
             }
         }

     // Sign in an existing user
     auth.signInWithEmailAndPassword(email, password)
         .addOnCompleteListener { task ->
             if (task.isSuccessful) {
                 val user = auth.currentUser
                 Log.d("Auth", "User signed in: ${user?.email}")
             } else {
                 Log.e("Auth", "Error: ${task.exception?.message}")
             }
         }
     ```

4. **Handle Session Management**:
   Firebase automatically manages user sessions. Use `FirebaseAuth.getInstance().currentUser` to check if a user is logged in.

5. **Sign Out**:
   ```kotlin
   FirebaseAuth.getInstance().signOut()
   ```

---

### **3. What is Firebase Realtime Database, and how does it work?**

#### **What is Firebase Realtime Database?**
The Firebase Realtime Database is a NoSQL cloud database that stores and syncs data in real-time across all connected clients. Data is stored in JSON format and updated in real-time, making it ideal for applications like chat apps, collaborative tools, or live feeds.

#### **How Does It Work?**
1. **Data Storage**: Data is stored as a hierarchical JSON tree.
2. **Real-Time Sync**: Changes to the database are propagated to all connected clients in real-time.
3. **Offline Support**: Data is cached locally, and changes are synchronized when the device reconnects to the internet.
4. **Security Rules**: Custom rules can be defined to control read/write access to data.

#### **Steps to Use Firebase Realtime Database**:
1. **Add Dependencies**:
   ```groovy
   implementation 'com.google.firebase:firebase-database'
   ```

2. **Access the Database**:
   ```kotlin
   val database = FirebaseDatabase.getInstance()
   val myRef = database.getReference("message")

   // Write data to the database
   myRef.setValue("Hello, World!")

   // Read data from the database
   myRef.addValueEventListener(object : ValueEventListener {
       override fun onDataChange(dataSnapshot: DataSnapshot) {
           val value = dataSnapshot.getValue(String::class.java)
           Log.d("RealtimeDatabase", "Value is: $value")
       }

       override fun onCancelled(error: DatabaseError) {
           Log.e("RealtimeDatabase", "Failed to read value.", error.toException())
       }
   })
   ```

---

### **4. How do you send push notifications using Firebase Cloud Messaging (FCM)?**

#### **What is Firebase Cloud Messaging (FCM)?**
FCM is a service provided by Firebase for sending push notifications to devices. It supports both "notification messages" (handled by the system tray) and "data messages" (handled by the app).

#### **Steps to Send Push Notifications Using FCM**:
1. **Set Up FCM**:
   - In the Firebase Console, go to the "Cloud Messaging" section and enable FCM.

2. **Add FCM Dependencies**:
   ```groovy
   implementation 'com.google.firebase:firebase-messaging'
   ```

3. **Receive Notifications in the App**:
   - Create a service that extends `FirebaseMessagingService`:
     ```kotlin
     class MyFirebaseMessagingService : FirebaseMessagingService() {
         override fun onMessageReceived(remoteMessage: RemoteMessage) {
             // Handle the received message
             Log.d("FCM", "Message received: ${remoteMessage.data}")
         }

         override fun onNewToken(token: String) {
             Log.d("FCM", "New token: $token")
         }
     }
     ```

   - Register the service in `AndroidManifest.xml`:
     ```xml
     <service android:name=".MyFirebaseMessagingService"
         android:exported="true">
         <intent-filter>
             <action android:name="com.google.firebase.MESSAGING_EVENT" />
         </intent-filter>
     </service>
     ```

4. **Send Notifications**:
   - Go to the Firebase Console and use the "Cloud Messaging" section to compose and send a notification.
   - Alternatively, send notifications programmatically via Firebase Admin SDK or REST API.

---


9. Permissions & Security
### **1. How do you request permissions in Android (e.g., camera, location)?**

In Android, permissions are required to access sensitive features like the camera, location, contacts, etc. Depending on the permission type, you may need to declare it in the app's `AndroidManifest.xml` and request it at runtime.

#### **Steps for Requesting Permissions:**
1. **Declare Permissions in `AndroidManifest.xml`:**
   Permissions must be declared in the manifest file for both normal and dangerous permissions.
   ```xml
   <manifest xmlns:android="http://schemas.android.com/apk/res/android">
       <uses-permission android:name="android.permission.CAMERA" />
       <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
   </manifest>
   ```

2. **Check Permission at Runtime:**
   Before using a feature, check if the app already has the necessary permission.
   ```kotlin
   if (ContextCompat.checkSelfPermission(this, Manifest.permission.CAMERA) != PackageManager.PERMISSION_GRANTED) {
       // Permission is not granted
   }
   ```

3. **Request Permission at Runtime:**
   If the permission is not granted, request it at runtime.
   ```kotlin
   ActivityCompat.requestPermissions(this, arrayOf(Manifest.permission.CAMERA), REQUEST_CODE_CAMERA)
   ```

4. **Handle the Permission Result:**
   Override the `onRequestPermissionsResult` method to handle the user's response.
   ```kotlin
   override fun onRequestPermissionsResult(requestCode: Int, permissions: Array<out String>, grantResults: IntArray) {
       when (requestCode) {
           REQUEST_CODE_CAMERA -> {
               if ((grantResults.isNotEmpty() && grantResults[0] == PackageManager.PERMISSION_GRANTED)) {
                   // Permission granted
               } else {
                   // Permission denied
               }
           }
       }
   }
   ```

---

### **2. What is the difference between runtime permissions and manifest permissions?**

| **Aspect**                  | **Runtime Permissions**                                           | **Manifest Permissions**                                      |
|-----------------------------|------------------------------------------------------------------|-------------------------------------------------------------|
| **Definition**              | Dangerous permissions that must be explicitly granted by the user at runtime. | Normal permissions that are granted automatically when the app is installed. |
| **Examples**                | `CAMERA`, `ACCESS_FINE_LOCATION`, `READ_CONTACTS`.              | `INTERNET`, `ACCESS_NETWORK_STATE`.                        |
| **User Prompt**             | Prompts the user to grant or deny the permission during runtime. | No runtime prompt; permissions are automatically granted.  |
| **Purpose**                 | Protect user-sensitive data or features.                        | Enable basic app functionality without user intervention.  |
| **Introduced In**           | Runtime permissions were introduced in Android 6.0 (API level 23). | Manifest-level permissions existed prior to Android 6.0.  |

---

### **3. How do you handle denied permissions in Android?**

When a user denies a permission request, you should handle it gracefully to avoid breaking the app's functionality. Here's how:

#### **Steps to Handle Denied Permissions:**
1. **Explain the Reason for the Permission:**
   Use `shouldShowRequestPermissionRationale()` to check if you should provide an explanation before re-requesting the permission.
   ```kotlin
   if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.CAMERA)) {
       // Show an explanation to the user
   } else {
       // Permission denied permanently
   }
   ```

2. **Handle Permanent Denial:**
   If the user selects "Don't ask again," redirect them to the app's settings to manually enable the permission.
   ```kotlin
   val intent = Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS)
   val uri = Uri.fromParts("package", packageName, null)
   intent.data = uri
   startActivity(intent)
   ```

3. **Fallback Functionality:**
   Provide alternative functionality if the permission is not critical. For example, use a default image instead of accessing the camera.

#### **Best Practices:**
- Always explain why the permission is needed to build user trust.
- Avoid repeatedly requesting denied permissions, as this can frustrate users.
- Use permissions sparingly to avoid overwhelming users with requests.

---

### **4. What is ProGuard, and how does it help in security?**

#### **What is ProGuard?**
ProGuard is a tool included in the Android build system that optimizes, obfuscates, and shrinks your app code. It removes unused code, renames classes and methods to meaningless names, and makes it harder for attackers to reverse-engineer your app.

#### **How Does ProGuard Work?**
1. **Code Shrinking**: Removes unused code and libraries to reduce the APK size.
2. **Obfuscation**: Renames classes, methods, and variables to obscure their original purpose (e.g., `UserManager` becomes `a`).
3. **Optimization**: Simplifies and optimizes bytecode for better runtime performance.
4. **Prevention of Reverse Engineering**: Makes it challenging for attackers to decompile and understand the app's logic.

#### **How to Enable ProGuard:**
1. **Enable ProGuard in `build.gradle`:**
   ```gradle
   buildTypes {
       release {
           minifyEnabled true
           proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
       }
   }
   ```

2. **Define ProGuard Rules (`proguard-rules.pro`):**
   You can customize ProGuard behavior using rules.
   ```pro
   # Keep class names for model classes used in serialization
   -keep class com.example.models.** { *; }

   # Keep all annotations
   -keepattributes *Annotation*
   ```

#### **Benefits of ProGuard:**
- Protects intellectual property by obfuscating code.
- Reduces the APK size, leading to faster downloads and better performance.
- Hinders reverse engineering, protecting sensitive logic and keys.

---

### **5. How do you store sensitive data securely in an Android app?**

#### **Best Practices for Storing Sensitive Data:**

1. **Use Encrypted Storage:**
   Use the [Android Encrypted SharedPreferences](https://developer.android.com/topic/security/data#using-encryptedsharedpreferences) or encrypt files before saving them.
   ```kotlin
   val masterKey = MasterKey.Builder(context)
       .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
       .build()

   val sharedPreferences = EncryptedSharedPreferences.create(
       context,
       "secure_prefs",
       masterKey,
       EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
       EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
   )

   sharedPreferences.edit().putString("api_key", "your_api_key").apply()
   ```

2. **Secure API Keys and Secrets:**
   - Do not hardcode API keys or secrets in your app.
   - Use the Android **Keystore System** to securely store cryptographic keys.
   - Consider using environment variables and retrieving secrets from a secure server.

3. **Use the Keystore System:**
   The Keystore System provides a secure container to store cryptographic keys and ensures they are not exposed to the app's process memory.
   ```kotlin
   val keyGenerator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES, "AndroidKeyStore")
   keyGenerator.init(
       KeyGenParameterSpec.Builder(
           "MyKeyAlias",
           KeyProperties.PURPOSE_ENCRYPT or KeyProperties.PURPOSE_DECRYPT
       ).setBlockModes(KeyProperties.BLOCK_MODE_GCM)
        .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_NONE)
        .build()
   )
   val key = keyGenerator.generateKey()
   ```

4. **Avoid Using External Storage for Sensitive Data:**
   External storage is not secure and can be accessed by other apps. Always use internal storage or the app's private directory.

5. **Use HTTPS for Network Communication:**
   Always use HTTPS to encrypt data in transit. Enable SSL pinning to prevent man-in-the-middle (MITM) attacks.

6. **Leverage Security Libraries:**
   Use libraries like [SQLCipher](https://www.zetetic.net/sqlcipher/) to encrypt SQLite databases.

7. **Regularly Update Dependencies:**
   Keep your app's dependencies and libraries up-to-date to avoid vulnerabilities in third-party code.

#### **Things to Avoid:**
- Hardcoding sensitive information like passwords or API keys in the app code.
- Storing sensitive data in plain text.
- Using weak encryption algorithms or self-implemented encryption logic.

---


10. Debugging & Testing
### **1. How do you debug an Android application using Logcat?**

#### **What is Logcat?**
Logcat is a command-line tool and a debugging window in Android Studio that shows real-time logs of system messages. These messages include:
- Logging messages from your app (`Log.d`, `Log.e`, etc.).
- Stack traces when exceptions occur.
- Garbage collection events.
- System events like device restarts, network activity, etc.

#### **How to Use Logcat for Debugging?**
1. **Open Logcat in Android Studio**:
   - Go to **View > Tool Windows > Logcat** or press `Alt+6` (on Windows/Linux) or `Command+6` (on macOS).

2. **Filter Logs**:
   - **Search Bar**: Use the search bar to filter logs by keywords like `TAG` or specific text.
   - **Log Levels**: Filter logs by severity levels:
     - **Verbose**: Shows all logs.
     - **Debug**: For debugging information.
     - **Info**: General information logs.
     - **Warn**: Potential issues.
     - **Error**: Errors that need attention.
     - **Assert**: Serious issues that should not occur under normal operations.

3. **Tagging Logs**:
   - Use `Log` class methods to generate logs in your app code:
     ```kotlin
     Log.v("TAG", "Verbose log")
     Log.d("TAG", "Debug log")
     Log.i("TAG", "Info log")
     Log.w("TAG", "Warning log")
     Log.e("TAG", "Error log")
     ```

4. **Analyze Exceptions**:
   - When an exception occurs, Logcat will show the stack trace. Use the stack trace to identify the source of the issue and pinpoint the problematic line of code.

5. **Clear Logs**:
   - Use the trash icon in the Logcat window to clear logs for better readability during debugging.

6. **Advanced Filters**:
   - You can create custom filters based on package names, tags, or log levels to focus on specific logs from your app.

7. **Real Device Debugging**:
   - To debug on a physical device, connect it via USB, enable USB Debugging on the device, and select it from the device dropdown in Logcat.

---

### **2. What is Logcat, and how do you use it for debugging?**

#### **What is Logcat?**
Logcat is a tool in Android Studio that captures and displays logs generated by the Android system and apps. It's an essential tool for debugging and troubleshooting.

#### **How to Use Logcat for Debugging?**
1. Add log statements in your code using the `Log` class. For example:
   ```kotlin
   Log.d("MainActivity", "Button clicked")
   ```
   This will generate a log message that can be viewed in Logcat.

2. Open Logcat in Android Studio and filter logs by:
   - **Tag**: To view only logs with a specific tag.
   - **PID** (Process ID): To view logs from a specific process.
   - **Log Level**: To filter by severity (e.g., Debug, Error).

3. Use logs to trace the execution flow of your app and identify issues like null pointer exceptions, crashes, or unexpected behaviors.

4. Analyze stack traces in Logcat to debug runtime errors. For example:
   ```
   java.lang.NullPointerException: Attempt to invoke virtual method 'int java.lang.String.length()' on a null object reference
   at com.example.MainActivity.onCreate(MainActivity.java:25)
   ```
   This stack trace indicates a `NullPointerException` at line 25 in `MainActivity`.

---

### **3. How do you set breakpoints in Android Studio?**

#### **What are Breakpoints?**
Breakpoints are markers set in your code to pause execution at specific points during debugging. They allow you to inspect variables, evaluate expressions, and step through code line by line.

#### **Steps to Set Breakpoints**:
1. Open the file in Android Studio where you want to debug.
2. Click in the left margin next to the line of code where you want to set a breakpoint. A red dot will appear, indicating the breakpoint.
3. Start the app in **Debug Mode**:
   - Click the green bug icon (`Debug`) instead of the normal run button.
4. When the breakpoint is hit, the debugger will pause execution, and you can:
   - **Inspect Variables**: View the values of variables in the `Variables` pane.
   - **Step Over**: Execute the current line of code and proceed to the next (`F8`).
   - **Step Into**: Enter the method being called on the current line (`F7`).
   - **Step Out**: Exit the current method and return to the caller (`Shift+F8`).
5. To remove a breakpoint, click the red dot again.

---

### **4. What is Unit Testing, and how do you write a basic test case?**

#### **What is Unit Testing?**
Unit testing involves testing individual components (units) of an application in isolation to ensure they work as expected. In Android, you can write unit tests using frameworks like **JUnit**.

#### **Steps to Write a Basic Test Case**:
1. **Add Testing Dependencies**:
   Add the following dependencies in your `build.gradle` file:
   ```gradle
   testImplementation 'junit:junit:4.13.2'
   testImplementation 'org.mockito:mockito-core:4.11.0'
   ```

2. **Create a Test Class**:
   - Test classes are usually placed in the `src/test/java` directory.
   ```kotlin
   class CalculatorTest {
       @Test
       fun addition_isCorrect() {
           val result = Calculator.add(2, 3)
           assertEquals(5, result)
       }
   }
   ```

3. **Run the Tests**:
   - Right-click the test class or method and select **Run**.
   - Android Studio will display the test results in the Run pane.

#### **Example of a Calculator Class and Unit Test**:
1. **Calculator Class**:
   ```kotlin
   object Calculator {
       fun add(a: Int, b: Int): Int {
           return a + b
       }
   }
   ```

2. **Unit Test**:
   ```kotlin
   class CalculatorTest {
       @Test
       fun addition_isCorrect() {
           val result = Calculator.add(2, 3)
           assertEquals(5, result)
       }
   }
   ```

---

### **5. What is Espresso, and how does it help in UI testing?**

#### **What is Espresso?**
Espresso is a UI testing framework provided by Android for writing automated tests to verify the behavior of your app's user interface.

#### **Key Features:**
1. **Simplicity**: Provides concise and readable APIs for writing UI tests.
2. **Synchronization**: Automatically waits for UI elements to become idle before interacting with them, reducing flaky tests.
3. **Assertions**: Verifies the state of UI elements (e.g., text, visibility).

#### **How Does Espresso Help in UI Testing?**
1. Automates repetitive UI testing tasks, ensuring consistency.
2. Detects UI bugs by verifying the correctness of user interactions.
3. Speeds up regression testing by running tests automatically for every new build.

#### **Steps to Write an Espresso Test:**
1. **Add Espresso Dependencies**:
   Add the following dependencies in your `build.gradle` file:
   ```gradle
   androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
   androidTestImplementation 'androidx.test.ext:junit:1.1.5'
   ```

2. **Write a Test Case**:
   - Espresso tests are placed in the `src/androidTest/java` directory.
   ```kotlin
   @RunWith(AndroidJUnit4::class)
   class MainActivityTest {
       @Test
       fun testButtonClick() {
           // Launch the activity
           ActivityScenario.launch(MainActivity::class.java)

           // Perform click action on button
           onView(withId(R.id.button)).perform(click())

           // Check if the text view displays the correct text
           onView(withId(R.id.textView)).check(matches(withText("Hello, World!")))
       }
   }
   ```

3. **Run the Test**:
   - Right-click the test class or method and select **Run**.
   - Espresso will simulate user actions and verify the UI behavior.

#### **Example of UI Test:**
1. **MainActivity Layout (XML)**:
   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:orientation="vertical">

       <Button
           android:id="@+id/button"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="Click Me" />

       <TextView
           android:id="@+id/textView"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="Default Text" />
   </LinearLayout>
   ```

2. **MainActivity Code**:
   ```kotlin
   class MainActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)

           val button = findViewById<Button>(R.id.button)
           val textView = findViewById<TextView>(R.id.textView)

           button.setOnClickListener {
               textView.text = "Hello, World!"
           }
       }
   }
   ```

3. **Espresso Test**:
   ```kotlin
   @RunWith(AndroidJUnit4::class)
   class MainActivityTest {
       @Test
       fun testButtonClick() {
           ActivityScenario.launch(MainActivity::class.java)
           onView(withId(R.id.button)).perform(click())
           onView(withId(R.id.textView)).check(matches(withText("Hello, World!")))
       }
   }
   ```

---





12. Activity & Fragment Lifecycle
---

### **1. What are the different states of an Activity lifecycle?**

The Activity lifecycle in Android describes the states an Activity goes through from creation to destruction. Each state is managed by lifecycle callback methods:

#### **Activity Lifecycle States and Methods**
1. **Created (`onCreate`)**
   - **State**: The Activity is being created.
   - **Callback**: `onCreate(Bundle savedInstanceState)`
   - **Purpose**:
     - Initialize components like views, variables, or services.
     - Set up the UI using `setContentView()`.
     - Restore saved state using the `savedInstanceState` parameter (if applicable).
   - **Example**:
     ```java
     @Override
     protected void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);
         setContentView(R.layout.activity_main);
     }
     ```

2. **Started (`onStart`)**
   - **State**: The Activity is becoming visible to the user.
   - **Callback**: `onStart()`
   - **Purpose**:
     - Prepare the UI for interaction but do not yet engage the user.
     - Start animations or update UI components.
   - **Example**:
     ```java
     @Override
     protected void onStart() {
         super.onStart();
         // Activity is now visible
     }
     ```

3. **Resumed (`onResume`)**
   - **State**: The Activity is in the foreground and interacting with the user.
   - **Callback**: `onResume()`
   - **Purpose**:
     - Resume tasks that were paused (e.g., start sensors, resume animations).
   - **Example**:
     ```java
     @Override
     protected void onResume() {
         super.onResume();
         // Activity is now in the foreground
     }
     ```

4. **Paused (`onPause`)**
   - **State**: The Activity is partially obscured (e.g., another Activity appears in front, but this one is still visible in the background).
   - **Callback**: `onPause()`
   - **Purpose**:
     - Pause ongoing tasks (e.g., animations, video playback).
     - Save transient UI state (e.g., scroll position).
   - **Example**:
     ```java
     @Override
     protected void onPause() {
         super.onPause();
         // Pause resources or tasks
     }
     ```

5. **Stopped (`onStop`)**
   - **State**: The Activity is completely hidden from the user.
   - **Callback**: `onStop()`
   - **Purpose**:
     - Release resources that are not needed when the activity is not visible (e.g., stop camera previews, unregister listeners).
   - **Example**:
     ```java
     @Override
     protected void onStop() {
         super.onStop();
         // Activity is now hidden
     }
     ```

6. **Destroyed (`onDestroy`)**
   - **State**: The Activity is being destroyed and removed from memory.
   - **Callback**: `onDestroy()`
   - **Purpose**:
     - Clean up resources like threads, listeners, or references to avoid memory leaks.
   - **Example**:
     ```java
     @Override
     protected void onDestroy() {
         super.onDestroy();
         // Cleanup logic
     }
     ```

---

### **2. What happens when you rotate the screen in Android?**

When the screen is rotated (e.g., from portrait to landscape):
1. **Configuration Change**:
   - A screen rotation triggers a **configuration change** (e.g., orientation change).
   - The system destroys the existing Activity instance and creates a new one.

2. **Lifecycle Methods Called**:
   - The Activity goes through the following lifecycle methods:
     - `onPause()` → `onStop()` → `onDestroy()`
     - `onCreate()` → `onStart()` → `onResume()` (for the new instance).

3. **Why is the Activity Recreated?**
   - The recreation ensures that the UI is redrawn to match the new orientation and resources (e.g., different layouts for `res/layout` and `res/layout-land`).

4. **Handling State During Rotation**:
   - **Temporary State**: Use `onSaveInstanceState(Bundle outState)` to save the state.
   - **Restore State**: Use `onRestoreInstanceState(Bundle savedInstanceState)` or the `savedInstanceState` parameter in `onCreate()`.

#### **Example for Saving and Restoring State:**
```java
@Override
protected void onSaveInstanceState(Bundle outState) {
    super.onSaveInstanceState(outState);
    outState.putString("key", "value");
}

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    if (savedInstanceState != null) {
        String value = savedInstanceState.getString("key");
    }
}
```

5. **Preventing Activity Recreation**:
   - You can handle configuration changes manually by adding the following in the `AndroidManifest.xml` file:
     ```xml
     <activity android:name=".MainActivity"
         android:configChanges="orientation|screenSize" />
     ```
   - **Caution**: You will need to handle the UI changes manually in `onConfigurationChanged()`.

---

### **3. How do you save and restore UI state in Android?**

1. **Save UI State**:
   - Use `onSaveInstanceState(Bundle outState)` to save transient UI data like text input, scroll position, or selected items.
   - Example:
     ```java
     @Override
     protected void onSaveInstanceState(Bundle outState) {
         super.onSaveInstanceState(outState);
         outState.putString("text", editText.getText().toString());
     }
     ```

2. **Restore UI State**:
   - Restore the saved state in `onRestoreInstanceState(Bundle savedInstanceState)` or `onCreate(Bundle savedInstanceState)`.
   - Example:
     ```java
     @Override
     protected void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);
         setContentView(R.layout.activity_main);
         if (savedInstanceState != null) {
             String text = savedInstanceState.getString("text");
             editText.setText(text);
         }
     }
     ```

3. **Alternative: ViewModel**:
   - Use a `ViewModel` to store UI data that survives configuration changes.
   - Example:
     ```java
     class MyViewModel extends ViewModel {
         MutableLiveData<String> text = new MutableLiveData<>();
     }
     ```

---

### **4. What are the lifecycle methods of a Fragment?**

Fragments have their own lifecycle methods, intertwined with their hosting Activity's lifecycle.

#### **Fragment Lifecycle Stages:**
1. **Created**:
   - `onAttach(Context context)`: Called when the Fragment is associated with its host Activity.
   - `onCreate(Bundle savedInstanceState)`: Initialize Fragment-level resources (e.g., ViewModels).

2. **Created View**:
   - `onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)`: Inflate the Fragment's layout.
   - `onViewCreated(View view, Bundle savedInstanceState)`: Perform setup tasks like initializing views.

3. **Started**:
   - `onStart()`: Fragment is visible to the user.

4. **Resumed**:
   - `onResume()`: Fragment is actively visible and interacting with the user.

5. **Paused**:
   - `onPause()`: Fragment is partially visible (e.g., another Fragment appears on top).

6. **Stopped**:
   - `onStop()`: Fragment is completely hidden.

7. **Destroyed View**:
   - `onDestroyView()`: Cleanup resources tied to the Fragment's view hierarchy.

8. **Detached**:
   - `onDestroy()`: Cleanup Fragment-level resources.
   - `onDetach()`: Fragment is detached from its host Activity.

---

### **5. How do you replace one Fragment with another dynamically?**

Fragments can be replaced dynamically during runtime using the `FragmentManager` and `FragmentTransaction`.

#### **Steps to Replace a Fragment Dynamically:**
1. **Define a Container in the Layout**:
   - Create a container (e.g., `FrameLayout`) in your layout file to hold the Fragment.
   ```xml
   <FrameLayout
       android:id="@+id/fragment_container"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

2. **Add/Replace the Fragment**:
   - Use `FragmentManager` and `FragmentTransaction` to replace the Fragment.
   ```java
   Fragment fragment = new ExampleFragment();
   FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();
   transaction.replace(R.id.fragment_container, fragment);
   transaction.addToBackStack(null); // Optional: Add to back stack
   transaction.commit();
   ```

3. **Add to Back Stack**:
   - Use `addToBackStack()` to allow the user to navigate back to the previous Fragment using the back button.

4. **Example**:
   ```java
   public void showFragment() {
       ExampleFragment newFragment = new ExampleFragment();
       FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();

       // Replace the current fragment with the new one
       transaction.replace(R.id.fragment_container, newFragment);

       // Add to back stack so the user can navigate back
       transaction.addToBackStack(null);

       // Commit the transaction
       transaction.commit();
   }
   ```

5. **Handle Back Navigation**:
   - Override `onBackPressed()` in the Activity to handle Fragment back navigation if required.

---




13. UI Components & Customization

---

### **1. What is the difference between `match_parent` and `wrap_content`?**

#### **`match_parent`**
- **Definition**: The view expands to fill the entire space of its parent container.
- **Use Case**: When you want the view to take up all available space.
- **Example**:
  ```xml
  <Button
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:text="Match Parent" />
  ```
  - In this case, the button will take up the full width of the parent container but only as much height as needed to fit its content.

#### **`wrap_content`**
- **Definition**: The view resizes itself just enough to fit its content.
- **Use Case**: When you want the view to adjust its size based on its content.
- **Example**:
  ```xml
  <Button
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="Wrap Content" />
  ```
  - In this case, the button will be as wide and tall as its text content.

---

### **2. How do you change the background color of a Button programmatically?**

You can change the background color of a `Button` programmatically using the following code:

#### **Example**:
```java
Button myButton = findViewById(R.id.my_button);

// Change background color using a color resource
myButton.setBackgroundColor(ContextCompat.getColor(this, R.color.teal_200));

// Change background color using a hardcoded color
myButton.setBackgroundColor(Color.parseColor("#FF5733"));
```

- **`ContextCompat.getColor()`**: Retrieves a color from the `res/values/colors.xml` file.
- **`Color.parseColor()`**: Converts a hex color string into a color integer.

---

### **3. How do you create a custom Toast message in Android?**

A custom `Toast` can be created by inflating a custom layout and attaching it to a `Toast` instance.

#### **Steps to Create a Custom Toast**:
1. **Create a Custom Layout (`toast_layout.xml`)**:
   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:orientation="horizontal"
       android:background="@drawable/toast_background"
       android:padding="10dp">

       <ImageView
           android:layout_width="40dp"
           android:layout_height="40dp"
           android:src="@drawable/ic_info" />

       <TextView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="Custom Toast Message"
           android:textColor="#FFFFFF"
           android:paddingStart="10dp" />
   </LinearLayout>
   ```

2. **Inflate and Show the Custom Toast**:
   ```java
   LayoutInflater inflater = getLayoutInflater();
   View layout = inflater.inflate(R.layout.toast_layout, null);

   Toast toast = new Toast(getApplicationContext());
   toast.setDuration(Toast.LENGTH_LONG);
   toast.setView(layout);
   toast.show();
   ```

---

### **4. What is a Snackbar, and how does it differ from a Toast?**

#### **What is a Snackbar?**
- A Snackbar is a lightweight, transient message that appears at the bottom of the screen and can include an optional action (e.g., "Undo").
- It is part of the Material Design Components.

#### **Differences Between Snackbar and Toast**:

| **Feature**       | **Snackbar**                               | **Toast**                                  |
|-------------------|--------------------------------------------|-------------------------------------------|
| **Actions**       | Can include an action (e.g., button).      | No actions supported.                     |
| **Appearance**    | Appears at the bottom of the screen.       | Appears anywhere on the screen.           |
| **Duration**      | Shorter duration with dismiss option.      | Can only show for short or long periods.  |
| **Customization** | Supports better customization (color, etc.)| Limited customization options.            |

#### **Example of a Snackbar**:
```java
Snackbar.make(findViewById(android.R.id.content), "Snackbar Message", Snackbar.LENGTH_LONG)
        .setAction("Undo", new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Handle action
            }
        }).show();
```

---

### **5. How do you implement a ProgressBar in Android?**

#### **What is a ProgressBar?**
A `ProgressBar` is a visual indicator of the progress of a task, often used for loading screens or ongoing operations.

#### **Types**:
1. **Determinate ProgressBar**: Displays a specific progress value.
2. **Indeterminate ProgressBar**: Indicates an ongoing process without showing exact progress.

#### **Steps to Implement a ProgressBar**:

1. **Add ProgressBar in the XML Layout**:
   - **Indeterminate ProgressBar**:
     ```xml
     <ProgressBar
         android:id="@+id/indeterminateProgressBar"
         android:layout_width="wrap_content"
         android:layout_height="wrap_content"
         android:indeterminate="true" />
     ```

   - **Determinate ProgressBar**:
     ```xml
     <ProgressBar
         android:id="@+id/determinateProgressBar"
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:max="100"
         android:progress="50" />
     ```

2. **Access and Control ProgressBar in Java/Kotlin**:
   - **Indeterminate**:
     ```java
     ProgressBar indeterminateProgressBar = findViewById(R.id.indeterminateProgressBar);
     indeterminateProgressBar.setVisibility(View.VISIBLE); // Show ProgressBar
     indeterminateProgressBar.setVisibility(View.GONE);   // Hide ProgressBar
     ```

   - **Determinate**:
     ```java
     ProgressBar determinateProgressBar = findViewById(R.id.determinateProgressBar);
     determinateProgressBar.setProgress(75); // Set progress to 75%
     determinateProgressBar.setVisibility(View.VISIBLE); // Show ProgressBar
     ```

3. **Integration with a Background Task**:
   - Use `Handler` or `AsyncTask` to update the progress dynamically.

   **Example with Handler**:
   ```java
   ProgressBar progressBar = findViewById(R.id.determinateProgressBar);
   progressBar.setMax(100);

   Handler handler = new Handler();
   for (int i = 0; i <= 100; i++) {
       int progress = i;
       handler.postDelayed(() -> progressBar.setProgress(progress), i * 100);
   }
   ```

   **Example with Coroutines (Kotlin)**:
   ```kotlin
   val progressBar = findViewById<ProgressBar>(R.id.determinateProgressBar)
   progressBar.max = 100

   CoroutineScope(Dispatchers.Main).launch {
       for (progress in 0..100) {
           delay(100) // Simulate work
           progressBar.progress = progress
       }
   }
   ```

4. **Customizing the ProgressBar**:
   - Use `android:progressDrawable` to style the bar.
   - Example:
     ```xml
     <ProgressBar
         android:id="@+id/customProgressBar"
         android:layout_width="match_parent"
         android:layout_height="wrap_content"
         android:progressDrawable="@drawable/custom_progress" />
     ```

   - `custom_progress.xml` (Drawable):
     ```xml
     <layer-list xmlns:android="http://schemas.android.com/apk/res/android">
         <item android:id="@android:id/background" android:drawable="@android:color/darker_gray" />
         <item android:id="@android:id/progress" android:drawable="@android:color/holo_blue_light" />
     </layer-list>
     ```

---




14. Event Handling & User Interaction

---

### **1. How do you detect a long press on a Button?**

To detect a long press on a `Button`, you can use the `setOnLongClickListener` method.

#### **Example**:
```java
Button myButton = findViewById(R.id.my_button);
myButton.setOnLongClickListener(new View.OnLongClickListener() {
    @Override
    public boolean onLongClick(View v) {
        // Action to perform on long press
        Toast.makeText(getApplicationContext(), "Button Long Pressed!", Toast.LENGTH_SHORT).show();
        return true; // Return true to indicate the event is consumed
    }
});
```

- **Key Points**:
  - `onLongClick(View v)`: Triggered when the user presses and holds the button.
  - **Return Value**:
    - `true`: Consumes the event (prevents further processing).
    - `false`: Allows the event to propagate.

---

### **2. What is the difference between `setOnClickListener` and `setOnLongClickListener`?**

| **Aspect**               | **setOnClickListener**                           | **setOnLongClickListener**                      |
|--------------------------|------------------------------------------------|-----------------------------------------------|
| **Event Trigger**         | Triggered on a short press or tap.             | Triggered on a long press (held for a while). |
| **Use Case**              | Used for quick actions like opening a screen.  | Used for secondary actions like showing a menu. |
| **Listener Method**       | `onClick(View v)`                              | `onLongClick(View v)`                         |
| **Return Value**          | Does not return a value.                       | Returns `boolean` to indicate event handling. |
| **Event Propagation**     | Always consumed and stops propagation.         | Can propagate if `false` is returned.         |

---

### **3. How do you handle user input using EditText?**

To handle user input in an `EditText`, you can retrieve the text entered by the user using the `getText()` method.

#### **Example: Handling User Input**
```java
EditText editText = findViewById(R.id.edit_text);
Button submitButton = findViewById(R.id.submit_button);

submitButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        String userInput = editText.getText().toString(); // Get user input
        Toast.makeText(getApplicationContext(), "Input: " + userInput, Toast.LENGTH_SHORT).show();
    }
});
```

#### **Key Points**:
1. **Input Validation**:
   - Check if the input is empty or meets specific criteria.
   ```java
   if (userInput.isEmpty()) {
       editText.setError("Field cannot be empty");
   }
   ```

2. **Listening for Text Changes**:
   - Use `TextWatcher` to listen for real-time text changes.
   ```java
   editText.addTextChangedListener(new TextWatcher() {
       @Override
       public void beforeTextChanged(CharSequence s, int start, int count, int after) {}

       @Override
       public void onTextChanged(CharSequence s, int start, int before, int count) {
           // React to text changes
       }

       @Override
       public void afterTextChanged(Editable s) {
           // React after text changes
       }
   });
   ```

---

### **4. How do you create a custom Dialog in Android?**

A custom `Dialog` can be created by defining a custom layout and inflating it in a `Dialog` instance.

#### **Steps to Create a Custom Dialog**:

1. **Define a Custom Layout (`dialog_layout.xml`)**:
   ```xml
   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:orientation="vertical"
       android:padding="16dp">

       <TextView
           android:id="@+id/dialog_title"
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="Custom Dialog Title"
           android:textSize="18sp"
           android:textStyle="bold" />

       <EditText
           android:id="@+id/dialog_input"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:hint="Enter something" />

       <Button
           android:id="@+id/dialog_button"
           android:layout_width="match_parent"
           android:layout_height="wrap_content"
           android:text="Submit" />
   </LinearLayout>
   ```

2. **Inflate and Show the Dialog**:
   ```java
   Button showDialogButton = findViewById(R.id.show_dialog_button);

   showDialogButton.setOnClickListener(new View.OnClickListener() {
       @Override
       public void onClick(View v) {
           // Create dialog
           Dialog dialog = new Dialog(MainActivity.this);
           dialog.setContentView(R.layout.dialog_layout);
           dialog.setCancelable(true);

           // Access dialog views
           EditText dialogInput = dialog.findViewById(R.id.dialog_input);
           Button dialogButton = dialog.findViewById(R.id.dialog_button);

           dialogButton.setOnClickListener(new View.OnClickListener() {
               @Override
               public void onClick(View v) {
                   String input = dialogInput.getText().toString();
                   Toast.makeText(getApplicationContext(), "Input: " + input, Toast.LENGTH_SHORT).show();
                   dialog.dismiss(); // Close dialog
               }
           });

           dialog.show(); // Show dialog
       }
   });
   ```

---

### **5. How do you handle gestures like swipe and pinch in an Android app?**

To handle gestures like swipe and pinch, you can use the `GestureDetector` and `ScaleGestureDetector` classes.

#### **Handling Swipe Gestures with GestureDetector**
1. **Implement GestureDetector**:
   ```java
   GestureDetector gestureDetector = new GestureDetector(this, new GestureDetector.SimpleOnGestureListener() {
       @Override
       public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY) {
           if (e1.getX() - e2.getX() > 100) {
               Toast.makeText(getApplicationContext(), "Swiped Left", Toast.LENGTH_SHORT).show();
               return true;
           } else if (e2.getX() - e1.getX() > 100) {
               Toast.makeText(getApplicationContext(), "Swiped Right", Toast.LENGTH_SHORT).show();
               return true;
           }
           return false;
       }
   });

   @Override
   public boolean onTouchEvent(MotionEvent event) {
       return gestureDetector.onTouchEvent(event);
   }
   ```

2. **Override Gesture Methods**:
   - Use methods like `onScroll`, `onFling`, and `onLongPress` to detect gestures.

---

#### **Handling Pinch Gestures with ScaleGestureDetector**
1. **Implement ScaleGestureDetector**:
   ```java
   ScaleGestureDetector scaleGestureDetector = new ScaleGestureDetector(this, new ScaleGestureDetector.SimpleOnScaleGestureListener() {
       @Override
       public boolean onScale(ScaleGestureDetector detector) {
           float scaleFactor = detector.getScaleFactor();
           if (scaleFactor > 1) {
               Toast.makeText(getApplicationContext(), "Zooming In", Toast.LENGTH_SHORT).show();
           } else {
               Toast.makeText(getApplicationContext(), "Zooming Out", Toast.LENGTH_SHORT).show();
           }
           return true;
       }
   });

   @Override
   public boolean onTouchEvent(MotionEvent event) {
       scaleGestureDetector.onTouchEvent(event);
       return super.onTouchEvent(event);
   }
   ```

---

#### **Using Both GestureDetector and ScaleGestureDetector Together**
1. Combine both detectors in your `onTouchEvent` method:
   ```java
   @Override
   public boolean onTouchEvent(MotionEvent event) {
       scaleGestureDetector.onTouchEvent(event);
       gestureDetector.onTouchEvent(event);
       return super.onTouchEvent(event);
   }
   ```

2. **Use Cases**:
   - **Swipe**: Navigate between screens or items.
   - **Pinch**: Zoom in/out of an image or map.

---


15. Navigation & Back Stack
---

### **1. What is the difference between `finish()` and `onBackPressed()`?**

#### **`finish()`**
- **Definition**: Ends the current Activity and removes it from the Activity stack.
- **Use Case**: Use it when you want to explicitly close an Activity, regardless of whether the back button was pressed.
- **Behavior**:
  - The `onDestroy()` lifecycle method is called.
  - The previous Activity in the stack is resumed.

#### **`onBackPressed()`**
- **Definition**: Simulates a back button press and navigates back in the Activity stack.
- **Use Case**: Use it when you want to programmatically trigger the same behavior as the back button.
- **Behavior**:
  - The `onBackPressed()` method is invoked.
  - If there are no more Activities in the stack, the app exits.

#### **Key Differences**:
| **Aspect**          | **finish()**                              | **onBackPressed()**                        |
|----------------------|-------------------------------------------|-------------------------------------------|
| **Trigger**          | Directly ends the Activity.               | Simulates a back button press.            |
| **Stack Behavior**   | Removes the current Activity from the stack. | Moves to the previous Activity in the stack. |
| **Customization**    | Cannot be overridden.                     | Can be overridden to customize behavior.   |

#### **Example**:
```java
@Override
public void onBackPressed() {
    // Custom behavior when back button is pressed
    Toast.makeText(this, "Back button pressed", Toast.LENGTH_SHORT).show();
    super.onBackPressed(); // Optional: Call the default behavior
}
```

---

### **2. How do you prevent an Activity from being recreated when the device is rotated?**

By default, rotating the device triggers a **configuration change**, causing the Activity to be destroyed and recreated. To prevent this behavior:

#### **Approach 1: Modify the Manifest**
- Add `android:configChanges` attribute in the `AndroidManifest.xml` file:
  ```xml
  <activity
      android:name=".MainActivity"
      android:configChanges="orientation|screenSize" />
  ```
- This prevents the Activity from being recreated and instead calls `onConfigurationChanged()`.

#### **Approach 2: Retain Data Using ViewModel**
- Use a `ViewModel` to retain UI-related data across configuration changes without recreating the Activity.
  ```java
  class MyViewModel extends ViewModel {
      MutableLiveData<String> data = new MutableLiveData<>();
  }
  ```

#### **Approach 3: Retain Fragment**
- Use a `Fragment` with `setRetainInstance(true)` to retain data and prevent recreation of the Fragment.

#### **Example of Handling Configuration Changes**:
```java
@Override
public void onConfigurationChanged(Configuration newConfig) {
    super.onConfigurationChanged(newConfig);
    // Handle configuration changes here
}
```

---

### **3. How do you navigate back to a specific Activity in the back stack?**

To navigate back to a specific Activity in the back stack, use the following methods:

#### **Method 1: Use `FLAG_ACTIVITY_CLEAR_TOP`**
- Add the `Intent.FLAG_ACTIVITY_CLEAR_TOP` flag to the `Intent`:
  ```java
  Intent intent = new Intent(this, TargetActivity.class);
  intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
  startActivity(intent);
  ```
- **Behavior**:
  - All Activities above the target Activity in the stack are cleared.
  - The target Activity is brought to the foreground.

#### **Method 2: Use `FLAG_ACTIVITY_REORDER_TO_FRONT`**
- Add the `Intent.FLAG_ACTIVITY_REORDER_TO_FRONT` flag:
  ```java
  Intent intent = new Intent(this, TargetActivity.class);
  intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
  startActivity(intent);
  ```
- **Behavior**:
  - The target Activity is brought to the front without clearing other Activities.

---

### **4. How do you open a website URL in a browser from an Android app?**

#### **Steps to Open a URL in a Browser**:
1. Create an `Intent` with the `ACTION_VIEW` action.
2. Pass the URL as a `Uri` to the `Intent`.
3. Start the `Intent`.

#### **Example**:
```java
String url = "https://www.example.com";
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse(url));
startActivity(intent);
```

- **Behavior**: This opens the URL in the default browser installed on the device.
- **Note**: Ensure the URL starts with `http://` or `https://`.

---

### **5. What is the difference between `startActivity()` and `startActivityForResult()`?**

| **Aspect**               | **startActivity()**                              | **startActivityForResult()**                   |
|--------------------------|-------------------------------------------------|-----------------------------------------------|
| **Definition**            | Starts a new Activity without expecting a result. | Starts a new Activity and expects a result.   |
| **Use Case**              | Navigate to another screen without requiring feedback. | Navigate to another screen and get feedback.  |
| **Data Flow**             | No data is returned to the calling Activity.   | Data is returned to the calling Activity.     |
| **Callback**              | No callback is triggered.                      | Triggers `onActivityResult()` for the result. |

#### **Example of `startActivity()`**:
```java
Intent intent = new Intent(this, SecondActivity.class);
startActivity(intent);
```

#### **Example of `startActivityForResult()`**:
1. **Start the Activity**:
   ```java
   Intent intent = new Intent(this, SecondActivity.class);
   startActivityForResult(intent, REQUEST_CODE);
   ```

2. **Handle the Result**:
   ```java
   @Override
   protected void onActivityResult(int requestCode, int resultCode, Intent data) {
       super.onActivityResult(requestCode, resultCode, data);
       if (requestCode == REQUEST_CODE && resultCode == RESULT_OK) {
           String result = data.getStringExtra("key");
           Toast.makeText(this, "Result: " + result, Toast.LENGTH_SHORT).show();
       }
   }
   ```

3. **Return Data from the Target Activity**:
   ```java
   Intent resultIntent = new Intent();
   resultIntent.putExtra("key", "value");
   setResult(RESULT_OK, resultIntent);
   finish();
   ```

---

16. Data Persistence & Storage

---

### **1. What is the difference between caching and permanent storage in Android?**

| **Aspect**             | **Caching**                                         | **Permanent Storage**                               |
|------------------------|----------------------------------------------------|---------------------------------------------------|
| **Definition**          | Temporary storage used for faster access to frequently used data. | Persistent storage where data is retained even after the app is closed or the device is restarted. |
| **Use Case**            | Storing data like images, API responses, or files for quick access. | Storing user preferences, files, or databases that need to persist over time. |
| **Lifespan**            | Data can be cleared by the system (e.g., when storage is low) or by the user. | Data persists until explicitly deleted by the app or user. |
| **Storage Location**    | Cache directory (`getCacheDir()` or `getExternalCacheDir()`). | Internal storage (`getFilesDir()`), external storage, or databases. |
| **System Management**   | Android may automatically clear cached data when storage runs low. | Permanent storage is not cleared automatically by the system. |
| **Example**             | Storing temporary images or JSON responses.       | Saving user-generated content like notes or saved preferences. |

#### **Example of Storing Data in Cache:**
```java
File cacheDir = getCacheDir();
File tempFile = new File(cacheDir, "temp_data.txt");
```

#### **Example of Storing Data in Permanent Storage:**
```java
File filesDir = getFilesDir();
File permanentFile = new File(filesDir, "user_data.txt");
```

---

### **2. How do you store an array of values in SharedPreferences?**

SharedPreferences does not directly support storing arrays, but you can convert arrays to a format like JSON or a `Set` and save them.

#### **Example 1: Using JSON**
1. **Save Array**:
   ```java
   SharedPreferences sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE);
   SharedPreferences.Editor editor = sharedPreferences.edit();

   String[] array = {"value1", "value2", "value3"};
   Gson gson = new Gson();
   String json = gson.toJson(array);

   editor.putString("array_key", json);
   editor.apply();
   ```

2. **Retrieve Array**:
   ```java
   String json = sharedPreferences.getString("array_key", null);
   String[] array = new Gson().fromJson(json, String[].class);
   ```

#### **Example 2: Using a Set (for String arrays only)**
1. **Save Array**:
   ```java
   Set<String> set = new HashSet<>(Arrays.asList("value1", "value2", "value3"));
   editor.putStringSet("array_key", set);
   editor.apply();
   ```

2. **Retrieve Array**:
   ```java
   Set<String> set = sharedPreferences.getStringSet("array_key", null);
   String[] array = set.toArray(new String[0]);
   ```

---

### **3. What are the advantages of using the Room database instead of SQLite?**

| **Feature**                | **Room**                                         | **SQLite**                                         |
|----------------------------|-------------------------------------------------|--------------------------------------------------|
| **Ease of Use**             | Provides an abstraction layer over SQLite, making database operations simpler. | Requires writing raw SQL queries manually.       |
| **Compile-Time Verification** | SQL queries are verified at compile time, reducing runtime errors. | No compile-time verification for queries.        |
| **Integration with LiveData** | Built-in support for `LiveData` and `Flow` to observe database changes. | Requires manual implementation for real-time updates. |
| **Boilerplate Code**        | Reduces boilerplate code by using annotations like `@Entity`, `@Dao`. | Requires more boilerplate code for table creation and management. |
| **Migration Support**       | Simplifies database versioning and migration.   | Requires manual handling of migrations.          |

#### **Example of Room Implementation**:
1. **Define an Entity**:
   ```java
   @Entity
   public class User {
       @PrimaryKey
       public int id;
       public String name;
   }
   ```

2. **Create a DAO**:
   ```java
   @Dao
   public interface UserDao {
       @Insert
       void insert(User user);

       @Query("SELECT * FROM User")
       List<User> getAllUsers();
   }
   ```

3. **Build the Database**:
   ```java
   @Database(entities = {User.class}, version = 1)
   public abstract class AppDatabase extends RoomDatabase {
       public abstract UserDao userDao();
   }
   ```

   ```java
   AppDatabase db = Room.databaseBuilder(getApplicationContext(),
           AppDatabase.class, "database-name").build();
   ```

---

### **4. How do you read and write files to internal storage?**

#### **Writing to Internal Storage**:
```java
String filename = "example.txt";
String fileContents = "Hello, World!";
try (FileOutputStream fos = openFileOutput(filename, Context.MODE_PRIVATE)) {
    fos.write(fileContents.getBytes());
}
```

- **`Context.MODE_PRIVATE`**: Ensures the file is private to the app.

#### **Reading from Internal Storage**:
```java
String filename = "example.txt";
try (FileInputStream fis = openFileInput(filename);
     InputStreamReader isr = new InputStreamReader(fis);
     BufferedReader bufferedReader = new BufferedReader(isr)) {

    StringBuilder stringBuilder = new StringBuilder();
    String line;
    while ((line = bufferedReader.readLine()) != null) {
        stringBuilder.append(line);
    }
    String fileContents = stringBuilder.toString();
}
```

#### **Key Points**:
- Internal storage is private to the app.
- Files stored here are deleted when the app is uninstalled.

---

### **5. How do you download and save a file from the internet in Android?**

#### **Steps to Download and Save a File**:
1. **Add Internet Permission**:
   - Add the following permission to the `AndroidManifest.xml`:
     ```xml
     <uses-permission android:name="android.permission.INTERNET" />
     ```

2. **Use `HttpURLConnection` to Download the File**:
   ```java
   private void downloadFile(String fileUrl, String fileName) {
       try {
           URL url = new URL(fileUrl);
           HttpURLConnection connection = (HttpURLConnection) url.openConnection();
           connection.connect();

           // Check for a successful response
           if (connection.getResponseCode() != HttpURLConnection.HTTP_OK) {
               throw new IOException("Server returned HTTP " + connection.getResponseCode());
           }

           // Input stream to read the file
           InputStream inputStream = connection.getInputStream();

           // Output stream to write the file to internal storage
           FileOutputStream outputStream = openFileOutput(fileName, Context.MODE_PRIVATE);

           byte[] buffer = new byte[1024];
           int bytesRead;
           while ((bytesRead = inputStream.read(buffer)) != -1) {
               outputStream.write(buffer, bytesRead);
           }

           // Close streams
           outputStream.close();
           inputStream.close();
           connection.disconnect();

           Toast.makeText(this, "File downloaded successfully", Toast.LENGTH_SHORT).show();
       } catch (Exception e) {
           e.printStackTrace();
           Toast.makeText(this, "Error downloading file", Toast.LENGTH_SHORT).show();
       }
   }
   ```

3. **Calling the Method**:
   ```java
   String fileUrl = "https://example.com/file.pdf";
   String fileName = "downloaded_file.pdf";
   downloadFile(fileUrl, fileName);
   ```

4. **Save to External Storage (Optional)**:
   If saving to external storage, ensure you request **WRITE_EXTERNAL_STORAGE** permission on older Android versions and use the correct directory:
   ```java
   File externalFile = new File(getExternalFilesDir(Environment.DIRECTORY_DOWNLOADS), fileName);
   FileOutputStream outputStream = new FileOutputStream(externalFile);
   ```

5. **Use DownloadManager (Optional)**:
   Alternatively, use the `DownloadManager` for system-managed downloads:
   ```java
   DownloadManager downloadManager = (DownloadManager) getSystemService(Context.DOWNLOAD_SERVICE);
   Uri uri = Uri.parse(fileUrl);

   DownloadManager.Request request = new DownloadManager.Request(uri);
   request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
   request.setDestinationInExternalFilesDir(this, Environment.DIRECTORY_DOWNLOADS, fileName);

   downloadManager.enqueue(request);
   ```

---




17. Networking & Internet Connectivity

---

### **1. How do you check if the device is connected to the internet?**

To check if the device is connected to the internet, you can use the `ConnectivityManager` class.

#### **Example**:
```java
import android.content.Context;
import android.net.ConnectivityManager;
import android.net.NetworkCapabilities;

public boolean isInternetAvailable(Context context) {
    ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
    if (connectivityManager != null) {
        NetworkCapabilities capabilities = connectivityManager.getNetworkCapabilities(connectivityManager.getActiveNetwork());
        return capabilities != null &&
               (capabilities.hasTransport(NetworkCapabilities.TRANSPORT_WIFI) ||
                capabilities.hasTransport(NetworkCapabilities.TRANSPORT_CELLULAR));
    }
    return false;
}
```

- **Key Points**:
  - `TRANSPORT_WIFI`: Checks if the device is connected via Wi-Fi.
  - `TRANSPORT_CELLULAR`: Checks if the device is connected via mobile data.
  - Always request the `ACCESS_NETWORK_STATE` permission in the `AndroidManifest.xml`:
    ```xml
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    ```

---

### **2. How do you make a simple HTTP GET request in Android?**

#### **Using `HttpURLConnection`**:
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public String makeGetRequest(String urlString) {
    try {
        URL url = new URL(urlString);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        connection.connect();

        // Check for a successful response
        int responseCode = connection.getResponseCode();
        if (responseCode == HttpURLConnection.HTTP_OK) {
            BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            StringBuilder result = new StringBuilder();
            String line;
            while ((line = reader.readLine()) != null) {
                result.append(line);
            }
            reader.close();
            return result.toString(); // JSON or response content
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
    return null;
}
```

- **Note**: This code works on a background thread (e.g., using `AsyncTask` or `Kotlin Coroutines`) to avoid blocking the UI thread.

#### **Using Retrofit (Recommended)**:
1. Add the Retrofit dependency in `build.gradle`:
   ```gradle
   implementation 'com.squareup.retrofit2:retrofit:2.9.0'
   implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
   ```

2. Create a Retrofit interface:
   ```java
   public interface ApiService {
       @GET("posts") // Example endpoint
       Call<List<Post>> getPosts();
   }
   ```

3. Make the request:
   ```java
   Retrofit retrofit = new Retrofit.Builder()
       .baseUrl("https://jsonplaceholder.typicode.com/")
       .addConverterFactory(GsonConverterFactory.create())
       .build();

   ApiService apiService = retrofit.create(ApiService.class);
   apiService.getPosts().enqueue(new Callback<List<Post>>() {
       @Override
       public void onResponse(Call<List<Post>> call, Response<List<Post>> response) {
           if (response.isSuccessful()) {
               List<Post> posts = response.body();
               // Handle the response
           }
       }

       @Override
       public void onFailure(Call<List<Post>> call, Throwable t) {
           t.printStackTrace();
       }
   });
   ```

---

### **3. What is the difference between synchronous and asynchronous network calls?**

| **Aspect**              | **Synchronous**                                     | **Asynchronous**                                   |
|-------------------------|----------------------------------------------------|--------------------------------------------------|
| **Definition**           | The request blocks the current thread until it is complete. | The request runs in a separate thread, allowing the main thread to continue execution. |
| **Thread Blocking**      | Blocks the thread, which could freeze the UI if run on the main thread. | Does not block the thread, ensuring smooth UI responsiveness. |
| **Use Case**             | Suitable for background threads or quick operations. | Preferred for network calls to avoid blocking the UI. |
| **Example**              | `HttpURLConnection` synchronous calls.            | Retrofit's `enqueue()` method.                   |

---

### **4. How do you parse a JSON response in Android?**

You can parse JSON in Android using libraries like **Gson** or **org.json**.

#### **Using `org.json`**:
```java
import org.json.JSONArray;
import org.json.JSONObject;

public void parseJson(String jsonResponse) {
    try {
        JSONObject jsonObject = new JSONObject(jsonResponse);
        String title = jsonObject.getString("title");

        JSONArray itemsArray = jsonObject.getJSONArray("items");
        for (int i = 0; i < itemsArray.length(); i++) {
            JSONObject item = itemsArray.getJSONObject(i);
            String name = item.getString("name");
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

#### **Using Gson Library (Recommended)**:
1. Add Gson dependency:
   ```gradle
   implementation 'com.google.code.gson:gson:2.8.9'
   ```

2. Create a Data Model:
   ```java
   public class Post {
       public int userId;
       public int id;
       public String title;
       public String body;
   }
   ```

3. Parse JSON:
   ```java
   Gson gson = new Gson();
   Post post = gson.fromJson(jsonResponse, Post.class);
   ```

- **Key Advantage of Gson**: Automatically maps JSON keys to Java object fields.

---

### **5. How do you load an image from a URL into an ImageView?**

#### **Using `Glide` (Recommended)**:
1. Add Glide dependency:
   ```gradle
   implementation 'com.github.bumptech.glide:glide:4.14.2'
   annotationProcessor 'com.github.bumptech.glide:compiler:4.14.2'
   ```

2. Load Image:
   ```java
   ImageView imageView = findViewById(R.id.imageView);
   Glide.with(this)
       .load("https://example.com/image.jpg")
       .placeholder(R.drawable.placeholder) // Optional placeholder
       .error(R.drawable.error_image)       // Error image
       .into(imageView);
   ```

#### **Using `Picasso`**:
1. Add Picasso dependency:
   ```gradle
   implementation 'com.squareup.picasso:picasso:2.8'
   ```

2. Load Image:
   ```java
   ImageView imageView = findViewById(R.id.imageView);
   Picasso.get()
       .load("https://example.com/image.jpg")
       .placeholder(R.drawable.placeholder) // Optional placeholder
       .error(R.drawable.error_image)       // Error image
       .into(imageView);
   ```

#### **Using `AsyncTask` and `BitmapFactory` (Manual Approach)**:
1. **Create an AsyncTask**:
   ```java
   private class DownloadImageTask extends AsyncTask<String, Void, Bitmap> {
       ImageView imageView;

       public DownloadImageTask(ImageView imageView) {
           this.imageView = imageView;
       }

       @Override
       protected Bitmap doInBackground(String... urls) {
           String imageUrl = urls[0];
           Bitmap bitmap = null;
           try {
               InputStream input = new java.net.URL(imageUrl).openStream();
               bitmap = BitmapFactory.decodeStream(input);
           } catch (Exception e) {
               e.printStackTrace();
           }
           return bitmap;
       }

       @Override
       protected void onPostExecute(Bitmap result) {
           imageView.setImageBitmap(result);
       }
   }
   ```

2. **Load Image**:
   ```java
   new DownloadImageTask(imageView).execute("https://example.com/image.jpg");
   ```

#### **Why Use Glide or Picasso?**
- **Ease of Use**: No need to manually handle threading.
- **Caching**: Both libraries cache images for better performance.
- **Error Handling**: Built-in support for placeholder and error images.
- **Additional Features**: Image transformations (e.g., cropping, resizing).

---


18. Background Tasks & Services
---

### **1. What is a Service in Android?**

A `Service` in Android is a component that performs long-running operations in the background without providing a user interface. It is useful for tasks that don't require user interaction, such as playing music, downloading files, or syncing data in the background.

#### **Key Features**:
- Runs independently of the Activity lifecycle.
- Can perform tasks even if the app is in the background.
- Does not interact directly with the user.

#### **Types of Services**:
1. **Foreground Service**: Runs in the foreground and shows a notification to the user (e.g., music player).
2. **Background Service**: Runs without user interaction and no visible notification.
3. **Bound Service**: Allows components (e.g., Activities) to bind to the service and interact with it.

#### **Example**:
```java
public class MyService extends Service {
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // Perform background work
        return START_STICKY; // Keeps the service running until explicitly stopped
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null; // Used for bound services
    }
}
```

---

### **2. What is the difference between a Foreground Service and a Background Service?**

| **Aspect**               | **Foreground Service**                                 | **Background Service**                                 |
|--------------------------|-------------------------------------------------------|------------------------------------------------------|
| **Definition**            | Runs in the foreground and shows a persistent notification to the user. | Runs in the background without user awareness.      |
| **Visibility**            | Visible to the user through a notification.           | Not visible to the user.                             |
| **Use Case**              | Tasks requiring user awareness, like media playback or location tracking. | Tasks like syncing data or uploading files.         |
| **System Restrictions**   | Less likely to be stopped by the system.              | Subject to stricter restrictions starting from Android 8 (Oreo). |
| **Example**               | Music player, step counter.                           | Data sync, periodic updates.                        |
| **Notification**          | Mandatory notification shown while running.           | No notification required.                           |

#### **Foreground Service Example**:
```java
public class MyForegroundService extends Service {
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Notification notification = new Notification.Builder(this, "channel_id")
            .setContentTitle("Service Running")
            .setContentText("Foreground Service is active")
            .setSmallIcon(R.drawable.ic_notification)
            .build();

        startForeground(1, notification); // Starts the service in the foreground
        return START_STICKY;
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```

---

### **3. How do you schedule a task to run at a specific time in Android?**

#### **Using `AlarmManager`**:
`AlarmManager` can be used to schedule tasks to run at a specific time, even if the app is not running.

#### **Steps**:
1. **Create a `PendingIntent`**:
   - This defines the action to be performed at the scheduled time.
2. **Set the Alarm**:
   - Use `setExact()` for precise scheduling or `setInexactRepeating()` for periodic tasks.

#### **Example**:
```java
AlarmManager alarmManager = (AlarmManager) getSystemService(Context.ALARM_SERVICE);
Intent intent = new Intent(this, MyReceiver.class);
PendingIntent pendingIntent = PendingIntent.getBroadcast(this, 0, intent, PendingIntent.FLAG_IMMUTABLE);

// Schedule the alarm
long triggerTime = System.currentTimeMillis() + 60000; // 1 minute from now
alarmManager.setExact(AlarmManager.RTC_WAKEUP, triggerTime, pendingIntent);
```

- **BroadcastReceiver to Handle Alarm**:
   ```java
   public class MyReceiver extends BroadcastReceiver {
       @Override
       public void onReceive(Context context, Intent intent) {
           // Perform the scheduled task here
       }
   }
   ```

#### **Using WorkManager (Recommended for Modern Apps)**:
- WorkManager is more robust and respects system restrictions for background tasks.
- Example:
   ```java
   OneTimeWorkRequest workRequest = new OneTimeWorkRequest.Builder(MyWorker.class)
       .setInitialDelay(1, TimeUnit.MINUTES) // Delay by 1 minute
       .build();
   WorkManager.getInstance(context).enqueue(workRequest);
   ```

---

### **4. What is the purpose of AlarmManager?**

`AlarmManager` is a system service that allows you to schedule tasks to run at specific times or intervals, regardless of whether the app is running.

#### **Key Features**:
- Allows precise scheduling of tasks.
- Can wake the device from sleep (`RTC_WAKEUP`).
- Suitable for time-sensitive tasks like alarms, reminders, or notifications.

#### **Common Use Cases**:
1. **One-Time Tasks**:
   - Use `setExact()` or `setExactAndAllowWhileIdle()` for precise, one-time alarms.
2. **Repeating Tasks**:
   - Use `setInexactRepeating()` for periodic tasks like syncing data.

#### **Limitations**:
- Starting from Android 6.0 (Marshmallow), `AlarmManager` is affected by Doze Mode, which restricts background execution.

---

### **5. How does WorkManager differ from JobScheduler?**

| **Aspect**               | **WorkManager**                                   | **JobScheduler**                                 |
|--------------------------|--------------------------------------------------|------------------------------------------------|
| **Definition**            | Part of Android Jetpack; designed for deferrable, guaranteed background tasks. | Native Android API for scheduling background jobs. |
| **Ease of Use**           | Simplified API with lifecycle-aware features.     | Requires more boilerplate code.                |
| **Backward Compatibility**| Works on Android 4.0+ (API 14) using compatibility libraries. | Available only on Android 5.0+ (API 21).       |
| **Task Execution**        | Supports both one-time and periodic tasks.        | Primarily used for periodic or network-related tasks. |
| **Chaining Tasks**        | Supports task chaining and dependencies.          | No support for chaining tasks.                 |
| **Constraints**           | Built-in constraints like network availability, charging state, and idle state. | Similar constraints but less flexibility.      |
| **Use Case**              | Preferred for most background work in modern apps. | Suitable for periodic or long-running jobs.    |

#### **Example of WorkManager**:
```java
// Define the Worker
public class MyWorker extends Worker {
    public MyWorker(@NonNull Context context, @NonNull WorkerParameters params) {
        super(context, params);
    }

    @NonNull
    @Override
    public Result doWork() {
        // Task to perform
        return Result.success();
    }
}

// Schedule the Work
WorkRequest workRequest = new OneTimeWorkRequest.Builder(MyWorker.class)
    .setConstraints(new Constraints.Builder()
        .setRequiredNetworkType(NetworkType.CONNECTED)
        .build())
    .build();

WorkManager.getInstance(context).enqueue(workRequest);
```

#### **Example of JobScheduler**:
```java
JobScheduler jobScheduler = (JobScheduler) getSystemService(Context.JOB_SCHEDULER_SERVICE);
JobInfo jobInfo = new JobInfo.Builder(1, new ComponentName(this, MyJobService.class))
    .setRequiredNetworkType(JobInfo.NETWORK_TYPE_ANY)
    .setPeriodic(15 * 60 * 1000) // 15 minutes interval
    .build();

jobScheduler.schedule(jobInfo);
```

#### **Why Use WorkManager?**
- It is more modern, flexible, and easier to implement.
- Automatically handles Doze Mode and battery optimizations.
- Supports task chaining and handles retries for failed tasks.

---



19. Firebase & Cloud Integration

---

### **1. How do you add Firebase to an Android project?**

#### **Steps to Add Firebase to Your Project**:
1. **Create a Firebase Project**:
   - Visit the [Firebase Console](https://console.firebase.google.com/).
   - Click "Add Project" and follow the setup prompts.

2. **Register Your Android App**:
   - In the Firebase Console, select your project.
   - Click "Add App" > "Android".
   - Enter your app's package name (e.g., `com.example.myapp`).
   - Download the `google-services.json` file provided.

3. **Add the `google-services.json` File**:
   - Place the `google-services.json` file in the `app/` directory of your Android project.

4. **Modify `build.gradle` Files**:
   - **Project-level `build.gradle`**:
     ```gradle
     dependencies {
         classpath 'com.google.gms:google-services:4.3.15'
     }
     ```
   - **App-level `build.gradle`**:
     ```gradle
     apply plugin: 'com.google.gms.google-services'

     dependencies {
         implementation platform('com.google.firebase:firebase-bom:32.1.1') // Firebase BOM
         implementation 'com.google.firebase:firebase-analytics' // Example service
     }
     ```

5. **Sync Your Project**:
   - Click **Sync Now** in Android Studio to apply changes.

---

### **2. What is Firestore, and how is it different from Firebase Realtime Database?**

| **Aspect**                | **Firestore**                                    | **Firebase Realtime Database**                     |
|---------------------------|-------------------------------------------------|---------------------------------------------------|
| **Data Model**             | Document-oriented (NoSQL), organized in collections of documents. | JSON tree-based, hierarchical structure.          |
| **Querying**               | Advanced querying and filtering (e.g., compound queries, range). | Limited querying options, basic filtering.        |
| **Scalability**            | Scales automatically with complex queries and large datasets. | Scales well but requires manual optimization for complex queries. |
| **Offline Support**        | Built-in offline support with automatic data synchronization. | Offline support is available but requires more configuration. |
| **Real-Time Updates**      | Supports real-time updates with listener callbacks. | Primarily designed for real-time data syncing.    |
| **Use Case**               | Ideal for complex apps requiring advanced querying and structured data. | Best for simple, real-time apps like chat or live feeds. |

---

### **3. How do you authenticate users using Firebase Authentication?**

#### **Steps to Use Firebase Authentication**:
1. **Enable Authentication in Firebase Console**:
   - Go to the Firebase Console > "Authentication" > "Sign-in Method".
   - Enable the desired authentication methods (e.g., Email/Password, Google, Phone).

2. **Add Firebase Authentication Dependency**:
   - Update `build.gradle`:
     ```gradle
     implementation 'com.google.firebase:firebase-auth'
     ```

3. **Authenticate Users (Example: Email/Password)**:
   ```java
   FirebaseAuth auth = FirebaseAuth.getInstance();

   // Sign up a new user
   auth.createUserWithEmailAndPassword(email, password)
       .addOnCompleteListener(task -> {
           if (task.isSuccessful()) {
               FirebaseUser user = auth.getCurrentUser();
               Log.d("Auth", "User created: " + user.getEmail());
           } else {
               Log.e("Auth", "Error: " + task.getException().getMessage());
           }
       });

   // Sign in an existing user
   auth.signInWithEmailAndPassword(email, password)
       .addOnCompleteListener(task -> {
           if (task.isSuccessful()) {
               FirebaseUser user = auth.getCurrentUser();
               Log.d("Auth", "User signed in: " + user.getEmail());
           } else {
               Log.e("Auth", "Error: " + task.getException().getMessage());
           }
       });
   ```

4. **Sign Out**:
   ```java
   FirebaseAuth.getInstance().signOut();
   ```

---

### **4. How do you send a Firebase push notification?**

#### **Steps to Send Push Notifications**:
1. **Set Up Firebase Cloud Messaging (FCM)**:
   - In the Firebase Console, go to "Cloud Messaging".
   - Obtain the **Server Key**.

2. **Add FCM Dependency**:
   ```gradle
   implementation 'com.google.firebase:firebase-messaging'
   ```

3. **Receive Notifications in Your App**:
   - Create a custom `FirebaseMessagingService`:
     ```java
     public class MyFirebaseMessagingService extends FirebaseMessagingService {
         @Override
         public void onMessageReceived(RemoteMessage remoteMessage) {
             // Handle received message
             Log.d("FCM", "Message received: " + remoteMessage.getData());
         }

         @Override
         public void onNewToken(String token) {
             Log.d("FCM", "New token: " + token);
         }
     }
     ```

   - Register the service in `AndroidManifest.xml`:
     ```xml
     <service android:name=".MyFirebaseMessagingService"
              android:exported="true">
         <intent-filter>
             <action android:name="com.google.firebase.MESSAGING_EVENT" />
         </intent-filter>
     </service>
     ```

4. **Send Notifications**:
   - Use the Firebase Console or a custom server to send notifications using the FCM API.

---

### **5. How do you upload an image to Firebase Storage?**

#### **Steps to Upload an Image**:
1. **Enable Firebase Storage**:
   - Go to the Firebase Console > "Storage".
   - Set up storage rules (default is read/write access only to authenticated users).

2. **Add Firebase Storage Dependency**:
   ```gradle
   implementation 'com.google.firebase:firebase-storage'
   ```

3. **Upload an Image**:
   - **Example: Select Image from Gallery and Upload**.
   
   ```java
   public void uploadImage(Uri fileUri) {
       FirebaseStorage storage = FirebaseStorage.getInstance();
       StorageReference storageRef = storage.getReference();
       StorageReference imageRef = storageRef.child("images/" + fileUri.getLastPathSegment());

       imageRef.putFile(fileUri)
           .addOnSuccessListener(taskSnapshot -> {
               imageRef.getDownloadUrl().addOnSuccessListener(uri -> {
                   String downloadUrl = uri.toString();
                   Log.d("FirebaseStorage", "Image uploaded: " + downloadUrl);
               });
           })
           .addOnFailureListener(e -> {
               Log.e("FirebaseStorage", "Upload failed: " + e.getMessage());
           });
   }
   ```

4. **Select Image from Gallery**:
   ```java
   Intent intent = new Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
   startActivityForResult(intent, PICK_IMAGE_REQUEST);
   ```

5. **Handle Image Selection**:
   ```java
   @Override
   protected void onActivityResult(int requestCode, int resultCode, Intent data) {
       super.onActivityResult(requestCode, resultCode, data);
       if (requestCode == PICK_IMAGE_REQUEST && resultCode == RESULT_OK) {
           Uri fileUri = data.getData(); // Get the image URI
           uploadImage(fileUri); // Upload the selected image
       }
   }
   ```

---




20. Permissions & Security

---

### **1. How do you request location permission in Android?**

#### **Steps to Request Location Permission**:
1. **Declare Location Permission in `AndroidManifest.xml`**:
   ```xml
   <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
   <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
   ```

2. **Check Permission at Runtime** (Android 6.0+ requires runtime permissions):
   ```java
   if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
           != PackageManager.PERMISSION_GRANTED) {
       // Permission is not granted, request it
       ActivityCompat.requestPermissions(this,
               new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
               LOCATION_REQUEST_CODE);
   }
   ```

3. **Handle Permission Result**:
   Override `onRequestPermissionsResult` to handle the user's response:
   ```java
   @Override
   public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
       if (requestCode == LOCATION_REQUEST_CODE) {
           if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
               // Permission granted
               Toast.makeText(this, "Location Permission Granted", Toast.LENGTH_SHORT).show();
           } else {
               // Permission denied
               Toast.makeText(this, "Location Permission Denied", Toast.LENGTH_SHORT).show();
           }
       }
   }
   ```

4. **Best Practices**:
   - Use `shouldShowRequestPermissionRationale()` to provide an explanation if the user denies the permission initially:
     ```java
     if (ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.ACCESS_FINE_LOCATION)) {
         // Show an explanation to the user
     }
     ```

---

### **2. How do you ask for multiple permissions at runtime?**

#### **Steps to Request Multiple Permissions**:
1. **Declare Permissions in `AndroidManifest.xml`**:
   ```xml
   <uses-permission android:name="android.permission.CAMERA" />
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   ```

2. **Request Permissions**:
   Use `ActivityCompat.requestPermissions()` to request multiple permissions:
   ```java
   String[] permissions = {
       Manifest.permission.CAMERA,
       Manifest.permission.READ_EXTERNAL_STORAGE
   };

   ActivityCompat.requestPermissions(this, permissions, MULTIPLE_PERMISSIONS_REQUEST_CODE);
   ```

3. **Handle the Permissions Result**:
   ```java
   @Override
   public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
       if (requestCode == MULTIPLE_PERMISSIONS_REQUEST_CODE) {
           for (int i = 0; i < permissions.length; i++) {
               if (grantResults[i] == PackageManager.PERMISSION_GRANTED) {
                   Log.d("Permissions", permissions[i] + " granted");
               } else {
                   Log.d("Permissions", permissions[i] + " denied");
               }
           }
       }
   }
   ```

4. **Best Practices**:
   - Check each permission individually using `ContextCompat.checkSelfPermission()`.
   - Always provide a rationale for critical permissions using `shouldShowRequestPermissionRationale()`.

---

### **3. What is the purpose of the Android Keystore System?**

#### **Purpose**:
The **Android Keystore System** provides a secure container for storing cryptographic keys and credentials. These keys are stored in a hardware-backed or software-protected environment, preventing unauthorized access even if the app's data is compromised.

#### **Key Features**:
1. **Key Storage**:
   - Keys are stored securely and cannot be exported from the Keystore.
2. **Hardware Security**:
   - On supported devices, keys are stored in a hardware-backed secure environment.
3. **Key Operations**:
   - Keys can perform cryptographic operations like encryption, decryption, signing, and verification.
4. **Use Cases**:
   - Securely store API keys, user credentials, or sensitive data encryption keys.

#### **Example: Generating and Using Keys**:
1. **Generate a Key**:
   ```java
   KeyGenerator keyGenerator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES, "AndroidKeyStore");
   keyGenerator.init(new KeyGenParameterSpec.Builder("MyKeyAlias",
           KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
           .setBlockModes(KeyProperties.BLOCK_MODE_GCM)
           .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_NONE)
           .build());
   SecretKey key = keyGenerator.generateKey();
   ```

2. **Encrypt Data**:
   ```java
   Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
   cipher.init(Cipher.ENCRYPT_MODE, key);
   byte[] encryptedData = cipher.doFinal(dataToEncrypt.getBytes());
   ```

3. **Decrypt Data**:
   ```java
   cipher.init(Cipher.DECRYPT_MODE, key, new GCMParameterSpec(128, cipher.getIV()));
   byte[] decryptedData = cipher.doFinal(encryptedData);
   ```

#### **Advantages**:
- Protects sensitive keys from unauthorized access.
- Ensures keys are not exposed in app memory or storage.

---

### **4. How do you prevent unauthorized access to an API key in an Android app?**

#### **Best Practices to Secure API Keys**:
1. **Avoid Hardcoding API Keys**:
   - Do not store API keys directly in your app's code (e.g., `BuildConfig`, strings.xml).

2. **Use Environment Variables**:
   - Store API keys in environment variables or external configuration files not included in the APK.

3. **Store Keys in the Android Keystore**:
   - Use the Android Keystore System to securely store sensitive keys.

4. **Use Backend Proxy**:
   - Do not call APIs directly from the client app. Instead, route requests through a secure backend server that adds the necessary credentials.

5. **Obfuscate Code**:
   - Use tools like **ProGuard** or **R8** to obfuscate your code and make it harder for attackers to decompile and extract keys.

6. **Restrict API Key Usage**:
   - Configure API key restrictions (e.g., use IP restrictions or domain restrictions in your API provider's dashboard).

7. **Monitor API Usage**:
   - Regularly monitor API usage to detect suspicious activity.

---

### **5. What security risks should you consider when developing an Android app?**

#### **Key Security Risks**:
1. **Data Leakage**:
   - Sensitive data (e.g., user credentials, API keys) stored in plaintext is vulnerable to theft if the app is decompiled or the device is compromised.
   - **Solution**: Use encrypted storage (e.g., Keystore, EncryptedSharedPreferences).

2. **Insecure Communication**:
   - Without proper encryption, data transmitted over the network can be intercepted (e.g., man-in-the-middle attacks).
   - **Solution**: Always use HTTPS and implement SSL/TLS certificate pinning.

3. **Code Injection**:
   - Malicious code can be injected into the app if it lacks proper validation.
   - **Solution**: Validate all inputs and sanitize data.

4. **Reverse Engineering**:
   - Attackers can decompile APKs to extract sensitive information like API keys or business logic.
   - **Solution**: Use obfuscation tools like ProGuard and R8.

5. **Weak Authentication**:
   - Poorly implemented authentication can lead to unauthorized access.
   - **Solution**: Use secure authentication methods like OAuth2, Firebase Authentication, or biometric authentication (e.g., fingerprint).

6. **Insecure Permissions**:
   - Over-requesting permissions can expose the app to abuse if permissions are exploited.
   - **Solution**: Request only necessary permissions and provide clear justifications to users.

7. **Unvalidated Data Storage**:
   - Storing unvalidated data (e.g., user-generated files) can lead to security vulnerabilities like path traversal.
   - **Solution**: Validate and sanitize all file paths and user input.

8. **Outdated Libraries and Dependencies**:
   - Using outdated libraries with known vulnerabilities can compromise app security.
   - **Solution**: Regularly update libraries and dependencies.

9. **Improper Session Management**:
   - Failure to securely handle user sessions can lead to session hijacking.
   - **Solution**: Use secure session tokens and implement session timeouts.

10. **Insufficient Error Handling**:
    - Revealing stack traces or error details in production can expose vulnerabilities.
    - **Solution**: Log errors securely without exposing sensitive information.

#### **Best Practices for Secure Android Development**:
- Use the **Android Keystore** to store sensitive data.
- Minimize permissions and follow the principle of least privilege.
- Enforce strong encryption for local storage and network communication.
- Implement strong authentication and authorization mechanisms.
- Regularly test your app for vulnerabilities using tools like **OWASP ZAP** or **Burp Suite**.

---



Medium level


1. Android Components & Lifecycle


---

### **1. What is the difference between `onCreate()` and `onStart()` in an Activity?**

| **Aspect**            | **`onCreate()`**                                     | **`onStart()`**                                   |
|-----------------------|-----------------------------------------------------|-------------------------------------------------|
| **Purpose**            | Called when the Activity is first created.          | Called when the Activity becomes visible to the user. |
| **Initialization**     | Used for initial setup such as inflating layouts, initializing components, and restoring savedInstanceState. | Used to prepare the UI for user interaction (e.g., starting animations or updating UI). |
| **Lifecycle State**    | Called once during the Activity’s lifecycle (unless recreated). | Can be called multiple times (e.g., when returning from the background). |
| **Execution Order**    | Called before `onStart()`.                          | Called after `onCreate()` but before `onResume()`. |
| **Use Case**           | Initialize resources like layouts, ViewModels, or variables. | Start tasks that make the Activity visible to the user (e.g., refreshing data). |

#### **Example**:
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main); // Set the layout
    Log.d("Lifecycle", "onCreate called");
}

@Override
protected void onStart() {
    super.onStart();
    Log.d("Lifecycle", "onStart called");
}
```

---

### **2. How does the Fragment lifecycle differ from the Activity lifecycle?**

#### **Fragment Lifecycle**:
The Fragment lifecycle is closely tied to its hosting Activity but has additional methods for managing its view hierarchy.

| **Lifecycle Stage**         | **Activity**                                   | **Fragment**                                   |
|-----------------------------|-----------------------------------------------|-----------------------------------------------|
| **Initialization**           | `onCreate()`                                 | `onAttach()` (when Fragment is attached to Activity), `onCreate()`. |
| **Creating View**            | N/A                                          | `onCreateView()` (inflate Fragment layout).   |
| **View Created**             | N/A                                          | `onViewCreated()` (perform view-related tasks). |
| **Visible to User**          | `onStart()` → `onResume()`                   | `onStart()` → `onResume()`.                   |
| **Stopping**                 | `onPause()` → `onStop()`                     | `onPause()` → `onStop()`.                     |
| **Destroying View**          | `onDestroy()`                                | `onDestroyView()` (destroy view hierarchy), `onDetach()` (detach Fragment from Activity). |

#### **Key Differences**:
1. **Fragment View Lifecycle**:
   - A Fragment has a separate lifecycle for its view (`onCreateView()` to `onDestroyView()`), which is different from its overall lifecycle.
   - This allows the Fragment to manage UI separately from its hosting Activity.

2. **Attachment and Detachment**:
   - Fragments are attached to and detached from their hosting Activity using `onAttach()` and `onDetach()`.

3. **Activity Dependency**:
   - A Fragment's lifecycle depends on its hosting Activity’s lifecycle.

#### **Example of Fragment Lifecycle Methods**:
```java
@Override
public void onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.fragment_layout, container, false);
    return view;
}

@Override
public void onDestroyView() {
    super.onDestroyView();
    // Cleanup view-related resources
}
```

---

### **3. What is the purpose of ViewModel in Android, and how does it survive configuration changes?**

#### **Purpose of ViewModel**:
The `ViewModel` is a part of Android's Architecture Components and is designed to store and manage **UI-related data** in a lifecycle-conscious way.

- **Key Benefits**:
  1. **Survives Configuration Changes**:
     - Retains data across configuration changes (e.g., screen rotation).
     - Eliminates the need to reload data or perform expensive operations.
  2. **Separation of Concerns**:
     - Keeps UI logic separate from the Activity or Fragment, ensuring cleaner architecture.
  3. **Lifecycle Awareness**:
     - Automatically cleared when the Activity or Fragment is permanently destroyed.

#### **How ViewModel Survives Configuration Changes?**:
- ViewModel instances are tied to the lifecycle of their owner (Activity/Fragment).
- When a configuration change occurs (e.g., screen rotation), the system retains the ViewModel and reattaches it to the new instance of the Activity or Fragment.

#### **Example**:
1. **Define a ViewModel**:
   ```java
   public class MyViewModel extends ViewModel {
       private MutableLiveData<String> data;

       public MutableLiveData<String> getData() {
           if (data == null) {
               data = new MutableLiveData<>();
           }
           return data;
       }
   }
   ```

2. **Use ViewModel in an Activity**:
   ```java
   MyViewModel viewModel = new ViewModelProvider(this).get(MyViewModel.class);

   viewModel.getData().observe(this, data -> {
       // Update the UI with the data
   });

   viewModel.getData().setValue("Hello, ViewModel!");
   ```

---

### **4. What happens if you call `finish()` inside `onCreate()`?**

- **Behavior**:
  - When `finish()` is called inside `onCreate()`, the Activity is immediately marked for destruction.
  - The `onStart()` and `onResume()` lifecycle methods are **not** invoked.
  - The system proceeds to call `onPause()`, `onStop()`, and `onDestroy()`.

- **Use Case**:
  - Often used to terminate an Activity conditionally (e.g., invalid input or unfulfilled prerequisites).

#### **Example**:
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    if (!isUserLoggedIn()) {
        finish(); // End the Activity if the user is not logged in
    }

    setContentView(R.layout.activity_main);
}
```

#### **Key Points**:
- Calling `finish()` in `onCreate()` prevents the Activity from being fully created.
- Be cautious, as this can lead to unexpected behavior if not handled properly.

---

### **5. How do you handle a scenario where a Fragment needs to communicate with its hosting Activity?**

#### **Best Practices for Fragment-Activity Communication**:
1. **Using an Interface** (Recommended):
   - Define an interface in the Fragment and implement it in the hosting Activity.

   ```java
   public class MyFragment extends Fragment {
       private FragmentListener listener;

       public interface FragmentListener {
           void onFragmentAction(String data);
       }

       @Override
       public void onAttach(Context context) {
           super.onAttach(context);
           if (context instanceof FragmentListener) {
               listener = (FragmentListener) context;
           } else {
               throw new RuntimeException(context.toString() + " must implement FragmentListener");
           }
       }

       @Override
       public void onDetach() {
           super.onDetach();
           listener = null; // Avoid memory leaks
       }

       public void someMethod() {
           if (listener != null) {
               listener.onFragmentAction("Some data");
           }
       }
   }
   ```

   - **Implement in Activity**:
     ```java
     public class MainActivity extends AppCompatActivity implements MyFragment.FragmentListener {
         @Override
         public void onFragmentAction(String data) {
             Log.d("FragmentCommunication", "Received data: " + data);
         }
     }
     ```

2. **Using `ViewModel`** (for Shared Data):
   - Use a shared `ViewModel` to communicate between the Fragment and its hosting Activity.
   - **Example**:
     ```java
     public class SharedViewModel extends ViewModel {
         private MutableLiveData<String> data = new MutableLiveData<>();

         public MutableLiveData<String> getData() {
             return data;
         }
     }
     ```

     - In the Fragment:
       ```java
       SharedViewModel viewModel = new ViewModelProvider(requireActivity()).get(SharedViewModel.class);
       viewModel.getData().setValue("Data from Fragment");
       ```

     - In the Activity:
       ```java
       viewModel.getData().observe(this, data -> {
           Log.d("ViewModelCommunication", "Received data: " + data);
       });
       ```

3. **Using `Bundle`**:
   - Pass data when adding the Fragment:
     ```java
     MyFragment fragment = new MyFragment();
     Bundle args = new Bundle();
     args.putString("key", "value");
     fragment.setArguments(args);
     ```

   - Retrieve data in the Fragment:
     ```java
     String value = getArguments().getString("key");
     ```

#### **Key Points**:
- Prefer using `ViewModel` for shared data across Fragments and Activities.
- Use interfaces when the Fragment needs to trigger actions in the Activity.

---



2. UI & UX

---

### **1. What is the difference between ConstraintLayout and RelativeLayout?**

| **Aspect**               | **ConstraintLayout**                              | **RelativeLayout**                              |
|--------------------------|--------------------------------------------------|-----------------------------------------------|
| **Definition**            | A flexible layout that allows positioning and sizing views using constraints to other views or parent. | A layout where views are positioned relative to other views or the parent using alignment rules. |
| **Performance**           | Better performance due to a flat view hierarchy (no nested layouts). | May require nested layouts for complex designs, which can lead to poorer performance. |
| **Flexibility**           | More flexible, supports chains, barriers, and guidelines for complex layouts. | Less flexible for complex layouts, relies on simple relative positioning. |
| **Ease of Use**           | Slightly harder to learn initially due to advanced features. | Easier to use for simple layouts. |
| **Use Case**              | Recommended for modern apps requiring complex or responsive designs. | Useful for simple relative positioning but largely replaced by ConstraintLayout. |

#### **Example**:
- **ConstraintLayout**:
  ```xml
  <androidx.constraintlayout.widget.ConstraintLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent">

      <TextView
          android:id="@+id/textView"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Hello, World!"
          app:layout_constraintTop_toTopOf="parent"
          app:layout_constraintStart_toStartOf="parent" />

      <Button
          android:id="@+id/button"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Click Me"
          app:layout_constraintTop_toBottomOf="@id/textView"
          app:layout_constraintStart_toStartOf="parent" />
  </androidx.constraintlayout.widget.ConstraintLayout>
  ```

- **RelativeLayout**:
  ```xml
  <RelativeLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent">

      <TextView
          android:id="@+id/textView"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Hello, World!"
          android:layout_alignParentTop="true"
          android:layout_alignParentStart="true" />

      <Button
          android:id="@+id/button"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="Click Me"
          android:layout_below="@id/textView"
          android:layout_alignParentStart="true" />
  </RelativeLayout>
  ```

---

### **2. How does ViewBinding differ from findViewById() and DataBinding?**

| **Aspect**                | **ViewBinding**                                  | **findViewById()**                              | **DataBinding**                              |
|---------------------------|-------------------------------------------------|-----------------------------------------------|---------------------------------------------|
| **Purpose**               | Provides type-safe access to views in your layout. | Finds views by their ID in the layout.         | Binds UI components to data sources with two-way binding. |
| **Ease of Use**           | Simplifies view access, avoids null pointer exceptions. | Manual and error-prone, can lead to runtime issues if IDs change. | Complex but powerful for MVVM architecture. |
| **Two-Way Binding**       | Not supported.                                  | Not supported.                                | Supported using `@={}` syntax.             |
| **Performance**           | Lightweight and faster than DataBinding.         | Lightweight but requires manual casting.       | Slightly slower due to data binding overhead. |
| **Use Case**              | Recommended for modern apps with simple view binding needs. | Suitable for small, simple apps.              | Ideal for apps using MVVM or complex UI interactions. |

#### **Example of ViewBinding**:
1. Enable ViewBinding in `build.gradle`:
   ```gradle
   android {
       viewBinding {
           enabled = true
       }
   }
   ```

2. Access Views:
   ```java
   ActivityMainBinding binding = ActivityMainBinding.inflate(getLayoutInflater());
   setContentView(binding.getRoot());
   binding.textView.setText("Hello, ViewBinding!");
   ```

#### **Example of DataBinding**:
1. Enable DataBinding in `build.gradle`:
   ```gradle
   android {
       dataBinding {
           enabled = true
       }
   }
   ```

2. Use DataBinding in XML:
   ```xml
   <layout xmlns:android="http://schemas.android.com/apk/res/android">
       <data>
           <variable
               name="viewModel"
               type="com.example.MyViewModel" />
       </data>
       <TextView
           android:text="@{viewModel.title}" />
   </layout>
   ```

---

### **3. How do you handle different screen sizes and densities in an Android app?**

#### **Best Practices**:
1. **Use `res/` Qualifiers**:
   - Create layout files for different screen sizes:
     - `res/layout` (default)
     - `res/layout-sw600dp` (for tablets or larger screens).
   - Create drawable resources for different densities:
     - `drawable-mdpi`, `drawable-hdpi`, `drawable-xhdpi`, etc.

2. **Use ConstraintLayout**:
   - Design responsive layouts using constraints, chains, and guidelines.

3. **Use `dimens.xml` for Scalable Dimensions**:
   - Define dimensions in separate files for different screen sizes:
     - `res/values/dimens.xml`
     - `res/values-sw600dp/dimens.xml`.

   ```xml
   <!-- dimens.xml -->
   <dimen name="text_size">16sp</dimen>

   <!-- dimens-sw600dp.xml -->
   <dimen name="text_size">20sp</dimen>
   ```

4. **Use `dp` and `sp` Units**:
   - Use `dp` for layout dimensions and `sp` for font sizes to ensure scaling across devices.

5. **Test on Multiple Devices**:
   - Use the Android Emulator or physical devices with different screen sizes and densities.

---

### **4. What are Snackbar, Toast, and Dialog, and when should you use each?**

| **Aspect**              | **Snackbar**                                   | **Toast**                                     | **Dialog**                                    |
|-------------------------|-----------------------------------------------|---------------------------------------------|---------------------------------------------|
| **Definition**           | A transient message displayed at the bottom of the screen with optional actions. | A brief message displayed on the screen.    | A modal window that blocks interaction until dismissed. |
| **User Interaction**     | Can include an action (e.g., Undo button).    | No interaction; just a message.             | Can include buttons, inputs, or other UI elements. |
| **Duration**             | Short or long; disappears automatically.      | Short or long; disappears automatically.     | Stays visible until explicitly dismissed.   |
| **Use Case**             | For quick feedback with optional action, such as "Deleted item, Undo?". | For brief notifications like "Login successful". | For critical user actions like confirmation or input. |

#### **Examples**:
1. **Snackbar**:
   ```java
   Snackbar.make(findViewById(android.R.id.content), "Item deleted", Snackbar.LENGTH_LONG)
           .setAction("Undo", v -> {
               // Handle undo action
           }).show();
   ```

2. **Toast**:
   ```java
   Toast.makeText(this, "Login Successful", Toast.LENGTH_SHORT).show();
   ```

3. **Dialog**:
   ```java
   new AlertDialog.Builder(this)
       .setTitle("Delete Item")
       .setMessage("Are you sure you want to delete this item?")
       .setPositiveButton("Yes", (dialog, which) -> {
           // Handle delete
       })
       .setNegativeButton("No", null)
       .show();
   ```

---

### **5. How would you implement a ViewPager with tabs using the ViewPager2 component?**

#### **Steps to Implement ViewPager2 with Tabs**:

1. **Add Dependencies**:
   Add the required dependencies in `build.gradle`:
   ```gradle
   implementation 'androidx.viewpager2:viewpager2:1.1.0-beta01'
   implementation 'com.google.android.material:material:1.10.0'
   ```

2. **Create Tab Fragments**:
   Create fragments for each tab (e.g., `TabFragment1`, `TabFragment2`).

   ```java
   public class TabFragment1 extends Fragment {
       @Nullable
       @Override
       public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
           return inflater.inflate(R.layout.fragment_tab1, container, false);
       }
   }
   ```

3. **Set Up ViewPager2 Adapter**:
   Create an adapter for the ViewPager2:
   ```java
   public class ViewPagerAdapter extends FragmentStateAdapter {
       public ViewPagerAdapter(@NonNull FragmentActivity fragmentActivity) {
           super(fragmentActivity);
       }

       @NonNull
       @Override
       public Fragment createFragment(int position) {
           switch (position) {
               case 0:
                   return new TabFragment1();
               case 1:
                   return new TabFragment2();
               default:
                   return new TabFragment1();
           }
       }

       @Override
       public int getItemCount() {
           return 2; // Number of tabs
       }
   }
   ```

4. **Set Up ViewPager2 and TabLayout**:
   In your Activity/Fragment:
   ```java
   ViewPager2 viewPager = findViewById(R.id.viewPager);
   TabLayout tabLayout = findViewById(R.id.tabLayout);

   ViewPagerAdapter adapter = new ViewPagerAdapter(this);
   viewPager.setAdapter(adapter);

   new TabLayoutMediator(tabLayout, viewPager, (tab, position) -> {
       switch (position) {
           case 0:
               tab.setText("Tab 1");
               break;
           case 1:
               tab.setText("Tab 2");
               break;
       }
   }).attach();
   ```

5. **Define Layout**:
   ```xml
   <com.google.android.material.tabs.TabLayout
       android:id="@+id/tabLayout"
       android:layout_width="match_parent"
       android:layout_height="wrap_content" />

   <androidx.viewpager2.widget.ViewPager2
       android:id="@+id/viewPager"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

---



3. Data Storage & Room Database
Here are detailed answers to your queries:

---

### **1. What is the difference between SharedPreferences, Room, and SQLite in Android?**

| **Feature**                 | **SharedPreferences**                                | **Room**                                            | **SQLite**                                         |
|-----------------------------|----------------------------------------------------|---------------------------------------------------|--------------------------------------------------|
| **Purpose**                  | Key-value storage for simple data (e.g., user preferences, flags). | Abstraction over SQLite for structured data storage using an object-oriented approach. | Low-level database for structured data storage.  |
| **Use Case**                 | Storing small key-value pairs.                     | Storing relational data with modern, lifecycle-aware APIs. | Storing relational data with raw SQL queries.    |
| **Ease of Use**              | Very simple API.                                   | High-level abstraction, integrates with LiveData and Kotlin Coroutines. | Requires manual implementation of SQL queries and schema management. |
| **Data Structure**           | Flat key-value pairs.                              | Entities, DAOs, and RoomDatabase classes.         | Tables, rows, and raw SQL queries.              |
| **Performance**              | Lightweight and fast for small data.               | Optimized with compile-time validation of queries. | Manual optimizations required.                  |
| **Migration Support**        | Not applicable.                                    | Built-in support for schema migrations.           | Requires manual schema migration.               |

---

### **2. How do you insert and retrieve data using Room Database?**

#### **Step-by-Step Implementation**:

1. **Add Room Dependencies**:
   Add the following dependencies in your `build.gradle`:
   ```gradle
   implementation "androidx.room:room-runtime:2.5.0"
   annotationProcessor "androidx.room:room-compiler:2.5.0"
   // For Kotlin projects
   kapt "androidx.room:room-compiler:2.5.0"
   ```

2. **Define an Entity**:
   An entity represents a table in the database.
   ```java
   @Entity(tableName = "user_table")
   public class User {
       @PrimaryKey(autoGenerate = true)
       public int id;

       @ColumnInfo(name = "name")
       public String name;

       @ColumnInfo(name = "email")
       public String email;
   }
   ```

3. **Create a DAO (Data Access Object)**:
   A DAO defines methods for accessing the database.
   ```java
   @Dao
   public interface UserDao {
       @Insert
       void insert(User user);

       @Query("SELECT * FROM user_table WHERE id = :id")
       User getUserById(int id);

       @Query("SELECT * FROM user_table")
       List<User> getAllUsers();
   }
   ```

4. **Define the Database**:
   The database class serves as the main access point to the Room database.
   ```java
   @Database(entities = {User.class}, version = 1)
   public abstract class AppDatabase extends RoomDatabase {
       public abstract UserDao userDao();
   }
   ```

5. **Initialize the Database**:
   ```java
   AppDatabase db = Room.databaseBuilder(getApplicationContext(),
           AppDatabase.class, "user_database").build();

   UserDao userDao = db.userDao();
   ```

6. **Insert Data**:
   ```java
   User user = new User();
   user.name = "John Doe";
   user.email = "john.doe@example.com";
   new Thread(() -> userDao.insert(user)).start();
   ```

7. **Retrieve Data**:
   ```java
   new Thread(() -> {
       User user = userDao.getUserById(1);
       Log.d("Room", "User: " + user.name);
   }).start();
   ```

---

### **3. What are DAOs in Room, and why are they important?**

#### **What is a DAO?**
A DAO (Data Access Object) is an interface in Room that provides methods to interact with the database. It abstracts the raw SQL queries and provides a clean API for database operations.

#### **Importance of DAOs**:
1. **Separation of Concerns**:
   - Keeps database logic separate from the rest of the application.
2. **Compile-Time Verification**:
   - Room validates the queries at compile-time, reducing runtime errors.
3. **Simplified Syntax**:
   - Eliminates the need for raw SQL, replacing it with annotations like `@Insert`, `@Query`, `@Update`, and `@Delete`.
4. **Integration with Lifecycle Components**:
   - DAOs work seamlessly with LiveData, Flow, and Coroutines.

#### **Example**:
```java
@Dao
public interface UserDao {
    @Insert
    void insert(User user);

    @Update
    void update(User user);

    @Delete
    void delete(User user);

    @Query("SELECT * FROM user_table")
    List<User> getAllUsers();
}
```

---

### **4. How do you implement database migration in Room?**

#### **What is Database Migration?**
When you update the database schema (e.g., add/remove columns, change table structure), a migration ensures that existing data is preserved.

#### **Steps to Implement Migration**:
1. **Increment the Database Version**:
   Update the `version` parameter in the `@Database` annotation.

   ```java
   @Database(entities = {User.class}, version = 2)
   public abstract class AppDatabase extends RoomDatabase {
       public abstract UserDao userDao();
   }
   ```

2. **Define a Migration**:
   Create a `Migration` object to specify how to handle the schema change.
   ```java
   static final Migration MIGRATION_1_2 = new Migration(1, 2) {
       @Override
       public void migrate(@NonNull SupportSQLiteDatabase database) {
           // Example: Add a new column
           database.execSQL("ALTER TABLE user_table ADD COLUMN age INTEGER DEFAULT 0 NOT NULL");
       }
   };
   ```

3. **Provide the Migration to Room**:
   Pass the migration object when building the database instance.
   ```java
   AppDatabase db = Room.databaseBuilder(getApplicationContext(),
           AppDatabase.class, "user_database")
           .addMigrations(MIGRATION_1_2)
           .build();
   ```

---

### **5. How can you optimize queries in Room for better performance?**

#### **Best Practices for Optimizing Queries in Room**:

1. **Use Paging for Large Datasets**:
   - Implement Room with Paging 3 to load data in chunks instead of retrieving all data at once.
   ```java
   @Query("SELECT * FROM user_table")
   PagingSource<Integer, User> getAllUsersPaged();
   ```

2. **Use Projections**:
   - Retrieve only the required columns instead of fetching entire rows.
   ```java
   @Query("SELECT name FROM user_table WHERE id = :id")
   String getUserNameById(int id);
   ```

3. **Index Columns**:
   - Use the `@Index` annotation on frequently queried columns to improve search performance.
   ```java
   @Entity(tableName = "user_table", indices = {@Index(value = "email", unique = true)})
   public class User {
       @PrimaryKey(autoGenerate = true)
       public int id;

       @ColumnInfo(name = "email")
       public String email;
   }
   ```

4. **Use Transactions**:
   - Group multiple operations into a single transaction to reduce overhead.
   ```java
   @Transaction
   public void insertAndDelete(User userToInsert, User userToDelete) {
       insert(userToInsert);
       delete(userToDelete);
   }
   ```

5. **Leverage LiveData and Flow**:
   - Use LiveData or Flow to observe database changes and avoid unnecessary queries.
   ```java
   @Query("SELECT * FROM user_table")
   LiveData<List<User>> getAllUsers();
   ```

6. **Use SQL Functions**:
   - Use built-in SQL functions (e.g., `COUNT`, `MAX`, etc.) for operations instead of processing data in memory.
   ```java
   @Query("SELECT COUNT(*) FROM user_table")
   int getUserCount();
   ```

7. **Precompile Queries**:
   - Room precompiles queries, so avoid dynamically building queries whenever possible.

8. **Use Room’s Built-in Caching**:
   - Room caches database objects, so avoid unnecessary reloading of the same data.

---


4. Networking & APIs
What are the key differences between Retrofit and Volley?


How do you handle API failures and retry requests in Retrofit?


What is an interceptor in OkHttp, and how can you use it?


How do you implement pagination in a REST API call using Retrofit?


How can you cache network responses in Android?



5. Multithreading & Coroutines
What is the difference between Thread, HandlerThread, and AsyncTask?


How do you launch a coroutine in Android, and what is CoroutineScope?


What is the difference between GlobalScope.launch and viewModelScope.launch?


How do you handle exceptions in Kotlin Coroutines?


What are the differences between suspend functions and regular functions?



6. Jetpack Components
What are the advantages of using LiveData over MutableStateFlow?


How does WorkManager differ from JobScheduler and AlarmManager?


How does Navigation Component help manage fragment transactions?


How do you pass data between fragments using Safe Args?


What is the difference between Hilt and Dagger in dependency injection?



7. Security
How can you store sensitive data securely in an Android app?


What is ProGuard, and how does it help with app security?


How do you implement biometric authentication in an Android app?


What security measures should be taken when making network requests?


How can you prevent decompilation of an APK?



8. Testing & Debugging
What are the differences between unit tests and UI tests?


How do you use Mockito to mock dependencies in tests?


What is Espresso, and how does it help with UI testing?


How do you debug memory leaks in an Android app?


How can you detect and fix an ANR (Application Not Responding) error?



9. Performance Optimization
How do you optimize RecyclerView for smooth scrolling?


What is ViewHolder pattern, and why is it used in RecyclerView?


How do you reduce the memory footprint of images in an Android app?


What are the benefits of using DiffUtil in RecyclerView?


How can you profile and optimize an Android app's performance?



10. Background Work
How do you schedule background tasks in Android?


What is the difference between WorkManager and Foreground Service?


How does Doze Mode affect background services?


How do you implement push notifications using Firebase Cloud Messaging (FCM)?


How do you handle long-running background tasks efficiently?
Here are some additional medium-level Android development questions to expand your knowledge:

1. Android Components & Lifecycle
How do you handle configuration changes without restarting an Activity?


What is the difference between onSaveInstanceState() and ViewModel for saving data?


How do you dynamically add and remove Fragments at runtime?


What is the difference between FragmentTransaction.replace() and FragmentTransaction.add()?


What happens if you don't call super.onCreate() in an Activity?



2. UI & Custom Views
How do you create a custom view in Android?


What is the difference between Canvas and Drawable in Android?


How do you create a BottomSheetDialogFragment?


What is a CoordinatorLayout, and how does it enhance UI behavior?


How do you implement drag-and-drop functionality in an Android app?



3. Data Persistence & Room Database
How do you implement a one-to-many relationship in Room Database?


What is the difference between Flow and LiveData in Room queries?


How do you use transactions in Room Database?


How do you handle a scenario where a database query returns a very large dataset?


What is database indexing, and how does it improve Room performance?



4. Networking & API Handling
How do you handle slow network connections in an Android app?


How do you implement exponential backoff retry in Retrofit?


How do you make parallel network requests in Retrofit?


How does Retrofit handle error responses, and how can you customize it?


What is WebSockets, and how do you implement it in an Android app?



5. Kotlin Coroutines & Multithreading
What is runBlocking, and when should it be used?


What is SupervisorJob(), and how does it differ from a regular Job?


What is the purpose of withContext(Dispatchers.IO)?


How do you cancel a coroutine safely in Android?


What is the difference between launch and async in Kotlin Coroutines?



6. Jetpack Components & Modern Android Development
What are the advantages of using ViewModel over onSaveInstanceState()?


How do you handle navigation between screens using Jetpack Navigation Component?


What are the key benefits of using Jetpack Paging 3?


How do you migrate from SharedPreferences to Jetpack DataStore?


What is WorkManager, and how does it handle background tasks differently than Services?



7. Dependency Injection & Hilt
What is Dependency Injection, and why is it used?


How does Hilt simplify Dependency Injection compared to Dagger?


What is the difference between @Inject, @Provides, and @Binds in Hilt?


How do you handle dependency injection for ViewModels using Hilt?


How do you inject dependencies into a WorkManager in Hilt?



8. Performance Optimization
How do you detect and fix memory leaks in an Android app?


What are the best practices for optimizing RecyclerView scrolling performance?


How do you improve UI rendering performance in Android?


What are the benefits of using Lottie for animations instead of GIFs?


How do you reduce APK size using ProGuard and R8?



9. Background Processing & Services
How do you schedule periodic tasks in WorkManager?


What is the difference between Foreground Service and Bound Service?


How do you use JobScheduler for background tasks?


How does Doze Mode affect background processes in Android?


How do you send and receive background push notifications in Firebase?



10. Security & Permissions
What are the best practices for securing API keys in Android apps?


How do you use Android Keystore to encrypt user credentials?


How do you prevent reverse engineering of your APK?


What is SafetyNet, and how does it improve app security?


How do you implement runtime permissions correctly in Android?



11. Testing & Debugging
How do you test ViewModel logic using JUnit and Mockito?


How do you write UI tests using Espresso?


What is Robolectric, and how does it help in testing?


How do you debug an ANR (Application Not Responding) issue?


What are some common tools used to analyze memory leaks in Android?



Would you like explanations or code samples for any of these questions? 🚀






Expert level 


1. Advanced Android Framework
How does the Android Activity lifecycle differ between configuration changes and process death?


Explain the implications of isTaskRoot() in an Android app.


How does Looper and Handler work internally? Why is Looper.prepare() needed in a thread?


What are the advantages and disadvantages of using LiveData vs. StateFlow in Jetpack Compose?


How does the Android system determine which activity to destroy when memory is low?


Explain how WorkManager handles constraints such as network availability and battery conditions.



2. Performance Optimization
How does Android’s ART (Android Runtime) optimize app performance compared to Dalvik?


How would you detect and prevent memory leaks in an Android app?


Explain how the StrictMode class helps improve app performance.


What are the best practices for optimizing RecyclerView performance?


How would you profile an app’s CPU, memory, and rendering performance using Android Studio?



3. Multithreading & Concurrency
How does the ExecutorService framework improve upon traditional AsyncTask?


How would you implement a thread-safe singleton in Kotlin?


What is the difference between Dispatchers.IO, Dispatchers.Default, and Dispatchers.Main in Kotlin Coroutines?


How does Job differ from CoroutineScope in Kotlin coroutines?


Explain how structured concurrency works in Kotlin.



4. Jetpack & Modern Android Development
What are the benefits of using Jetpack DataStore over SharedPreferences?


Explain how Hilt and Dagger differ in dependency injection.


What are the key improvements in Jetpack Compose compared to the XML-based UI?


How does Paging 3 improve memory efficiency when loading large datasets?


How do you manage complex navigation stacks using the Jetpack Navigation component?



5. Database & Persistence
What are the differences between Room, SQLite, and Realm databases in Android?


How does Room ensure type safety and optimize database queries?


Explain how transactions work in Room and their benefits.


What is database migration in Room, and how would you handle it without data loss?


How can you optimize Room queries for large datasets?



6. Security
How would you store API keys securely in an Android app?


What are the differences between Keystore and EncryptedSharedPreferences?


Explain how ProGuard and R8 help protect an Android app from reverse engineering.


How does biometric authentication work in Android?


What measures would you take to prevent man-in-the-middle (MITM) attacks in an Android app?



7. Networking & APIs
How does OkHttp handle connection pooling and request caching?


What are the advantages of using Retrofit over Volley?


How would you implement efficient WebSocket communication in an Android app?


Explain how GraphQL differs from REST and when to use it.


How would you handle API versioning in an Android app?



8. Testing & Debugging
What are the differences between unit tests and instrumentation tests in Android?


How would you mock dependencies in a ViewModel for testing?


What is Espresso, and how does it improve UI testing in Android?


Explain how you would test a coroutine-based function in Kotlin.


How do you debug ANRs (Application Not Responding) errors effectively?



9. Android Internals
How does the Zygote process work in Android?


Explain the Binder IPC mechanism in Android.


How does Android handle background execution restrictions in recent API levels?


What are the different process states in Android, and how does the system manage them?


Explain the difference between Parcelable and Serializable, and which one is recommended.




1. Android Framework & Internals
How does the Android Runtime (ART) differ from Dalvik VM?


What happens internally when you start an Activity using startActivity()?


How does the Zygote process work in Android?


What is the Binder mechanism, and how does it facilitate IPC (Inter-Process Communication)?


How does the Android system handle memory management and garbage collection?



2. Advanced UI & Custom Views
How do you implement a highly optimized, custom ViewGroup?


How do you efficiently handle complex animations using MotionLayout?


How do you create a custom Drawable in Android?


How do you measure, layout, and draw a custom View in Android?


What is the difference between invalidate(), requestLayout(), and postInvalidate()?



3. Performance Optimization & Memory Management
How do you analyze memory leaks using LeakCanary?


How do you use the Android Profiler to diagnose performance issues?


How do you optimize battery usage in an Android app?


How do you avoid excessive object allocations and garbage collection overhead?


What is StrictMode, and how can it help improve app performance?



4. Advanced Multithreading & Coroutines
How do you implement thread pooling in Android?


What is the difference between Dispatchers.IO, Dispatchers.Default, and Dispatchers.Main?


How do you handle coroutine exceptions properly using CoroutineExceptionHandler?


How do you optimize coroutine-based networking to avoid excessive API calls?


What are structured concurrency and cooperative cancellation in Kotlin coroutines?



5. Jetpack Compose & Modern UI Development
How does Jetpack Compose compare with XML-based UI development in terms of performance?


How do you manage state efficiently in Jetpack Compose?


How do you create a custom Composable function with a custom layout modifier?


How do you handle complex animations and transitions in Jetpack Compose?


How do you integrate Jetpack Compose with existing View-based UI?



6. Advanced Dependency Injection & Modularization
How do you implement multi-module architecture in Android for better scalability?


What are the performance implications of dependency injection using Hilt/Dagger?


How do you inject dependencies into Android Services using Hilt?


What are Assisted Injection and Lazy Injection in Dagger/Hilt?


How do you manage dependency injection in a large-scale Android project?



7. Background Processing & Foreground Services
How do you schedule long-running background tasks efficiently in Android?


How does WorkManager ensure task execution, even if the app is killed?


How do you handle foreground services in Android 13+ with the new restrictions?


What is JobIntentService, and when should it be used?


How do you optimize Firebase Cloud Messaging for real-time updates?



8. Security & Reverse Engineering Protection
How do you prevent an APK from being decompiled or modified?


What are DexGuard and R8, and how do they improve app security?


How do you implement root detection in an Android app?


How does SafetyNet help detect device integrity and secure transactions?


What measures can you take to prevent man-in-the-middle attacks in Android?



9. Networking & API Optimization
How do you implement WebSockets efficiently in an Android app?


How do you optimize GraphQL API calls in Android?


What is gRPC, and how does it compare to REST for Android apps?


How do you implement caching for offline support in Retrofit?


What are the best practices for handling API pagination in a large dataset?



10. Advanced Testing & Debugging
How do you implement test-driven development (TDD) in an Android project?


How do you write end-to-end tests using Espresso and UIAutomator?


How do you mock dependencies in complex ViewModels using Mockito and Dagger?


What are the benefits of running tests on Firebase Test Lab?


How do you debug native crashes using the Android NDK and stack traces?







