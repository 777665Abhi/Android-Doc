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


What is an Activity in Android?


What is the difference between an Activity and a Fragment?


What is an Intent, and how do you use it to navigate between activities?


What is the purpose of the AndroidManifest.xml file?


What is the role of Gradle in an Android project?


How do you run an Android application on a real device?



2. User Interface (UI)
What is an XML layout file in Android?


What are the different types of layouts available in Android?


What is the difference between LinearLayout and RelativeLayout?


How do you display a simple TextView and Button in an Android app?


What is the purpose of findViewById()?


How do you handle button clicks in Android?


What is a RecyclerView, and how is it different from ListView?


How do you change the theme or color scheme of an Android app?



3. Intents & Navigation
What is an explicit intent vs. an implicit intent?


How do you pass data between activities using Intent?


What is the back stack in Android?


How do you open a new activity using an Intent?


What is the purpose of startActivityForResult()?



4. Data Storage
What are SharedPreferences in Android?


How do you store and retrieve a simple key-value pair using SharedPreferences?


What is the difference between Internal Storage and External Storage in Android?


How does SQLite work in Android?


What is the Room database, and why is it recommended over SQLite?



5. Networking
What is an API, and how do you call an API in Android?


What is Retrofit, and why is it commonly used for network calls?


How do you make an HTTP request in Android?


What is the purpose of JSON in API communication?


What is OkHttp, and how does it help in networking?



6. Multithreading
What is a thread in Android?


What is the difference between a UI thread and a background thread?


Why should network operations not be performed on the main thread?


What is an AsyncTask, and why is it discouraged?


What are Kotlin Coroutines, and how do they improve background tasks?



7. Jetpack Components
What is ViewModel, and why is it used?


What is LiveData, and how does it work?


What is Navigation Component, and how does it simplify navigation?


What is WorkManager, and when should it be used?


What is the difference between DataBinding and ViewBinding?



8. Firebase & Notifications
What is Firebase, and how can it be used in an Android app?


How do you integrate Firebase Authentication into an Android app?


What is Firebase Realtime Database, and how does it work?


How do you send push notifications using Firebase Cloud Messaging (FCM)?



9. Permissions & Security
How do you request permissions in Android (e.g., camera, location)?


What is the difference between runtime permissions and manifest permissions?


How do you handle denied permissions in Android?


What is ProGuard, and how does it help in security?


How do you store sensitive data securely in an Android app?



10. Debugging & Testing
How do you debug an Android application using Logcat?


What is Logcat, and how do you use it for debugging?


How do you set breakpoints in Android Studio?


What is unit testing, and how do you write a basic test case?


What is Espresso, and how does it help in UI testing?

11. Android Project Structure
What are the main folders in an Android project, and what is their purpose?


What is the res folder used for in an Android project?


What is the purpose of the build.gradle file?


What is the difference between res/drawable, res/mipmap, and res/raw folders?


How do you add an image or icon to an Android project?



12. Activity & Fragment Lifecycle
What are the different states of an Activity lifecycle?


What happens when you rotate the screen in Android?


How do you save and restore UI state in Android?


What are the lifecycle methods of a Fragment?


How do you replace one Fragment with another dynamically?



13. UI Components & Customization
What is the difference between match_parent and wrap_content?


How do you change the background color of a Button programmatically?


How do you create a custom Toast message in Android?


What is a Snackbar, and how does it differ from a Toast?


How do you implement a ProgressBar in Android?



14. Event Handling & User Interaction
How do you detect a long press on a Button?


What is the difference between setOnClickListener and setOnLongClickListener?


How do you handle user input using EditText?


How do you create a custom Dialog in Android?


How do you handle gestures like swipe and pinch in an Android app?



15. Navigation & Back Stack
What is the difference between finish() and onBackPressed()?


How do you prevent an Activity from being recreated when the device is rotated?


How do you navigate back to a specific Activity in the back stack?


How do you open a website URL in a browser from an Android app?


What is the difference between startActivity() and startActivityForResult()?



16. Data Persistence & Storage
What is the difference between caching and permanent storage in Android?


How do you store an array of values in SharedPreferences?


What are the advantages of using the Room database instead of SQLite?


How do you read and write files to internal storage?


How do you download and save a file from the internet in Android?



17. Networking & Internet Connectivity
How do you check if the device is connected to the internet?


How do you make a simple HTTP GET request in Android?


What is the difference between synchronous and asynchronous network calls?


How do you parse a JSON response in Android?


How do you load an image from a URL into an ImageView?



18. Background Tasks & Services
What is a Service in Android?


What is the difference between a Foreground Service and a Background Service?


How do you schedule a task to run at a specific time in Android?


What is the purpose of AlarmManager?


How does WorkManager differ from JobScheduler?



19. Firebase & Cloud Integration
How do you add Firebase to an Android project?


What is Firestore, and how is it different from Firebase Realtime Database?


How do you authenticate users using Firebase Authentication?


How do you send a Firebase push notification?


How do you upload an image to Firebase Storage?



20. Permissions & Security
How do you request location permission in Android?


How do you ask for multiple permissions at runtime?


What is the purpose of the Android Keystore System?


How do you prevent unauthorized access to an API key in an Android app?


What security risks should you consider when developing an Android app?



Would you like explanations or code snippets for any of these? 🚀






Medium level


1. Android Components & Lifecycle
What is the difference between onCreate() and onStart() in an Activity?


How does the Fragment lifecycle differ from the Activity lifecycle?


What is the purpose of ViewModel in Android, and how does it survive configuration changes?


What happens if you call finish() inside onCreate()?


How do you handle a scenario where a Fragment needs to communicate with its hosting Activity?



2. UI & UX
What is the difference between ConstraintLayout and RelativeLayout?


How does ViewBinding differ from findViewById() and DataBinding?


How do you handle different screen sizes and densities in an Android app?


What are Snackbar, Toast, and Dialog, and when should you use each?


How would you implement a ViewPager with tabs using the ViewPager2 component?



3. Data Storage & Room Database
What is the difference between SharedPreferences, Room, and SQLite in Android?


How do you insert and retrieve data using Room Database?


What are DAOs in Room, and why are they important?


How do you implement database migration in Room?


How can you optimize queries in Room for better performance?



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







