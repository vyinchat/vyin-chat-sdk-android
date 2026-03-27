# Vyin Chat SDK for Android

Vyin Chat SDK for Android enables you to add real-time chat into your Android app with minimal effort. It provides messaging, channel management, user presence, push notifications, and local caching out of the box.

## Requirements

- Android API 21+
- Firebase Cloud Messaging (required for push notifications)

## Installation

### Step 1 — Add the Maven repository

**`settings.gradle` (Gradle 6.8+)**

```kotlin
dependencyResolutionManagement {
    repositories {
        maven { setUrl("https://vyinchat.github.io/vyin-chat-sdk-android/maven") }
    }
}
```

<details>
<summary>Gradle 6.7 or lower</summary>

**`build.gradle` (root)**

```kotlin
allprojects {
    repositories {
        maven { setUrl("https://vyinchat.github.io/vyin-chat-sdk-android/maven") }
    }
}
```

</details>

### Step 2 — Add the dependency

```kotlin
dependencies {
    implementation("com.gamania.gim:gim-chat:LATEST_VERSION")
}
```

Replace `LATEST_VERSION` with the version from [Releases](https://github.com/vyinchat/vyin-chat-sdk-android/releases).

### Step 3 — Add permissions

Add the following to your `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## Quick Start

### 1. Initialize SDK

Create your application on the [Vyin Chat Console](https://console.gamania.chat/) to obtain your `APP_ID`.

```kotlin
GIMChat.init(
    InitParams(APP_ID, applicationContext, useCaching = true),
    object : InitResultHandler {
        override fun onMigrationStarted() {}
        override fun onInitFailed(exception: GIMException) {}
        override fun onInitSucceed() {
            // Call connect() here after initialization is complete
        }
    }
)
```

### 2. Connect User

```kotlin
GIMChat.connect(userId) { user, e ->
    if (e != null) {
        // Handle error
        return@connect
    }
    // Connected successfully
}
```

### 3. Create a Group Channel

```kotlin
val params = GroupChannelCreateParams().apply {
    userIds = listOf(userId)
}

GroupChannel.createChannel(params) { channel, e ->
    if (e != null) {
        // Handle error
        return@createChannel
    }
    // Channel created
}
```

### 4. Send a Message

```kotlin
// Use channel from Step 3
channel.sendUserMessage(MESSAGE) { message, e ->
    if (e != null) {
        // Handle error
        return@sendUserMessage
    }
    // Message sent
}
```

### 5. Receive Messages in Real-time

```kotlin
GIMChat.addChannelHandler(
    UNIQUE_HANDLER_ID,
    object : GroupChannelHandler() {
        override fun onMessageReceived(channel: BaseChannel, message: BaseMessage) {
            // Handle incoming message
        }
    }
)

// Remove when no longer needed
override fun onDestroy() {
    super.onDestroy()
    GIMChat.removeChannelHandler(UNIQUE_HANDLER_ID)
}
```

### 6. Disconnect

```kotlin
GIMChat.disconnect {
    // Disconnected
}
```

## Documentation

Full documentation is available at [Vyin Chat SDK for Android](https://github.com/vyinchat/vyin-chat-docs/tree/main/sdk/android).

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a full history of changes.

## License

This SDK is provided under the Vyin Chat SDK License Agreement.
See [LICENSE.md](LICENSE.md) for details.
