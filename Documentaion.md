-----

# Wave Spawner Pro - Comprehensive Documentation

## Table of Contents

1.  [Overview](#1-overview)
2.  [Features](https://www.google.com/search?q=%232-features)
3.  [Installation](https://www.google.com/search?q=%233-installation)
4.  [Quick Start Guide](https://www.google.com/search?q=%234-quick-start-guide)
      * [Creating a WaveManager via Editor Menu](https://www.google.com/search?q=%23creating-a-wavemanager-via-editor-menu)
5.  [Core Concepts](https://www.google.com/search?q=%235-core-concepts)
      * [WaveManager](https://www.google.com/search?q=%23wavemanager)
      * [Wave](https://www.google.com/search?q=%23wave)
      * [BurstSpawnEntry](https://www.google.com/search?q=%23burstspawnentry)
      * [EnemyTypeInBurst](https://www.google.com/search?q=%23enemytypeinburst)
6.  [Inspector Reference](https://www.google.com/search?q=%236-inspector-reference)
      * [Spawn Positions](https://www.google.com/search?q=%23spawn-positions)
      * [Visual Feedback](https://www.google.com/search?q=%23visual-feedback)
      * [Timing Settings](https://www.google.com/search?q=%23timing-settings)
      * [Wave Configuration](https://www.google.com/search?q=%23wave-configuration)
      * [Performance Options](https://www.google.com/search?q=%23performance-options)
      * [Debugging](https://www.google.com/search?q=%23debugging)
7.  [API Reference & Integration](https://www.google.com/search?q=%237-api-reference--integration)
      * [Subscribing to Events](https://www.google.com/search?q=%23subscribing-to-events)
      * [Returning Enemies to Pool](https://www.google.com/search?q=%23returning-enemies-to-pool)
      * [Manually Starting Waves](https://www.google.com/search?q=%23manually-starting-waves)
      * [Retrieving Wave Information](https://www.google.com/search?q=%23retrieving-wave-information)
8.  [Best Practices & Tips](https://www.google.com/search?q=%238-best-practices--tips)
9.  [Troubleshooting & FAQ](https://www.google.com/search?q=%239-troubleshooting--faq)
10. [Support](https://www.google.com/search?q=%2310-support)
11. [Version History](https://www.google.com/search?q=%2311-version-history)

-----

## 1\. Overview

**Wave Spawner Pro** is a robust and flexible Unity asset designed to streamline the creation and management of enemy waves and spawning logic for your game. Whether you're building a tower defense, survival, action, or any game requiring structured enemy encounters, Wave Spawner Pro provides an intuitive Inspector-based setup combined with powerful event-driven APIs for seamless integration into your project. With built-in object pooling, it's optimized for performance and scalability, ensuring smooth gameplay even with a high volume of enemies.

-----

## 2\. Features

  * **Quick Setup via Editor Menu:** Instantly create a `WaveManager` GameObject directly from the Hierarchy right-click menu.
  * **Intuitive Inspector Setup:** Easily configure waves, enemy types, and spawn timings directly within the Unity Editor.
  * **Multi-Prefab Support:** Define multiple enemy prefabs within each wave burst.
  * **Flexible Spawning:** Control the order of enemy bursts (sequential or random) within a wave.
  * **Multiple Spawn Positions:** Utilize a list of pre-defined spawn points, with dynamic selection to prevent overlapping.
  * **Optional Visual Pre-Spawn Feedback:** Show a customizable sprite at spawn locations before enemies appear.
  * **Adjustable Timing:** Fine-tune delays between bursts and and between waves.
  * **Integrated Object Pooling:** Automatically pre-instantiate enemies and manage their reuse, significantly improving performance and reducing garbage collection spikes.
  * **Event-Driven Architecture:** Subscribe to powerful C\# events for wave start, wave end, first wave, and last wave completion, enabling seamless integration with your game logic (UI updates, audio cues, game state changes).
  * **Developer-Friendly Debugging:** Toggle informational debug logs on/off directly from the Inspector.
  * **Modular Design:** Optimized for use with Unity Assembly Definitions for faster compile times.

-----

## 3\. Installation

To install Wave Spawner Pro:

1.  **Download:** Purchase and download the asset from the Unity Asset Store.
2.  **Import:** In your Unity project, go to `Assets > Import Package > Custom Package...` and select the downloaded `.unitypackage` file.
3.  **Select All:** In the import dialog, ensure all items are selected and click `Import`.

**Recommended Project Structure (Assembly Definitions):**
For optimal performance and faster compile times, it is highly recommended to utilize Unity's Assembly Definitions. Wave Spawner Pro is structured with these in mind:

  * **`Assets/CelerisLab/WaveSpawnerPro/Runtime/`**: Contains the core `WaveManager.cs` script and its related classes (`Wave`, `BurstSpawnEntry`, `EnemyTypeInBurst`). This folder includes `CelerisLab.WaveSpawnerPro.Runtime.asmdef`.
  * **`Assets/CelerisLab/WaveSpawnerPro/Editor/`**: Contains Editor-only scripts, like the **`WaveManagerCreator.cs`** (which adds the Hierarchy menu item). This folder includes `CelerisLab.WaveSpawnerPro.Editor.asmdef`, which references the `Runtime` assembly.
  * **`Assets/CelerisLab/WaveSpawnerPro/Demo/`**: Contains example scenes and demo-specific scripts. This folder includes `CelerisLab.WaveSpawnerPro.Demo.asmdef`, which references the `Runtime` assembly.

If you have your own scripts in separate Assembly Definitions, ensure that any of your `.asmdef` files that need to interact with `WaveManager` (e.g., a `PlayerController` or `UIManager` assembly) add a reference to `CelerisLab.WaveSpawnerPro.Runtime` in their Inspector settings.

-----

## 4\. Quick Start Guide

Follow these steps to get your first wave spawning in minutes:

### Creating a WaveManager via Editor Menu

The easiest way to get started is by using the custom Editor menu item:

1.  **Right-Click in Hierarchy:** In your Unity scene, right-click anywhere in the **Hierarchy window**.
2.  **Navigate to Menu:** Hover over `CelerisLab`.
3.  **Select Option:** Click on `Create Wave Manager`.

This will instantly create a new GameObject named "WaveManager" in your scene, with the `WaveManager` script already attached and selected in the Inspector.

-----

**After creating the `WaveManager` GameObject (using the menu or manually):**

1.  **Define Spawn Positions:**

      * Create a few empty GameObjects in your scene at the locations where you want enemies to appear. Name them something like `SpawnPoint1`, `SpawnPoint2`, etc.
      * Select the `WaveManager` GameObject.
      * In the `WaveManager` component, locate the **"Spawn Positions"** list.
      * Set its `Size` to the number of spawn points you created.
      * Drag and drop your `SpawnPoint` GameObjects from the Hierarchy into the `Element` slots of the `Spawn Positions` list.

2.  **Prepare an Enemy Prefab:**

      * Create a simple enemy GameObject (e.g., a Cube with a `Rigidbody` and a script that handles its destruction).
      * Drag this GameObject from your Hierarchy into your Project window to create a Prefab.

3.  **Configure Your First Wave:**

      * Select the `WaveManager` GameObject.
      * In the `WaveManager` component, locate the **"Wave Configuration"** section.
      * Expand the `Waves` list. Set its `Size` to `1`.
      * Expand `Element 0` (this is your first wave).
      * **Inside `Element 0 (Wave)`:**
          * Expand `Burst Spawn Entries`. Set its `Size` to `1`.
          * Expand `Element 0` (this is your first burst).
          * **Inside `Element 0 (Burst Spawn Entry)`:**
              * Expand `Enemies In This Burst`. Set its `Size` to `1`.
              * Expand `Element 0`.
              * Drag your enemy Prefab into the `Enemy Prefab` slot.
              * Set the `Count` to `5` (to spawn 5 enemies in this burst).

4.  **Run the Scene:**

      * Press Play in the Unity Editor.
      * The `WaveManager` will automatically start the wave routine, spawn your 5 enemies, and wait for them to be defeated before logging the wave completion.

5.  **Implement Enemy Defeat (Crucial for Wave Progression):**

      * For the `WaveManager` to know when enemies are "defeated" and progress to the next wave, enemies must be removed from the scene.
      * **If `Use Object Pooling` is `true` (default and recommended):** Your enemy's defeat script should call `WaveManager.Instance.ReturnEnemyToPool(gameObject);` when it's defeated.
      * **If `Use Object Pooling` is `false`:** Your enemy's defeat script should call `Destroy(gameObject);` when it's defeated.

**(See [Returning Enemies to Pool](https://www.google.com/search?q=%23returning-enemies-to-pool) for a detailed example.)**

-----

## 5\. Core Concepts

Wave Spawner Pro organizes enemy spawning around four main data structures:

### WaveManager

The central MonoBehaviour script (`WaveManager.cs`) that orchestrates the entire wave system. It holds all configuration data, manages the spawning routine, handles object pooling, and dispatches events.

### Wave

A `Wave` represents a single stage or "round" of enemy encounters. Each `Wave` consists of one or more `Burst Spawn Entries`.

  * **`Random Spawn Order` (bool):** If `true`, the `Burst Spawn Entries` within this wave will be spawned in a random order. If `false`, they will spawn sequentially as they appear in the list.
  * **`Burst Spawn Entries` (List):** A list of `BurstSpawnEntry` objects that define groups of enemies to be spawned together as a single event.

### BurstSpawnEntry

A `BurstSpawnEntry` defines a group of enemies that will spawn simultaneously or in rapid succession as one "burst." A single `BurstSpawnEntry` can contain multiple `EnemyTypeInBurst` definitions.

  * **`Enemies In This Burst` (List):** A list of `EnemyTypeInBurst` objects defining which enemy prefabs and how many of each will be spawned in this specific burst.

### EnemyTypeInBurst

This class specifies a particular enemy `GameObject` prefab and the `count` of that enemy to spawn within a `BurstSpawnEntry`.

  * **`Enemy Prefab` (GameObject):** The enemy prefab to be instantiated.
  * **`Count` (int):** The number of instances of this specific `Enemy Prefab` to spawn within its `BurstSpawnEntry`. Must be at least 1.

-----

## 6\. Inspector Reference

Attach the `WaveManager.cs` script to an empty GameObject in your scene to configure it. (Or use the `CelerisLab/Create Wave Manager` menu item).

#### Spawn Positions

  * **`Spawn Positions` (List\<Transform\>):**
      * A list of `Transform` components representing the possible locations where enemies can appear.
      * **How it works:** For each enemy spawned in a burst, the system will attempt to pick a unique spawn position from this list. If there are more enemies than unique spawn positions, positions will be reused randomly, and a warning will be logged (if debug logs are enabled).
      * **Setup:** Create empty GameObjects in your scene, place them at your desired spawn points, and drag their `Transform` components into this list.

#### Visual Feedback

  * **`Spawn Sprite Prefab` (SpriteRenderer):**
      * An optional `SpriteRenderer` prefab that will be instantiated at each enemy's spawn location just before the enemy appears. This provides a visual "warning" or "coming soon" indicator for the player.
      * **Setup:** Create a prefab of a `GameObject` with a `SpriteRenderer` component (e.g., a circle, an "X", or a glowing effect). Drag this prefab into this slot. Leave empty if you don't want a visual cue.
  * **`Time Between Spawn And Spawn Sprite` (float):**
      * The duration (in seconds) that the `Spawn Sprite Prefab` is visible before the actual enemy `GameObject` appears at that location.
      * Set to `0` for instant enemy spawning after the sprite.

#### Timing Settings

  * **`Time Between Spawns` (float):**
      * The delay (in seconds) between the completion of one `Burst Spawn Entry` (group of enemies) and the start of the next `Burst Spawn Entry` within the *same* wave.
      * This controls the pacing of enemy groups within a single wave.
  * **`Time Between Waves` (float):**
      * The delay (in seconds) between the completion of *all* enemies in the current wave and the start of the next wave.
      * This provides a pause or "breather" period between rounds.

#### Wave Configuration

  * **`Waves` (List\<Wave\>):**
      * This is the core of your enemy progression. Add `Wave` elements to define each stage of your game.
      * Expand each `Wave` element to configure its `Random Spawn Order` and `Burst Spawn Entries`.
      * Within each `Burst Spawn Entry`, define the `Enemy Prefab` and `Count` for each `EnemyTypeInBurst`.

#### Performance Options

  * **`Use Object Pooling` (bool):**
      * If `true` (recommended), enemies will be pre-instantiated in an object pool at `Start()` and reused when needed. This significantly reduces garbage collection and improves performance, especially with many enemies.
      * If `false`, enemies will be instantiated (`Instantiate`) and destroyed (`Destroy`) for each spawn, which can lead to performance spikes.
      * **Important:** When using object pooling, your enemy scripts *must* call `WaveManager.Instance.ReturnEnemyToPool(gameObject);` instead of `Destroy(gameObject);` when they are defeated or no longer needed. See [Returning Enemies to Pool](https://www.google.com/search?q=%23returning-enemies-to-pool).

#### Debugging

  * **`Enable Debug Logs` (bool):**
      * If `true` (default), informational `Debug.Log` messages from the WaveManager will be displayed in the console, providing updates on wave progress and spawning.
      * `Debug.LogError` and `Debug.LogWarning` messages will always be displayed, regardless of this setting, as they indicate critical issues or potential problems.

-----

## 7\. API Reference & Integration

The `WaveManager` provides static events and public methods for seamless integration with your game's logic.

### Subscribing to Events

You can subscribe to these events from any other script to react to wave changes.

```csharp
using CelerisLab.WaveSystem; // Make sure to include your namespace
using UnityEngine;

public class MyGameEventHandler : MonoBehaviour
{
    void OnEnable()
    {
        // Subscribe to events when this script is enabled
        WaveManager.OnFirstWaveStart += HandleFirstWaveStart;
        WaveManager.OnWaveStart += HandleWaveStart;
        WaveManager.OnWaveEnd += HandleWaveEnd;
        WaveManager.OnLastWaveEnd += HandleLastWaveEnd;
    }

    void OnDisable()
    {
        // Unsubscribe from events when this script is disabled to prevent memory leaks
        WaveManager.OnFirstWaveStart -= HandleFirstWaveStart;
        WaveManager.OnWaveStart -= HandleWaveStart;
        WaveManager.OnWaveEnd -= HandleWaveEnd;
        WaveManager.OnLastWaveEnd -= HandleLastWaveEnd;
    }

    void HandleFirstWaveStart()
    {
        Debug.Log("GAME: The very first wave has officially begun!");
        // Example: Show a "Round 1" UI message
    }

    void HandleWaveStart(int waveIndex)
    {
        Debug.Log($"GAME: Wave {waveIndex + 1} has started!");
        // Example: Update wave number in UI, play wave start sound
    }

    void HandleWaveEnd()
    {
        Debug.Log("GAME: Current wave has ended (all enemies defeated/spawned).");
        // Example: Award points, show "Wave Clear!" message, prepare for next wave
    }

    void HandleLastWaveEnd()
    {
        Debug.Log("GAME: All waves in the game have been completed!");
        // Example: Trigger game win condition, show end-game screen
    }
}
```

### Returning Enemies to Pool

If `Use Object Pooling` is enabled (which is highly recommended for performance), your enemy scripts must call `WaveManager.Instance.ReturnEnemyToPool(gameObject);` instead of `Destroy(gameObject);` when they are defeated or no longer needed.

```csharp
using CelerisLab.WaveSystem; // Make sure to include your namespace
using UnityEngine;

public class EnemyHealth : MonoBehaviour
{
    public int health = 10;

    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
        {
            Die();
        }
    }

    private void Die()
    {
        Debug.Log($"{gameObject.name} was defeated!");

        // IMPORTANT: Check if WaveManager instance exists and pooling is used
        // In the next version, you might want to consider making WaveManager a singleton.
        if (FindObjectOfType<WaveManager>() != null && FindObjectOfType<WaveManager>().useObjectPooling)
        {
            // Return to pool if pooling is enabled
            FindObjectOfType<WaveManager>().ReturnEnemyToPool(gameObject);
        }
        else
        {
            // Otherwise, destroy the GameObject
            Destroy(gameObject);
        }
    }

    // Optional: Reset enemy state when it's activated from the pool
    void OnEnable()
    {
        health = 10; // Reset health for new life
        // Reset any other relevant states (e.g., movement speed, target)
    }
}
```

### Manually Starting Waves

You can programmatically start a specific wave (useful for level selection, debugging, or custom game flow).

```csharp
using CelerisLab.WaveSystem;
using UnityEngine;

public class GameFlowController : MonoBehaviour
{
    public WaveManager waveManager; // Drag your WaveManager GameObject here in the Inspector

    void Start()
    {
        // Example: Wait 5 seconds, then start Wave 3 (index 2)
        // Make sure your WaveManager is NOT set to auto-start waves if you're controlling them manually.
        Invoke("StartCustomWave", 5.0f);
    }

    void StartCustomWave()
    {
        if (waveManager != null)
        {
            int waveIndexToStart = 2; // Starts the 3rd wave (0-based index)
            waveManager.StartSpecificWave(waveIndexToStart);
        }
        else
        {
            Debug.LogError("GameFlowController: WaveManager reference not set!");
        }
    }
}
```

**Note:** Calling `StartSpecificWave` will stop any currently running wave routine and clear any active enemies from the previous wave (by returning them to the pool or destroying them).

### Retrieving Wave Information

You can query the `WaveManager` for current wave status:

```csharp
using CelerisLab.WaveSystem;
using UnityEngine;

public class GameUI : MonoBehaviour
{
    public WaveManager waveManager; // Drag your WaveManager GameObject here

    void Update()
    {
        if (waveManager != null)
        {
            int currentWaveNumber = waveManager.GetCurrentWaveIndex() + 1; // +1 for 1-based display
            int totalWaves = waveManager.GetTotalWavesCount();
            bool isSpawning = waveManager.IsSpawningWave();

            // Example: Update UI text
            // myWaveText.text = $"Wave: {currentWaveNumber}/{totalWaves}";
            // mySpawnStatusText.text = isSpawning ? "Spawning..." : "Waiting...";
        }
    }
}
```

  * **`int GetCurrentWaveIndex()`:** Returns the 0-based index of the wave that is currently active or has just finished. Returns -1 before the first wave starts.
  * **`bool IsSpawningWave()`:** Returns `true` if the `WaveManager` is currently in the process of spawning enemies within a wave (i.e., not waiting for enemies to be defeated or between waves).
  * **`int GetTotalWavesCount()`:** Returns the total number of waves configured in the `WaveManager`.

-----

## 8\. Best Practices & Tips

  * **Empty GameObject for Spawn Points:** Use simple empty `GameObject`s in your scene to define spawn positions. Position them precisely where you want enemies to appear.
  * **Enemy Prefab Cleanup:** Ensure your enemy prefabs are "clean." If they have child objects or components you don't want active while pooled, disable them when returning to the pool and re-enable them `OnEnable()`.
  * **Disable Enemy Colliders When Pooled (Optional but Recommended):** If your enemies have complex colliders that might interfere with physics when inactive, consider disabling their colliders (and `Rigidbody` if applicable) when returning them to the pool, and re-enabling them when activated. This can prevent unexpected physics interactions.
  * **Consider Game State:** Integrate the WaveManager with your overall game state (e.g., pause menu, game over). You might want to `StopAllCoroutines()` on the `WaveManager` component during pauses or game over screens, and potentially restart the wave routine upon resuming.

-----

## 9\. Troubleshooting & FAQ

  * **Q: "No spawn positions assigned\!" error in console.**

      * **A:** You must assign at least one `Transform` to the `Spawn Positions` list in the `WaveManager` Inspector. Without places to spawn, the system cannot function.

  * **Q: "No waves configured\!" warning in console.**

      * **A:** Add `Wave` elements to the `Waves` list in the `WaveManager` Inspector. The system will not run any waves until they are defined.

  * **Q: My waves aren't progressing, or enemies are stuck after being defeated.**

      * **A:** If `Use Object Pooling` is `true`, ensure your enemy defeat logic calls `FindObjectOfType<WaveManager>().ReturnEnemyToPool(gameObject);` (or `WaveManager.Instance.ReturnEnemyToPool(gameObject);` if you implement a Singleton pattern). If `false`, ensure it calls `Destroy(gameObject);`. The `WaveManager` waits for all active enemies of a wave to be disabled/destroyed before progressing.

  * **Q: I'm getting a lot of `Instantiate` calls even with pooling enabled.**

      * **A:** This can happen if the `Count` of enemies in your waves exceeds the initial pre-instantiated pool size. The pool will automatically expand if needed, but for optimal performance, try to set up your waves so that `PreInstantiateEnemiesForPooling()` creates a sufficient initial pool. Review your `PreInstantiateEnemiesForPooling()` debug logs to see how many of each enemy type were pre-instantiated.

  * **Q: Why don't my `Debug.Log` messages from `WaveManager` appear?**

      * **A:** Check the `Enable Debug Logs` checkbox in the `Debugging` section of the `WaveManager` Inspector. If it's unchecked, informational logs are suppressed. `Debug.LogError` and `Debug.LogWarning` will always appear.

  * **Q: I moved the `WaveManager` scripts into an Assembly Definition, and now other scripts can't find it.**

      * **A:** Ensure that any `.asmdef` file containing scripts that need to access `WaveManager` has explicitly added a reference to your `WaveManager`'s Runtime Assembly Definition (`CelerisLab.WaveSpawnerPro.Runtime`) in its Inspector settings under `Assembly Definition References`.

-----

## 10\. Support

If you encounter any issues, have questions, or require further assistance, please don't hesitate to reach out\!

  * **Email:** apricots.business1@gmail.com

Please provide your Unity version, a detailed description of the issue, and steps to reproduce it, if possible.

-----

## 11\. Version History

**Version 1.0.0 (June 2025)**

  * Initial Release of Wave Spawner Pro.
  * Core wave spawning, burst configuration.
  * Object pooling implementation.
  * Event system for wave lifecycle.
  * Optional spawn sprite visual feedback.
  * Manual wave start functionality.
  * Debug log toggle.
  * **New:** Added Editor menu item (`CelerisLab/Create Wave Manager`) for quick setup.

-----
