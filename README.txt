ESP-ENG


(ESP)

## Multi-user balance management

El contrato está diseñado para funcionar en modo multiusuario.
Cada wallet interactúa con su propio balance interno mediante el uso
de la siguiente estructura:

mapping(address => uint256) public userBalance;

Este mapping asocia cada dirección Ethereum con su saldo en ETH,
permitiendo que múltiples usuarios depositen y retiren fondos
de forma independiente dentro del mismo contrato.

---

## Core functions

### depositEther()
Función payable que permite a cualquier usuario depositar ETH
en el contrato.

El monto depositado se obtiene a través de `msg.value` y se acredita
al balance del usuario que ejecuta la transacción (`msg.sender`).

---

### withdrawEther(uint256 amount)
Permite a un usuario retirar ETH previamente depositado.

Antes de realizar la transferencia, la función:
- Verifica que el monto sea mayor a cero
- Valida que el usuario tenga saldo suficiente

El balance se actualiza antes de enviar el ETH al usuario,
siguiendo el patrón Checks-Effects-Interactions para mayor seguridad.

---

### modifyBalance(...)
Función administrativa utilizada para modificar balances internos
en escenarios controlados (por ejemplo: correcciones o testing).

Esta función no está pensada para el uso general de los usuarios
y debe estar restringida a un rol autorizado (owner / internal),
para evitar manipulaciones indebidas de los saldos.

---
(ENG)
## Multi-user balance management

The contract is designed to operate in a multi-user environment.
Each wallet manages its own internal balance through the following
data structure:

mapping(address => uint256) public userBalance;

This mapping associates each Ethereum address with its ETH balance,
allowing multiple users to deposit and withdraw funds independently
within the same smart contract.

---

## Core functions

### depositEther()
Payable function that allows any user to deposit ETH into the contract.

The deposited amount is obtained via `msg.value` and is credited
to the balance of the address executing the transaction (`msg.sender`).

---

### withdrawEther(uint256 amount)
Allows a user to withdraw previously deposited ETH.

Before executing the transfer, the function:
- Ensures the withdrawal amount is greater than zero
- Validates that the user has sufficient balance

The user's balance is updated before sending ETH,
following the Checks-Effects-Interactions pattern
to improve security.

---

### modifyBalance(...)
Administrative function used to modify internal balances
in controlled scenarios (e.g. corrections or testing).

This function is not intended for general user interaction
and should be restricted to an authorized role
(owner or internal access) to prevent unauthorized balance manipulation.

---
