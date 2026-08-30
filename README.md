# Base Guild Community

Bienvenido al espacio principal de la comunidad del **Base Guild**.

Base es una Layer 2 de Ethereum desarrollada por Coinbase. Ofrece transacciones rápidas, costos muy bajos y compatibilidad total con el ecosistema EVM.

Este repositorio sirve para coordinar actividades, dar la bienvenida a nuevos miembros y fomentar la colaboración on-chain.

# ¿Por qué construir en Base?

- Costos de gas muy bajos
- Alta velocidad de transacciones
- Integración con el ecosistema Coinbase
- Buena infraestructura de desarrollo
- Foco en productos reales y usabilidad

Ideal para iterar rápido y experimentar.

# Links útiles

- Docs: https://docs.base.org
- Bridge: https://bridge.base.org
- Explorer: https://basescan.org
- Status: https://status.base.org

Mantendremos esta lista actualizada.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Counter {
    uint256 public count;

    event CountChanged(uint256 newCount, address indexed by);

    function increment() external {
        count += 1;
        emit CountChanged(count, msg.sender);
    }

    function decrement() external {
        require(count > 0, "Count is zero");
        count -= 1;
        emit CountChanged(count, msg.sender);
    }

    function reset() external {
        count = 0;
        emit CountChanged(count, msg.sender);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Toggle {
    bool public isActive;

    event Toggled(bool newState, address indexed by);

    function toggle() external {
        isActive = !isActive;
        emit Toggled(isActive, msg.sender);
    }

    function setState(bool state) external {
        isActive = state;
        emit Toggled(state, msg.sender);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EventCounter {
    uint256 public count;
    mapping(address => uint256) public userCounts;

    event Incremented(address indexed user, uint256 newTotal, uint256 userTotal);

    function increment() external {
        count += 1;
        userCounts[msg.sender] += 1;
        emit Incremented(msg.sender, count, userCounts[msg.sender]);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Timestamp {
    uint256 public lastUpdate;
    address public lastUpdater;

    event Updated(address indexed user, uint256 timestamp);

    function update() external {
        lastUpdate = block.timestamp;
        lastUpdater = msg.sender;
        emit Updated(msg.sender, block.timestamp);
    }

    function getTimeSinceUpdate() external view returns (uint256) {
        if (lastUpdate == 0) return 0;
        return block.timestamp - lastUpdate;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Greeter {
    string private greeting;

    event GreetingUpdated(string newGreeting, address indexed by);

    constructor(string memory initialGreeting) {
        greeting = initialGreeting;
    }

    function setGreeting(string calldata newGreeting) external {
        greeting = newGreeting;
        emit GreetingUpdated(newGreeting, msg.sender);
    }

    function greet() external view returns (string memory) {
        return greeting;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ScoreBoard {
    mapping(address => uint256) public scores;

    event ScoreUpdated(address indexed user, uint256 newScore);

    function addScore(uint256 points) external {
        scores[msg.sender] += points;
        emit ScoreUpdated(msg.sender, scores[msg.sender]);
    }

    function setScore(uint256 newScore) external {
        scores[msg.sender] = newScore;
        emit ScoreUpdated(msg.sender, newScore);
    }

    function getScore(address user) external view returns (uint256) {
        return scores[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CounterWithLimit {
    uint256 public count;
    uint256 public constant MAX_COUNT = 100;

    event Incremented(uint256 newCount);
    event Reset();

    function increment() external {
        require(count < MAX_COUNT, "Max limit reached");
        count += 1;
        emit Incremented(count);
    }

    function reset() external {
        count = 0;
        emit Reset();
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Calculator {
    function add(uint256 a, uint256 b) external pure returns (uint256) {
        return a + b;
    }

    function subtract(uint256 a, uint256 b) external pure returns (uint256) {
        require(a >= b, "Result would be negative");
        return a - b;
    }

    function multiply(uint256 a, uint256 b) external pure returns (uint256) {
        return a * b;
    }

    function divide(uint256 a, uint256 b) external pure returns (uint256) {
        require(b > 0, "Cannot divide by zero");
        return a / b;
    }
}// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Rating {
    mapping(address => uint256) public ratings;
    mapping(address => bool) public hasRated;

    event Rated(address indexed user, uint256 score);

    function rate(uint256 score) external {
        require(score >= 1 && score <= 5, "Score must be 1-5");
        require(!hasRated[msg.sender], "Already rated");

        hasRated[msg.sender] = true;
        ratings[msg.sender] = score;
        emit Rated(msg.sender, score);
    }

    function getRating(address user) external view returns (uint256) {
        return ratings[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Bookmark {
    mapping(address => string) public bookmarks;

    event BookmarkSet(address indexed user, string url);

    function setBookmark(string calldata url) external {
        bookmarks[msg.sender] = url;
        emit BookmarkSet(msg.sender, url);
    }

    function getBookmark(address user) external view returns (string memory) {
        return bookmarks[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract NotePad {
    mapping(address => string) public notes;

    event NoteUpdated(address indexed user, string note);

    function writeNote(string calldata note) external {
        notes[msg.sender] = note;
        emit NoteUpdated(msg.sender, note);
    }

    function readNote(address user) external view returns (string memory) {
        return notes[user];
    }

    function clearNote() external {
        notes[msg.sender] = "";
        emit NoteUpdated(msg.sender, "");
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract FavoriteColor {
    mapping(address => string) public colors;

    event ColorSet(address indexed user, string color);

    function setColor(string calldata color) external {
        colors[msg.sender] = color;
        emit ColorSet(msg.sender, color);
    }

    function getColor(address user) external view returns (string memory) {
        return colors[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PingPong {
    string public lastAction;
    address public lastPlayer;
    uint256 public pingCount;
    uint256 public pongCount;

    event Ping(address indexed player);
    event Pong(address indexed player);

    function ping() external {
        lastAction = "ping";
        lastPlayer = msg.sender;
        pingCount += 1;
        emit Ping(msg.sender);
    }

    function pong() external {
        lastAction = "pong";
        lastPlayer = msg.sender;
        pongCount += 1;
        emit Pong(msg.sender);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StepCounter {
    mapping(address => uint256) public steps;

    event StepsAdded(address indexed user, uint256 amount, uint256 total);

    function addSteps(uint256 amount) external {
        require(amount > 0, "Amount must be > 0");
        steps[msg.sender] += amount;
        emit StepsAdded(msg.sender, amount, steps[msg.sender]);
    }

    function getSteps(address user) external view returns (uint256) {
        return steps[user];
    }

    function resetSteps() external {
        steps[msg.sender] = 0;
        emit StepsAdded(msg.sender, 0, 0);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Temperature {
    int256 public temperature;
    address public lastUpdater;

    event TemperatureUpdated(int256 newTemp, address indexed by);

    function setTemperature(int256 temp) external {
        temperature = temp;
        lastUpdater = msg.sender;
        emit TemperatureUpdated(temp, msg.sender);
    }

    function increase(int256 amount) external {
        temperature += amount;
        lastUpdater = msg.sender;
        emit TemperatureUpdated(temperature, msg.sender);
    }

    function decrease(int256 amount) external {
        temperature -= amount;
        lastUpdater = msg.sender;
        emit TemperatureUpdated(temperature, msg.sender);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CoinFlip {
    enum Side { Heads, Tails }

    event FlipResult(address indexed player, Side choice, Side result, bool won);

    function flip(Side choice) external view returns (Side result, bool won) {
        uint256 random = uint256(keccak256(abi.encodePacked(block.timestamp, block.prevrandao, msg.sender)));
        result = Side(random % 2);
        won = (choice == result);
        return (result, won);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract GreetingCard {
    string public message;
    address public author;
    uint256 public createdAt;

    event CardCreated(address indexed author, string message);

    constructor(string memory initialMessage) {
        message = initialMessage;
        author = msg.sender;
        createdAt = block.timestamp;
        emit CardCreated(msg.sender, initialMessage);
    }

    function updateMessage(string calldata newMessage) external {
        require(msg.sender == author, "Only author");
        message = newMessage;
        emit CardCreated(msg.sender, newMessage);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CounterReset {
    uint256 public count;
    uint256 public resetCount;

    event Incremented(uint256 newCount);
    event Reset(uint256 timesReset);

    function increment() external {
        count += 1;
        emit Incremented(count);
    }

    function reset() external {
        count = 0;
        resetCount += 1;
        emit Reset(resetCount);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LevelSystem {
    mapping(address => uint256) public experience;
    mapping(address => uint256) public level;

    event ExperienceGained(address indexed user, uint256 amount, uint256 newLevel);

    function gainExperience(uint256 amount) external {
        experience[msg.sender] += amount;
        uint256 newLevel = experience[msg.sender] / 100;
        level[msg.sender] = newLevel;
        emit ExperienceGained(msg.sender, amount, newLevel);
    }

    function getStats(address user) external view returns (uint256 exp, uint256 lvl) {
        return (experience[user], level[user]);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PointSystem {
    mapping(address => uint256) public points;
    address public owner;

    event PointsAdded(address indexed user, uint256 amount);
    event PointsSpent(address indexed user, uint256 amount);

    constructor() {
        owner = msg.sender;
    }

    function addPoints(address user, uint256 amount) external {
        require(msg.sender == owner, "Not owner");
        points[user] += amount;
        emit PointsAdded(user, amount);
    }

    function spendPoints(uint256 amount) external {
        require(points[msg.sender] >= amount, "Not enough points");
        points[msg.sender] -= amount;
        emit PointsSpent(msg.sender, amount);
    }

    function getPoints(address user) external view returns (uint256) {
        return points[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Streak {
    mapping(address => uint256) public lastAction;
    mapping(address => uint256) public streak;

    event StreakUpdated(address indexed user, uint256 newStreak);

    function action() external {
        uint256 today = block.timestamp / 1 days;

        if (lastAction[msg.sender] == today) {
            return;
        }

        if (lastAction[msg.sender] + 1 == today) {
            streak[msg.sender] += 1;
        } else {
            streak[msg.sender] = 1;
        }

        lastAction[msg.sender] = today;
        emit StreakUpdated(msg.sender, streak[msg.sender]);
    }

    function getStreak(address user) external view returns (uint256) {
        return streak[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Mute {
    mapping(address => bool) public muted;
    address public admin;

    event Muted(address indexed user);
    event Unmuted(address indexed user);

    constructor() {
        admin = msg.sender;
    }

    modifier onlyAdmin() {
        require(msg.sender == admin, "Not admin");
        _;
    }

    function mute(address user) external onlyAdmin {
        muted[user] = true;
        emit Muted(user);
    }

    function unmute(address user) external onlyAdmin {
        muted[user] = false;
        emit Unmuted(user);
    }

    function isMuted(address user) external view returns (bool) {
        return muted[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Reputation {
    mapping(address => int256) public reputation;
    mapping(address => mapping(address => bool)) public hasVoted;

    event ReputationChanged(address indexed user, int256 change, int256 newRep);

    function upvote(address user) external {
        require(user != msg.sender, "Cannot vote yourself");
        require(!hasVoted[msg.sender][user], "Already voted");
        hasVoted[msg.sender][user] = true;
        reputation[user] += 1;
        emit ReputationChanged(user, 1, reputation[user]);
    }

    function downvote(address user) external {
        require(user != msg.sender, "Cannot vote yourself");
        require(!hasVoted[msg.sender][user], "Already voted");
        hasVoted[msg.sender][user] = true;
        reputation[user] -= 1;
        emit ReputationChanged(user, -1, reputation[user]);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Session {
    mapping(address => uint256) public sessionStart;
    mapping(address => bool) public isActive;

    event SessionStarted(address indexed user, uint256 timestamp);
    event SessionEnded(address indexed user, uint256 duration);

    function startSession() external {
        require(!isActive[msg.sender], "Session already active");
        sessionStart[msg.sender] = block.timestamp;
        isActive[msg.sender] = true;
        emit SessionStarted(msg.sender, block.timestamp);
    }

    function endSession() external {
        require(isActive[msg.sender], "No active session");
        uint256 duration = block.timestamp - sessionStart[msg.sender];
        isActive[msg.sender] = false;
        emit SessionEnded(msg.sender, duration);
    }

    function getDuration(address user) external view returns (uint256) {
        if (!isActive[user]) return 0;
        return block.timestamp - sessionStart[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Karma {
    mapping(address => int256) public karma;

    event KarmaChanged(address indexed user, int256 change, int256 newKarma);

    function giveKarma(address user, int256 amount) external {
        require(user != msg.sender, "Cannot give to yourself");
        require(amount != 0, "Amount cannot be zero");
        karma[user] += amount;
        emit KarmaChanged(user, amount, karma[user]);
    }

    function getKarma(address user) external view returns (int256) {
        return karma[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Attendance {
    mapping(address => uint256) public attendanceCount;
    mapping(address => uint256) public lastAttendance;

    event Attended(address indexed user, uint256 total);

    function attend() external {
        uint256 today = block.timestamp / 1 days;
        require(lastAttendance[msg.sender] != today, "Already attended today");

        lastAttendance[msg.sender] = today;
        attendanceCount[msg.sender] += 1;
        emit Attended(msg.sender, attendanceCount[msg.sender]);
    }

    function getAttendance(address user) external view returns (uint256) {
        return attendanceCount[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Cooldown {
    mapping(address => uint256) public lastAction;
    uint256 public cooldownTime = 1 hours;

    event ActionPerformed(address indexed user, uint256 timestamp);

    function performAction() external {
        require(block.timestamp >= lastAction[msg.sender] + cooldownTime, "Cooldown active");
        lastAction[msg.sender] = block.timestamp;
        emit ActionPerformed(msg.sender, block.timestamp);
    }

    function timeLeft(address user) external view returns (uint256) {
        uint256 next = lastAction[user] + cooldownTime;
        if (block.timestamp >= next) return 0;
        return next - block.timestamp;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Energy {
    mapping(address => uint256) public energy;
    uint256 public maxEnergy = 100;

    event EnergyGained(address indexed user, uint256 amount);
    event EnergySpent(address indexed user, uint256 amount);

    function gainEnergy(uint256 amount) external {
        require(energy[msg.sender] + amount <= maxEnergy, "Exceeds max");
        energy[msg.sender] += amount;
        emit EnergyGained(msg.sender, amount);
    }

    function spendEnergy(uint256 amount) external {
        require(energy[msg.sender] >= amount, "Not enough energy");
        energy[msg.sender] -= amount;
        emit EnergySpent(msg.sender, amount);
    }

    function getEnergy(address user) external view returns (uint256) {
        return energy[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BadgeCounter {
    mapping(address => uint256) public badges;
    address public minter;

    event BadgeMinted(address indexed user, uint256 totalBadges);

    constructor() {
        minter = msg.sender;
    }

    function mintBadge(address user) external {
        require(msg.sender == minter, "Not minter");
        badges[user] += 1;
        emit BadgeMinted(user, badges[user]);
    }

    function getBadges(address user) external view returns (uint256) {
        return badges[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract DailyLimit {
    mapping(address => uint256) public dailySpent;
    mapping(address => uint256) public lastDay;
    uint256 public limit = 1 ether;

    event Spent(address indexed user, uint256 amount, uint256 remaining);

    function spend() external payable {
        uint256 today = block.timestamp / 1 days;
        if (lastDay[msg.sender] != today) {
            lastDay[msg.sender] = today;
            dailySpent[msg.sender] = 0;
        }

        require(dailySpent[msg.sender] + msg.value <= limit, "Daily limit exceeded");
        dailySpent[msg.sender] += msg.value;
        emit Spent(msg.sender, msg.value, limit - dailySpent[msg.sender]);
    }

    function getRemaining(address user) external view returns (uint256) {
        uint256 today = block.timestamp / 1 days;
        if (lastDay[user] != today) return limit;
        return limit - dailySpent[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Stamina {
    mapping(address => uint256) public stamina;
    uint256 public maxStamina = 50;

    event StaminaRecovered(address indexed user, uint256 amount);
    event StaminaUsed(address indexed user, uint256 amount);

    function recover(uint256 amount) external {
        require(stamina[msg.sender] + amount <= maxStamina, "Exceeds max stamina");
        stamina[msg.sender] += amount;
        emit StaminaRecovered(msg.sender, amount);
    }

    function use(uint256 amount) external {
        require(stamina[msg.sender] >= amount, "Not enough stamina");
        stamina[msg.sender] -= amount;
        emit StaminaUsed(msg.sender, amount);
    }

    function getStamina(address user) external view returns (uint256) {
        return stamina[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Combo {
    mapping(address => uint256) public combo;
    mapping(address => uint256) public lastAction;

    event ComboIncreased(address indexed user, uint256 newCombo);
    event ComboReset(address indexed user);

    function action() external {
        if (block.timestamp <= lastAction[msg.sender] + 1 minutes) {
            combo[msg.sender] += 1;
        } else {
            combo[msg.sender] = 1;
        }
        lastAction[msg.sender] = block.timestamp;
        emit ComboIncreased(msg.sender, combo[msg.sender]);
    }

    function resetCombo() external {
        combo[msg.sender] = 0;
        emit ComboReset(msg.sender);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Habit {
    mapping(address => uint256) public habitCount;
    mapping(address => uint256) public lastHabitDay;

    event HabitLogged(address indexed user, uint256 total);

    function logHabit() external {
        uint256 today = block.timestamp / 1 days;
        require(lastHabitDay[msg.sender] != today, "Already logged today");

        lastHabitDay[msg.sender] = today;
        habitCount[msg.sender] += 1;
        emit HabitLogged(msg.sender, habitCount[msg.sender]);
    }

    function getHabitCount(address user) external view returns (uint256) {
        return habitCount[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Momentum {
    mapping(address => uint256) public momentum;
    mapping(address => uint256) public lastUpdate;

    event MomentumUpdated(address indexed user, uint256 value);

    function update() external {
        uint256 timePassed = block.timestamp - lastUpdate[msg.sender];
        if (timePassed < 1 hours) {
            momentum[msg.sender] += 1;
        } else {
            momentum[msg.sender] = 1;
        }
        lastUpdate[msg.sender] = block.timestamp;
        emit MomentumUpdated(msg.sender, momentum[msg.sender]);
    }

    function getMomentum(address user) external view returns (uint256) {
        return momentum[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Quest {
    mapping(address => bool) public completed;
    mapping(address => uint256) public completedAt;
    string public questName;

    event QuestCompleted(address indexed user, uint256 timestamp);

    constructor(string memory _questName) {
        questName = _questName;
    }

    function complete() external {
        require(!completed[msg.sender], "Already completed");
        completed[msg.sender] = true;
        completedAt[msg.sender] = block.timestamp;
        emit QuestCompleted(msg.sender, block.timestamp);
    }

    function isCompleted(address user) external view returns (bool) {
        return completed[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract DailyGoal {
    mapping(address => uint256) public goal;
    mapping(address => uint256) public progress;
    mapping(address => uint256) public lastDay;

    event GoalSet(address indexed user, uint256 goal);
    event ProgressAdded(address indexed user, uint256 amount, uint256 total);

    function setGoal(uint256 _goal) external {
        require(_goal > 0, "Goal must be > 0");
        goal[msg.sender] = _goal;
        emit GoalSet(msg.sender, _goal);
    }

    function addProgress(uint256 amount) external {
        uint256 today = block.timestamp / 1 days;
        if (lastDay[msg.sender] != today) {
            lastDay[msg.sender] = today;
            progress[msg.sender] = 0;
        }
        progress[msg.sender] += amount;
        emit ProgressAdded(msg.sender, amount, progress[msg.sender]);
    }

    function isGoalReached(address user) external view returns (bool) {
        return progress[user] >= goal[user] && goal[user] > 0;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract StreakTracker {
    mapping(address => uint256) public currentStreak;
    mapping(address => uint256) public longestStreak;
    mapping(address => uint256) public lastDay;

    event StreakUpdated(address indexed user, uint256 current, uint256 longest);

    function checkIn() external {
        uint256 today = block.timestamp / 1 days;

        if (lastDay[msg.sender] == today) {
            return;
        }

        if (lastDay[msg.sender] + 1 == today) {
            currentStreak[msg.sender] += 1;
        } else {
            currentStreak[msg.sender] = 1;
        }

        if (currentStreak[msg.sender] > longestStreak[msg.sender]) {
            longestStreak[msg.sender] = currentStreak[msg.sender];
        }

        lastDay[msg.sender] = today;
        emit StreakUpdated(msg.sender, currentStreak[msg.sender], longestStreak[msg.sender]);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LevelUp {
    mapping(address => uint256) public xp;
    mapping(address => uint256) public level;

    event XpGained(address indexed user, uint256 amount, uint256 newLevel);

    function gainXp(uint256 amount) external {
        xp[msg.sender] += amount;
        uint256 newLevel = xp[msg.sender] / 50;
        level[msg.sender] = newLevel;
        emit XpGained(msg.sender, amount, newLevel);
    }

    function getStats(address user) external view returns (uint256, uint256) {
        return (xp[user], level[user]);
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Achievement {
    mapping(address => mapping(string => bool)) public achievements;
    mapping(address => uint256) public totalAchievements;

    event AchievementUnlocked(address indexed user, string achievement);

    function unlock(string calldata name) external {
        require(!achievements[msg.sender][name], "Already unlocked");
        achievements[msg.sender][name] = true;
        totalAchievements[msg.sender] += 1;
        emit AchievementUnlocked(msg.sender, name);
    }

    function hasAchievement(address user, string calldata name) external view returns (bool) {
        return achievements[user][name];
    }
}
