# FundMe — Solidity · Foundry

Smart contract de financiación en **Solidity** que acepta ETH únicamente si su valor es **≥ $5 USD**, utilizando **Chainlink Price Feeds**.  
El proyecto incluye **tests unitarios**, **tests de integración** y **scripts de despliegue e interacción** con Foundry.

---

## Stack Tecnológico

- Solidity `^0.8.19`
- Foundry (forge, anvil)
- Chainlink Price Feeds
- foundry-devops
- Makefile

---

## Contrato Principal (`FundMe.sol`)

- Mínimo de financiación: `MINIMUM_USD = 5e18`
- Conversión ETH/USD vía Chainlink
- Owner declarado como `immutable`
- Registro de funders y montos financiados
- Funciones `withdraw()` y `cheaperWithdraw()` (optimizada en gas)
- Funciones `fallback()` y `receive()` delegan a `fund()`
- Custom error: `FundMe__NotOwner`

---

## Tests

### Tests Unitarios

`test/FundMeTest.t.sol`

- Validación del mínimo en USD
- Verificación del owner
- Lógica de funding
- Withdraw con uno y múltiples funders
- Comparación de consumo de gas

### Tests de Integración

`test/integration/InteractionsTest.sol`

- Ejecución de scripts reales
- Flujo completo fund → withdraw

### Ejecutar tests:

`forge test`

---

## Scripts

`DeployFundMe.s.sol`

`Interactions.s.sol` (`FundFundMe`,`WithdrawFundMe`)

### Uso:

```
make deploy
make fund
make withdraw
```

## Redes Soportadas

- Anvil (local)
- Sepolia
- zkSync (local / testnet)
