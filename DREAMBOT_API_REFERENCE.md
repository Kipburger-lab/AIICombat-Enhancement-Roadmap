# DreamBot API Reference Guide 📚

Comprehensive reference for DreamBot API usage in the AIICombat enhancement project.

## Core API Classes and Methods

### Player Management
```java
// Players class - Managing player entities
Players.getLocal()                    // Get local player
Players.getLocal().isInCombat()      // Check if in combat
Players.getLocal().getHealthPercent() // Get health percentage
Players.getLocal().getTile()         // Get current position
Players.getLocal().isMoving()        // Check if moving
Players.getLocal().isAnimating()     // Check if animating
Players.getLocal().getAnimation()    // Get current animation ID

// Player interactions
Players.getLocal().interact("Walk here");
Players.getLocal().getRealLevel(Skill.ATTACK);
Players.getLocal().getCurrentLevel(Skill.HITPOINTS);
```

### NPC Management
```java
// NPCs class - Managing NPC entities
NPCs.closest("Goblin")               // Find closest NPC by name
NPCs.closest(npc -> npc.hasAction("Attack"))  // Find by condition
NPCs.all(npc -> npc.distance() < 10) // Get all NPCs within distance

// NPC properties
npc.getName()                        // Get NPC name
npc.getId()                          // Get NPC ID
npc.getHealthPercent()               // Get health percentage
npc.isInCombat()                     // Check if in combat
npc.distance()                       // Distance from player
npc.hasAction("Attack")              // Check if has specific action
npc.getTile()                        // Get NPC position
npc.getBounds()                      // Get screen bounds

// NPC interactions
npc.interact("Attack");
npc.interact("Examine");
```

### Combat System
```java
// Combat class - Combat-related methods
Combat.getAttackStyle()              // Get current attack style
Combat.setAttackStyle(AttackStyle.ACCURATE);
Combat.getSpecialPercentage()        // Get special attack percentage
Combat.toggleSpecialAttack(true)     // Toggle special attack
Combat.isAutoRetaliateOn()           // Check auto-retaliate status
Combat.toggleAutoRetaliate(true)     // Toggle auto-retaliate

// Attack styles
AttackStyle.ACCURATE
AttackStyle.AGGRESSIVE
AttackStyle.DEFENSIVE
AttackStyle.CONTROLLED
```

### Inventory Management
```java
// Inventory class - Inventory operations
Inventory.contains("Lobster")         // Check if contains item
Inventory.count("Coins")              // Count specific items
Inventory.isFull()                   // Check if inventory is full
Inventory.isEmpty()                  // Check if inventory is empty
Inventory.getEmptySlots()            // Get number of empty slots

// Item interactions
Item food = Inventory.get("Lobster");
if (food != null) {
    food.interact("Eat");
}

// Item filtering
Inventory.all(item -> item.getName().contains("potion"));
Inventory.onlyContains("Lobster", "Sword", "Shield");
```

### Equipment Management
```java
// Equipment class - Equipment operations
Equipment.contains("Rune sword")     // Check if wearing item
Equipment.get(EquipmentSlot.WEAPON)  // Get equipped weapon
Equipment.get(EquipmentSlot.SHIELD)  // Get equipped shield

// Equipment slots
EquipmentSlot.HELMET
EquipmentSlot.CAPE
EquipmentSlot.AMULET
EquipmentSlot.WEAPON
EquipmentSlot.CHEST
EquipmentSlot.SHIELD
EquipmentSlot.LEGS
EquipmentSlot.GLOVES
EquipmentSlot.BOOTS
EquipmentSlot.RING
EquipmentSlot.AMMO
```

### Prayer System
```java
// Prayer class - Prayer management
Prayer.getPrayerPoints()             // Get current prayer points
Prayer.PROTECT_FROM_MELEE.isActive() // Check if prayer is active
Prayer.PROTECT_FROM_MELEE.toggle(true); // Activate/deactivate prayer

// Common prayers
Prayer.THICK_SKIN
Prayer.BURST_OF_STRENGTH
Prayer.CLARITY_OF_THOUGHT
Prayer.PROTECT_FROM_MELEE
Prayer.PROTECT_FROM_MISSILES
Prayer.PROTECT_FROM_MAGIC
Prayer.EAGLE_EYE
Prayer.MYSTIC_MIGHT
Prayer.PIETY
```

### Movement and Walking
```java
// Walking class - Movement operations
Walking.walk(tile)                   // Walk to specific tile
Walking.walkExact(tile)              // Walk to exact tile
Walking.isRunEnabled()               // Check if run is enabled
Walking.toggleRun(true)              // Toggle run mode
Walking.getDestination()             // Get current destination
Walking.isMoving()                   // Check if currently moving

// Pathfinding
Walking.shouldWalk(5)                // Check if should walk (distance threshold)
Walking.getRunEnergy()               // Get current run energy
```

