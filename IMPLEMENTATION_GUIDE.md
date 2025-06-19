# Implementation Guide 🛠️

Detailed technical implementation guidance for each phase of the AIICombat enhancement roadmap.

## Phase 1: Foundation & Core Improvements

### 1.1 Code Structure & Architecture

#### Package Structure
```
org.example.aiicombat/
├── core/
│   ├── AIICombatScript.java
│   ├── ScriptManager.java
│   └── ConfigurationManager.java
├── combat/
│   ├── CombatManager.java
│   ├── TargetSelector.java
│   ├── CombatStyle.java
│   └── strategies/
│       ├── MeleeStrategy.java
│       ├── RangedStrategy.java
│       └── MagicStrategy.java
├── ui/
│   ├── MainPanel.java
│   ├── ConfigPanel.java
│   ├── StatsPanel.java
│   └── components/
├── utils/
│   ├── Sleep.java
│   ├── MouseMotion.java
│   ├── Logger.java
│   └── MathUtils.java
├── antiban/
│   ├── AntiBanManager.java
│   ├── HumanBehavior.java
│   └── patterns/
├── data/
│   ├── ItemData.java
│   ├── NPCData.java
│   └── LocationData.java
└── resources/
    ├── configurations/
    ├── ui/
    └── data/
```

#### Configuration System Implementation
```java
// ConfigurationManager.java
public class ConfigurationManager {
    private static final String CONFIG_FILE = "aiicombat_config.json";
    private JsonObject config;
    
    public void loadConfiguration() {
        try {
            String content = Files.readString(Paths.get(CONFIG_FILE));
            config = JsonParser.parseString(content).getAsJsonObject();
        } catch (Exception e) {
            loadDefaultConfiguration();
        }
    }
    
    public void saveConfiguration() {
        try (FileWriter writer = new FileWriter(CONFIG_FILE)) {
            Gson gson = new GsonBuilder().setPrettyPrinting().create();
            gson.toJson(config, writer);
        } catch (IOException e) {
            Logger.error("Failed to save configuration: " + e.getMessage());
        }
    }
    
    private void loadDefaultConfiguration() {
        config = new JsonObject();
        // Set default values
        config.addProperty("combatStyle", "MELEE");
        config.addProperty("eatAtHealth", 50);
        config.addProperty("usePrayer", false);
        // ... more defaults
    }
}
```

#### Enhanced Logging System
```java
// Logger.java
public class Logger {
    private static final java.util.logging.Logger LOGGER = 
        java.util.logging.Logger.getLogger("AIICombat");
    private static FileHandler fileHandler;
    
    static {
        try {
            fileHandler = new FileHandler("aiicombat.log", true);
            fileHandler.setFormatter(new SimpleFormatter());
            LOGGER.addHandler(fileHandler);
            LOGGER.setLevel(Level.INFO);
        } catch (IOException e) {
            System.err.println("Failed to initialize logger: " + e.getMessage());
        }
    }
    
    public static void info(String message) {
        LOGGER.info(message);
    }
    
    public static void debug(String message) {
        LOGGER.fine(message);
    }
    
    public static void error(String message) {
        LOGGER.severe(message);
    }
    
    public static void error(String message, Throwable throwable) {
        LOGGER.log(Level.SEVERE, message, throwable);
    }
}
```

### 1.2 Basic Combat Enhancements

#### Combat Strategy Pattern
```java
// CombatStrategy.java
public interface CombatStrategy {
    boolean canEngage(NPC target);
    void engage(NPC target);
    void handleCombat();
    boolean shouldEat();
    boolean shouldDrink();
}

// MeleeStrategy.java
public class MeleeStrategy implements CombatStrategy {
    @Override
    public boolean canEngage(NPC target) {
        return target != null && 
               target.hasAction("Attack") && 
               !Players.getLocal().isInCombat() &&
               target.distance() <= 1;
    }
    
    @Override
    public void engage(NPC target) {
        if (target.interact("Attack")) {
            Sleep.sleepUntil(() -> Players.getLocal().isInCombat(), 3000);
        }
    }
    
    @Override
    public void handleCombat() {
        if (shouldEat()) {
            eatFood();
        }
        if (shouldUseSpecial()) {
            useSpecialAttack();
        }
    }
    
    private boolean shouldUseSpecial() {
        return Combat.getSpecialPercentage() >= 50 && 
               Players.getLocal().isInCombat();
    }
}
```

