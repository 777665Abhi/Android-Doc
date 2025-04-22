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
9. [Android Jetpack Components](#android-jetpack-components)
   - 1. Foundation Components
     - A. AppCompat
     - B. Android KTX
     - C. Test
   - 2. Architecture Components
     - A. ViewModel
     - B. LiveData
     - C. Room
     - D. DataStore
   - 3. UI Components
     - A. Compose
     - B. Fragment
     - C. Navigation
   - 4. Behavior Components
     - A. WorkManager
     - B. Paging
     - C. Lifecycle
   - 5. Additional Components
     - A. CameraX
     - B. Security
6. [Media & Graphics](#media--graphics)
   - A. ExoPlayer
   - B. Canvas & Custom Drawing
7. [Performance Optimization](#performance-optimization)
   - A. Memory Profiling
   - B. Network Optimization
8. [Firebase Integration](#firebase-integration)
   - A. Cloud Messaging (FCM)
   - B. Crashlytics
9. [Modern Android Architecture](#modern-android-architecture)
   - A. Clean Architecture with MVI
   - B. Dependency Injection with Koin
10. [Modern UI Patterns](#modern-ui-patterns)
    - A. Motion Layout
    - B. Material Design 3

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

## Android Jetpack Components

### 1. Foundation Components

#### A. AppCompat
- Provides backward compatibility for newer Android features
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // Use MaterialToolbar with AppCompat
        val toolbar = findViewById<MaterialToolbar>(R.id.toolbar)
        setSupportActionBar(toolbar)
    }
}
```

#### B. Android KTX
- Kotlin extensions for concise and idiomatic code
```kotlin
// Without KTX
sharedPreferences
    .edit()
    .putString("key", "value")
    .apply()

// With KTX
sharedPreferences.edit {
    putString("key", "value")
}
```

#### C. Test
- Testing frameworks and rules
```kotlin
@RunWith(AndroidJUnit4::class)
class ExampleInstrumentedTest {
    @get:Rule
    val activityRule = ActivityScenarioRule(MainActivity::class.java)
    
    @Test
    fun testExample() {
        onView(withId(R.id.button))
            .perform(click())
            .check(matches(isDisplayed()))
    }
}
```

### 2. Architecture Components

#### A. ViewModel
- Manages UI-related data in a lifecycle-conscious way
```kotlin
@HiltViewModel
class UserViewModel @Inject constructor(
    private val repository: UserRepository
) : ViewModel() {
    private val _users = MutableStateFlow<List<User>>(emptyList())
    val users: StateFlow<List<User>> = _users.asStateFlow()
    
    fun loadUsers() {
        viewModelScope.launch {
            repository.getUsers()
                .catch { error -> _users.emit(emptyList()) }
                .collect { users -> _users.emit(users) }
        }
    }
}
```

#### B. LiveData
- Lifecycle-aware observable data holder
```kotlin
class UserViewModel : ViewModel() {
    private val _user = MutableLiveData<User>()
    val user: LiveData<User> = _user

    fun updateUser(user: User) {
        _user.value = user
    }
}
```

#### C. Room
- SQLite database abstraction
```kotlin
@Entity(tableName = "users")
data class User(
    @PrimaryKey val id: String,
    val name: String,
    val email: String
)

@Dao
interface UserDao {
    @Query("SELECT * FROM users")
    fun getAllUsers(): Flow<List<User>>

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun insertUser(user: User)
}

@Database(entities = [User::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```

#### D. DataStore
- Modern data storage solution
```kotlin
class UserPreferences(private val context: Context) {
    private val Context.dataStore by preferencesDataStore("user_preferences")

    val userFlow: Flow<User> = context.dataStore.data
        .catch { exception ->
            emit(emptyPreferences())
        }
        .map { preferences ->
            User(
                id = preferences[USER_ID] ?: "",
                name = preferences[USER_NAME] ?: ""
            )
        }

    suspend fun saveUser(user: User) {
        context.dataStore.edit { preferences ->
            preferences[USER_ID] = user.id
            preferences[USER_NAME] = user.name
        }
    }

    companion object {
        private val USER_ID = stringPreferencesKey("user_id")
        private val USER_NAME = stringPreferencesKey("user_name")
    }
}
```

### 3. UI Components

#### A. Compose
- Modern toolkit for building native UI
```kotlin
@Composable
fun UserList(
    users: List<User>,
    onUserClick: (User) -> Unit
) {
    LazyColumn {
        items(users) { user ->
            UserItem(
                user = user,
                onClick = { onUserClick(user) }
            )
        }
    }
}

@Composable
fun UserItem(
    user: User,
    onClick: () -> Unit
) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp)
            .clickable(onClick = onClick),
        elevation = 4.dp
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(
                text = user.name,
                style = MaterialTheme.typography.h6
            )
            Text(
                text = user.email,
                style = MaterialTheme.typography.body2
            )
        }
    }
}
```

#### B. Fragment
- Modular sections of an activity
```kotlin
class UserFragment : Fragment() {
    private val viewModel: UserViewModel by viewModels()
    
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        return inflater.inflate(R.layout.fragment_user, container, false)
    }
    
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        
        viewLifecycleOwner.lifecycleScope.launch {
            viewLifecycleOwner.repeatOnLifecycle(Lifecycle.State.STARTED) {
                viewModel.users.collect { users ->
                    // Update UI
                }
            }
        }
    }
}
```

#### C. Navigation
- Framework for navigating between destinations
```kotlin
// nav_graph.xml
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/nav_graph"
    app:startDestination="@id/userListFragment">

    <fragment
        android:id="@+id/userListFragment"
        android:name=".UserListFragment">
        <action
            android:id="@+id/toUserDetail"
            app:destination="@id/userDetailFragment">
            <argument
                android:name="userId"
                app:argType="string" />
        </action>
    </fragment>

    <fragment
        android:id="@+id/userDetailFragment"
        android:name=".UserDetailFragment" />
</navigation>

// Usage in Fragment
class UserListFragment : Fragment() {
    private val navController by lazy {
        findNavController()
    }
    
    private fun navigateToDetail(userId: String) {
        val action = UserListFragmentDirections
            .toUserDetail(userId)
        navController.navigate(action)
    }
}
```

### 4. Behavior Components

#### A. WorkManager
- API for background work
```kotlin
@HiltWorker
class SyncWorker @AssistedInject constructor(
    @Assisted context: Context,
    @Assisted params: WorkerParameters,
    private val repository: UserRepository
) : CoroutineWorker(context, params) {
    
    override suspend fun doWork(): Result {
        return try {
            repository.syncUsers()
            Result.success()
        } catch (e: Exception) {
            Result.retry()
        }
    }
}

// Schedule work
class WorkScheduler @Inject constructor(
    private val workManager: WorkManager
) {
    fun scheduleSyncWork() {
        val constraints = Constraints.Builder()
            .setRequiredNetworkType(NetworkType.CONNECTED)
            .build()
            
        val syncRequest = PeriodicWorkRequestBuilder<SyncWorker>(
            repeatInterval = 1,
            repeatIntervalTimeUnit = TimeUnit.HOURS
        )
            .setConstraints(constraints)
            .build()
            
        workManager.enqueueUniquePeriodicWork(
            "sync_work",
            ExistingPeriodicWorkPolicy.KEEP,
            syncRequest
        )
    }
}
```

#### B. Paging
- Load and display pages of data
```kotlin
@Dao
interface UserDao {
    @Query("SELECT * FROM users")
    fun getPagingSource(): PagingSource<Int, User>
}

class UserRepository @Inject constructor(
    private val api: UserApi,
    private val db: AppDatabase
) {
    fun getPagedUsers(): Flow<PagingData<User>> {
        return Pager(
            config = PagingConfig(
                pageSize = 20,
                enablePlaceholders = false
            ),
            remoteMediator = UserRemoteMediator(api, db),
            pagingSourceFactory = { db.userDao().getPagingSource() }
        ).flow
    }
}

@Composable
fun UserList(
    users: LazyPagingItems<User>
) {
    LazyColumn {
        items(users) { user ->
            user?.let {
                UserItem(user = it)
            }
        }
    }
}
```

#### C. Lifecycle
- Manage activity and fragment lifecycles
```kotlin
class MainViewModel : ViewModel() {
    private val _events = MutableSharedFlow<UiEvent>()
    val events = _events.asSharedFlow()
    
    fun processLifecycleEvent(event: Lifecycle.Event) {
        when (event) {
            Lifecycle.Event.ON_RESUME -> {
                // Handle resume
            }
            Lifecycle.Event.ON_PAUSE -> {
                // Handle pause
            }
            else -> { /* Handle other events */ }
        }
    }
}

class MainActivity : AppCompatActivity() {
    private val viewModel: MainViewModel by viewModels()
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        lifecycle.addObserver(LifecycleEventObserver { _, event ->
            viewModel.processLifecycleEvent(event)
        })
    }
}
```

### 5. Additional Components

#### A. CameraX
- Camera app development made easy
```kotlin
class CameraFragment : Fragment() {
    private lateinit var cameraProvider: ProcessCameraProvider
    
    private fun startCamera() {
        val preview = Preview.Builder().build()
        val imageCapture = ImageCapture.Builder().build()
        
        val cameraSelector = CameraSelector.DEFAULT_BACK_CAMERA
        
        cameraProvider.unbindAll()
        cameraProvider.bindToLifecycle(
            viewLifecycleOwner,
            cameraSelector,
            preview,
            imageCapture
        )
    }
    
    private fun takePhoto() {
        val imageCapture = imageCapture ?: return
        
        val photoFile = File(
            outputDirectory,
            "Photo_${System.currentTimeMillis()}.jpg"
        )
        
        val outputOptions = ImageCapture.OutputFileOptions
            .Builder(photoFile)
            .build()
            
        imageCapture.takePicture(
            outputOptions,
            ContextCompat.getMainExecutor(requireContext()),
            object : ImageCapture.OnImageSavedCallback {
                override fun onImageSaved(output: ImageCapture.OutputFileResults) {
                    // Handle saved image
                }
                
                override fun onError(exc: ImageCaptureException) {
                    // Handle error
                }
            }
        )
    }
}
```

#### B. Security
- Security-related features
```kotlin
class SecurityManager(private val context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()
        
    private val encryptedSharedPreferences = EncryptedSharedPreferences.create(
        context,
        "secret_prefs",
        masterKey,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )
    
    private val encryptedFile = EncryptedFile.Builder(
        context,
        File(context.filesDir, "secret.txt"),
        masterKey,
        EncryptedFile.FileEncryptionScheme.AES256_GCM_HKDF_4KB
    ).build()
}
```

## Media & Graphics

### A. ExoPlayer
- Advanced media playback
```kotlin
class VideoPlayerActivity : AppCompatActivity() {
    private lateinit var player: ExoPlayer
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        // Initialize ExoPlayer
        player = ExoPlayer.Builder(this).build()
        