### Ground Items
```java
// GroundItems class - Ground item management
GroundItems.closest("Coins")         // Find closest ground item
GroundItems.all(item -> item.getValue() > 100); // Filter by value

// Ground item properties
groundItem.getName()                 // Get item name
groundItem.getId()                   // Get item ID
groundItem.getAmount()               // Get item amount
groundItem.getValue()                // Get item value
groundItem.distance()                // Distance from player
groundItem.getTile()                 // Get item position

// Ground item interactions
groundItem.interact("Take");
```

### Banking
```java
// Bank class - Banking operations
Bank.isOpen()                        // Check if bank is open
Bank.open()                          // Open bank
Bank.close()                         // Close bank
Bank.contains("Lobster")             // Check if bank contains item
Bank.count("Coins")                  // Count items in bank

// Banking operations
Bank.deposit("Lobster", 10)          // Deposit specific amount
Bank.depositAll("Lobster")           // Deposit all of item
Bank.depositAllExcept("Sword", "Shield"); // Deposit all except specified
Bank.withdraw("Lobster", 10)         // Withdraw specific amount
Bank.withdrawAll("Lobster")          // Withdraw all of item
```

### Interface and Tabs
```java
// Tabs class - Game tab management
Tabs.open(Tab.INVENTORY)             // Open inventory tab
Tabs.open(Tab.STATS)                 // Open stats tab
Tabs.open(Tab.COMBAT)                // Open combat tab
Tabs.open(Tab.PRAYER)                // Open prayer tab
Tabs.isOpen(Tab.INVENTORY)           // Check if tab is open

// Available tabs
Tab.COMBAT
Tab.STATS
Tab.QUEST
Tab.INVENTORY
Tab.EQUIPMENT
Tab.PRAYER
Tab.MAGIC
Tab.CLAN
Tab.FRIENDS
Tab.ACCOUNT
Tab.LOGOUT
Tab.SETTINGS
Tab.EMOTES
Tab.MUSIC
```

### Camera Control
```java
// Camera class - Camera management
Camera.getYaw()                      // Get current yaw (rotation)
Camera.getPitch()                    // Get current pitch (angle)
Camera.rotateToYaw(180)              // Rotate to specific yaw
Camera.rotateToPitch(90)             // Rotate to specific pitch
Camera.rotateToEntity(npc)           // Rotate camera to entity
```

### Mouse and Keyboard
```java
// Mouse class - Mouse operations
Mouse.click(x, y)                    // Click at coordinates
Mouse.move(x, y)                     // Move mouse to coordinates
Mouse.getPosition()                  // Get current mouse position
Mouse.isPressed()                    // Check if mouse is pressed

// Keyboard class - Keyboard operations
Keyboard.type("Hello world")         // Type text
Keyboard.pressKey(KeyEvent.VK_ENTER) // Press specific key
Keyboard.holdKey(KeyEvent.VK_SHIFT)  // Hold key down
Keyboard.releaseKey(KeyEvent.VK_SHIFT); // Release key
```

### Utilities
```java
// Sleep class - Timing utilities
Sleep.sleep(1000)                    // Sleep for milliseconds
Sleep.sleepUntil(() -> condition, 5000); // Sleep until condition or timeout
Sleep.sleepWhile(() -> condition, 5000); // Sleep while condition is true

// Random class - Random number generation
Random.nextInt(100)                  // Random integer 0-99
Random.nextDouble()                  // Random double 0.0-1.0
Random.nextGaussian()                // Random gaussian distribution

// Calculate class - Mathematical utilities
Calculate.distanceBetween(tile1, tile2); // Distance between tiles
Calculate.getRandomBetween(min, max);     // Random number in range
```

## Advanced API Usage Patterns

### Conditional Waiting
```java
// Wait for combat to start
Sleep.sleepUntil(() -> Players.getLocal().isInCombat(), 3000);

// Wait for movement to complete
Sleep.sleepUntil(() -> !Players.getLocal().isMoving(), 5000);

// Wait for animation to finish
Sleep.sleepUntil(() -> !Players.getLocal().isAnimating(), 2000);

// Wait for health to reach threshold
Sleep.sleepUntil(() -> Players.getLocal().getHealthPercent() > 50, 10000);
```

### Entity Filtering
```java
// Complex NPC filtering
NPC target = NPCs.closest(npc -> 
    npc != null &&
    npc.hasAction("Attack") &&
    !npc.isInCombat() &&
    npc.getHealthPercent() > 0 &&
    npc.distance() <= 10 &&
    Arrays.asList("Goblin", "Cow").contains(npc.getName())
);

// Ground item filtering by value
List<GroundItem> valuableItems = GroundItems.all(item ->
    item.getValue() > 1000 &&
    item.distance() <= 5
);

// Inventory item filtering
List<Item> food = Inventory.all(item ->
    item.getName().contains("fish") ||
    item.getName().contains("bread") ||
    item.getName().contains("meat")
);
```