#### Enhanced Target Selection
```java
// TargetSelector.java
public class TargetSelector {
    private List<String> targetNames;
    private int maxDistance;
    private boolean prioritizeClosest;
    
    public NPC selectTarget() {
        List<NPC> validTargets = NPCs.all(npc -> 
            isValidTarget(npc) && 
            npc.distance() <= maxDistance &&
            !npc.isInCombat()
        );
        
        if (validTargets.isEmpty()) {
            return null;
        }
        
        if (prioritizeClosest) {
            return validTargets.stream()
                .min(Comparator.comparing(Entity::distance))
                .orElse(null);
        }
        
        return validTargets.get(Random.nextInt(validTargets.size()));
    }
    
    private boolean isValidTarget(NPC npc) {
        return npc != null &&
               npc.hasAction("Attack") &&
               targetNames.contains(npc.getName()) &&
               npc.getHealthPercent() > 0;
    }
}
```

## Phase 2: Advanced Combat Features

### 2.1 Safespotting System
```java
// SafespotManager.java
public class SafespotManager {
    private List<Tile> knownSafespots;
    private Tile currentSafespot;
    
    public boolean isInSafespot() {
        return currentSafespot != null && 
               Players.getLocal().getTile().equals(currentSafespot);
    }
    
    public boolean moveToSafespot(NPC target) {
        Tile safespot = findNearestSafespot(target);
        if (safespot != null) {
            if (Walking.walk(safespot)) {
                currentSafespot = safespot;
                return Sleep.sleepUntil(() -> 
                    Players.getLocal().getTile().equals(safespot), 5000);
            }
        }
        return false;
    }
    
    private Tile findNearestSafespot(NPC target) {
        return knownSafespots.stream()
            .filter(tile -> canAttackFrom(tile, target))
            .min(Comparator.comparing(tile -> 
                tile.distance(Players.getLocal().getTile())))
            .orElse(null);
    }
    
    private boolean canAttackFrom(Tile tile, NPC target) {
        // Check if we can attack the target from this tile
        // and if the target cannot reach us
        return tile.distance(target.getTile()) <= 10 && // Attack range
               !isReachableByNPC(tile, target);
    }
}
```

### 2.2 Prayer Management
```java
// PrayerManager.java
public class PrayerManager {
    private Map<Prayer, Integer> prayerPriorities;
    private int minPrayerPoints;
    
    public void handlePrayer(NPC target) {
        if (Prayer.getPrayerPoints() < minPrayerPoints) {
            drinkPrayerPotion();
            return;
        }
        
        if (target != null && target.isInCombat()) {
            activateDefensivePrayers(target);
        }
        
        activateOffensivePrayers();
    }
    
    private void activateDefensivePrayers(NPC target) {
        String attackStyle = getTargetAttackStyle(target);
        
        switch (attackStyle) {
            case "MELEE":
                if (!Prayer.PROTECT_FROM_MELEE.isActive()) {
                    Prayer.PROTECT_FROM_MELEE.toggle(true);
                }
                break;
            case "RANGED":
                if (!Prayer.PROTECT_FROM_MISSILES.isActive()) {
                    Prayer.PROTECT_FROM_MISSILES.toggle(true);
                }
                break;
            case "MAGIC":
                if (!Prayer.PROTECT_FROM_MAGIC.isActive()) {
                    Prayer.PROTECT_FROM_MAGIC.toggle(true);
                }
                break;
        }
    }
}
```

## Phase 3: Anti-Detection Implementation