        // Create media item
        val mediaItem = MediaItem.fromUri("https://example.com/video.mp4")
        player.setMediaItem(mediaItem)
        
        // Prepare and play
        player.prepare()
        player.play()
        
        // Handle player events
        player.addListener(object : Player.Listener {
            override fun onPlaybackStateChanged(state: Int) {
                when (state) {
                    Player.STATE_READY -> showPlaybackControls()
                    Player.STATE_BUFFERING -> showLoadingSpinner()
                    Player.STATE_ENDED -> showReplayButton()
                }
            }
        })
    }
    
    override fun onDestroy() {
        super.onDestroy()
        player.release()
    }
}
```

### B. Canvas & Custom Drawing
- Custom graphics and animations
```kotlin
class CustomView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null
) : View(context, attrs) {
    private val paint = Paint().apply {
        color = Color.BLUE
        style = Paint.Style.FILL
        isAntiAlias = true
    }
    
    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        
        // Draw shapes
        canvas.drawCircle(width/2f, height/2f, 100f, paint)
        
        // Draw text
        paint.textSize = 50f
        canvas.drawText("Hello Canvas!", 50f, 50f, paint)
        
        // Draw custom path
        val path = Path().apply {
            moveTo(0f, 0f)
            lineTo(width.toFloat(), height.toFloat())
            close()
        }
        canvas.drawPath(path, paint)
    }
}
```

Key Canvas Features:
- Drawing basic shapes (rectangles, circles, lines)
- Custom paths and curves
- Text rendering
- Transformations (rotate, scale, translate)
- Clipping regions
- Gradients and shaders

## Performance Optimization

### A. Memory Profiling
```kotlin
class MemoryOptimizationExample {
    // Object pooling for frequently created objects
    private val objectPool = ObjectPool(
        maxSize = 50,
        factory = { MyExpensiveObject() }
    )
    
    // Weak references for cache
    private val imageCache = WeakHashMap<String, Bitmap>()
    
    // Memory-efficient collections
    private val sparseArray = SparseArray<MyObject>()
    
    fun loadBitmap(context: Context, imageUrl: String, maxSize: Int) {
        BitmapFactory.Options().run {
            inJustDecodeBounds = true
            BitmapFactory.decodeResource(context.resources, R.drawable.image, this)
            inSampleSize = calculateInSampleSize(this, maxSize, maxSize)
            inJustDecodeBounds = false
            
            val bitmap = BitmapFactory.decodeResource(
                context.resources, 
                R.drawable.image, 
                this
            )
            imageCache[imageUrl] = bitmap
        }
    }
}
```

### B. Network Optimization
```kotlin
class NetworkOptimizer {
    private val cache = Cache(
        directory = File(context.cacheDir, "http_cache"),
        maxSize = 50L * 1024L * 1024L // 50 MiB
    )
    
    private val okHttpClient = OkHttpClient.Builder()
        .cache(cache)
        .addInterceptor { chain ->
            val request = chain.request()
            val response = chain.proceed(request)
            
            val maxAge = 60 // Cache for 1 minute
            response.newBuilder()
                .header("Cache-Control", "public, max-age=$maxAge")
                .removeHeader("Pragma")
                .build()
        }
        .build()
        
    private val imageLoader = ImageLoader.Builder(context)
        .memoryCache {
            MemoryCache.Builder(context)
                .maxSizePercent(0.25)
                .build()
        }
        .diskCache {
            DiskCache.Builder()
                .directory(context.cacheDir.resolve("image_cache"))
                .maxSizePercent(0.02)
                .build()
        }
        .build()
}
```

Best Practices for Performance:
1. Memory Management
   - Use WeakReferences for caching
   - Implement object pooling for expensive objects
   - Clear unused resources promptly
   - Monitor memory leaks using LeakCanary

2. Network Optimization
   - Implement proper caching strategies
   - Use efficient image loading libraries
   - Compress network payloads
   - Implement retry mechanisms with exponential backoff

3. UI Performance
   - Avoid overdraw
   - Use efficient layouts (ConstraintLayout)
   - Implement view recycling
   - Optimize list views with DiffUtil

4. Background Processing
   - Use Coroutines for async operations
   - Implement WorkManager for deferrable tasks
   - Handle configuration changes properly
   - Batch network requests when possible

## Firebase Integration

### A. Cloud Messaging (FCM)
```kotlin
@HiltAndroidApp
class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        Firebase.initialize(this)
    }
}

class MyFirebaseMessagingService : FirebaseMessagingService() {
    override fun onMessageReceived(message: RemoteMessage) {
        super.onMessageReceived(message)
        
        val notification = NotificationCompat.Builder(this, CHANNEL_ID)
            .setContentTitle(message.notification?.title)
            .setContentText(message.notification?.body)
            .setSmallIcon(R.drawable.ic_notification)
            .setAutoCancel(true)
            .build()
            
        NotificationManagerCompat.from(this)
            .notify(NOTIFICATION_ID, notification)
    }
    
    override fun onNewToken(token: String) {
        // Send token to server
    }
}
```

### B. Crashlytics
```kotlin
class CrashReporting {
    fun initializeCrashlytics() {
        Firebase.crashlytics.apply {
            setCustomKey("user_id", getCurrentUserId())
            setCustomKey("build_type", BuildConfig.BUILD_TYPE)
        }
    }
    
    fun logException(exception: Exception) {
        Firebase.crashlytics.recordException(exception)
    }
    
    fun logEvent(event: String, params: Bundle) {
        Firebase.analytics.logEvent(event) {
            param("user_type", "premium")
            param("item_id", "12345")
        }
    }
}
```

### Authentication
Implement Firebase Authentication:

```kotlin
class AuthManager {
    private val auth = Firebase.auth
    
    fun signInWithEmail(email: String, password: String) {
        auth.signInWithEmailAndPassword(email, password)
            .addOnSuccessListener { result ->
                val user = result.user
                // Handle successful sign-in
            }
            .addOnFailureListener { e ->
                // Handle sign-in failure
            }
    }
    
    fun signInWithGoogle(idToken: String) {
        val credential = GoogleAuthProvider.getCredential(idToken, null)
        auth.signInWithCredential(credential)
            .addOnSuccessListener { result ->
                val user = result.user
                // Handle successful Google sign-in
            }
    }
}
```

### Firestore Database
Implement Firestore operations:

```kotlin
class FirestoreManager {
    private val db = Firebase.firestore
    
    fun addUser(user: User) {
        db.collection("users")
            .document(user.id)
            .set(user)
            .addOnSuccessListener {
                // Document added successfully
            }
            .addOnFailureListener { e ->
                // Handle failure
            }
    }
    
    fun getUserUpdates(userId: String) {
        db.collection("users")
            .document(userId)
            .addSnapshotListener { snapshot, e ->
                if (e != null) {
                    // Handle error
                    return@addSnapshotListener
                }
                
                snapshot?.let {
                    val user = it.toObject<User>()
                    // Handle user data update
                }
            }
    }
}
```

### Cloud Storage
Handle file uploads and downloads:

```kotlin
class StorageManager {
    private val storage = Firebase.storage
    private val storageRef = storage.reference
    
    fun uploadImage(uri: Uri, path: String) {
        val imageRef = storageRef.child("images/$path")
        
        imageRef.putFile(uri)
            .addOnProgressListener { taskSnapshot ->
                val progress = (100.0 * taskSnapshot.bytesTransferred) / taskSnapshot.totalByteCount
                // Update upload progress
            }
            .addOnSuccessListener {
                // Get download URL
                imageRef.downloadUrl.addOnSuccessListener { downloadUri ->
                    // Handle successful upload with download URL
                }
            }
    }
    
    fun downloadImage(path: String, maxSize: Long) {
        val imageRef = storageRef.child("images/$path")
        
        imageRef.getBytes(maxSize)
            .addOnSuccessListener { bytes ->
                // Handle successful download
                val bitmap = BitmapFactory.decodeByteArray(bytes, 0, bytes.size)
            }
            .addOnFailureListener {
                // Handle failed download
            }
    }
}
```

### Cloud Messaging (FCM)
Implement push notifications:

```kotlin
class MessagingService : FirebaseMessagingService() {
    override fun onNewToken(token: String) {
        // Send token to server
    }
    
    override fun onMessageReceived(message: RemoteMessage) {
        message.notification?.let { notification ->
            // Create and show notification
            val notificationBuilder = NotificationCompat.Builder(this, CHANNEL_ID)
                .setContentTitle(notification.title)
                .setContentText(notification.body)
                .setSmallIcon(R.drawable.ic_notification)
                .setAutoCancel(true)
            
            NotificationManagerCompat.from(this)
                .notify(NOTIFICATION_ID, notificationBuilder.build())
        }
    }
}
```

Key Firebase Features:
1. Authentication
   - Email/Password authentication
   - Social media integration (Google, Facebook, Twitter)
   - Phone number authentication
   - Anonymous authentication

2. Cloud Firestore
   - Real-time data synchronization
   - Offline data persistence
   - Complex queries and filtering
   - Security rules

3. Cloud Storage
   - Secure file uploads/downloads
   - Progress monitoring
   - Access control
   - Client-side file validation

4. Cloud Messaging
   - Push notifications
   - Topic-based messaging
   - Message targeting
   - Notification channels

5. Analytics
   - User behavior tracking
   - Custom events
   - Conversion tracking
   - Crash reporting

## Modern Android Architecture

### A. Clean Architecture with MVI
```kotlin
// Intent (User Actions)
sealed class UserIntent {
    object LoadUsers : UserIntent()
    data class SearchUser(val query: String) : UserIntent()
    data class DeleteUser(val userId: String) : UserIntent()
}

// State
data class UserState(
    val users: List<User> = emptyList(),
    val isLoading: Boolean = false,
    val error: String? = null
)

