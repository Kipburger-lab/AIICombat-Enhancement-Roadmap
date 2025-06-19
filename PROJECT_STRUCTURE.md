# Project Structure Template 📁

Recommended project structure for the enhanced AIICombat script following modern Java development practices.

## Directory Structure

```
AIICombat/
├── pom.xml                          # Maven configuration
├── README.md                        # Project documentation
├── CHANGELOG.md                     # Version history
├── LICENSE                          # License file
├── .gitignore                       # Git ignore rules
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org/
│   │   │       └── example/
│   │   │           └── aiicombat/
│   │   │               ├── AIICombatScript.java
│   │   │               ├── core/
│   │   │               │   ├── ScriptManager.java
│   │   │               │   ├── ConfigurationManager.java
│   │   │               │   ├── StatisticsManager.java
│   │   │               │   └── EventManager.java
│   │   │               ├── combat/
│   │   │               │   ├── CombatManager.java
│   │   │               │   ├── TargetSelector.java
│   │   │               │   ├── CombatState.java
│   │   │               │   ├── strategies/
│   │   │               │   │   ├── CombatStrategy.java
│   │   │               │   │   ├── MeleeStrategy.java
│   │   │               │   │   ├── RangedStrategy.java
│   │   │               │   │   ├── MagicStrategy.java
│   │   │               │   │   └── HybridStrategy.java
│   │   │               │   ├── prayer/
│   │   │               │   │   ├── PrayerManager.java
│   │   │               │   │   └── PrayerStrategy.java
│   │   │               │   └── special/
│   │   │               │       ├── SpecialAttackManager.java
│   │   │               │       └── WeaponSpecials.java
│   │   │               ├── movement/
│   │   │               │   ├── MovementManager.java
│   │   │               │   ├── SafespotManager.java
│   │   │               │   ├── PathfindingManager.java
│   │   │               │   └── AreaManager.java
│   │   │               ├── inventory/
│   │   │               │   ├── InventoryManager.java
│   │   │               │   ├── FoodManager.java
│   │   │               │   ├── PotionManager.java
│   │   │               │   └── EquipmentManager.java
│   │   │               ├── looting/
│   │   │               │   ├── LootManager.java
│   │   │               │   ├── LootFilter.java
│   │   │               │   └── LootPriority.java
│   │   │               ├── banking/
│   │   │               │   ├── BankManager.java
│   │   │               │   ├── BankingStrategy.java
│   │   │               │   └── WithdrawPlan.java
│   │   │               ├── antiban/
│   │   │               │   ├── AntiBanManager.java
│   │   │               │   ├── HumanBehavior.java
│   │   │               │   ├── MouseMovement.java
│   │   │               │   ├── CameraManager.java
│   │   │               │   ├── BreakManager.java
│   │   │               │   └── patterns/
│   │   │               │       ├── BehaviorPattern.java
│   │   │               │       ├── IdlePattern.java
│   │   │               │       ├── MistakePattern.java
│   │   │               │       └── AttentionPattern.java
│   │   │               ├── ui/
│   │   │               │   ├── MainPanel.java
│   │   │               │   ├── ConfigPanel.java
│   │   │               │   ├── StatsPanel.java
│   │   │               │   ├── LogPanel.java
│   │   │               │   ├── components/
│   │   │               │   │   ├── ModernButton.java
│   │   │               │   │   ├── ModernSlider.java
│   │   │               │   │   ├── ModernComboBox.java
│   │   │               │   │   ├── ProgressBar.java
│   │   │               │   │   └── StatusIndicator.java
│   │   │               │   ├── themes/
│   │   │               │   │   ├── Theme.java
│   │   │               │   │   ├── DarkTheme.java
│   │   │               │   │   ├── LightTheme.java
│   │   │               │   │   └── CustomTheme.java
│   │   │               │   └── dialogs/
│   │   │               │       ├── SetupWizard.java
│   │   │               │       ├── SettingsDialog.java
│   │   │               │       └── AboutDialog.java
│   │   │               ├── utils/
│   │   │               │   ├── Sleep.java
│   │   │               │   ├── MouseMotion.java
│   │   │               │   ├── Logger.java
│   │   │               │   ├── MathUtils.java
│   │   │               │   ├── StringUtils.java
│   │   │               │   ├── TimeUtils.java
│   │   │               │   └── ValidationUtils.java
│   │   │               ├── data/
│   │   │               │   ├── ItemData.java
│   │   │               │   ├── NPCData.java
│   │   │               │   ├── LocationData.java
│   │   │               │   ├── PriceData.java
│   │   │               │   └── GameConstants.java
│   │   │               ├── ai/
│   │   │               │   ├── DecisionEngine.java
│   │   │               │   ├── LearningAlgorithm.java
│   │   │               │   ├── PatternRecognition.java
│   │   │               │   └── OptimizationEngine.java
│   │   │               └── exceptions/
│   │   │                   ├── CombatException.java
│   │   │                   ├── ConfigurationException.java
│   │   │                   ├── BankingException.java
│   │   │                   └── MovementException.java
│   │   └── resources/
│   │       ├── configurations/
│   │       │   ├── default_config.json
│   │       │   ├── combat_profiles/
│   │       │   │   ├── melee_training.json
│   │       │   │   ├── ranged_training.json
│   │       │   │   ├── magic_training.json
│   │       │   │   └── boss_combat.json
│   │       │   └── location_profiles/
│   │       │       ├── lumbridge_cows.json
│   │       │       ├── varrock_guards.json
│   │       │       ├── edgeville_men.json
│   │       │       └── stronghold_security.json
│   │       ├── data/
│   │       │   ├── items.json
│   │       │   ├── npcs.json
│   │       │   ├── locations.json
│   │       │   └── prices.json
│   │       ├── ui/
│   │       │   ├── icons/
│   │       │   │   ├── combat.png
│   │       │   │   ├── stats.png
│   │       │   │   ├── settings.png
│   │       │   │   └── logo.png
│   │       │   ├── themes/
│   │       │   │   ├── dark.css
│   │       │   │   ├── light.css
│   │       │   │   └── custom.css
│   │       │   └── layouts/
│   │       │       ├── main_layout.xml
│   │       │       ├── config_layout.xml
│   │       │       └── stats_layout.xml
│   │       └── scripts/
│   │           ├── setup.sql
│   │           └── migration.sql
│   └── test/
│       ├── java/
│       │   └── org/
│       │       └── example/
│       │           └── aiicombat/
│       │               ├── combat/
│       │               │   ├── CombatManagerTest.java
│       │               │   ├── TargetSelectorTest.java
│       │               │   └── strategies/
│       │               │       ├── MeleeStrategyTest.java
│       │               │       ├── RangedStrategyTest.java
│       │               │       └── MagicStrategyTest.java
│       │               ├── inventory/
│       │               │   ├── InventoryManagerTest.java
│       │               │   ├── FoodManagerTest.java
│       │               │   └── PotionManagerTest.java
│       │               ├── antiban/
│       │               │   ├── AntiBanManagerTest.java
│       │               │   └── HumanBehaviorTest.java
│       │               ├── utils/
│       │               │   ├── SleepTest.java
│       │               │   ├── MathUtilsTest.java
│       │               │   └── ValidationUtilsTest.java
│       │               └── integration/
│       │                   ├── CombatIntegrationTest.java
│       │                   ├── BankingIntegrationTest.java
│       │                   └── FullScriptTest.java
│       └── resources/
│           ├── test_configurations/
│           │   ├── test_config.json
│           │   └── mock_data.json
│           └── test_data/
│               ├── sample_items.json
│               └── sample_npcs.json
├── docs/
│   ├── API_DOCUMENTATION.md
│   ├── USER_GUIDE.md
│   ├── DEVELOPER_GUIDE.md
│   ├── TROUBLESHOOTING.md
│   ├── CHANGELOG.md
│   └── images/
│       ├── screenshots/
│       ├── diagrams/
│       └── tutorials/
├── scripts/
│   ├── build.bat
│   ├── build.sh
│   ├── deploy.bat
│   ├── deploy.sh
│   ├── test.bat
│   └── test.sh
└── tools/
    ├── code_formatter.xml
    ├── checkstyle.xml
    ├── findbugs.xml
    └── pmd.xml
```