### 3.1 Human-like Mouse Movement
```java
// HumanMouseMovement.java
public class HumanMouseMovement {
    private static final Random random = new Random();
    
    public static void humanClick(Entity entity) {
        Rectangle bounds = entity.getBounds();
        if (bounds != null) {
            // Add randomness to click position
            int x = bounds.x + random.nextInt(bounds.width);
            int y = bounds.y + random.nextInt(bounds.height);
            
            // Simulate human-like movement
            moveMouseHumanLike(x, y);
            
            // Random delay before click
            Sleep.sleep(50 + random.nextInt(100));
            
            Mouse.click(x, y);
        }
    }
    
    private static void moveMouseHumanLike(int targetX, int targetY) {
        Point current = Mouse.getPosition();
        
        // Calculate bezier curve points
        List<Point> path = generateBezierPath(current, new Point(targetX, targetY));
        
        for (Point point : path) {
            Mouse.move(point.x, point.y);
            Sleep.sleep(10 + random.nextInt(20));
        }
    }
    
    private static List<Point> generateBezierPath(Point start, Point end) {
        List<Point> path = new ArrayList<>();
        
        // Generate control points for bezier curve
        Point control1 = new Point(
            start.x + random.nextInt(100) - 50,
            start.y + random.nextInt(100) - 50
        );
        Point control2 = new Point(
            end.x + random.nextInt(100) - 50,
            end.y + random.nextInt(100) - 50
        );
        
        // Generate path points along bezier curve
        for (double t = 0; t <= 1; t += 0.1) {
            Point point = calculateBezierPoint(t, start, control1, control2, end);
            path.add(point);
        }
        
        return path;
    }
}
```

### 3.2 Behavioral Randomization
```java
// BehaviorRandomizer.java
public class BehaviorRandomizer {
    private static final Random random = new Random();
    private long lastIdleAction;
    private long lastCameraMovement;
    
    public void performRandomBehavior() {
        long currentTime = System.currentTimeMillis();
        
        // Random idle actions every 30-120 seconds
        if (currentTime - lastIdleAction > (30000 + random.nextInt(90000))) {
            performIdleAction();
            lastIdleAction = currentTime;
        }
        
        // Random camera movements every 10-60 seconds
        if (currentTime - lastCameraMovement > (10000 + random.nextInt(50000))) {
            randomCameraMovement();
            lastCameraMovement = currentTime;
        }
        
        // Occasional misclicks (1% chance)
        if (random.nextInt(100) == 0) {
            performMisclick();
        }
    }
    
    private void performIdleAction() {
        int action = random.nextInt(5);
        
        switch (action) {
            case 0:
                // Check skills
                Tabs.open(Tab.STATS);
                Sleep.sleep(1000 + random.nextInt(2000));
                break;
            case 1:
                // Check inventory
                Tabs.open(Tab.INVENTORY);
                Sleep.sleep(500 + random.nextInt(1000));
                break;
            case 2:
                // Right-click examine something
                examineRandomObject();
                break;
            case 3:
                // Move camera slightly
                Camera.rotateToYaw(Camera.getYaw() + random.nextInt(60) - 30);
                break;
            case 4:
                // Brief pause (thinking)
                Sleep.sleep(2000 + random.nextInt(3000));
                break;
        }
    }
}
```

## Phase 4: Modern UI Implementation