// ViewModel
@HiltViewModel
class UserViewModel @Inject constructor(
    private val userRepository: UserRepository
) : ViewModel() {
    private val _state = MutableStateFlow(UserState())
    val state: StateFlow<UserState> = _state.asStateFlow()
    
    fun processIntent(intent: UserIntent) {
        when (intent) {
            is UserIntent.LoadUsers -> loadUsers()
            is UserIntent.SearchUser -> searchUser(intent.query)
            is UserIntent.DeleteUser -> deleteUser(intent.userId)
        }
    }
    
    private fun loadUsers() {
        viewModelScope.launch {
            _state.update { it.copy(isLoading = true) }
            try {
                val users = userRepository.getUsers()
                _state.update { it.copy(users = users, isLoading = false) }
            } catch (e: Exception) {
                _state.update { it.copy(error = e.message, isLoading = false) }
            }
        }
    }
}
```

### B. Dependency Injection with Koin
```kotlin
// Module definition
val appModule = module {
    single { Room.databaseBuilder(get(), AppDatabase::class.java, "app.db").build() }
    single { get<AppDatabase>().userDao() }
    single<UserRepository> { UserRepositoryImpl(get()) }
    viewModel { UserViewModel(get()) }
}

// Application class
class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        startKoin {
            androidContext(this@MyApplication)
            modules(appModule)
        }
    }
}

// Usage in Activity/Fragment
class UserActivity : AppCompatActivity() {
    private val viewModel: UserViewModel by viewModel()
}
```

## Modern UI Patterns

### A. Motion Layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<MotionLayout
    android:id="@+id/motionLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layoutDescription="@xml/scene_animation">

    <ImageView
        android:id="@+id/image"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@drawable/icon" />

</MotionLayout>

<!-- scene_animation.xml -->
<MotionScene>
    <Transition
        motion:constraintSetStart="@+id/start"
        motion:constraintSetEnd="@+id/end"
        motion:duration="1000">
        <OnSwipe
            motion:touchAnchorId="@+id/image"
            motion:touchAnchorSide="bottom"
            motion:dragDirection="dragUp" />
    </Transition>

    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/image"
            android:layout_width="100dp"
            android:layout_height="100dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent" />
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/image"
            android:layout_width="200dp"
            android:layout_height="200dp"
            motion:layout_constraintTop_toTopOf="parent"
            motion:layout_constraintEnd_toEndOf="parent" />
    </ConstraintSet>
</MotionScene>
```

### B. Material Design 3
```kotlin
@Composable
fun MaterialDesign3Example() {
    MaterialTheme(
        colorScheme = dynamicLightColorScheme(LocalContext.current),
        typography = Typography(
            headlineLarge = TextStyle(
                fontSize = 32.sp,
                lineHeight = 40.sp,
                fontWeight = FontWeight.Bold
            )
        )
    ) {
        Surface(
            modifier = Modifier.fillMaxSize(),
            color = MaterialTheme.colorScheme.background
        ) {
            Column(
                modifier = Modifier.padding(16.dp)
            ) {
                Text(
                    text = "Material Design 3",
                    style = MaterialTheme.typography.headlineLarge,
                    color = MaterialTheme.colorScheme.primary
                )
                
                ElevatedButton(
                    onClick = { /* Handle click */ },
                    colors = ButtonDefaults.elevatedButtonColors(
                        containerColor = MaterialTheme.colorScheme.primaryContainer
                    )
                ) {
                    Text("Elevated Button")
                }
                
                Card(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(vertical = 8.dp),
                    colors = CardDefaults.cardColors(
                        containerColor = MaterialTheme.colorScheme.surfaceVariant
                    )
                ) {
                    Text(
                        text = "Card Content",
                        modifier = Modifier.padding(16.dp)
                    )
                }
            }
        }
    }
}
```

These additional topics cover important aspects of modern Android development. Would you like me to:
1. Add more topics (like AR/VR, Android Auto, or Wear OS)?
2. Expand on any particular topic with more examples?
3. Add implementation patterns and advanced usage scenarios?
4. Include troubleshooting guides for common issues?

Let me know what interests you most!

## Android Interview Preparation

### Core Android Concepts

#### 1. Activity Lifecycle Questions

**Q: Explain the complete activity lifecycle**
A: The activity lifecycle consists of 6 main callbacks:
1. `onCreate()`: Called when activity is first created. Initialize essential components.
2. `onStart()`: Activity becomes visible but not interactive.
3. `onResume()`: Activity is visible and interactive.
4. `onPause()`: Activity is partially visible but losing focus.
5. `onStop()`: Activity is no longer visible.
6. `onDestroy()`: Activity is being destroyed.

**Q: What happens when screen rotation occurs?**
A: During screen rotation:
1. Activity is destroyed (`onPause()` → `onStop()` → `onDestroy()`)
2. Activity is recreated (`onCreate()` → `onStart()` → `onResume()`)
3. `onSaveInstanceState()` is called before destruction to save state
4. Saved state bundle is received in `onCreate()` or `onRestoreInstanceState()`

```kotlin
override fun onSaveInstanceState(outState: Bundle) {
    super.onSaveInstanceState(outState)
    outState.putString("key", "value")
}

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    savedInstanceState?.getString("key") // Restore state
}
```

**Q: How to handle configuration changes?**
A: Several approaches:
1. Use ViewModel to retain data:
```kotlin
class MyViewModel : ViewModel() {
    private val data = MutableLiveData<String>()
    // Data survives configuration changes
}
```

2. Use `onSaveInstanceState()`:
```kotlin
override fun onSaveInstanceState(outState: Bundle) {
    super.onSaveInstanceState(outState)
    outState.putParcelable("data", myData)
}
```

3. Add `android:configChanges` in manifest:
```xml
<activity
    android:name=".MainActivity"
    android:configChanges="orientation|screenSize" />
```

**Q: Difference between `onPause()` and `onStop()`**
A:
- `onPause()`: Activity is partially visible but has lost focus. Quick operations only.
- `onStop()`: Activity is completely hidden. Can perform heavy shutdown operations.

**Q: When to use `onSaveInstanceState()`?**
A: Use it to:
1. Save temporary UI state
2. Handle configuration changes
3. Save data before process death
4. Store small amounts of data (avoid large objects)

#### 2. Fragment Lifecycle Questions

**Q: Difference between add() vs replace() in FragmentTransaction**
A:
- `add()`: Adds fragment on top of existing fragments
- `replace()`: Removes existing fragments and adds new one
```kotlin
// Using add()
supportFragmentManager.beginTransaction()
    .add(R.id.container, newFragment)
    .commit()

// Using replace()
supportFragmentManager.beginTransaction()
    .replace(R.id.container, newFragment)
    .commit()
```

**Q: Fragment backstack management**
A: Best practices:
```kotlin
// Add to backstack
supportFragmentManager.beginTransaction()
    .replace(R.id.container, newFragment)
    .addToBackStack(null)
    .commit()

// Pop backstack
supportFragmentManager.popBackStack()

// Clear backstack
supportFragmentManager.popBackStack(null, FragmentManager.POP_BACK_STACK_INCLUSIVE)
```

**Q: Fragment communication patterns**
A: Several approaches:
1. ViewModel sharing:
```kotlin
class SharedViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> = _data
}

// In fragments
private val viewModel: SharedViewModel by activityViewModels()
```

2. Interface callback:
```kotlin
interface FragmentCallback {
    fun onDataPassed(data: String)
}

class FragmentA : Fragment() {
    private var callback: FragmentCallback? = null
    
    override fun onAttach(context: Context) {
        super.onAttach(context)
        callback = context as? FragmentCallback
    }
}
```

3. Fragment Result API:
```kotlin
// Sender fragment
setFragmentResult("requestKey", bundleOf("data" to "value"))

// Receiver fragment
setFragmentResultListener("requestKey") { key, bundle ->
    val result = bundle.getString("data")
}
```

#### 3. Services Questions

**Q: Types of services and their differences**
A:
1. Foreground Service:
```kotlin
class ForegroundService : Service() {
    override fun onCreate() {
        super.onCreate()
        startForeground(NOTIFICATION_ID, createNotification())
    }
}
```

2. Background Service:
```kotlin
class BackgroundService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // Do background work
        return START_STICKY
    }
}
```

3. Bound Service:
```kotlin
class BoundService : Service() {
    private val binder = LocalBinder()
    
    inner class LocalBinder : Binder() {
        fun getService(): BoundService = this@BoundService
    }
    
    override fun onBind(intent: Intent): IBinder = binder
}
```

**Q: Service lifecycle**
A: Main callbacks:
1. `onCreate()`: Service is created
2. `onStartCommand()`: Service is started
3. `onBind()`: Client binds to service
4. `onUnbind()`: All clients unbind
5. `onDestroy()`: Service is destroyed

**Q: When to use IntentService vs Service**
A:
- IntentService (Deprecated):
  - Automatically handles background threading
  - Stops itself when work is done
  - Sequential work queue

- Service:
  - More flexible
  - Requires manual threading
  - Must manage its own lifecycle

Modern alternative - WorkManager:
```kotlin
class MyWorker(context: Context, params: WorkerParameters) : Worker(context, params) {
    override fun doWork(): Result {
        // Do background work
        return Result.success()
    }
}

// Schedule work
WorkManager.getInstance(context)
    .enqueueUniqueWork(
        "work_name",
        ExistingWorkPolicy.REPLACE,
        OneTimeWorkRequestBuilder<MyWorker>().build()
    )
```

#### 4. Broadcast Receivers Questions

**Q: Types of broadcasts**
A:
1. Normal Broadcasts:
```kotlin
// Send broadcast
context.sendBroadcast(Intent("ACTION_NAME"))

// Receive broadcast
class MyReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        // Handle broadcast
    }
}
```

2. Ordered Broadcasts:
```kotlin
// Send ordered broadcast
context.sendOrderedBroadcast(
    Intent("ACTION_NAME"),
    null, // Permission
    MyResultReceiver(),
    null, // Handler
    Activity.RESULT_OK,
    null, // Initial data
    null  // Initial extras
)
```

**Q: Dynamic vs Static receivers**
A:
1. Dynamic (In code):
```kotlin
private val receiver = MyReceiver()

override fun onResume() {
    super.onResume()
    registerReceiver(receiver, IntentFilter("ACTION_NAME"))
}

override fun onPause() {
    super.onPause()
    unregisterReceiver(receiver)
}
```

