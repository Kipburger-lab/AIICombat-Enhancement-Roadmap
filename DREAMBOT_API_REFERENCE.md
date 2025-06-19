# DreamBot API Reference

This document provides comprehensive reference information for the DreamBot API, including core classes, methods, and usage patterns for developing sophisticated OSRS scripts.

## Core API Classes and Methods

### Player Management
- **getLocalPlayer()**: Returns the local player instance
- **getPlayers()**: Access to all players in the area
- **Player.getHealthPercent()**: Get player health percentage
- **Player.getAnimation()**: Get current player animation
- **Player.isMoving()**: Check if player is moving
- **Player.getTile()**: Get player's current tile position
- **Player.getInteracting()**: Get entity player is interacting with

### NPC Management
- **getNPCs()**: Access to all NPCs in the area
- **NPC.getHealthPercent()**: Get NPC health percentage
- **NPC.isInCombat()**: Check if NPC is in combat
- **NPC.getInteracting()**: Get entity NPC is interacting with
- **NPC.distance()**: Calculate distance to NPC
- **NPC.interact()**: Interact with NPC

### Combat System
- **getCombat()**: Access combat methods
- **Combat.isInCombat()**: Check if player is in combat
- **Combat.getTarget()**: Get current combat target
- **Combat.attack()**: Attack specified target
- **Combat.setAutoRetaliate()**: Enable/disable auto retaliate
- **Combat.getWildernessLevel()**: Get wilderness level
- **Combat.canAttack()**: Check if target can be attacked

### Inventory Management
- **getInventory()**: Access inventory methods
- **Inventory.contains()**: Check if inventory contains item
- **Inventory.count()**: Count items in inventory
- **Inventory.interact()**: Interact with inventory item
- **Inventory.drop()**: Drop item from inventory
- **Inventory.use()**: Use item on target
- **Inventory.getEmptySlots()**: Get number of empty slots
- **Inventory.isFull()**: Check if inventory is full

### Equipment Management
- **getEquipment()**: Access equipment methods
- **Equipment.contains()**: Check if equipment contains item
- **Equipment.getWeapon()**: Get equipped weapon
- **Equipment.getArmour()**: Get equipped armour pieces
- **Equipment.interact()**: Interact with equipped item

### Prayer System
- **getPrayer()**: Access prayer methods
- **Prayer.isActive()**: Check if prayer is active
- **Prayer.toggle()**: Toggle prayer on/off
- **Prayer.getPoints()**: Get current prayer points
- **Prayer.canUse()**: Check if prayer can be used

### Movement and Walking
- **getWalking()**: Access walking methods
- **Walking.walk()**: Walk to specified tile/area
- **Walking.walkPath()**: Walk along specified path
- **Walking.isRunEnabled()**: Check if run is enabled
- **Walking.setRun()**: Enable/disable running
- **Walking.getDestination()**: Get current walking destination
- **Walking.isMoving()**: Check if player is moving

### Ground Items
- **getGroundItems()**: Access ground items
- **GroundItem.interact()**: Interact with ground item
- **GroundItem.distance()**: Calculate distance to item
- **GroundItem.getTile()**: Get item's tile position

### Banking
- **getBank()**: Access banking methods
- **Bank.isOpen()**: Check if bank is open
- **Bank.open()**: Open bank interface
- **Bank.close()**: Close bank interface
- **Bank.contains()**: Check if bank contains item
- **Bank.withdraw()**: Withdraw items from bank
- **Bank.deposit()**: Deposit items to bank
- **Bank.depositAll()**: Deposit all items
- **Bank.depositAllExcept()**: Deposit all except specified items

### Interface and Tabs
- **getTabs()**: Access game tabs
- **Tabs.open()**: Open specified tab
- **Tabs.isOpen()**: Check if tab is open
- **getDialogues()**: Access dialogue system
- **Dialogues.inDialogue()**: Check if in dialogue
- **Dialogues.continueDialogue()**: Continue dialogue
- **Dialogues.selectOption()**: Select dialogue option

### Camera Control
- **getCamera()**: Access camera methods
- **Camera.rotateToTile()**: Rotate camera to tile
- **Camera.rotateTo()**: Rotate camera to angle
- **Camera.mouseRotate()**: Rotate using mouse
- **Camera.getPitch()**: Get camera pitch
- **Camera.getYaw()**: Get camera yaw

