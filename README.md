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