2. Static (In manifest):
```xml
<receiver
    android:name=".MyReceiver"
    android:exported="false">
    <intent-filter>
        <action android:name="ACTION_NAME" />
    </intent-filter>
</receiver>
```

### Architecture & Design Patterns

#### 1. MVVM Architecture Questions

**Q: Explain MVVM components and their responsibilities**
A:
1. Model: Data and business logic
2. View: UI elements and events
3. ViewModel: Mediator between Model and View

```kotlin
// Model
data class User(val id: String, val name: String)

// ViewModel
class UserViewModel : ViewModel() {
    private val _users = MutableStateFlow<List<User>>(emptyList())
    val users = _users.asStateFlow()
    
    fun loadUsers() {
        viewModelScope.launch {
            val result = repository.getUsers()
            _users.value = result
        }
    }
}

// View
class UserFragment : Fragment() {
    private val viewModel: UserViewModel by viewModels()
    
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        
        viewLifecycleOwner.lifecycleScope.launch {
            viewModel.users.collect { users ->
                // Update UI
            }
        }
    }
}
```

#### 2. Clean Architecture Questions

**Q: Explain the layers in Clean Architecture**
A: Clean Architecture has three main layers:
1. Presentation Layer (UI):
```kotlin
class UserViewModel(private val getUsersUseCase: GetUsersUseCase) : ViewModel()
```

2. Domain Layer (Business Logic):
```kotlin
class GetUsersUseCase(private val repository: UserRepository) {
    suspend operator fun invoke(): List<User> = repository.getUsers()
}
```

3. Data Layer (Data Sources):
```kotlin
class UserRepositoryImpl(
    private val api: UserApi,
    private val dao: UserDao
) : UserRepository {
    override suspend fun getUsers(): List<User> {
        return api.getUsers().map { it.toDomain() }
    }
}
```

**Q: Benefits of Clean Architecture**
A:
1. Separation of concerns
2. Testability
3. Maintainability
4. Independence of frameworks
5. Independence of UI

#### 3. Design Patterns Questions

**Q: Singleton pattern implementation**
A:
```kotlin
// Object declaration (Kotlin)
object MySingleton {
    fun doSomething() {}
}

// Traditional singleton (Java-style)
class MySingleton private constructor() {
    companion object {
        @Volatile
        private var instance: MySingleton? = null
        
        fun getInstance(): MySingleton {
            return instance ?: synchronized(this) {
                instance ?: MySingleton().also { instance = it }
            }
        }
    }
}
```

**Q: Factory pattern implementation**
A:
```kotlin
interface Animal {
    fun makeSound()
}

class Dog : Animal {
    override fun makeSound() = println("Woof!")
}

class Cat : Animal {
    override fun makeSound() = println("Meow!")
}

class AnimalFactory {
    fun createAnimal(type: String): Animal {
        return when (type.lowercase()) {
            "dog" -> Dog()
            "cat" -> Cat()
            else -> throw IllegalArgumentException("Unknown animal type")
        }
    }
}
```

**Q: Observer pattern in Android**
A:
1. Using LiveData:
```kotlin
class MyViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> = _data
    
    fun updateData(newData: String) {
        _data.value = newData
    }
}
```

2. Using Flow:
```kotlin
class MyViewModel : ViewModel() {
    private val _data = MutableStateFlow<String>("")
    val data = _data.asStateFlow()
    
    fun updateData(newData: String) {
        _data.value = newData
    }
}
```

### Memory Management Questions

**Q: Common causes of memory leaks**
A:
1. Static Activity or View references:
```kotlin
// Bad practice
class MyActivity : AppCompatActivity() {
    companion object {
        private lateinit var instance: MyActivity // Memory leak!
    }
}
```

2. Inner classes holding implicit references:
```kotlin
// Bad practice
class MyActivity : AppCompatActivity() {
    private val myRunnable = object : Runnable { // Implicit reference to activity
        override fun run() {
            // Do something
        }
    }
}

// Good practice
class MyActivity : AppCompatActivity() {
    private val myRunnable = Runnable { // No implicit reference
        // Do something
    }
}
```

3. Unregistered listeners:
```kotlin
// Bad practice - listener not unregistered
override fun onDestroy() {
    super.onDestroy()
    // Missing: someObject.removeListener(listener)
}

// Good practice
override fun onDestroy() {
    super.onDestroy()
    someObject.removeListener(listener)
}
```

**Q: How to detect memory leaks**
A:
1. Using LeakCanary:
```gradle
dependencies {
    debugImplementation 'com.squareup.leakcanary:leakcanary-android:2.x'
}
```

2. Using Android Studio Memory Profiler
3. Using Heap Dumps

**Q: WeakReference vs SoftReference**
A:
```kotlin
// WeakReference - collected when no strong references exist
class Cache {
    private val cache = WeakHashMap<String, Bitmap>()
    
    fun put(key: String, bitmap: Bitmap) {
        cache[key] = bitmap
    }
}

// SoftReference - collected only when memory is tight
class Cache {
    private val cache = HashMap<String, SoftReference<Bitmap>>()
    
    fun put(key: String, bitmap: Bitmap) {
        cache[key] = SoftReference(bitmap)
    }
}
```

### Concurrency Questions

**Q: Coroutines vs Threads**
A:
```kotlin
// Thread
Thread {
    // Blocking operation
}.start()

// Coroutine
CoroutineScope(Dispatchers.IO).launch {
    // Suspending operation
}
```

Key differences:
1. Coroutines are lightweight
2. Coroutines support structured concurrency
3. Coroutines have built-in cancellation
4. Coroutines provide better error handling

**Q: Coroutine Scopes**
A:
```kotlin
// Different scopes
class MyViewModel : ViewModel() {
    // Cancelled when ViewModel is cleared
    fun operation1() = viewModelScope.launch {
        // Coroutine operation
    }
}

class MyFragment : Fragment() {
    // Cancelled when fragment's view is destroyed
    fun operation2() = viewLifecycleOwner.lifecycleScope.launch {
        // Coroutine operation
    }
}

// Custom scope
val scope = CoroutineScope(SupervisorJob() + Dispatchers.Main)
```

**Q: Error handling in Coroutines**
A:
```kotlin
// Try-catch
viewModelScope.launch {
    try {
        // Risky operation
    } catch (e: Exception) {
        // Handle error
    }
}

// CoroutineExceptionHandler
val handler = CoroutineExceptionHandler { _, exception ->
    // Handle error
}

viewModelScope.launch(handler) {
    // Risky operation
}

// supervisorScope
supervisorScope {
    launch { // Child 1 - failure doesn't affect siblings
        throw Exception()
    }
    launch { // Child 2 - continues running
        // Operation
    }
}
```

### Data Management Questions

**Q: Room vs SQLite**
A:
Room advantages:
1. Compile-time verification
2. Less boilerplate
3. Easy integration with LiveData/Flow
4. Built-in migration support

```kotlin
// Room implementation
@Entity(tableName = "users")
data class User(
    @PrimaryKey val id: String,
    val name: String
)

@Dao
interface UserDao {
    @Query("SELECT * FROM users")
    fun getUsers(): Flow<List<User>>
    
    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun insertUser(user: User)
}

// SQLite implementation
class DatabaseHelper(context: Context) : SQLiteOpenHelper(context, "database", null, 1) {
    override fun onCreate(db: SQLiteDatabase) {
        db.execSQL("""
            CREATE TABLE users (
                id TEXT PRIMARY KEY,
                name TEXT
            )
        """)
    }
}
```

**Q: Migration strategies**
A:
```kotlin
// Room migration
val MIGRATION_1_2 = object : Migration(1, 2) {
    override fun migrate(database: SupportSQLiteDatabase) {
        database.execSQL("""
            ALTER TABLE users 
            ADD COLUMN age INTEGER NOT NULL DEFAULT 0
        """)
    }
}

Room.databaseBuilder(context, AppDatabase::class.java, "database")
    .addMigrations(MIGRATION_1_2)
    .build()
```

**Q: Type converters**
A:
```kotlin
class Converters {
    @TypeConverter
    fun fromTimestamp(value: Long?): Date? {
        return value?.let { Date(it) }
    }
    
    @TypeConverter
    fun dateToTimestamp(date: Date?): Long? {
        return date?.time
    }
}

@Database(entities = [User::class], version = 1)
@TypeConverters(Converters::class)
abstract class AppDatabase : RoomDatabase()
```

### Networking Questions

**Q: Retrofit configuration**
A:
```kotlin
// Basic setup
interface ApiService {
    @GET("users")
    suspend fun getUsers(): Response<List<User>>
}

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .client(okHttpClient)
    .build()

val apiService = retrofit.create(ApiService::class.java)

// With interceptors
val okHttpClient = OkHttpClient.Builder()
    .addInterceptor(HttpLoggingInterceptor())
    .addInterceptor { chain ->
        val request = chain.request()
        val response = chain.proceed(request)
        
        val maxAge = 60 // Cache for 1 minute
        response.newBuilder()
            .header("Cache-Control", "public, max-age=$maxAge")
            .removeHeader("Pragma")
            .build()
    }
    .build()
```

**Q: Error handling**
A:
```kotlin
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
}

class Repository(private val api: ApiService) {
    suspend fun getUsers(): Result<List<User>> {
        return try {
            val response = api.getUsers()
            if (response.isSuccessful) {
                Result.Success(response.body()!!)
            } else {
                Result.Error(HttpException(response))
            }
        } catch (e: Exception) {
            Result.Error(e)
        }
    }
}
```

**Q: Caching strategies**
A:
```kotlin
// OkHttp cache
val cache = Cache(
    directory = File(context.cacheDir, "http_cache"),
    maxSize = 50L * 1024L * 1024L // 50 MiB
)

val okHttpClient = OkHttpClient.Builder()
    .cache(cache)
    .addInterceptor { chain ->
        var request = chain.request()
        
        if (!isNetworkAvailable()) {
            request = request.newBuilder()
                .header("Cache-Control", "public, only-if-cached, max-stale=${60 * 60 * 24}")
                .build()
        }
        
        chain.proceed(request)
    }
    .build()
```

### Testing Questions