### Mouse and Keyboard
- **getMouse()**: Access mouse methods
- **Mouse.click()**: Click at coordinates
- **Mouse.move()**: Move mouse to coordinates
- **Mouse.drag()**: Drag mouse between coordinates
- **getKeyboard()**: Access keyboard methods
- **Keyboard.type()**: Type text
- **Keyboard.pressKey()**: Press specific key

### Utilities
- **Timer**: Time-based operations
- **Sleep**: Delay execution
- **Random**: Generate random values
- **Condition**: Wait for conditions
- **Filter**: Filter collections

### Grand Exchange System
- **getGrandExchange()**: Access Grand Exchange methods
- **GrandExchange.isOpen()**: Check if GE interface is open
- **GrandExchange.open()**: Open Grand Exchange interface
- **GrandExchange.close()**: Close Grand Exchange interface
- **GrandExchange.buyItem()**: Place buy offer for item
- **GrandExchange.sellItem()**: Place sell offer for item
- **GrandExchange.getOffers()**: Get current GE offers
- **GrandExchange.collectOffer()**: Collect completed offer
- **GrandExchange.cancelOffer()**: Cancel active offer
- **GrandExchange.getOfferStatus()**: Get status of specific offer
- **GrandExchange.setPrice()**: Set price for offer
- **GrandExchange.setQuantity()**: Set quantity for offer

### Live Prices System
- **getLivePrices()**: Access live price data
- **LivePrices.get()**: Get current price for item
- **LivePrices.getAverage()**: Get average price for item
- **LivePrices.getHigh()**: Get high price for item
- **LivePrices.getLow()**: Get low price for item
- **LivePrices.getLastUpdate()**: Get last price update time
- **LivePrices.isAvailable()**: Check if price data is available
- **LivePrices.getMarginData()**: Get profit margin information
- **LivePrices.getTrend()**: Get price trend data

### Widget System
- **getWidgets()**: Access widget methods
- **Widgets.get()**: Get widget by ID
- **Widgets.getWidgetChild()**: Get child widget
- **Widgets.isVisible()**: Check if widget is visible
- **Widgets.interact()**: Interact with widget
- **Widgets.getText()**: Get widget text content
- **Widgets.getChildren()**: Get all child widgets
- **Widgets.find()**: Find widgets matching criteria
- **Widget.click()**: Click on widget
- **Widget.hover()**: Hover over widget
- **Widget.getBounds()**: Get widget boundaries
- **Widget.getItemId()**: Get item ID from widget
- **Widget.getItemAmount()**: Get item amount from widget

## Advanced API Usage Patterns

### Conditional Waiting
```java
// Wait for condition with timeout
Condition.wait(() -> getLocalPlayer().isMoving(), 5000, 100);

// Wait for combat to end
Condition.wait(() -> !getCombat().isInCombat(), 10000, 500);

// Wait for inventory change
Condition.wait(() -> getInventory().contains("Logs"), 3000, 200);
```

### Entity Filtering
```java
// Filter NPCs by name and combat status
List<NPC> targets = getNPCs().all(npc -> 
    npc.getName().equals("Goblin") && 
    !npc.isInCombat() && 
    npc.getHealthPercent() == 100
);

// Filter ground items by value
List<GroundItem> valuableItems = getGroundItems().all(item -> 
    getLivePrices().get(item.getID()) > 1000
);
```

### Area Management
```java
// Define combat area
Area combatArea = new Area(3200, 3200, 3210, 3210);

// Check if player is in area
if (combatArea.contains(getLocalPlayer())) {
    // Execute combat logic
}

// Walk to area if not present
if (!combatArea.contains(getLocalPlayer())) {
    getWalking().walk(combatArea.getRandomTile());
}
```

### State Management
```java
public enum ScriptState {
    BANKING,
    WALKING_TO_COMBAT,
    FIGHTING,
    LOOTING,
    RESTOCKING
}

public ScriptState getCurrentState() {
    if (getInventory().isFull()) {
        return ScriptState.BANKING;
    } else if (getCombat().isInCombat()) {
        return ScriptState.FIGHTING;
    }
    // Additional state logic
    return ScriptState.WALKING_TO_COMBAT;
}
```

### Grand Exchange Trading
```java
// Check item prices before trading
int currentPrice = getLivePrices().get(itemId);
int averagePrice = getLivePrices().getAverage(itemId);

// Place buy offer with margin
if (getGrandExchange().isOpen()) {
    getGrandExchange().buyItem(itemId, quantity, currentPrice + 100);
}

// Monitor offer status
if (getGrandExchange().getOfferStatus(0) == OfferStatus.COMPLETED) {
    getGrandExchange().collectOffer(0);
}
```