## Key Components Description

### Core Package (`core/`)
- **ScriptManager**: Main script lifecycle management
- **ConfigurationManager**: Settings and configuration handling
- **StatisticsManager**: Performance tracking and analytics
- **EventManager**: Event-driven architecture support

### Combat Package (`combat/`)
- **CombatManager**: Central combat coordination
- **TargetSelector**: Intelligent target selection logic
- **CombatState**: State machine for combat phases
- **Strategies**: Different combat approach implementations
- **Prayer**: Prayer management and switching
- **Special**: Special attack coordination

### Movement Package (`movement/`)
- **MovementManager**: Pathfinding and navigation
- **SafespotManager**: Safespot detection and utilization
- **PathfindingManager**: Advanced pathfinding algorithms
- **AreaManager**: Area-based logic and boundaries

### Inventory Package (`inventory/`)
- **InventoryManager**: Inventory space and item management
- **FoodManager**: Food consumption strategies
- **PotionManager**: Potion usage optimization
- **EquipmentManager**: Equipment switching and management

### Looting Package (`looting/`)
- **LootManager**: Ground item collection
- **LootFilter**: Item value and priority filtering
- **LootPriority**: Dynamic priority adjustment

### Banking Package (`banking/`)
- **BankManager**: Banking operations coordination
- **BankingStrategy**: Different banking approaches
- **WithdrawPlan**: Optimized withdrawal planning

### Anti-ban Package (`antiban/`)
- **AntiBanManager**: Anti-detection coordination
- **HumanBehavior**: Human-like behavior simulation
- **MouseMovement**: Realistic mouse patterns
- **CameraManager**: Natural camera movements
- **BreakManager**: Break scheduling and management
- **Patterns**: Specific behavior pattern implementations

### UI Package (`ui/`)
- **MainPanel**: Primary user interface
- **ConfigPanel**: Configuration interface
- **StatsPanel**: Statistics display
- **LogPanel**: Logging and debug information
- **Components**: Custom UI components
- **Themes**: Visual theme management
- **Dialogs**: Modal dialogs and wizards