**Q: Unit Testing ViewModels**
A:
```kotlin
@ExperimentalCoroutinesApi
class UserViewModelTest {
    @get:Rule
    val mainDispatcherRule = MainDispatcherRule()
    
    private lateinit var viewModel: UserViewModel
    private lateinit var repository: FakeUserRepository
    
    @Before
    fun setup() {
        repository = FakeUserRepository()
        viewModel = UserViewModel(repository)
    }
    
    @Test
    fun `load users success`() = runTest {
        // Given
        repository.setUsers(listOf(User("1", "Test")))
        
        // When
        viewModel.loadUsers()
        
        // Then
        assertEquals(viewModel.users.value, listOf(User("1", "Test")))
    }
}
```

**Q: Testing Coroutines**
A:
```kotlin
@ExperimentalCoroutinesApi
class CoroutineTest {
    @get:Rule
    val mainDispatcherRule = MainDispatcherRule()

    private lateinit var viewModel: MyViewModel
    private lateinit var testDispatcher: TestDispatcher

    @Before
    fun setup() {
        testDispatcher = StandardTestDispatcher()
        Dispatchers.setMain(testDispatcher)
        viewModel = MyViewModel()
    }

    @After
    fun tearDown() {
        Dispatchers.resetMain()
    }

    @Test
    fun `test coroutine operation`() = runTest {
        // Given
        val expected = "Result"

        // When
        viewModel.performOperation()
        testDispatcher.scheduler.advanceUntilIdle()

        // Then
        assertEquals(expected, viewModel.result.value)
    }
}

class MainDispatcherRule : TestWatcher() {
    private val testDispatcher = StandardTestDispatcher()

    override fun starting(description: Description) {
        Dispatchers.setMain(testDispatcher)
    }

    override fun finished(description: Description) {
        Dispatchers.resetMain()
    }
}
```

### Performance Optimization Questions

**Q: ANR handling**
A:
1. Move heavy operations off main thread:
```kotlin
// Bad practice
fun onButtonClick() {
    // Heavy operation on main thread
    processLargeData()
}

// Good practice
fun onButtonClick() {
    viewModelScope.launch(Dispatchers.IO) {
        // Heavy operation on background thread
        val result = processLargeData()
        withContext(Dispatchers.Main) {
            // Update UI
        }
    }
}
```

2. Use coroutines for async operations
3. Implement proper threading
4. Monitor ANR using Firebase Crashlytics

**Q: Layout optimization**
A:
1. Use ConstraintLayout:
```xml
<ConstraintLayout>
    <TextView
        android:id="@+id/title"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent" />
        
    <TextView
        android:id="@+id/description"
        app:layout_constraintTop_toBottomOf="@id/title"
        app:layout_constraintStart_toStartOf="parent" />
</ConstraintLayout>
```

2. Avoid nested layouts
3. Use `<merge>` tags
4. Use `<include>` for reusable layouts
5. Use ViewStub for conditional layouts

**Q: Memory optimization**
A:
1. Bitmap handling:
```kotlin
fun loadBitmap(context: Context, @DrawableRes resourceId: Int): Bitmap {
    return BitmapFactory.Options().run {
        inJustDecodeBounds = true
        BitmapFactory.decodeResource(context.resources, resourceId, this)
        
        inSampleSize = calculateInSampleSize(this, reqWidth, reqHeight)
        inJustDecodeBounds = false
        
        BitmapFactory.decodeResource(context.resources, resourceId, this)
    }
}
```

2. RecyclerView optimization:
```kotlin
class MyAdapter : RecyclerView.Adapter<MyViewHolder>() {
    // Use DiffUtil
    private val differ = AsyncListDiffer(this, DIFF_CALLBACK)

    companion object {
        private val DIFF_CALLBACK = object : DiffUtil.ItemCallback<Item>() {
            override fun areItemsTheSame(oldItem: Item, newItem: Item): Boolean {
                return oldItem.id == newItem.id
            }

            override fun areContentsTheSame(oldItem: Item, newItem: Item): Boolean {
                return oldItem == newItem
            }
        }
    }

    // ViewHolder pattern
    class ViewHolder(
        private val binding: ItemBinding
    ) : RecyclerView.ViewHolder(binding.root) {
        fun bind(item: Item) {
            binding.apply {
                // Use ViewBinding
                title.text = item.title
                // Load images efficiently
                Glide.with(image)
                    .load(item.imageUrl)
                    .transition(DrawableTransitionOptions.withCrossFade())
                    .into(image)
            }
        }
    }

    // Efficient view recycling
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        return ViewHolder(
            ItemBinding.inflate(
                LayoutInflater.from(parent.context),
                parent,
                false
            )
        )
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        holder.bind(differ.currentList[position])
    }
}
```

### Security Questions

**Q: Encryption methods**
A:
```kotlin
// Encrypt data
fun encrypt(data: String, key: SecretKey): String {
    val cipher = Cipher.getInstance("AES/GCM/NoPadding")
    cipher.init(Cipher.ENCRYPT_MODE, key)
    
    val encrypted = cipher.doFinal(data.toByteArray())
    return Base64.encodeToString(encrypted, Base64.DEFAULT)
}

// Decrypt data
fun decrypt(encryptedData: String, key: SecretKey): String {
    val cipher = Cipher.getInstance("AES/GCM/NoPadding")
    cipher.init(Cipher.DECRYPT_MODE, key)
    
    val decoded = Base64.decode(encryptedData, Base64.DEFAULT)
    return String(cipher.doFinal(decoded))
}
```

**Q: Secure storage**
A:
```kotlin
// Using EncryptedSharedPreferences
class SecureStorage(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()

    private val prefs = EncryptedSharedPreferences.create(
        context,
        "secret_prefs",
        masterKey,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )

    fun saveSecureData(key: String, value: String) {
        prefs.edit().putString(key, value).apply()
    }

    fun getSecureData(key: String): String? {
        return prefs.getString(key, null)
    }
}

// Using EncryptedFile
class SecureFileStorage(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()

    fun writeSecureFile(fileName: String, data: String) {
        val file = File(context.filesDir, fileName)
        val encryptedFile = EncryptedFile.Builder(
            context,
            file,
            masterKey,
            EncryptedFile.FileEncryptionScheme.AES256_GCM_HKDF_4KB
        ).build()

        encryptedFile.openFileOutput().use { outputStream ->
            outputStream.write(data.toByteArray())
        }
    }
}
```

**Q: Certificate pinning**
A:
```kotlin
val certificatePinner = CertificatePinner.Builder()
    .add("api.example.com", "sha256/XXXX=")
    .build()

val okHttpClient = OkHttpClient.Builder()
    .certificatePinner(certificatePinner)
    .build()
```

### Modern Android Development Questions

**Q: Compose vs XML layouts**
A:
Compose advantages:
1. Less boilerplate
2. Preview support
3. State management
4. Reusable components

```kotlin
// XML layout
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">
    
    <TextView
        android:id="@+id/title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
        
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
</LinearLayout>

// Compose equivalent
@Composable
fun MyScreen() {
    Column {
        Text(text = "Title")
        Button(onClick = { /* Handle click */ }) {
            Text("Click me")
        }
    }
}
```

**Q: State management in Compose**
A:
```kotlin
// ViewModel state
class MyViewModel : ViewModel() {
    private val _state = MutableStateFlow(UiState())
    val state = _state.asStateFlow()
}

// Composable state
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increment")
        }
    }
}

// State hoisting
@Composable
fun StatefulCounter() {
    var count by remember { mutableStateOf(0) }
    StatelessCounter(count = count, onIncrement = { count++ })
}

@Composable
fun StatelessCounter(count: Int, onIncrement: () -> Unit) {
    Column {
        Text("Count: $count")
        Button(onClick = onIncrement) {
            Text("Increment")
        }
    }
}
```

### Behavioral Questions

**Q: How do you handle technical disagreements in a team?**
A: Approach:
1. Listen to all perspectives
2. Focus on data and facts
3. Consider trade-offs
4. Propose compromises
5. Document decisions and reasoning

**Q: Describe a challenging bug you fixed**
A: Structure the answer:
1. Context: What was the bug?
2. Impact: Who was affected?
3. Investigation: How did you debug?
4. Solution: How did you fix it?
5. Prevention: What measures were put in place?

**Q: How do you stay updated with Android development?**
A: Methods:
1. Official Android documentation
2. Android Developer blog
3. Tech conferences
4. Online courses
5. Open source projects
6. Tech podcasts
7. Android community forums

Remember these key points during interviews:
1. Always provide examples
2. Explain your reasoning
3. Consider trade-offs
4. Show problem-solving approach
5. Demonstrate best practices
6. Keep up with latest Android developments

### Additional Interview Questions

#### 1. Kotlin-Specific Questions

**Q: What are the advantages of Kotlin over Java?**
A:
1. Null safety
2. Extension functions
3. Data classes
4. Smart casts
5. Coroutines support
6. Property delegation
7. Higher-order functions

```kotlin
// Null safety
val nullableName: String? = null
val length = nullableName?.length ?: 0

// Extension functions
fun String.addHello(): String = "Hello $this"
"World".addHello() // Returns "Hello World"

// Data class
data class User(
    val id: String,
    val name: String,
    val email: String
)

// Smart cast
when (value) {
    is String -> value.length // Automatically cast to String
    is Int -> value.toString()
}

// Property delegation
class Example {
    var name: String by Delegates.observable("") { _, old, new ->
        println("Name changed from $old to $new")
    }
}
```

**Q: Explain Kotlin's scope functions**
A:
```kotlin
// let - operates on nullable objects
nullableObject?.let { obj ->
    // Use obj safely here
}

// with - groups operations on an object
with(user) {
    name = "John"
    email = "john@example.com"
    save()
}

// run - combines let and with
user?.run {
    name = "John"
    email = "john@example.com"
    save()
}

// apply - object configuration
val user = User().apply {
    name = "John"
    email = "john@example.com"
}

// also - additional operations
user.also {
    println("User created: ${it.name}")
}
```

#### 2. Android Architecture Components

