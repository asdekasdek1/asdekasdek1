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