### Widget Interaction
```java
// Interact with specific widget
Widget geWidget = getWidgets().get(465, 7); // GE interface
if (geWidget != null && geWidget.isVisible()) {
    geWidget.click();
}

// Find and interact with dynamic widgets
List<Widget> buttons = getWidgets().find(w -> 
    w.getText().contains("Buy") && w.isVisible()
);
```

## Error Handling Best Practices

### Null Checking
```java
Player target = getPlayers().closest("PlayerName");
if (target != null && target.isValid()) {
    // Safe to interact
    target.interact("Trade with");
}
```

### Exception Handling
```java
try {
    getWalking().walk(destinationTile);
} catch (Exception e) {
    log("Walking failed: " + e.getMessage());
    // Implement fallback logic
}
```

### Timeout Handling
```java
long timeout = System.currentTimeMillis() + 10000;
while (System.currentTimeMillis() < timeout) {
    if (condition) {
        break;
    }
    sleep(100);
}
```

## Performance Optimization

### Efficient Entity Queries
```java
// Use closest() instead of iterating all entities
NPC target = getNPCs().closest("Goblin");

// Cache frequently accessed entities
private NPC cachedTarget;
private long lastTargetUpdate;

public NPC getTarget() {
    if (System.currentTimeMillis() - lastTargetUpdate > 1000) {
        cachedTarget = getNPCs().closest("Goblin");
        lastTargetUpdate = System.currentTimeMillis();
    }
    return cachedTarget;
}
```

### Minimize API Calls
```java
// Store frequently used values
Player localPlayer = getLocalPlayer();
Tile playerTile = localPlayer.getTile();
int playerHealth = localPlayer.getHealthPercent();

// Use stored values instead of repeated API calls
if (playerHealth < 30) {
    // Emergency logic
}
```

### Conditional Processing
```java
// Only process when necessary
if (getCombat().isInCombat()) {
    // Combat-specific logic only when in combat
    handleCombat();
} else if (getInventory().isFull()) {
    // Banking logic only when inventory is full
    handleBanking();
}
```

## UI Integration

### Creating Custom Panels
```java
public class ScriptGUI extends JPanel {
    private JLabel statusLabel;
    private JButton startButton;
    
    public ScriptGUI() {
        setLayout(new BorderLayout());
        initializeComponents();
    }
    
    private void initializeComponents() {
        statusLabel = new JLabel("Status: Idle");
        startButton = new JButton("Start");
        
        add(statusLabel, BorderLayout.NORTH);
        add(startButton, BorderLayout.SOUTH);
    }
    
    public void updateStatus(String status) {
        SwingUtilities.invokeLater(() -> {
            statusLabel.setText("Status: " + status);
        });
    }
}
```

### Real-time Updates
```java
// Update GUI with current script state
public void onLoop() {
    if (gui != null) {
        gui.updateStatus(getCurrentState().toString());
        gui.updateStats(getExperienceGained(), getItemsLooted());
    }
}
```

## Price Checking and Market Analysis

### Real-time Price Monitoring
```java
// Monitor price changes
public void monitorPrices(int itemId) {
    int currentPrice = getLivePrices().get(itemId);
    int averagePrice = getLivePrices().getAverage(itemId);
    
    if (currentPrice < averagePrice * 0.9) {
        // Price is 10% below average - good buy opportunity
        log("Buy opportunity detected for item: " + itemId);
    }
}

// Calculate profit margins
public int calculateProfit(int itemId, int buyPrice, int sellPrice) {
    int geFeeBuy = (int) (buyPrice * 0.01); // 1% GE fee
    int geFeeSell = (int) (sellPrice * 0.01);
    return sellPrice - buyPrice - geFeeBuy - geFeeSell;
}
```

### Market Trend Analysis
```java
// Analyze price trends
public boolean isPriceRising(int itemId) {
    // Implementation would track price history
    return getLivePrices().getTrend(itemId) > 0;
}

// Find profitable items
public List<Integer> findProfitableItems(List<Integer> itemIds) {
    return itemIds.stream()
        .filter(id -> calculateProfit(id, 
            getLivePrices().getLow(id), 
            getLivePrices().getHigh(id)) > 1000)
        .collect(Collectors.toList());
}
```

This reference provides the foundation for building sophisticated, efficient, and user-friendly OSRS scripts using the DreamBot API. Always ensure your scripts follow DreamBot's terms of service and OSRS rules.