**Q: Explain the difference between LiveData and StateFlow**
A:
```kotlin
// LiveData
class MyViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> = _data

    fun updateData(newData: String) {
        _data.value = newData // Main thread only
        _data.postValue(newData) // Any thread
    }
}

// StateFlow
class MyViewModel : ViewModel() {
    private val _data = MutableStateFlow<String>("")
    val data = _data.asStateFlow()

    fun updateData(newData: String) {
        _data.value = newData // Thread-safe
    }
}

// Collection in Activity/Fragment
class MyFragment : Fragment() {
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        
        // LiveData
        viewModel.data.observe(viewLifecycleOwner) { data ->
            // Handle data
        }
        
        // StateFlow
        viewLifecycleOwner.lifecycleScope.launch {
            viewModel.data.collect { data ->
                // Handle data
            }
        }
    }
}
```

**Q: How does SavedStateHandle work in ViewModel?**
A:
```kotlin
class MyViewModel(private val savedStateHandle: SavedStateHandle) : ViewModel() {
    // Read initial value
    private var count = savedStateHandle.get<Int>("count") ?: 0
        set(value) {
            field = value
            // Save value automatically
            savedStateHandle["count"] = value
        }

    // Using StateFlow with SavedStateHandle
    private val _data = savedStateHandle.getStateFlow("data", "")
    val data = _data.asStateFlow()

    fun updateData(newData: String) {
        savedStateHandle["data"] = newData
    }
}
```

#### 3. Custom Views

**Q: How to create a custom View?**
A:
```kotlin
class CustomView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0
) : View(context, attrs, defStyleAttr) {

    private val paint = Paint(Paint.ANTI_ALIAS_FLAG)
    private var radius = 0f

    init {
        // Read custom attributes
        context.theme.obtainStyledAttributes(
            attrs,
            R.styleable.CustomView,
            0, 0
        ).apply {
            try {
                radius = getDimension(R.styleable.CustomView_radius, 0f)
            } finally {
                recycle()
            }
        }
    }

    override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
        val desiredWidth = suggestedMinimumWidth + paddingLeft + paddingRight
        val desiredHeight = suggestedMinimumHeight + paddingTop + paddingBottom

        setMeasuredDimension(
            resolveSize(desiredWidth, widthMeasureSpec),
            resolveSize(desiredHeight, heightMeasureSpec)
        )
    }

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        canvas.drawCircle(width / 2f, height / 2f, radius, paint)
    }
}
```

#### 4. Android Security

**Q: How to implement secure data storage?**
A:
```kotlin
// Using EncryptedSharedPreferences
class SecureStorage(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()

    private val prefs = EncryptedSharedPreferences.create(
        context,
        "secret_prefs",
        masterKey,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )

    fun saveSecureData(key: String, value: String) {
        prefs.edit().putString(key, value).apply()
    }

    fun getSecureData(key: String): String? {
        return prefs.getString(key, null)
    }
}

// Using EncryptedFile
class SecureFileStorage(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()

    fun writeSecureFile(fileName: String, data: String) {
        val file = File(context.filesDir, fileName)
        val encryptedFile = EncryptedFile.Builder(
            context,
            file,
            masterKey,
            EncryptedFile.FileEncryptionScheme.AES256_GCM_HKDF_4KB
        ).build()

        encryptedFile.openFileOutput().use { outputStream ->
            outputStream.write(data.toByteArray())
        }
    }
}
```

#### 5. WorkManager Scenarios

**Q: How to implement complex work chains with WorkManager?**
A:
```kotlin
class WorkManagerExample(context: Context) {
    private val workManager = WorkManager.getInstance(context)

    fun scheduleComplexWork() {
        // Define work requests
        val uploadWork = OneTimeWorkRequestBuilder<UploadWorker>()
            .setConstraints(
                Constraints.Builder()
                    .setRequiredNetworkType(NetworkType.CONNECTED)
                    .build()
            )
            .build()

        val processWork = OneTimeWorkRequestBuilder<ProcessWorker>()
            .build()

        val notifyWork = OneTimeWorkRequestBuilder<NotifyWorker>()
            .build()

        // Create work chain
        workManager
            .beginUniqueWork(
                "complex_work",
                ExistingWorkPolicy.REPLACE,
                uploadWork
            )
            .then(processWork)
            .then(notifyWork)
            .enqueue()
    }

    // Example Worker
    class UploadWorker(
        context: Context,
        params: WorkerParameters
    ) : CoroutineWorker(context, params) {
        override fun doWork(): Result {
            return try {
                // Do background work
                Result.success()
            } catch (e: Exception) {
                Result.retry()
            }
        }
    }
}
```

#### 6. Android Testing

**Q: How to test Coroutines with different dispatchers?**
A:
```kotlin
@ExperimentalCoroutinesApi
class CoroutineTest {
    @get:Rule
    val mainDispatcherRule = MainDispatcherRule()

    private lateinit var viewModel: MyViewModel
    private lateinit var testDispatcher: TestDispatcher

    @Before
    fun setup() {
        testDispatcher = StandardTestDispatcher()
        Dispatchers.setMain(testDispatcher)
        viewModel = MyViewModel()
    }

    @After
    fun tearDown() {
        Dispatchers.resetMain()
    }

    @Test
    fun `test coroutine operation`() = runTest {
        // Given
        val expected = "Result"

        // When
        viewModel.performOperation()
        testDispatcher.scheduler.advanceUntilIdle()

        // Then
        assertEquals(expected, viewModel.result.value)
    }
}

class MainDispatcherRule : TestWatcher() {
    private val testDispatcher = StandardTestDispatcher()

    override fun starting(description: Description) {
        Dispatchers.setMain(testDispatcher)
    }

    override fun finished(description: Description) {
        Dispatchers.resetMain()
    }
}
```

#### 7. Dependency Injection

**Q: Compare Hilt vs Koin**
A:
```kotlin
// Hilt implementation
@HiltAndroidApp
class MyApplication : Application()

@AndroidEntryPoint
class MainActivity : AppCompatActivity() {
    @Inject
    lateinit var repository: UserRepository
}

@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun provideRepository(
        api: ApiService,
        db: AppDatabase
    ): UserRepository = UserRepositoryImpl(api, db)
}

// Koin implementation
class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        startKoin {
            androidContext(this@MyApplication)
            modules(appModule)
        }
    }
}

val appModule = module {
    single { UserRepositoryImpl(get(), get()) as UserRepository }
    viewModel { UserViewModel(get()) }
}

class MainActivity : AppCompatActivity() {
    private val repository: UserRepository by inject()
}
```

#### 8. App Performance

**Q: How to optimize RecyclerView performance?**
A:
```kotlin
class MyAdapter : RecyclerView.Adapter<MyViewHolder>() {
    // Use DiffUtil
    private val differ = AsyncListDiffer(this, DIFF_CALLBACK)

    companion object {
        private val DIFF_CALLBACK = object : DiffUtil.ItemCallback<Item>() {
            override fun areItemsTheSame(oldItem: Item, newItem: Item): Boolean {
                return oldItem.id == newItem.id
            }

            override fun areContentsTheSame(oldItem: Item, newItem: Item): Boolean {
                return oldItem == newItem
            }
        }
    }

    // ViewHolder pattern
    class ViewHolder(
        private val binding: ItemBinding
    ) : RecyclerView.ViewHolder(binding.root) {
        fun bind(item: Item) {
            binding.apply {
                // Use ViewBinding
                title.text = item.title
                // Load images efficiently
                Glide.with(image)
                    .load(item.imageUrl)
                    .transition(DrawableTransitionOptions.withCrossFade())
                    .into(image)
            }
        }
    }

    // Efficient view recycling
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        return ViewHolder(
            ItemBinding.inflate(
                LayoutInflater.from(parent.context),
                parent,
                false
            )
        )
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        holder.bind(differ.currentList[position])
    }
}
```

#### 9. Jetpack Compose

**Q: How to handle side effects in Compose?**
A:
```kotlin
@Composable
fun SideEffectExample() {
    // LaunchedEffect - for coroutine scoped to composition
    LaunchedEffect(key1 = Unit) {
        // Run suspending operations
    }

    // SideEffect - for non-compose code
    SideEffect {
        // Update non-compose system
    }

    // DisposableEffect - cleanup when leaving composition
    DisposableEffect(key1 = Unit) {
        onDispose {
            // Cleanup
        }
    }

    // rememberCoroutineScope - for launching coroutines from callbacks
    val scope = rememberCoroutineScope()
    Button(onClick = {
        scope.launch {
            // Handle click
        }
    }) {
        Text("Click me")
    }
}

// Recomposition handling
@Composable
fun RecompositionExample() {
    // Remember - preserve value across recompositions
    val count by remember { mutableStateOf(0) }

    // derivedStateOf - computed state
    val isEven by remember {
        derivedStateOf { count.value % 2 == 0 }
    }

    // produceState - convert non-compose state to compose state
    val data by produceState(initialValue = "") {
        value = fetchData()
    }
}
```

#### 10. App Architecture

**Q: How to implement Clean Architecture with MVI pattern?**
A:
```kotlin
// Intent (User Actions)
sealed class UserIntent {
    object LoadUsers : UserIntent()
    data class SearchUser(val query: String) : UserIntent()
    data class DeleteUser(val userId: String) : UserIntent()
}

// State
data class UserState(
    val users: List<User> = emptyList(),
    val isLoading: Boolean = false,
    val error: String? = null
)

// Effect (Side Effects)
sealed class UserEffect {
    data class ShowToast(val message: String) : UserEffect()
    object NavigateToDetails : UserEffect()
}

// ViewModel
@HiltViewModel
class UserViewModel @Inject constructor(
    private val getUsersUseCase: GetUsersUseCase,
    private val deleteUserUseCase: DeleteUserUseCase
) : ViewModel() {
    private val _state = MutableStateFlow(UserState())
    val state = _state.asStateFlow()

    private val _effect = Channel<UserEffect>()
    val effect = _effect.receiveAsFlow()

    fun processIntent(intent: UserIntent) {
        when (intent) {
            is UserIntent.LoadUsers -> loadUsers()
            is UserIntent.SearchUser -> searchUsers(intent.query)
            is UserIntent.DeleteUser -> deleteUser(intent.userId)
        }
    }
    
    private fun loadUsers() {
        viewModelScope.launch {
            _state.update { it.copy(isLoading = true) }
            try {
                val users = getUsersUseCase()
                _state.update { 
                    it.copy(users = users, isLoading = false)
                }
            } catch (e: Exception) {
                _state.update { 
                    it.copy(error = e.message, isLoading = false)
                }
                _effect.send(UserEffect.ShowToast(e.message ?: "Error"))
            }
        }
    }
}
```