### Utils Package (`utils/`)
- **Sleep**: Enhanced sleep utilities
- **MouseMotion**: Mouse movement utilities
- **Logger**: Comprehensive logging system
- **MathUtils**: Mathematical calculations
- **StringUtils**: String manipulation utilities
- **TimeUtils**: Time and duration utilities
- **ValidationUtils**: Input validation utilities

### Data Package (`data/`)
- **ItemData**: Item information and properties
- **NPCData**: NPC information and behavior
- **LocationData**: Location-specific data
- **PriceData**: Item pricing information
- **GameConstants**: Game-related constants

### AI Package (`ai/`)
- **DecisionEngine**: AI-driven decision making
- **LearningAlgorithm**: Machine learning implementations
- **PatternRecognition**: Pattern detection and analysis
- **OptimizationEngine**: Performance optimization

### Exceptions Package (`exceptions/`)
- Custom exception classes for different error scenarios

## Configuration Files

### Maven Configuration (`pom.xml`)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>org.example</groupId>
    <artifactId>aiicombat</artifactId>
    <version>2.0.0</version>
    <packaging>jar</packaging>
    
    <name>AII Combat Script</name>
    <description>Advanced combat script for DreamBot with AI features</description>
    
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    
    <dependencies>
        <!-- DreamBot API -->
        <dependency>
            <groupId>org.dreambot</groupId>
            <artifactId>dreambot-api</artifactId>
            <version>LATEST</version>
            <scope>provided</scope>
        </dependency>
        
        <!-- JSON Processing -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.10.1</version>
        </dependency>
        
        <!-- Logging -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>2.0.7</version>
        </dependency>
        
        <!-- Testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
        
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-core</artifactId>
            <version>5.3.1</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
            
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.1.2</version>
            </plugin>
            
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.5.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

### Git Ignore (`.gitignore`)
```
# Compiled class files
*.class

# Log files
*.log

# Package files
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# Maven
target/
pom.xml.tag
pom.xml.releaseBackup
pom.xml.versionsBackup
pom.xml.next
release.properties
dependency-reduced-pom.xml
buildNumber.properties
.mvn/timing.properties
.mvn/wrapper/maven-wrapper.jar

# IDE files
.idea/
*.iws
*.iml
*.ipr
.vscode/
*.swp
*.swo
*~

# OS generated files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# Configuration files with sensitive data
config/local_config.json
config/production_config.json
*.key
*.pem

# Runtime files
runtime/
logs/
temp/
cache/

# Test output
test-output/
```

### Default Configuration (`src/main/resources/configurations/default_config.json`)
```json
{
  "script": {
    "name": "AII Combat Script",
    "version": "2.0.0",
    "author": "Your Name"
  },
  "combat": {
    "style": "MELEE",
    "targets": ["Goblin", "Cow"],
    "maxDistance": 10,
    "prioritizeClosest": true,
    "useSpecialAttack": true,
    "specialAttackThreshold": 50
  },
  "food": {
    "enabled": true,
    "types": ["Lobster", "Swordfish", "Tuna"],
    "eatAtHealth": 50,
    "emergencyEatAtHealth": 30
  },
  "prayer": {
    "enabled": false,
    "restoreAtPoints": 10,
    "potionTypes": ["Prayer potion", "Super restore"]
  },
  "looting": {
    "enabled": true,
    "minimumValue": 100,
    "priorityItems": ["Coins", "Rune items"],
    "maxLootDistance": 5
  },
  "banking": {
    "enabled": true,
    "bankWhenFull": true,
    "keepItems": ["Weapon", "Shield", "Food"]
  },
  "antiban": {
    "enabled": true,
    "mouseVariation": 5,
    "cameraMovement": true,
    "idleActions": true,
    "breakSystem": {
      "enabled": true,
      "minBreakTime": 300000,
      "maxBreakTime": 900000,
      "breakFrequency": 7200000
    }
  },
  "ui": {
    "theme": "DARK",
    "showStatistics": true,
    "showLogs": true,
    "updateInterval": 1000
  }
}
```

## Development Guidelines

### Package Naming Conventions
- Use lowercase package names
- Follow reverse domain naming (org.example.aiicombat)
- Group related functionality in packages
- Keep package names concise but descriptive

### Class Naming Conventions
- Use PascalCase for class names
- Use descriptive names that indicate purpose
- Suffix interfaces with appropriate terms (Manager, Strategy, etc.)
- Use meaningful abbreviations sparingly

### File Organization
- One public class per file
- File name matches class name
- Group related classes in same package
- Separate test classes in test directory structure

### Resource Management
- Store configuration files in resources/configurations/
- Keep data files in resources/data/
- Organize UI resources in resources/ui/
- Use appropriate file formats (JSON for config, PNG for images)

### Testing Structure
- Mirror main package structure in test directory
- Use descriptive test method names
- Group related tests in same test class
- Separate unit tests from integration tests

This project structure provides a solid foundation for developing a sophisticated, maintainable, and scalable combat script that can grow from basic functionality to advanced AI-driven features.