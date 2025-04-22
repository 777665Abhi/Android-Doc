# Android Development Guide

## Table of Contents
1. [Android Fundamentals](#android-fundamentals)
   - What is Android?
   - Android Architecture
2. [Core Components](#core-components)
   - Activities
   - Services
   - Broadcast Receivers
   - Content Providers
3. [Project Structure](#project-structure)
   - Main Folders
   - Resource Management
   - Build Configuration
4. [Activity & Fragment Lifecycle](#activity--fragment-lifecycle)
   - Activity Lifecycle
   - Fragment Lifecycle
   - Lifecycle Methods
5. [Navigation & Communication](#navigation--communication)
   - Intents
   - Activity-Fragment Communication
   - Navigation Components
6. [User Interface](#user-interface)
   - XML Layouts
   - Layout Types
   - UI Components
7. [Data Storage & Management](#data-storage--management)
   - Local Storage
   - Remote Data
   - Data Synchronization
8. [Performance & Best Practices](#performance--best-practices)
   - Memory Management
   - Battery Efficiency
   - Security
   - Testing

## Android Fundamentals

### What is Android?
**Android** is an **open-source** operating system developed by **Google**, primarily designed for **mobile devices** such as smartphones, tablets, smart TVs, and even wearables.  

- It is based on the **Linux kernel**.  
- Written mainly in **Java, Kotlin, and C++**.  
- Android powers **billions of devices** around the world.  
- It supports a huge ecosystem of **apps via Google Play Store**.

### Android Architecture
Android is structured in **layers**, where each layer interacts with the one above or below it:

#### 1. Linux Kernel (Bottom Layer)  
- Acts as a bridge between hardware and software.  
- Handles **low-level device operations**: memory management, security, drivers, etc.  

#### 2. Hardware Abstraction Layer (HAL)  
- Acts as an interface between the hardware and the higher Android system.  
- Converts function calls from higher layers to hardware-specific commands.

#### 3. Android Runtime (ART)  
- Replaces the older Dalvik VM.  
- Converts bytecode to native instructions using **Ahead-of-Time (AOT)** and **Just-in-Time (JIT)** compilation.  
- Handles garbage collection and app execution.  

#### 4. Native Libraries (C/C++)  
- Includes core libraries like SQLite (database), WebKit (browser engine), OpenGL (graphics), etc.  
- These are used internally or via NDK (Native Development Kit).  

#### 5. Java/Kotlin Libraries & Framework  
- Provide essential APIs (Activity Manager, View System, Location, etc.)  
- Android app developers use these via Java or Kotlin.  

#### 6. Application Framework  
- High-level services that developers use, like:  
  - Activity Manager  
  - Notification Manager  
  - Resource Manager  
  - Content Providers  

#### 7. Applications (Top Layer)  
- These are the actual apps: Gmail, WhatsApp, Camera, etc.  
- Installed apps interact with the OS using SDK & APIs provided in the framework.

## Core Components

The **four main components** of an Android application are:

### Activities
- Represents a **single screen with a user interface (UI)**.
- It's where users **interact** with your app.
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

### Services
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

### Broadcast Receivers
- Listens for **system-wide broadcast events** (e.g., battery low, airplane mode).
- Apps can also **send custom broadcasts**.
- It doesn't display a UI, but can **trigger notifications** or start other components.

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

### Content Providers
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

### Component Comparison
| Component         | Purpose                          | Has UI? |
|------------------|----------------------------------|---------|
| **Activity**      | Represents a screen              | ✅ Yes  |
| **Service**       | Background processing            | ❌ No   |
| **BroadcastReceiver** | Listens/responds to system events | ❌ No   |
| **ContentProvider**   | Shares app data with others       | ❌ No   |

## Project Structure

### Main Folders
An Android project follows a specific directory structure. Here are the main folders and their purposes:

1. **`src/main/java`**:
   - Contains the Java or Kotlin source code for your app
   - Includes Activities, ViewModels, Adapters, and other logical components
   - Organized by package structure

2. **`src/main/res`**:
   - Contains all app resources (layouts, images, strings, etc.)
   - Organized into type-specific subfolders

3. **`src/main/AndroidManifest.xml`**:
   - Configuration file for app components and metadata
   - Defines Activities, Services, permissions, themes, etc.

4. **`build/`**:
   - Contains build-generated files
   - Not manually modified

5. **`gradle/`**:
   - Contains Gradle wrapper files
   - Manages build system configuration

6. **`libs/`**:
   - Stores external library files (`.jar` or `.aar`)

7. **`src/test/`** and **`src/androidTest/`**:
   - Contains unit tests and instrumented tests

### Resource Management
The **`res` (resources)** folder contains all non-code assets, organized into subfolders:

1. **`res/drawable`**:
   - XML drawable files and images
   - UI graphics and icons

2. **`res/layout`**:
   - XML files defining UI layouts
   - Activity and Fragment layouts

3. **`res/values`**:
   - `strings.xml`: Text strings
   - `colors.xml`: Color definitions
   - `dimens.xml`: Dimensions
   - `styles.xml`: Themes and styles

4. **`res/mipmap`**:
   - App launcher icons
   - Different density versions

5. **`res/raw`**:
   - Raw resource files
   - Audio, video, or other binary files

6. **`res/menu`**:
   - Menu definitions
   - Options and context menus

### Build Configuration
The build system in Android uses Gradle, with configuration at two levels:

#### Project-Level `build.gradle`:
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

#### Module-Level `build.gradle`:
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
```

## Activity & Fragment Lifecycle

### Activity Lifecycle
Activities go through various states during their lifetime:

#### Lifecycle Methods
1. **`onCreate()`**
   - Called when Activity is first created
   - Used for initial setup (layout inflation, variable initialization)
   - Only called once in the Activity lifecycle

2. **`onStart()`**
   - Called when Activity becomes visible
   - Good place to start UI updates

3. **`onResume()`**
   - Activity is in the foreground
   - User can interact with the Activity
   - Good place to start animations or acquire resources

4. **`onPause()`**
   - Activity is partially visible but not focused
   - Save data and stop animations
   - Must complete quickly

5. **`onStop()`**
   - Activity is no longer visible
   - Release heavy resources

6. **`onDestroy()`**
   - Activity is being destroyed
   - Clean up any remaining resources

#### Lifecycle Diagram
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
      Activity no longer visible
                       |
                       v
               +--------------+
               |   onStop()   |
               +--------------+
                       |
     Activity is finishing
                       |
                       v
              +----------------+
              |  onDestroy()   |
              +----------------+
```

### Fragment Lifecycle
Fragments have a more complex lifecycle as they depend on both their host Activity's lifecycle and their own lifecycle events.

#### Fragment Lifecycle Methods
1. **`onAttach()`**
   - Fragment is attached to an Activity
   - Access to Activity context

2. **`onCreate()`**
   - Fragment is being created
   - Initialize non-view components

3. **`onCreateView()`**
   - Create and return the Fragment's UI
   - Inflate layout and initialize views

4. **`onViewCreated()`**
   - Called after onCreateView()
   - View hierarchy is created
   - Safe to access views

5. **`onStart()`**, **`onResume()`**, **`onPause()`**, **`onStop()`**
   - Similar to Activity lifecycle methods
   - Dependent on host Activity's state

6. **`onDestroyView()`**
   - View hierarchy is being destroyed
   - Clean up view references

7. **`onDestroy()`**
   - Fragment is being destroyed
   - Clean up resources

8. **`onDetach()`**
   - Fragment is being detached from Activity
   - Clean up Activity references

## Navigation & Communication

### Intents
An Intent is a messaging object used to request an action from another app component.

#### Types of Intents
1. **Explicit Intents**
   - Specify the exact component to start
   - Used for in-app navigation
   ```kotlin
   val intent = Intent(this, SecondActivity::class.java)
   startActivity(intent)
   ```

2. **Implicit Intents**
   - Describe the type of action to perform
   - System finds appropriate component
   ```kotlin
   val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://example.com"))
   startActivity(intent)
   ```

#### Passing Data with Intents
```kotlin
// Sending data
intent.putExtra("key", "value")

// Receiving data
val data = intent.getStringExtra("key")
```

### Activity-Fragment Communication

#### Activity to Fragment
```kotlin
val fragment = MyFragment().apply {
    arguments = Bundle().apply {
        putString("key", "value")
    }
}
```

#### Fragment to Activity
```kotlin
interface FragmentCallback {
    fun onActionPerformed(data: String)
}

class MyFragment : Fragment() {
    private var callback: FragmentCallback? = null
    
    override fun onAttach(context: Context) {
        super.onAttach(context)
        callback = context as? FragmentCallback
    }
}
```

## User Interface

### XML Layouts
XML layouts define the user interface of app screens:

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

### Layout Types
| Layout Type          | Description |
|----------------------|-------------|
| **LinearLayout**     | Single row or column arrangement |
| **RelativeLayout**   | Position relative to other elements |
| **ConstraintLayout** | Complex UIs with flat view hierarchies |
| **FrameLayout**      | Single child or stacked views |
| **TableLayout**      | Row and column arrangement |
| **GridLayout**       | Grid-like structure |
| **CoordinatorLayout**| Material design interactions |
| **ScrollView**       | Scrollable content |

## Data Storage & Management

### Local Storage
- SQLite Database
- Room Persistence Library
- Shared Preferences
- File Storage

### Remote Data
- Network Operations
- REST APIs
- Data Synchronization

## Performance & Best Practices

### Memory Management
- Resource cleanup
- Memory leaks prevention
- Bitmap handling

### Battery Efficiency
- Background operations
- Wake locks
- Network efficiency

### Security
- Permissions handling
- Data encryption
- Secure communication

### Testing
- Unit testing
- Integration testing
- UI testing
- Test automation

## Common Questions

### What is Android?
Android is an open-source operating system developed by Google, primarily designed for mobile devices. It's based on the Linux kernel and written mainly in Java, Kotlin, and C++. See the [Android Fundamentals](#android-fundamentals) section for more details.

### What are the four main components of an Android application?
The four main components are:
1. Activities - UI screens
2. Services - Background processes
3. Broadcast Receivers - System event handlers
4. Content Providers - Data sharing
See the [Core Components](#core-components) section for detailed explanations.

### How does the Android build system work?
The Android build system uses Gradle and follows these key steps:

1. **Compilation**
   - Compiles source code
   - Processes resources
   - Generates R.java file

2. **Packaging**
   - Combines compiled files
   - Creates APK/Bundle
   - Signs the package

3. **Deployment**
   - Installs on device/emulator
   - Handles different build variants

### What is the difference between Activity and Fragment?
**Activity:**
- Complete screen or window
- Independent component
- Has its own lifecycle
- Can contain multiple fragments

**Fragment:**
- Portion of UI within an Activity
- Reusable component
- Dependent on Activity
- More flexible for UI compositions

### How do you handle configuration changes?
1. **Save State:**
   ```kotlin
   override fun onSaveInstanceState(outState: Bundle) {
       outState.putString("key", "value")
       super.onSaveInstanceState(outState)
   }
   ```

2. **Restore State:**
   ```kotlin
   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
       savedInstanceState?.getString("key")
   }
   ```

3. **Alternative Methods:**
   - ViewModel
   - onRetainNonConfigurationInstance()
   - Configuration change handling in manifest

### What are the best practices for memory management?
1. **Resource Cleanup**
   - Close cursors
   - Release media players
   - Clear references

2. **Memory Leaks Prevention**
   - Avoid static Activity/Context
   - Use WeakReferences
   - Handle AsyncTask properly

3. **Bitmap Handling**
   - Scale appropriately
   - Recycle when done
   - Use proper decode options

### How do you implement data persistence?
1. **SharedPreferences**
   - Key-value pairs
   - Small data sets
   - App settings

2. **SQLite Database**
   - Structured data
   - Large datasets
   - Complex queries

3. **Room Persistence Library**
   - ORM solution
   - Type safety
   - Compile-time verification

### What are the different types of services?
1. **Foreground Service**
   - Visible to user
   - Higher priority
   - Must show notification

2. **Background Service**
   - No user visibility
   - Lower priority
   - Subject to background limits

3. **Bound Service**
   - Client-server interface
   - Multiple components binding
   - Lifecycle tied to binding

### How do you handle permissions?
1. **Declaration**
   ```xml
   <uses-permission android:name="android.permission.PERMISSION_NAME" />
   ```

2. **Runtime Checking**
   ```kotlin
   if (checkSelfPermission(permission) != PackageManager.PERMISSION_GRANTED) {
       requestPermissions(arrayOf(permission), REQUEST_CODE)
   }
   ```

3. **Result Handling**
   ```kotlin
   override fun onRequestPermissionsResult(
       requestCode: Int,
       permissions: Array<String>,
       grantResults: IntArray
   ) {
       if (requestCode == REQUEST_CODE && 
           grantResults[0] == PackageManager.PERMISSION_GRANTED) {
           // Permission granted
       }
   }
   ```

### What are the different types of Intents?
1. **Explicit Intents**
   - Specific component
   - Within same app
   ```kotlin
   Intent(context, TargetActivity::class.java)
   ```

2. **Implicit Intents**
   - Action-based
   - System chooses handler
   ```kotlin
   Intent(Intent.ACTION_VIEW, Uri.parse("https://example.com"))
   ```

### How do you implement multi-threading?
1. **Coroutines**
   ```kotlin
   lifecycleScope.launch {
       withContext(Dispatchers.IO) {
           // Background work
       }
   }
   ```

2. **WorkManager**
   ```kotlin
   val work = OneTimeWorkRequestBuilder<MyWorker>().build()
   WorkManager.getInstance(context).enqueue(work)
   ```

3. **AsyncTask (Legacy)**
   - Deprecated in Android 11
   - Replace with Coroutines or WorkManager