Remember these additional key points for interviews:
1. Be prepared to explain architectural decisions
2. Understand the trade-offs of different approaches
3. Know how to handle edge cases
4. Be familiar with latest Android best practices
5. Be able to discuss real-world applications
6. Understand performance implications
7. Consider security aspects
8. Think about testing strategies
9. Be ready to discuss migration approaches
10. Know how to handle backward compatibility

### Trade-offs and Comparisons in Android Development

#### 1. State Management Approaches

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| **LiveData** | - Lifecycle aware<br>- No memory leaks<br>- No boilerplate | - Main thread only<br>- Limited operators<br>- No backpressure handling |
| **StateFlow** | - Thread-safe<br>- Rich operators<br>- Backpressure support | - More boilerplate<br>- Requires coroutine scope<br>- Must set initial value |
| **SharedFlow** | - Multiple observers<br>- Configurable replay<br>- No initial value required | - More complex setup<br>- Higher memory usage<br>- Manual lifecycle handling |

Example Implementation Comparison:
```kotlin
// LiveData
class LiveDataViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> = _data

    fun updateData(value: String) {
        _data.value = value // Must be on main thread
    }
}

// StateFlow
class StateFlowViewModel : ViewModel() {
    private val _data = MutableStateFlow<String>("")
    val data = _data.asStateFlow()

    fun updateData(value: String) {
        _data.value = value // Thread-safe
    }
}

// SharedFlow
class SharedFlowViewModel : ViewModel() {
    private val _events = MutableSharedFlow<String>()
    val events = _events.asSharedFlow()

    fun emitEvent(value: String) {
        viewModelScope.launch {
            _events.emit(value)
        }
    }
}
```

#### 2. UI Development Approaches

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| **XML Layouts** | - Visual editor<br>- Familiar to most developers<br>- Easy to understand | - Inflation cost<br>- Limited dynamic layouts<br>- View hierarchy complexity |
| **Jetpack Compose** | - Declarative UI<br>- Better performance<br>- More dynamic | - Learning curve<br>- New tooling<br>- Limited legacy support |
| **Custom Views** | - Full control<br>- High performance<br>- Complex animations | - More code<br>- Harder to maintain<br>- Manual optimization |

Example Implementation Comparison:
```kotlin
// XML Layout
// layout.xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">
    <TextView
        android:id="@+id/title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
</LinearLayout>

// Activity/Fragment
class MyFragment : Fragment(R.layout.layout) {
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        view.findViewById<Button>(R.id.button).setOnClickListener {
            // Handle click
        }
    }
}

// Jetpack Compose
@Composable
fun MyScreen() {
    Column {
        Text("Title")
        Button(onClick = { /* Handle click */ }) {
            Text("Click me")
        }
    }
}

// Custom View
class CustomView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null
) : View(context, attrs) {
    override fun onDraw(canvas: Canvas) {
        // Custom drawing
    }
}
```

#### 3. Architecture Patterns

| Pattern | Advantages | Disadvantages |
|---------|------------|---------------|
| **MVI** | - Unidirectional data flow<br>- Predictable states<br>- Easy testing | - More boilerplate<br>- Learning curve<br>- Memory overhead |
| **MVVM** | - Clear separation<br>- Lifecycle aware<br>- Good for complex UIs | - Potential overuse<br>- ViewModel bloat<br>- Testing complexity |
| **MVP** | - Simple to understand<br>- Easy testing<br>- Clear contracts | - Tight coupling<br>- Manual lifecycle<br>- More interfaces |

Example Implementation Comparison:
```kotlin
// MVI
sealed class Intent {
    object LoadData : Intent()
    data class UpdateData(val value: String) : Intent()
}

data class State(
    val data: String = "",
    val isLoading: Boolean = false
)

class MviViewModel : ViewModel() {
    private val _state = MutableStateFlow(State())
    val state = _state.asStateFlow()

    fun processIntent(intent: Intent) {
        when (intent) {
            is Intent.LoadData -> loadData()
            is Intent.UpdateData -> updateData(intent.value)
        }
    }
}

// MVVM
class MvvmViewModel : ViewModel() {
    private val _data = MutableLiveData<String>()
    val data: LiveData<String> = _data

    fun loadData() {
        // Load data
    }
}

// MVP
interface MyView {
    fun showData(data: String)
    fun showLoading()
}

class MyPresenter(private val view: MyView) {
    fun loadData() {
        view.showLoading()
        // Load data
        view.showData("Data")
    }
}
```

#### 4. Database Solutions

| Solution | Advantages | Disadvantages |
|----------|------------|---------------|
| **Room** | - Type safety<br>- SQL validation<br>- LiveData/Flow support | - Setup overhead<br>- Migration complexity<br>- Learning curve |
| **SQLite** | - Direct control<br>- No abstraction<br>- Lower overhead | - More boilerplate<br>- Manual SQL<br>- Error-prone |
| **Realm** | - Object-oriented<br>- Real-time updates<br>- Cross-platform | - Different paradigm<br>- Memory usage<br>- Limited queries |

Example Implementation Comparison:
```kotlin
// Room
@Entity(tableName = "users")
data class User(
    @PrimaryKey val id: String,
    val name: String
)

@Dao
interface UserDao {
    @Query("SELECT * FROM users")
    fun getUsers(): Flow<List<User>>
}

// SQLite
class DatabaseHelper(context: Context) : SQLiteOpenHelper(context, "db", null, 1) {
    override fun onCreate(db: SQLiteDatabase) {
        db.execSQL("""
            CREATE TABLE users (
                id TEXT PRIMARY KEY,
                name TEXT
            )
        """)
    }
}

// Realm
class User : RealmObject {
    @PrimaryKey
    var id: String = ""
    var name: String = ""
}

val realm = Realm.getDefaultInstance()
realm.executeTransaction { 
    it.copyToRealm(user)
}
```

#### 5. Network Layer Implementation

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| **Retrofit** | - Type safety<br>- Easy configuration<br>- Coroutines support | - Learning curve<br>- Generated code<br>- Dependency size |
| **OkHttp** | - Full control<br>- Lower level<br>- Interceptors | - More boilerplate<br>- Manual parsing<br>- Complex setup |
| **Ktor** | - Kotlin first<br>- Multiplatform<br>- Flexible | - Less Android-specific<br>- Smaller community<br>- Documentation |

Example Implementation Comparison:
```kotlin
// Retrofit
interface ApiService {
    @GET("users")
    suspend fun getUsers(): List<User>
}

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()

// OkHttp
val client = OkHttpClient.Builder()
    .addInterceptor { chain ->
        val request = chain.request()
        chain.proceed(request)
    }
    .build()

val request = Request.Builder()
    .url("https://api.example.com/users")
    .build()

// Ktor
val client = HttpClient(Android) {
    install(JsonFeature) {
        serializer = KotlinxSerializer()
    }
}

suspend fun getUsers(): List<User> {
    return client.get("https://api.example.com/users")
}
```

#### 6. Dependency Injection

| Framework | Advantages | Disadvantages |
|-----------|------------|---------------|
| **Hilt** | - Android specific<br>- Compile-time validation<br>- Less boilerplate | - Android only<br>- Larger APK<br>- Complex errors |
| **Koin** | - Kotlin first<br>- Simple setup<br>- Lightweight | - Runtime validation<br>- Performance overhead<br>- Less features |
| **Manual DI** | - Full control<br>- No dependencies<br>- Simple | - More code<br>- Manual management<br>- No validation |

Example Implementation Comparison:
```kotlin
// Hilt
@HiltAndroidApp
class MyApplication : Application()

@AndroidEntryPoint
class MainActivity : AppCompatActivity() {
    @Inject lateinit var repository: Repository
}

@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    fun provideRepository(): Repository = RepositoryImpl()
}

// Koin
class MyApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        startKoin {
            modules(appModule)
        }
    }
}

val appModule = module {
    single<Repository> { RepositoryImpl() }
}

// Manual DI
class AppContainer {
    private val repository: Repository = RepositoryImpl()
    val viewModel: MainViewModel = MainViewModel(repository)
}
```

#### 7. Testing Approaches

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| **Unit Tests** | - Fast execution<br>- Isolated<br>- Early feedback | - Limited integration<br>- Mocking complexity<br>- Setup overhead |
| **Integration Tests** | - Real components<br>- Better coverage<br>- More realistic | - Slower execution<br>- More complex<br>- Flaky tests |
| **UI Tests** | - End-to-end testing<br>- User perspective<br>- Full flow | - Very slow<br>- Most complex<br>- Most flaky |

Example Implementation Comparison:
```kotlin
// Unit Test
class ViewModelTest {
    @Test
    fun `test data loading`() = runTest {
        val repository = FakeRepository()
        val viewModel = MainViewModel(repository)
        
        viewModel.loadData()
        
        assertEquals("data", viewModel.data.value)
    }
}

// Integration Test
@MediumTest
class RepositoryTest {
    private lateinit var database: AppDatabase
    
    @Before
    fun setup() {
        database = Room.inMemoryDatabaseBuilder(
            ApplicationProvider.getApplicationContext(),
            AppDatabase::class.java
        ).build()
    }
    
    @Test
    fun testDatabaseAndRepository() {
        val repository = RepositoryImpl(database)
        // Test with real database
    }
}

// UI Test
@LargeTest
class MainActivityTest {
    @get:Rule
    val activityRule = ActivityScenarioRule(MainActivity::class.java)
    
    @Test
    fun testUserFlow() {
        onView(withId(R.id.button))
            .perform(click())
            
        onView(withId(R.id.result))
            .check(matches(withText("Success")))
    }
}
```

#### 8. Background Processing

| Approach | Advantages | Disadvantages |
|----------|------------|---------------|
| **Coroutines** | - Structured concurrency<br>- Cancellation support<br>- Kotlin native | - Learning curve<br>- Error handling<br>- Debug complexity |
| **WorkManager** | - System friendly<br>- Constraints support<br>- Persistent | - Setup overhead<br>- Limited control<br>- API restrictions |
| **Services** | - Full control<br>- Long running<br>- System integration | - Complex lifecycle<br>- Battery impact<br>- Android restrictions |

