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