### Area Management
```java
// Define areas
Area combatArea = new Area(
    new Tile(3200, 3200, 0),
    new Tile(3210, 3210, 0)
);

// Check if player is in area
if (combatArea.contains(Players.getLocal())) {
    // Player is in combat area
}

// Find NPCs in specific area
List<NPC> npcsInArea = NPCs.all(npc ->
    combatArea.contains(npc.getTile())
);
```

### State Management
```java
// Comprehensive state checking
public enum ScriptState {
    FINDING_TARGET,
    MOVING_TO_TARGET,
    ENGAGING_COMBAT,
    IN_COMBAT,
    LOOTING,
    EATING,
    BANKING,
    IDLE
}

public ScriptState getCurrentState() {
    if (Players.getLocal().isInCombat()) {
        return ScriptState.IN_COMBAT;
    }
    
    if (Players.getLocal().getHealthPercent() < 50 && hasFood()) {
        return ScriptState.EATING;
    }
    
    if (Inventory.isFull() && hasValuableLoot()) {
        return ScriptState.BANKING;
    }
    
    if (hasNearbyLoot()) {
        return ScriptState.LOOTING;
    }
    
    NPC target = findTarget();
    if (target != null) {
        if (target.distance() > 1) {
            return ScriptState.MOVING_TO_TARGET;
        } else {
            return ScriptState.ENGAGING_COMBAT;
        }
    }
    
    return ScriptState.FINDING_TARGET;
}
```

## Error Handling Best Practices

### Null Checking
```java
// Always check for null entities
NPC target = NPCs.closest("Goblin");
if (target != null && target.hasAction("Attack")) {
    if (target.interact("Attack")) {
        Sleep.sleepUntil(() -> Players.getLocal().isInCombat(), 3000);
    }
}

// Safe item interactions
Item food = Inventory.get("Lobster");
if (food != null && food.interact("Eat")) {
    Sleep.sleepUntil(() -> 
        Players.getLocal().getHealthPercent() > previousHealth, 2000);
}
```

### Exception Handling
```java
// Wrap risky operations in try-catch
try {
    if (Bank.open()) {
        Sleep.sleepUntil(() -> Bank.isOpen(), 3000);
        Bank.depositAllExcept("Weapon", "Shield");
    }
} catch (Exception e) {
    Logger.error("Banking error: " + e.getMessage());
    // Implement recovery logic
}
```

### Timeout Handling
```java
// Always use timeouts for sleepUntil
boolean success = Sleep.sleepUntil(() -> 
    Players.getLocal().isInCombat(), 5000);
    
if (!success) {
    Logger.warn("Failed to enter combat within timeout");
    // Implement fallback logic
}
```

## Performance Optimization

### Efficient Entity Queries
```java
// Cache frequently accessed entities
private NPC cachedTarget;
private long lastTargetUpdate;

public NPC getTarget() {
    long currentTime = System.currentTimeMillis();
    
    // Update cache every 1 second
    if (currentTime - lastTargetUpdate > 1000 || 
        cachedTarget == null || 
        !cachedTarget.exists()) {
        
        cachedTarget = NPCs.closest("Goblin");
        lastTargetUpdate = currentTime;
    }
    
    return cachedTarget;
}
```

### Minimize API Calls
```java
// Store frequently used values
Player localPlayer = Players.getLocal();
int currentHealth = localPlayer.getHealthPercent();
boolean inCombat = localPlayer.isInCombat();
Tile playerTile = localPlayer.getTile();

// Use stored values instead of repeated API calls
if (currentHealth < 50 && !inCombat) {
    eatFood();
}
```

### Conditional Processing
```java
// Only process when necessary
if (Players.getLocal().isInCombat()) {
    handleCombat();
} else if (shouldEat()) {
    eatFood();
} else if (shouldLoot()) {
    lootItems();
} else {
    findAndAttackTarget();
}
```

## UI Integration

### Creating Custom Panels
```java
// Extend DreamBot's UI components
public class CombatConfigPanel extends JPanel {
    @Override
    public void onStart() {
        // Initialize UI components
        setLayout(new GridBagLayout());
        
        // Add configuration options
        addTargetSelection();
        addCombatSettings();
        addAntiBanSettings();
    }
    
    private void addTargetSelection() {
        JComboBox<String> targetCombo = new JComboBox<>();
        targetCombo.addItem("Goblins");
        targetCombo.addItem("Cows");
        targetCombo.addItem("Guards");
        
        add(new JLabel("Target:"));
        add(targetCombo);
    }
}
```

### Real-time Updates
```java
// Update UI from script thread
SwingUtilities.invokeLater(() -> {
    statsPanel.updateXP(getXPGained());
    statsPanel.updateProfit(getProfit());
    statsPanel.updateRuntime(getRuntime());
});
```

This reference guide provides comprehensive coverage of the DreamBot API methods and patterns most relevant to combat script development. Use this as a quick reference while implementing the enhancement roadmap.