Example Implementation Comparison:
```kotlin
// Coroutines
class CoroutineExample {
    private val scope = CoroutineScope(Dispatchers.IO + Job())
    
    fun doWork() {
        scope.launch {
            // Background work
            withContext(Dispatchers.Main) {
                // Update UI
            }
        }
    }
}

// WorkManager
class MyWorker(
    context: Context,
    params: WorkerParameters
) : CoroutineWorker(context, params) {
    override suspend fun doWork(): Result {
        // Background work
        return Result.success()
    }
}

val workRequest = OneTimeWorkRequestBuilder<MyWorker>()
    .setConstraints(Constraints.Builder()
        .setRequiredNetworkType(NetworkType.CONNECTED)
        .build())
    .build()

// Service
class MyService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        // Long running operation
        return START_STICKY
    }
}
```



### Project Requirements and Constraints Analysis

#### 1. Technical Requirements

| Requirement | Considerations | Implementation Strategy |
|------------|----------------|------------------------|
| **Minimum SDK** | - Market reach<br>- Feature availability<br>- Security updates | - Use AndroidX<br>- Feature detection<br>- Graceful degradation |
| **Performance** | - Memory usage<br>- Battery life<br>- App size | - Lazy loading<br>- Resource optimization<br>- Code proguard |
| **Offline Support** | - Data persistence<br>- Sync strategy<br>- Conflict resolution | - Room database<br>- WorkManager<br>- Sync adapters |
| **Security** | - Data encryption<br>- Network security<br>- Authentication | - Security-crypto<br>- Certificate pinning<br>- Biometric auth |

Example Implementation:
```kotlin
// Minimum SDK handling
@RequiresApi(Build.VERSION_CODES.S)
fun useNewFeature() {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
        // Use Android 12 specific feature
    } else {
        // Fallback implementation
    }
}

// Performance optimization
class ImageLoader {
    private val cache = LruCache<String, Bitmap>(
        (Runtime.getRuntime().maxMemory() / 1024 / 8).toInt()
    )
    
    fun loadImage(url: String, target: ImageView) {
        cache.get(url)?.let {
            target.setImageBitmap(it)
            return
        }
        
        lifecycleScope.launch(Dispatchers.IO) {
            // Load and cache image
        }
    }
}

// Offline support
@Entity(tableName = "cached_data")
data class CachedData(
    @PrimaryKey val id: String,
    val content: String,
    val timestamp: Long,
    val syncStatus: SyncStatus
)

enum class SyncStatus {
    SYNCED, PENDING, CONFLICT
}

// Security implementation
class SecurityManager(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()
        
    private val encryptedPrefs = EncryptedSharedPreferences.create(
        context,
        "secure_prefs",
        masterKey,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )
}
```

#### 2. Business Requirements

| Requirement | Considerations | Implementation Strategy |
|------------|----------------|------------------------|
| **Time to Market** | - MVP features<br>- Development speed<br>- Resource allocation | - Agile methodology<br>- Feature prioritization<br>- CI/CD pipeline |
| **Scalability** | - User growth<br>- Data volume<br>- Feature expansion | - Clean architecture<br>- Modular design<br>- Cloud services |
| **Maintenance** | - Code quality<br>- Documentation<br>- Testing coverage | - Code standards<br>- Documentation tools<br>- Test automation |
| **Cost** | - Development resources<br>- Infrastructure<br>- Third-party services | - Resource optimization<br>- Service selection<br>- Cost monitoring |

Example Implementation:
```kotlin
// Modular architecture
interface PaymentGateway {
    suspend fun processPayment(amount: Double): Result<Transaction>
}

class StripeGateway : PaymentGateway {
    override suspend fun processPayment(amount: Double): Result<Transaction> {
        // Stripe implementation
    }
}

class PayPalGateway : PaymentGateway {
    override suspend fun processPayment(amount: Double): Result<Transaction> {
        // PayPal implementation
    }
}

// Feature flags for gradual rollout
object FeatureFlags {
    private val remoteConfig = Firebase.remoteConfig
    
    fun isFeatureEnabled(feature: String): Boolean {
        return remoteConfig.getBoolean(feature)
    }
}

// Analytics for monitoring
class AnalyticsManager {
    fun trackEvent(event: String, params: Map<String, Any>) {
        Firebase.analytics.logEvent(event) {
            params.forEach { (key, value) ->
                param(key, value.toString())
            }
        }
    }
}
```

#### 3. User Requirements

| Requirement | Considerations | Implementation Strategy |
|------------|----------------|------------------------|
| **UI/UX** | - Accessibility<br>- Localization<br>- User feedback | - Material Design<br>- A11y support<br>- Analytics |
| **Performance** | - Load times<br>- Responsiveness<br>- Data usage | - Lazy loading<br>- Caching<br>- Compression |
| **Reliability** | - Error handling<br>- Data backup<br>- Crash reporting | - Exception handling<br>- Auto backup<br>- Crashlytics |
| **Privacy** | - Data collection<br>- Permissions<br>- Compliance | - Privacy policy<br>- Runtime permissions<br>- Data encryption |

Example Implementation:
```kotlin
// Accessibility support
@Composable
fun AccessibleButton(
    onClick: () -> Unit,
    contentDescription: String,
    content: @Composable () -> Unit
) {
    Button(
        onClick = onClick,
        modifier = Modifier.semantics {
            this.contentDescription = contentDescription
        }
    ) {
        content()
    }
}

// Performance monitoring
class PerformanceMonitor {
    private val trace = Firebase.performance.newTrace("operation_name")
    
    fun startOperation() {
        trace.start()
    }
    
    fun endOperation() {
        trace.stop()
    }
}

// Error handling
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
    object Loading : Result<Nothing>()
}

// Privacy-aware data collection
class PrivacyManager {
    fun collectData(
        data: UserData,
        privacyConsent: Boolean
    ): Flow<Result<Unit>> = flow {
        if (!privacyConsent) {
            throw PrivacyException("User consent required")
        }
        
        // Process data with privacy considerations
    }
}
```

#### 4. Technical Constraints

| Constraint | Impact | Mitigation Strategy |
|------------|--------|-------------------|
| **Device Compatibility** | - Feature limitations<br>- Testing complexity<br>- User experience | - Feature detection<br>- Fallback options<br>- Device testing |
| **Network Conditions** | - Data sync<br>- User experience<br>- Battery life | - Offline first<br>- Data compression<br>- Batch operations |
| **Memory Limitations** | - App performance<br>- Background processes<br>- Cache size | - Memory optimization<br>- Process lifecycle<br>- Resource cleanup |
| **Battery Usage** | - Background work<br>- Location updates<br>- Network calls | - WorkManager<br>- Geofencing<br>- Batch networking |

Example Implementation:
```kotlin
// Device compatibility
class DeviceCapabilities(private val context: Context) {
    fun hasFeature(feature: String): Boolean {
        return context.packageManager.hasSystemFeature(feature)
    }
    
    fun getScreenMetrics(): DisplayMetrics {
        return context.resources.displayMetrics
    }
}

// Network-aware operations
class NetworkAwareRepository(
    private val context: Context,
    private val api: ApiService,
    private val db: AppDatabase
) {
    private val connectivityManager = 
        context.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
            
    suspend fun getData(): Flow<Result<Data>> = flow {
        emit(Result.Loading)
        
        if (isNetworkAvailable()) {
            try {
                val data = api.fetchData()
                db.dataDao().insert(data)
                emit(Result.Success(data))
            } catch (e: Exception) {
                emit(Result.Error(e))
            }
        } else {
            emit(Result.Success(db.dataDao().getLocalData()))
        }
    }
}

// Memory management
class MemoryAwareImageCache {
    private val maxMemory = (Runtime.getRuntime().maxMemory() / 1024).toInt()
    private val cacheSize = maxMemory / 8
    
    private val memoryCache = object : LruCache<String, Bitmap>(cacheSize) {
        override fun sizeOf(key: String, bitmap: Bitmap): Int {
            return bitmap.byteCount / 1024
        }
    }
    
    fun addBitmapToCache(key: String, bitmap: Bitmap) {
        if (getBitmapFromCache(key) == null) {
            memoryCache.put(key, bitmap)
        }
    }
}

// Battery-efficient location updates
class LocationManager(private val context: Context) {
    private val fusedLocationClient = LocationServices.getFusedLocationProviderClient(context)
    
    fun startLocationUpdates() {
        val request = LocationRequest.create().apply {
            priority = LocationRequest.PRIORITY_BALANCED_POWER_ACCURACY
            interval = TimeUnit.MINUTES.toMillis(15)
            fastestInterval = TimeUnit.MINUTES.toMillis(5)
        }
        
        fusedLocationClient.requestLocationUpdates(
            request,
            locationCallback,
            Looper.getMainLooper()
        )
    }
}
```

#### 5. Project Planning Considerations

1. **Timeline Planning**
   - Feature prioritization
   - Resource allocation
   - Milestone definition
   - Risk assessment

2. **Resource Allocation**
   - Team composition
   - Skill requirements
   - Training needs
   - External dependencies

3. **Quality Assurance**
   - Testing strategy
   - Code review process
   - Performance benchmarks
   - Security audits

4. **Deployment Strategy**
   - Release planning
   - Version management
   - Update mechanism
   - Rollback procedures

Example Project Structure:
```kotlin
// Project structure
project/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   ├── data/
│   │   │   │   ├── domain/
│   │   │   │   ├── presentation/
│   │   │   │   └── di/
│   │   │   ├── res/
│   │   │   └── AndroidManifest.xml
│   │   ├── test/
│   │   └── androidTest/
│   ├── build.gradle
│   └── proguard-rules.pro
├── buildSrc/
│   └── src/
│       └── main/
│           └── kotlin/
│               └── Dependencies.kt
├── core/
│   ├── src/
│   │   └── main/
│   │       └── java/
│   │           ├── utils/
│   │           ├── extensions/
│   │           └── base/
│   └── build.gradle
├── features/
│   ├── feature1/
│   ├── feature2/
│   └── feature3/
├── build.gradle
└── settings.gradle
```

Remember these key considerations:
1. Always validate requirements against technical constraints
2. Plan for scalability from the start
3. Consider maintenance and long-term support
4. Balance user needs with technical limitations
5. Document decisions and trade-offs
6. Plan for testing and quality assurance
7. Consider security implications
8. Account for future updates and changes
9. Monitor and measure performance
10. Plan for gradual feature rollout