### 4.1 Custom UI Framework
```java
// ModernPanel.java
public class ModernPanel extends JPanel {
    private Color primaryColor = new Color(45, 45, 45);
    private Color accentColor = new Color(0, 150, 255);
    private Color textColor = Color.WHITE;
    
    public ModernPanel() {
        setBackground(primaryColor);
        setLayout(new BorderLayout());
        setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
    }
    
    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D) g.create();
        
        // Enable anti-aliasing
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, 
                           RenderingHints.VALUE_ANTIALIAS_ON);
        
        // Draw rounded corners
        g2d.setColor(primaryColor);
        g2d.fillRoundRect(0, 0, getWidth(), getHeight(), 10, 10);
        
        g2d.dispose();
    }
}

// StatsPanel.java
public class StatsPanel extends ModernPanel {
    private JLabel xpGainedLabel;
    private JLabel profitLabel;
    private JLabel runtimeLabel;
    private Timer updateTimer;
    
    public StatsPanel() {
        super();
        initializeComponents();
        startUpdateTimer();
    }
    
    private void initializeComponents() {
        setLayout(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        
        // Title
        JLabel titleLabel = new JLabel("Statistics");
        titleLabel.setFont(new Font("Arial", Font.BOLD, 16));
        titleLabel.setForeground(Color.WHITE);
        gbc.gridx = 0; gbc.gridy = 0; gbc.gridwidth = 2;
        add(titleLabel, gbc);
        
        // XP Gained
        gbc.gridwidth = 1; gbc.gridy++;
        add(new JLabel("XP Gained:"), gbc);
        gbc.gridx = 1;
        xpGainedLabel = new JLabel("0");
        add(xpGainedLabel, gbc);
        
        // Profit
        gbc.gridx = 0; gbc.gridy++;
        add(new JLabel("Profit:"), gbc);
        gbc.gridx = 1;
        profitLabel = new JLabel("0 gp");
        add(profitLabel, gbc);
        
        // Runtime
        gbc.gridx = 0; gbc.gridy++;
        add(new JLabel("Runtime:"), gbc);
        gbc.gridx = 1;
        runtimeLabel = new JLabel("00:00:00");
        add(runtimeLabel, gbc);
    }
    
    private void startUpdateTimer() {
        updateTimer = new Timer(1000, e -> updateStats());
        updateTimer.start();
    }
    
    private void updateStats() {
        // Update statistics display
        SwingUtilities.invokeLater(() -> {
            xpGainedLabel.setText(String.valueOf(getXPGained()));
            profitLabel.setText(formatGold(getProfit()) + " gp");
            runtimeLabel.setText(formatRuntime(getRuntime()));
        });
    }
}
```

## Testing Guidelines

### Unit Testing Example
```java
// TargetSelectorTest.java
public class TargetSelectorTest {
    private TargetSelector targetSelector;
    
    @Before
    public void setUp() {
        targetSelector = new TargetSelector();
        targetSelector.setTargetNames(Arrays.asList("Goblin", "Cow"));
        targetSelector.setMaxDistance(10);
    }
    
    @Test
    public void testSelectTarget_ValidTargets() {
        // Mock NPCs
        NPC mockNPC = mock(NPC.class);
        when(mockNPC.getName()).thenReturn("Goblin");
        when(mockNPC.hasAction("Attack")).thenReturn(true);
        when(mockNPC.distance()).thenReturn(5.0);
        when(mockNPC.isInCombat()).thenReturn(false);
        when(mockNPC.getHealthPercent()).thenReturn(100);
        
        // Test target selection
        NPC selected = targetSelector.selectTarget();
        assertNotNull(selected);
        assertEquals("Goblin", selected.getName());
    }
    
    @Test
    public void testSelectTarget_NoValidTargets() {
        // Test with no valid targets
        NPC selected = targetSelector.selectTarget();
        assertNull(selected);
    }
}
```

### Integration Testing
```java
// CombatIntegrationTest.java
public class CombatIntegrationTest {
    @Test
    public void testFullCombatCycle() {
        // Test complete combat cycle from target selection to looting
        CombatManager combatManager = new CombatManager();
        
        // Setup test environment
        combatManager.initialize();
        
        // Simulate combat cycle
        combatManager.findAndEngageTarget();
        combatManager.handleCombat();
        combatManager.lootItems();
        
        // Verify expected outcomes
        assertTrue("Combat cycle should complete successfully", 
                  combatManager.isIdle());
    }
}
```

This implementation guide provides concrete code examples and patterns for each major component of the enhancement roadmap. Each section builds upon the previous one while maintaining script functionality throughout the development process.