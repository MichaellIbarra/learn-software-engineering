## BLOCKCHAIN

**¿De qué trata?**
- Tecnología de registro distribuido (DLT - Distributed Ledger Technology)
- Base de datos descentralizada e inmutable
- Bloques de transacciones enlazados criptográficamente
- Red peer-to-peer sin autoridad central
- Consenso distribuido entre participantes

**¿Por qué se utiliza?**
- Eliminar intermediarios (desintermediación)
- Garantizar transparencia e inmutabilidad
- Reducir costos de transacciones
- Automatizar procesos con smart contracts
- Crear sistemas resistentes a censura
- Establecer confianza sin terceros (trustless)

**Ventajas/Beneficios:**
- **Descentralización:** No hay punto único de fallo
- **Inmutabilidad:** Datos no pueden ser alterados retroactivamente
- **Transparencia:** Historial completo visible
- **Seguridad:** Criptografía avanzada
- **Trazabilidad:** Seguimiento completo de transacciones
- **Automatización:** Smart contracts ejecutan automáticamente
- **Reducción de costos:** Elimina intermediarios

**Desventajas:**
- **Escalabilidad limitada:** TPS (transacciones por segundo) bajo
- **Consumo energético:** Proof of Work consume mucha energía
- **Irreversibilidad:** Errores no se pueden deshacer
- **Complejidad técnica:** Curva de aprendizaje alta
- **Regulación incierta:** Marco legal en evolución
- **Velocidad:** Confirmaciones pueden tardar minutos
- **Costo de transacciones:** Gas fees pueden ser altos

**Componentes de Blockchain:**

**1. Bloques**
```
Estructura de un Bloque:
┌────────────────────────────────┐
│ BLOCK HEADER                   │
├────────────────────────────────┤
│ - Version                      │
│ - Previous Block Hash          │
│ - Merkle Root                  │
│ - Timestamp                    │
│ - Difficulty Target            │
│ - Nonce                        │
├────────────────────────────────┤
│ TRANSACTIONS                   │
├────────────────────────────────┤
│ - Tx 1: A → B (10 BTC)        │
│ - Tx 2: C → D (5 ETH)         │
│ - Tx 3: E → F (100 tokens)    │
│ - ...                          │
└────────────────────────────────┘
```

**2. Cadena de Bloques**
```
Genesis Block → Block 1 → Block 2 → Block 3 → ...
Hash: 0x000...  Hash: 0x001... Hash: 0x002... Hash: 0x003...
       ↑             ↑             ↑
Previous Hash   Previous Hash   Previous Hash
```

**3. Criptografía**
- **Hash SHA-256:** Función criptográfica unidireccional
- **Firma Digital:** ECDSA (Elliptic Curve Digital Signature Algorithm)
- **Clave Pública/Privada:** Asimetría criptográfica

**4. Consenso**
- **Proof of Work (PoW):** Bitcoin, Ethereum (pre-Merge)
- **Proof of Stake (PoS):** Ethereum 2.0, Cardano
- **Delegated PoS:** EOS, Tron
- **Proof of Authority (PoA):** Redes privadas
- **Byzantine Fault Tolerance (BFT):** Hyperledger

**Tipos de Blockchain:**

| Tipo            | Acceso      | Participación | Ejemplos           | Uso                    |
|-----------------|-------------|---------------|--------------------|------------------------|
| **Pública**     | Abierto     | Permissionless| Bitcoin, Ethereum  | Criptomonedas, DeFi    |
| **Privada**     | Restringido | Permissioned  | Hyperledger Fabric | Empresas, consorcios   |
| **Consorcio**   | Semi-privado| Permissioned  | R3 Corda           | Bancos, industrias     |
| **Híbrida**     | Mixto       | Mixto         | Dragonchain        | Casos específicos      |

**Arquitectura de Red:**

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   NODE 1     │────│   NODE 2     │────│   NODE 3     │
│  Full Node   │    │  Full Node   │    │  Light Node  │
└──────┬───────┘    └──────┬───────┘    └──────┬───────┘
       │                   │                   │
       │                   │                   │
       └───────────────────┴───────────────────┘
                P2P Network
                (Peer-to-Peer)

- Full Node: Copia completa de blockchain
- Light Node: Solo headers de bloques
- Mining Node: Valida y crea nuevos bloques
```

**Ciclo de Vida de una Transacción:**

```
1. CREACIÓN
   Usuario crea transacción
   - From: 0xABC...
   - To: 0xDEF...
   - Amount: 1 ETH
   - Gas: 21000

2. FIRMA
   Firma con clave privada (ECDSA)
   - Genera firma digital
   - Demuestra propiedad sin revelar clave privada

3. BROADCAST
   Transmite a red P2P
   - Propagación a nodos vecinos
   - Difusión a toda la red

4. MEMPOOL
   Transacción en espera (pending)
   - Pool de transacciones no confirmadas
   - Ordenadas por gas price

5. MINADO/VALIDACIÓN
   Minero incluye en bloque
   - Selecciona transacciones del mempool
   - Resuelve problema criptográfico (PoW)
   - Crea nuevo bloque

6. CONFIRMACIÓN
   Bloque añadido a blockchain
   - Primera confirmación (1 block)
   - Confirmaciones adicionales (6+ recomendado)

7. FINALIZACIÓN
   Transacción irreversible
   - Después de N confirmaciones
   - Estado actualizado en ledger
```

**Ejemplo: Transacción Bitcoin**

```
Transaction:
{
  "txid": "a1b2c3d4...",
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "prev_tx_hash",
      "vout": 0,
      "scriptSig": "signature + public_key",
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 0.5,
      "n": 0,
      "scriptPubKey": {
        "addresses": ["1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa"]
      }
    },
    {
      "value": 0.3,
      "n": 1,
      "scriptPubKey": {
        "addresses": ["1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2"]
      }
    }
  ]
}

UTXO Model:
- Input: 1 BTC (de transacción anterior)
- Output 1: 0.5 BTC (destinatario)
- Output 2: 0.3 BTC (cambio propio)
- Fee: 0.2 BTC (para mineros)
```

**Principales Blockchains:**

**1. Bitcoin (BTC)**
```
Lanzado: 2009
Creador: Satoshi Nakamoto
Consenso: Proof of Work (SHA-256)
Block Time: ~10 minutos
TPS: ~7 transacciones/segundo
Uso: Moneda digital, store of value
```

**2. Ethereum (ETH)**
```
Lanzado: 2015
Creador: Vitalik Buterin
Consenso: Proof of Stake (desde The Merge 2022)
Block Time: ~12 segundos
TPS: ~15-30 (layer 1), 1000+ (layer 2)
Uso: Smart contracts, dApps, DeFi, NFTs
Lenguaje: Solidity, Vyper
```

**3. Binance Smart Chain (BSC)**
```
Lanzado: 2020
Consenso: Proof of Staked Authority
Block Time: ~3 segundos
TPS: ~160
Uso: DeFi, dApps (compatible con EVM)
```

**4. Solana (SOL)**
```
Lanzado: 2020
Consenso: Proof of History + PoS
Block Time: ~400ms
TPS: 2,000-3,000 (teórico: 65,000)
Uso: DeFi, NFTs, Web3
Lenguaje: Rust
```

**5. Polkadot (DOT)**
```
Lanzado: 2020
Creador: Gavin Wood (co-fundador Ethereum)
Consenso: Nominated PoS
Arquitectura: Parachains
Uso: Interoperabilidad entre blockchains
```

**Puertos y Servicios Comunes:**

```
Bitcoin:
- Mainnet RPC: 8332
- Testnet RPC: 18332
- P2P: 8333

Ethereum:
- Geth HTTP: 8545
- Geth WebSocket: 8546
- P2P: 30303

IPFS:
- Gateway: 8080
- API: 5001
- Swarm: 4001

Ganache (Desarrollo local):
- HTTP: 7545 o 8545
```

**Herramientas del Ecosistema:**

**Wallets:**
- MetaMask (navegador)
- Ledger, Trezor (hardware)
- Trust Wallet (móvil)
- MyEtherWallet (web)

**Exploradores de Blockchain:**
- Etherscan.io (Ethereum)
- Blockchain.com (Bitcoin)
- BscScan.com (BSC)

**Nodos como Servicio:**
- Infura (Ethereum)
- Alchemy
- QuickNode
- GetBlock

**Frameworks de Desarrollo:**
- Truffle Suite
- Hardhat
- Foundry
- Brownie (Python)

**Habilitación Básica:**
1. Instalar wallet (MetaMask)
2. Obtener criptomonedas (exchange o faucet testnet)
3. Conectar a red blockchain
4. Realizar primera transacción
5. Explorar dApps (Uniswap, OpenSea, etc.)
6. Para desarrollo: instalar herramientas (Node.js, Truffle, Ganache)

---

### Fundamentos de blockchain y base de datos distribuidos y sus características

**¿De qué trata?**
- Bases de datos distribuidas: información replicada en múltiples nodos
- Blockchain: tipo específico de base de datos distribuida
- Diferencias entre bases de datos tradicionales y blockchain
- Propiedades únicas de sistemas descentralizados

**¿Por qué se utiliza?**
- Eliminar punto único de fallo
- Resistencia a censura y ataques
- Alta disponibilidad (24/7)
- Transparencia y auditabilidad
- Confianza sin intermediarios

---

**Características Fundamentales:**

### **1. Descentralización**

**Centralizado vs Descentralizado vs Distribuido:**

```
CENTRALIZADO               DESCENTRALIZADO           DISTRIBUIDO
    ┌───┐                      ┌───┐                  ┌───┐   ┌───┐
    │ A │                  ┌───│ A │───┐          ┌───│ A │───│ B │───┐
    └─┬─┘                  │   └───┘   │          │   └───┘   └───┘   │
  ┌───┼───┐              ┌─┴─┐       ┌─┴─┐      ┌─┴─┐       ┌─┴─┐   ┌─┴─┐
  B   C   D              │ B │       │ C │      │ C │       │ D │   │ E │
                         └───┘       └───┘      └───┘       └───┘   └───┘

Single Point         No Central         Equal
of Failure          Authority          Participants
```

**Ventajas Descentralización:**
- No censura ni control único
- Resistencia a ataques
- Democrático (todos pueden participar)
- Mayor transparencia

**Desventajas:**
- Más lento que sistemas centralizados
- Mayor consumo de recursos
- Coordinación compleja

---

### **2. Inmutabilidad**

**¿De qué trata?**
- Una vez registrados, los datos no pueden ser modificados
- Historial completo permanente
- Cambios requieren consenso de la red

**Cómo funciona:**
```
Intento de modificación:

Block N-1           Block N             Block N+1
Hash: 0xABC...     Hash: 0xDEF...      Hash: 0x123...
Previous: 0x999    Previous: 0xABC     Previous: 0xDEF
Data: "A → B: 10"  Data: "C → D: 5"    Data: "E → F: 3"

Si modifico Block N:
- Hash de Block N cambia
- Previous Hash de Block N+1 no coincide
- Cadena rota, cambio detectado
- Red rechaza modificación

Para modificar:
- Requiere recalcular hash de Block N
- Recalcular todos los bloques subsiguientes
- Convencer al 51% de la red (ataque 51%)
- Costo computacional prohibitivo
```

**Ventajas:**
- Confianza en el historial
- Auditoría transparente
- No repudiación

**Desventajas:**
- Errores permanentes
- No borrado de datos sensibles
- Problemas con GDPR (derecho al olvido)

---

### **3. Transparencia**

**¿De qué trata?**
- Todo el historial de transacciones es público
- Cualquiera puede verificar
- Pseudonimidad (direcciones, no nombres reales)

**Ejemplo:**
```
Bitcoin Block Explorer:

Block #825,450
- Timestamp: 2026-01-25 10:30:00 UTC
- Transactions: 2,450
- Total Output: 6,254.35 BTC
- Mined by: AntPool

Transacciones visibles:
1. 1A1zP1... → 1BvBMS... (0.5 BTC)
2. 3J98t1W... → 1FeexV... (2.3 BTC)
3. bc1qxy2... → 3EktnH... (0.1 BTC)

Cualquiera puede ver:
- Monto transferido
- Direcciones origen/destino
- Timestamp
- Fee pagado

NO puede ver:
- Identidad real de propietarios (sin KYC)
```

---

### **4. Consenso Distribuido**

**¿De qué trata?**
- Acuerdo entre nodos sobre estado de blockchain
- Mecanismos para validar transacciones sin autoridad central

**Algoritmos de Consenso:**

**a) Proof of Work (PoW)**
```
¿Cómo funciona?
1. Mineros compiten por resolver problema matemático
2. Problema: Encontrar nonce que genere hash < target
3. Ejemplo: Hash debe empezar con 0000...
4. Primer minero en resolver gana recompensa
5. Bloque validado y añadido a cadena

Ejemplo:
Block Data: "A → B: 10 BTC"
Nonce: ???

Hash = SHA256(Block Data + Nonce)

Intentos:
Nonce 1: Hash = 0xABCD... ❌ (no empieza con 0000)
Nonce 2: Hash = 0x1234... ❌
...
Nonce 45,829: Hash = 0x0000ABC... ✅ (válido!)

Dificultad ajustada cada 2016 bloques (~2 semanas)
para mantener block time ~10 min
```

**Ventajas PoW:**
- Muy seguro (51% ataque costoso)
- Probado en Bitcoin desde 2009

**Desventajas PoW:**
- Consumo energético masivo
- Centralización en pools de minería
- Hardware especializado (ASICs)

**b) Proof of Stake (PoS)**
```
¿Cómo funciona?
1. Validadores "stakean" (bloquean) criptomonedas
2. Algoritmo selecciona validador aleatoriamente
3. Probabilidad de selección proporcional a stake
4. Validador propone nuevo bloque
5. Otros validadores votan para aprobar
6. Recompensa para validador y votantes

Ejemplo Ethereum 2.0:
- Stake mínimo: 32 ETH
- Recompensa: ~4-5% APR
- Slashing: penalización por mala conducta

Ventajas PoS:
- 99.95% menos consumo energético que PoW
- No requiere hardware especializado
- Más escalable

Desventajas PoS:
- "Nothing at stake" problem
- Menos probado que PoW
- Favorece a holders grandes
```

**c) Delegated Proof of Stake (DPoS)**
```
Ejemplo EOS:
- 21 Block Producers (BP) elegidos
- Token holders votan por BPs
- BPs rotan para crear bloques
- Más rápido: 0.5 segundos/bloque

Ventajas:
- Alta velocidad (miles de TPS)
- Eficiente energéticamente

Desventajas:
- Más centralizado (solo 21 validadores)
- Riesgo de colusión
```

---

### **5. Criptografía**

**Hash Functions (SHA-256):**
```javascript
// Propiedades:
// 1. Determinístico: mismo input → mismo output
// 2. Unidireccional: no se puede revertir
// 3. Avalanche effect: pequeño cambio → hash completamente diferente

Ejemplo:
Input: "Hola Mundo"
SHA256: "a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e"

Input: "Hola mundo"  (cambió solo una letra)
SHA256: "b5f0c0b88b5a36e1afbd9dc47e33d7dd2e6d0ccb2eb6e0d9a7a7f8c1e5a2b3c4"

Completamente diferente!
```

**Firma Digital (ECDSA):**
```
Proceso de Firma:

1. Usuario tiene:
   - Clave Privada: 0x1234ABCD... (secreta)
   - Clave Pública: 0x5678EFGH... (compartida)

2. Firmar transacción:
   Firma = ECDSA_Sign(Private_Key, Transaction_Hash)

3. Verificar firma:
   ECDSA_Verify(Public_Key, Signature, Transaction_Hash)
   → True (válida) / False (inválida)

Propiedades:
- Solo quien tiene clave privada puede firmar
- Cualquiera puede verificar con clave pública
- No se puede derivar clave privada desde pública
```

**Direcciones de Wallet:**
```
Generación de Dirección Ethereum:

1. Generar clave privada (256 bits aleatorios)
   Private Key: 0x4c0883a69102937d6231471b5dbb6204fe5129617082792ae468d01a3f362318

2. Derivar clave pública (ECDSA secp256k1)
   Public Key: 0x04b9c0...

3. Hash keccak256 de clave pública
   Hash: 0x8a7d...

4. Tomar últimos 20 bytes
   Address: 0x8a7d9f6e4b3c2a1d5e8f9a0b1c2d3e4f5a6b7c8d

Checksum (EIP-55):
Final: 0x8a7D9f6E4b3c2A1d5E8F9A0b1C2D3E4F5a6B7c8D
       (mezcla mayúsculas/minúsculas para validación)
```

---

### **6. Merkle Trees**

**¿De qué trata?**
- Estructura de datos para verificación eficiente
- Permite probar que transacción está en bloque sin descargar todo

**Estructura:**
```
                Root Hash
              /            \
         H(AB)              H(CD)
        /     \            /     \
      H(A)   H(B)       H(C)    H(D)
       |       |         |        |
     Tx A    Tx B      Tx C     Tx D

Merkle Root = H(H(H(A) + H(B)) + H(H(C) + H(D)))

Ventajas:
- Verificar Tx A requiere solo: H(A), H(B), H(CD), Root
- No necesita descargar Tx B, C, D
- SPV (Simple Payment Verification) en wallets ligeros
```

---

### **7. Comparación: Blockchain vs Base de Datos Tradicional**

| Característica           | Blockchain                | BD Tradicional (SQL)      |
|--------------------------|---------------------------|---------------------------|
| **Arquitectura**         | Descentralizada           | Centralizada              |
| **Control**              | Distribuido (consenso)    | Administrador único       |
| **Escritura**            | Solo append (agregar)     | CRUD completo             |
| **Modificación**         | Inmutable                 | Editable/borrable         |
| **Transparencia**        | Pública (mayormente)      | Privada                   |
| **Confianza**            | Criptografía y consenso   | Autoridad central         |
| **Velocidad Lectura**    | Rápida                    | Muy rápida                |
| **Velocidad Escritura**  | Lenta (minutos)           | Rápida (milisegundos)     |
| **Escalabilidad**        | Limitada (TPS bajo)       | Alta                      |
| **Costo**                | Alto (gas fees, mining)   | Bajo                      |
| **Recuperación Datos**   | Difícil/imposible         | Fácil (backups)           |
| **Uso Principal**        | Descentralización, trust  | Eficiencia, flexibilidad  |

**Cuándo usar Blockchain:**
- ✅ Múltiples partes sin confianza mutua
- ✅ Transparencia requerida
- ✅ Inmutabilidad crítica
- ✅ Eliminación de intermediarios valiosa

**Cuándo NO usar Blockchain:**
- ❌ Aplicación centralizada tradicional
- ❌ Velocidad crítica (miles de TPS)
- ❌ Datos confidenciales/privados
- ❌ Necesidad de editar/borrar datos
- ❌ Presupuesto limitado

---

### **8. Tipos de Datos en Blockchain**

**On-Chain (en la cadena):**
```
- Transacciones
- Balances de cuentas
- Smart contracts (bytecode)
- Estados de contratos
- Logs de eventos

Ventajas:
- Inmutable y verificable
- Disponible siempre

Desventajas:
- Costoso almacenar
- Tamaño limitado
- Permanente (no borrable)
```

**Off-Chain (fuera de la cadena):**
```
- Archivos grandes (imágenes, videos)
- Metadatos de NFTs
- Datos privados
- Computación intensiva

Soluciones:
- IPFS (almacenamiento distribuido)
- Oracles (datos del mundo real)
- Layer 2 (rollups, state channels)
- Sidechains

Ejemplo NFT:
On-chain: Token ID, Owner address, Contract address
Off-chain (IPFS): Imagen, Metadata JSON
```

---

**Ejemplo Práctico: Sistema de Votación Blockchain**

**Requisitos:**
```
- Transparente: todos pueden verificar resultados
- Inmutable: votos no pueden ser alterados
- Anónimo: no vincular votante con voto
- Único: una persona, un voto
```

**Implementación:**
```solidity
// Smart Contract en Solidity
contract VotingSystem {
    struct Candidate {
        string name;
        uint voteCount;
    }
    
    Candidate[] public candidates;
    mapping(address => bool) public hasVoted;
    
    constructor(string[] memory candidateNames) {
        for (uint i = 0; i < candidateNames.length; i++) {
            candidates.push(Candidate({
                name: candidateNames[i],
                voteCount: 0
            }));
        }
    }
    
    function vote(uint candidateIndex) public {
        require(!hasVoted[msg.sender], "Ya has votado");
        require(candidateIndex < candidates.length, "Candidato inválido");
        
        hasVoted[msg.sender] = true;
        candidates[candidateIndex].voteCount++;
        
        emit VoteCast(msg.sender, candidateIndex);
    }
    
    function getResults() public view returns (Candidate[] memory) {
        return candidates;
    }
}
```

**Flujo:**
```
1. Deploy contract en blockchain
2. Usuarios se registran (wallet address)
3. Usuario envía transacción vote(candidateIndex)
4. Contract verifica: no ha votado antes
5. Incrementa contador del candidato
6. Marca address como votado
7. Transacción registrada en blockchain
8. Resultados visibles en tiempo real
9. Después de elección: resultados inmutables

Ventajas:
✅ Transparente: código público
✅ Verificable: anyone can audit
✅ Inmutable: no puede cambiar votos
✅ Descentralizado: no manipulación central

Desafíos:
⚠ Costo de gas por voto
⚠ Anonimidad limitada (address visible)
⚠ Requiere wallet y crypto
⚠ Escalabilidad para millones de votantes
```

---

**Habilitación:**
1. Entender diferencia entre centralizado vs descentralizado
2. Aprender criptografía básica (hash, firmas)
3. Comprender consenso (PoW vs PoS)
4. Experimentar con blockchain explorer
5. Crear wallet y hacer transacciones testnet
6. Leer whitepaper Bitcoin y Ethereum
7. Practicar con herramientas de desarrollo

---

### Smart Contracts, Oracle, IPFS y CBDCs

**¿De qué trata?**
- **Smart Contracts:** Programas autoejecutables en blockchain
- **Oracles:** Puentes entre blockchain y mundo real
- **IPFS:** Sistema de archivos distribuido
- **CBDCs:** Monedas digitales de bancos centrales

**¿Por qué se utiliza?**
- Automatizar acuerdos sin intermediarios
- Conectar blockchain con datos externos
- Almacenar archivos descentralizadamente
- Modernizar sistemas monetarios nacionales

---

## **SMART CONTRACTS**

**¿De qué trata?**
- Contratos autoejecutables escritos en código
- Se ejecutan automáticamente cuando se cumplen condiciones
- Desplegados en blockchain (inmutables)
- Sin necesidad de intermediarios

**¿Por qué se utiliza?**
- Automatización de acuerdos
- Eliminar intermediarios (abogados, notarios, bancos)
- Reducir costos y tiempos
- Garantizar cumplimiento automático
- Transparencia total

**Ventajas:**
- **Automatización:** Ejecución sin intervención humana
- **Confianza:** Código es ley (code is law)
- **Transparencia:** Código público y verificable
- **Ahorro:** Sin intermediarios
- **Precisión:** Elimina errores humanos
- **Velocidad:** Ejecución instantánea

**Desventajas:**
- **Inmutabilidad:** Bugs permanentes (sin updates fáciles)
- **Costo:** Gas fees pueden ser altos
- **Complejidad:** Requiere programación especializada
- **Vulnerabilidades:** Hacks (DAO hack, reentrancy)
- **Legalidad:** Marco legal no claro
- **Datos externos:** Depende de oracles

**Lenguajes de Smart Contracts:**

**1. Solidity (Ethereum)**
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 private storedData;
    
    event DataStored(uint256 indexed newValue, address indexed by);
    
    function set(uint256 x) public {
        storedData = x;
        emit DataStored(x, msg.sender);
    }
    
    function get() public view returns (uint256) {
        return storedData;
    }
}
```

**2. Vyper (Ethereum - Python-like)**
```python
# @version ^0.3.0

storedData: public(uint256)

@external
def set(x: uint256):
    self.storedData = x

@external
@view
def get() -> uint256:
    return self.storedData
```

**3. Rust (Solana, NEAR)**
```rust
use anchor_lang::prelude::*;

#[program]
pub mod simple_storage {
    use super::*;
    
    pub fn set(ctx: Context<Set>, data: u64) -> Result<()> {
        let storage = &mut ctx.accounts.storage;
        storage.data = data;
        Ok(())
    }
}
```

**Ejemplo Completo: Sistema de Pagos Escrow**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @title Escrow
 * @dev Contrato de depósito en garantía
 * Comprador deposita fondos, vendedor entrega producto,
 * comprador libera fondos o disputa
 */
contract Escrow {
    enum State { AWAITING_PAYMENT, AWAITING_DELIVERY, COMPLETE, REFUNDED }
    
    struct Transaction {
        address payable buyer;
        address payable seller;
        uint256 amount;
        State state;
        uint256 createdAt;
    }
    
    mapping(uint256 => Transaction) public transactions;
    uint256 public transactionCount;
    address public arbiter;
    uint256 public constant TIMEOUT = 30 days;
    
    event TransactionCreated(uint256 indexed txId, address buyer, address seller, uint256 amount);
    event PaymentDeposited(uint256 indexed txId);
    event PaymentReleased(uint256 indexed txId);
    event PaymentRefunded(uint256 indexed txId);
    
    constructor(address _arbiter) {
        arbiter = _arbiter;
    }
    
    modifier onlyBuyer(uint256 _txId) {
        require(msg.sender == transactions[_txId].buyer, "Only buyer");
        _;
    }
    
    modifier inState(uint256 _txId, State _state) {
        require(transactions[_txId].state == _state, "Invalid state");
        _;
    }
    
    function createTransaction(address payable _seller) external payable {
        require(msg.value > 0, "Amount must be > 0");
        require(_seller != address(0), "Invalid seller");
        require(_seller != msg.sender, "Cannot be yourself");
        
        uint256 txId = transactionCount++;
        
        transactions[txId] = Transaction({
            buyer: payable(msg.sender),
            seller: _seller,
            amount: msg.value,
            state: State.AWAITING_DELIVERY,
            createdAt: block.timestamp
        });
        
        emit TransactionCreated(txId, msg.sender, _seller, msg.value);
        emit PaymentDeposited(txId);
    }
    
    function confirmDelivery(uint256 _txId) 
        external 
        onlyBuyer(_txId) 
        inState(_txId, State.AWAITING_DELIVERY) 
    {
        Transaction storage txn = transactions[_txId];
        txn.state = State.COMPLETE;
        
        txn.seller.transfer(txn.amount);
        
        emit PaymentReleased(_txId);
    }
    
    function refund(uint256 _txId) external {
        Transaction storage txn = transactions[_txId];
        
        require(
            msg.sender == arbiter || 
            (msg.sender == txn.buyer && block.timestamp > txn.createdAt + TIMEOUT),
            "Not authorized"
        );
        
        require(txn.state == State.AWAITING_DELIVERY, "Invalid state");
        
        txn.state = State.REFUNDED;
        txn.buyer.transfer(txn.amount);
        
        emit PaymentRefunded(_txId);
    }
    
    function getTransactionDetails(uint256 _txId) 
        external 
        view 
        returns (
            address buyer,
            address seller,
            uint256 amount,
            State state,
            uint256 createdAt
        ) 
    {
        Transaction memory txn = transactions[_txId];
        return (
            txn.buyer,
            txn.seller,
            txn.amount,
            txn.state,
            txn.createdAt
        );
    }
}
```

**Ciclo de Vida:**
```
1. DESARROLLO
   - Escribir código Solidity
   - Unit tests (Hardhat, Truffle)
   - Auditoría de seguridad

2. COMPILACIÓN
   - Compilar a bytecode EVM
   - Generar ABI (Application Binary Interface)

3. DEPLOYMENT
   - Deploy a testnet (Goerli, Sepolia)
   - Pruebas exhaustivas
   - Deploy a mainnet

4. INTERACCIÓN
   - Llamar funciones (read/write)
   - Enviar transacciones
   - Escuchar eventos

5. MANTENIMIENTO
   - Monitoreo de eventos
   - Upgrades (si implementado con proxy)
   - Responder a vulnerabilidades
```

**Usos Comunes:**
- **DeFi:** Uniswap, Aave, Compound
- **NFTs:** OpenSea, marketplaces
- **DAOs:** Gobernanza descentralizada
- **Gaming:** Axie Infinity, The Sandbox
- **Identity:** Sistemas de identidad digital
- **Supply Chain:** Trazabilidad de productos

---

## **ORACLES**

**¿De qué trata?**
- Servicios que proveen datos externos a blockchain
- Puente entre on-chain y off-chain
- Permiten a smart contracts acceder a datos del mundo real

**¿Por qué se utiliza?**
- Blockchain no puede acceder a internet directamente
- Smart contracts necesitan datos externos (precios, clima, eventos)
- Conectar con APIs, bases de datos, IoT

**Problema del Oracle (Oracle Problem):**
```
Blockchain es determinista:
- Todos los nodos deben llegar al mismo resultado
- Datos externos pueden variar (API caída, datos diferentes)

Solución:
- Oracles descentralizados
- Múltiples fuentes de datos
- Consenso sobre valor verdadero
```

**Tipos de Oracles:**

**1. Software Oracles**
```
Fuentes: APIs web, bases de datos
Ejemplo: Precio de ETH/USD desde exchanges
```

**2. Hardware Oracles**
```
Fuentes: Sensores IoT, RFID, dispositivos físicos
Ejemplo: Temperatura, GPS, código de barras
```

**3. Inbound Oracles**
```
Traen datos a blockchain
Ejemplo: Precio de acciones, resultados deportivos
```

**4. Outbound Oracles**
```
Envían datos desde blockchain al exterior
Ejemplo: Notificar pago recibido, activar IoT
```

**5. Consensus-based Oracles**
```
Múltiples oracles votan sobre valor correcto
Ejemplo: Chainlink (red descentralizada)
```

**Chainlink (Líder de Oracles):**

```solidity
// Consumir precio de ETH/USD con Chainlink
pragma solidity ^0.8.0;

import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract PriceConsumer {
    AggregatorV3Interface internal priceFeed;
    
    constructor() {
        // ETH/USD Price Feed en Ethereum Mainnet
        priceFeed = AggregatorV3Interface(
            0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419
        );
    }
    
    function getLatestPrice() public view returns (int) {
        (
            /*uint80 roundID*/,
            int price,
            /*uint startedAt*/,
            /*uint timeStamp*/,
            /*uint80 answeredInRound*/
        ) = priceFeed.latestRoundData();
        
        return price; // Precio con 8 decimales
    }
}

// Uso:
// ETH/USD = 2,500.00
// getLatestPrice() retorna: 250000000000 (2500 * 10^8)
```

**Arquitectura Chainlink:**
```
Smart Contract           Chainlink Network        Data Sources
     │                         │                       │
     │──Request Data──────────>│                       │
     │                         │──Query───────────────>│
     │                         │                   ┌───┴───┐
     │                         │                   │API 1  │
     │                         │<─────────────────┤API 2  │
     │                         │                   │API 3  │
     │                         │                   └───────┘
     │                         │
     │                   [Aggregation]
     │                   Median de 3 fuentes
     │                         │
     │<───Return Data──────────│
     │
```

**Ejemplos de Uso:**

**1. Seguro de Vuelo Automatizado**
```solidity
contract FlightInsurance {
    using Chainlink for Chainlink.Request;
    
    function checkFlightStatus(string memory flightNumber) public {
        // Llamar a Oracle de API de vuelos
        Chainlink.Request memory req = buildChainlinkRequest(...);
        req.add("flight", flightNumber);
        req.add("date", "2026-01-25");
        
        sendChainlinkRequestTo(oracle, req, fee);
    }
    
    function fulfill(bytes32 requestId, bool isDelayed) public {
        if (isDelayed) {
            // Pagar compensación automáticamente
            payable(passenger).transfer(compensationAmount);
        }
    }
}
```

**2. DeFi: Préstamo Colateralizado**
```solidity
contract LendingProtocol {
    function getLoanAmount(uint ethCollateral) public view returns (uint) {
        int ethPrice = priceOracle.getLatestPrice(); // Oracle
        uint loanValue = (ethCollateral * uint(ethPrice)) / 2; // 50% LTV
        return loanValue;
    }
    
    function checkLiquidation(address borrower) public {
        uint collateralValue = getCollateralValue(borrower); // Usa Oracle
        uint debtValue = getDebtValue(borrower);
        
        if (collateralValue < debtValue * 120 / 100) { // <120% ratio
            liquidate(borrower);
        }
    }
}
```

**Ventajas Oracles:**
- Conectan blockchain con mundo real
- Permiten casos de uso complejos
- Descentralizados (Chainlink)

**Desventajas:**
- Punto de centralización potencial
- Costo adicional (LINK token para Chainlink)
- Latencia en obtener datos
- Confianza en proveedor de oracle

---

## **IPFS (InterPlanetary File System)**

**¿De qué trata?**
- Sistema de archivos distribuido peer-to-peer
- Alternativa descentralizada a HTTP
- Almacenamiento de archivos por contenido (no ubicación)
- Usado para NFTs, dApps, almacenamiento descentralizado

**¿Por qué se utiliza?**
- Blockchain limitada para almacenar archivos grandes
- HTTP centralizado (servidores pueden caer)
- Censura resistente
- Permanencia de contenido

**Cómo Funciona:**

**Direccionamiento por Contenido:**
```
HTTP (por ubicación):
https://ejemplo.com/imagen.jpg
- Si servidor cae, archivo no disponible

IPFS (por contenido):
ipfs://QmYwAPJzv5CZsnAzt8auVZRn215TDhYBLgLgJKWsHF9
- Hash del contenido (CID - Content Identifier)
- Archivo disponible mientras exista en algún nodo
- Mismo archivo siempre tiene mismo hash
```

**Ejemplo:**
```bash
# Agregar archivo a IPFS
$ ipfs add imagen.png
added QmYwAPJzv5CZsnA... imagen.png

# Acceder desde navegador
https://ipfs.io/ipfs/QmYwAPJzv5CZsnA...

# O desde gateway local
http://localhost:8080/ipfs/QmYwAPJzv5CZsnA...

# Listar contenido
$ ipfs cat QmYwAPJzv5CZsnA... > imagen_descargada.png
```

**Arquitectura IPFS:**
```
       User Upload                 IPFS Network
           │                            │
     ┌─────┴──────┐            ┌────────┴────────┐
     │  File.jpg  │            │                 │
     └─────┬──────┘       ┌────┤  Node 1 (pin)   │
           │              │    └─────────────────┘
      [Hash SHA-256]      │
           │              │    ┌─────────────────┐
      QmXYZ123...         ├────┤  Node 2 (pin)   │
           │              │    └─────────────────┘
     ┌─────┴──────┐       │
     │ Chunked    │       │    ┌─────────────────┐
     │ + Merkle   │       └────┤  Node 3 (cache) │
     │ DAG        │            └─────────────────┘
     └────────────┘
           │
      Distributed
      across nodes

Pinning: Mantener archivo permanentemente en nodo
Cache: Temporal, puede ser eliminado
```

**Uso con NFTs:**

```solidity
// NFT con metadata en IPFS
contract MyNFT is ERC721 {
    mapping(uint256 => string) private _tokenURIs;
    
    function mint(address to, uint256 tokenId, string memory ipfsHash) public {
        _mint(to, tokenId);
        
        // Guardar hash IPFS de metadata
        _tokenURIs[tokenId] = string(
            abi.encodePacked("ipfs://", ipfsHash)
        );
    }
    
    function tokenURI(uint256 tokenId) public view override returns (string memory) {
        return _tokenURIs[tokenId];
    }
}

// Metadata en IPFS (JSON):
{
  "name": "NFT #1",
  "description": "Mi primer NFT",
  "image": "ipfs://QmYwAPJzv5CZsnA.../imagen.png",
  "attributes": [
    {"trait_type": "Rarity", "value": "Legendary"},
    {"trait_type": "Power", "value": 95}
  ]
}
```

**Servicios IPFS:**

**1. Pinata**
```
- Pinning service (almacenamiento permanente)
- API fácil de usar
- Gratis hasta 1 GB

API Example:
curl -X POST "https://api.pinata.cloud/pinning/pinFileToIPFS" \
  -H "Authorization: Bearer YOUR_JWT" \
  -F file=@imagen.png
```

**2. NFT.Storage**
```
- Gratis para NFTs
- Patrocinado por Filecoin
- Persistencia a largo plazo
```

**3. Infura IPFS**
```
- API de IPFS
- Integrado con Ethereum
- Pago por uso
```

**Ventajas IPFS:**
- Descentralizado (no single point of failure)
- Censura resistente
- Deduplicación (mismo archivo, un solo hash)
- Permanencia (mientras alguien pinee)
- Eficiente (P2P, cacheo local)

**Desventajas:**
- No garantiza permanencia (requiere pinning)
- Velocidad variable (depende de nodos)
- No adecuado para datos privados (todo público)
- Requiere gateway o nodo local
- Costo de pinning services

**Puertos IPFS:**
- API: 5001
- Gateway: 8080
- Swarm (P2P): 4001

---

## **CBDCs (Central Bank Digital Currencies)**

**¿De qué trata?**
- Moneda digital emitida por banco central
- Versión digital de moneda fiat nacional
- Respaldada por gobierno (no criptomoneda)
- Blockchain/DLT como infraestructura (opcional)

**¿Por qué se utiliza?**
- Modernizar sistema de pagos
- Inclusión financiera (no bancarizados)
- Reducir costos de efectivo (imprimir, transportar)
- Combatir lavado de dinero
- Competir con criptomonedas privadas
- Pagos transfronterizos eficientes

**Tipos de CBDCs:**

**1. Retail CBDC (Para consumidores)**
```
Usuarios: Público general
Uso: Compras diarias, transferencias P2P
Similares a: Efectivo digital

Ejemplos:
- e-CNY (Yuan Digital de China)
- Sand Dollar (Bahamas)
- DCash (Caribe Oriental)
```

**2. Wholesale CBDC (Para instituciones)**
```
Usuarios: Bancos, instituciones financieras
Uso: Liquidaciones interbancarias
Similares a: Reservas bancarias digitales

Ejemplos:
- Project Ubin (Singapur)
- Jasper (Canadá)
```

**Arquitectura CBDC:**

**Modelo Centralizado:**
```
                Banco Central
                      │
      ┌───────────────┼───────────────┐
      │               │               │
   Banco 1         Banco 2         Banco 3
      │               │               │
   ┌──┼──┐         ┌──┼──┐         ┌──┼──┐
   │  │  │         │  │  │         │  │  │
User User User  User User User  User User User

- BC controla todo
- Bancos como intermediarios
- BC tiene datos de todas las transacciones
```

**Modelo Híbrido (Blockchain):**
```
            Banco Central
            (Smart Contract)
                  │
     Blockchain Network (Permissioned)
                  │
      ┌───────────┼───────────┐
      │           │           │
   Banco 1     Banco 2     Banco 3
  (Validador) (Validador) (Validador)
      │           │           │
   Usuarios    Usuarios    Usuarios

- Consenso distribuido
- BC supervisa, no controla cada tx
- Mayor privacidad
- Más resiliente
```

**Ejemplo: e-CNY (Yuan Digital de China)**

```
Lanzamiento: Piloto 2020, expansión gradual

Características:
- Controlado por People's Bank of China
- Wallets en smartphones
- Funciona offline (NFC)
- Trazabilidad completa por gobierno
- No requiere cuenta bancaria

Usos:
- Pagos en tiendas (QR code)
- Transferencias P2P
- Pagos de servicios públicos
- Transporte

Privacidad:
- "Controlable anonimidad"
- Pequeñas transacciones anónimas
- Grandes transacciones rastreables
```

**Comparación:**

| Característica      | CBDC               | Criptomoneda (Bitcoin) | Efectivo         |
|---------------------|--------------------|------------------------|------------------|
| **Emisor**          | Banco Central      | Protocolo descentralizado | Banco Central |
| **Descentralizado** | No                 | Sí                     | N/A              |
| **Anónimo**         | Parcial/No         | Pseudónimo             | Sí               |
| **Programable**     | Sí (smart contract)| Sí (limitado)          | No               |
| **Offline**         | Posible (NFC)      | No                     | Sí               |
| **Estabilidad**     | Estable (=fiat)    | Volátil                | Estable          |
| **Reverseible**     | Sí (por autoridad) | No                     | No               |

**Casos de Uso CBDC:**

**1. Pagos Gubernamentales**
```solidity
contract GovernmentPayments {
    mapping(address => uint256) public citizenBalance;
    address public government;
    
    function distributeSocialWelfare(address[] memory recipients, uint amount) 
        external 
    {
        require(msg.sender == government, "Only gov");
        
        for (uint i = 0; i < recipients.length; i++) {
            citizenBalance[recipients[i]] += amount;
            emit WelfareDistributed(recipients[i], amount);
        }
    }
}

Ventajas:
- Distribución instantánea
- Sin intermediarios bancarios
- Trackeo de uso (combate fraude)
```

**2. Pagos Transfronterizos**
```
Problema Actual:
A (USA) → SWIFT → Bancos intermediarios → B (India)
Tiempo: 3-5 días
Costo: 3-7%

Con CBDC:
A (Digital Dollar) → Blockchain → B (Digital Rupee)
Tiempo: Segundos
Costo: <0.1%

Proyecto mBridge:
- Hong Kong, China, Tailandia, UAE
- Plataforma común CBDC
- Liquidaciones instantáneas
```

**3. Política Monetaria Programable**
```solidity
contract ProgrammableCBDC {
    uint256 public expiryDate;
    
    // "Helicóptero de dinero" con expiración
    function issueStimulus(address citizen, uint amount) external {
        // Dinero expira en 90 días
        expiryDate = block.timestamp + 90 days;
        
        // Fuerza gasto, no ahorro
        // Estimula economía post-crisis
    }
    
    // Restricciones de uso
    mapping(address => bool) public approvedMerchants;
    
    function transfer(address to, uint amount) external {
        require(approvedMerchants[to], "Only approved merchants");
        // Ej: Solo para alimentos, no alcohol
    }
}
```

**Preocupaciones sobre CBDCs:**

**Privacidad:**
```
Gobierno puede:
- Ver todas las transacciones
- Bloquear pagos específicos
- Confiscar fondos
- Rastrear comportamiento de gasto

Comparado con:
- Efectivo: Completamente privado
- Crypto: Pseudónimo (Bitcoin), privado (Monero)
```

**Control Gubernamental:**
```
Posibles abusos:
- Censura de transacciones
- Discriminación (bloquear disidentes)
- Dinero programable con restricciones
- Congelamiento de cuentas sin proceso legal
```

**Proyectos CBDC Activos (2026):**

```
Lanzados:
✅ Bahamas - Sand Dollar (2020)
✅ Nigeria - eNaira (2021)
✅ Jamaica - JAM-DEX (2022)
✅ Caribe Oriental - DCash

Pilotos Avanzados:
🔄 China - e-CNY (millones de usuarios)
🔄 India - e-Rupee
🔄 Brasil - Real Digital
🔄 Suecia - e-Krona

En Investigación:
🔍 USA - Digital Dollar (Fed research)
🔍 Eurozona - Digital Euro
🔍 UK - Britcoin
🔍 Japón - Digital Yen
```

**Habilitación:**
- Estudiar arquitecturas (centralizada vs distribuida)
- Explorar pilotos existentes (e-CNY)
- Entender implicaciones de privacidad
- Seguir regulaciones emergentes
- Tecnologías: Hyperledger, Corda, custom blockchains

---

### Reconocer las potencialidades del blockchain para generar soluciones disruptivas

**¿De qué trata?**
- Identificar problemas que blockchain resuelve mejor
- Casos de uso innovadores y disruptivos
- Transformación de industrias tradicionales
- Creación de nuevos modelos de negocio

**¿Por qué se utiliza?**
- Eliminar intermediarios ineficientes
- Crear confianza sin autoridades centrales
- Habilitar nuevos modelos económicos
- Democratizar acceso a servicios
- Innovar en industrias estancadas

---

**Sectores Transformados por Blockchain:**

### **1. Finanzas (DeFi - Decentralized Finance)**

**Problema Tradicional:**
```
- Bancos como intermediarios (tarifas altas)
- Acceso limitado (no bancarizados)
- Horarios de operación limitados
- Procesos lentos (días para transferencias)
- Opacidad en tasas y comisiones
```

**Solución Blockchain:**
```
✅ Préstamos P2P sin bancos (Aave, Compound)
✅ Trading 24/7 (Uniswap, PancakeSwap)
✅ Staking y yield farming (rendimientos pasivos)
✅ Stablecoins (USDC, DAI)
✅ Seguros descentralizados (Nexus Mutual)
```

**Ejemplo: Uniswap (DEX - Exchange Descentralizado)**
```solidity
// Protocolo Automated Market Maker (AMM)
contract UniswapV2Pair {
    uint public reserve0;  // ETH
    uint public reserve1;  // TOKEN
    
    // Fórmula: x * y = k (constant product)
    function swap(uint amountIn, address tokenIn) external {
        uint amountOut = getAmountOut(amountIn, reserve0, reserve1);
        // Transfer tokens
        // Nadie puede manipular precio (algoritmo)
    }
}

Ventajas:
- Sin registro, sin KYC
- Trading sin intermediario
- Liquidez provista por usuarios (LP tokens)
- No puede ser censurado
- Tarifas transparentes (0.3%)

Impacto:
- Volumen >$1 trillion (2023)
- Miles de tokens listados sin permiso
- Democratización de trading
```

**Yield Farming (Agricultura de Rendimiento):**
```
Flujo:
1. Usuario deposita USDC en Aave
2. Recibe aUSDC (token de depósito) + 3% APY
3. Usa aUSDC como colateral para préstamo
4. Pide prestado DAI (paga 2% APY)
5. Deposita DAI en Curve (recibe 8% APY + CRV tokens)
6. Stakea CRV en Convex (recibe 15% APY + CVX tokens)

Rendimiento Neto: 3% + 8% + 15% - 2% = 24% APY
(Simplificado, riesgos incluyen smart contract hacks, impermanent loss)
```

---

### **2. Supply Chain (Cadena de Suministro)**

**Problema Tradicional:**
```
- Falta de trazabilidad (productos falsificados)
- Documentación papel (lenta, propensa a errores)
- Múltiples intermediarios (opacidad)
- Dificulta recall de productos defectuosos
```

**Solución Blockchain:**
```
✅ Trazabilidad completa (farm-to-table)
✅ Autenticidad verificable (anti-falsificación)
✅ Smart contracts para pagos automáticos
✅ Transparencia para consumidores
```

**Ejemplo: VeChain (Supply Chain Blockchain)**
```
Caso: Vino de Lujo

1. Viñedo (Francia)
   - IoT sensor registra: temperatura, humedad, cosecha
   - QR code único en botella
   - Tx en blockchain: Origin, Date, Vineyard

2. Transporte
   - GPS tracker actualiza ubicación en blockchain
   - Sensor de temperatura (cadena de frío)
   - Smart contract verifica condiciones óptimas

3. Aduana
   - Escanea QR, verifica autenticidad
   - Registra inspección en blockchain
   - Smart contract libera pago a transportista

4. Distribuidor
   - Verifica historial completo
   - Confirma no es falsificación
   - Agrega su etapa a blockchain

5. Consumidor
   - Escanea QR con smartphone
   - Ve: Viñedo, Fecha cosecha, Ruta completa
   - Verifica autenticidad en blockchain

Beneficios:
- Reducción 90% falsificaciones
- Recall 10x más rápido (tracking preciso)
- Transparencia genera confianza
- Pagos automáticos reducen disputas
```

**IBM Food Trust (Walmart, Carrefour):**
```
Producto: Mangos

Sin Blockchain:
- Rastrear origen: 7 días
- Proceso manual: papel, llamadas

Con Blockchain:
- Rastrear origen: 2.2 segundos
- Escaneo QR → historial completo
- Granja → Transporte → Tienda (cada paso registrado)

Resultado:
- Seguridad alimentaria mejorada
- Recall instantáneo si contaminación
- Confianza del consumidor
```

---

### **3. Salud (Healthcare)**

**Problema Tradicional:**
```
- Historias clínicas fragmentadas (cada hospital diferente)
- Paciente sin control de sus datos
- Difícil compartir entre médicos
- Fraude en seguros médicos
- Ensayos clínicos opacos
```

**Solución Blockchain:**
```
✅ Historia clínica unificada e interoperable
✅ Paciente controla acceso a sus datos
✅ Compartir datos médicos seguro (encryption)
✅ Trazabilidad de medicamentos (anti-falsificación)
✅ Ensayos clínicos transparentes
```

**Ejemplo: MedRec (MIT)**
```solidity
contract MedicalRecords {
    struct Record {
        address patient;
        address provider;
        string ipfsHash; // Datos encriptados en IPFS
        uint timestamp;
    }
    
    mapping(address => Record[]) public patientRecords;
    mapping(address => mapping(address => bool)) public accessPermissions;
    
    function addRecord(
        address patient, 
        string memory ipfsHash
    ) external {
        require(
            accessPermissions[patient][msg.sender],
            "No permission"
        );
        
        patientRecords[patient].push(Record({
            patient: patient,
            provider: msg.sender,
            ipfsHash: ipfsHash,
            timestamp: block.timestamp
        }));
        
        emit RecordAdded(patient, msg.sender);
    }
    
    function grantAccess(address doctor) external {
        accessPermissions[msg.sender][doctor] = true;
    }
    
    function revokeAccess(address doctor) external {
        accessPermissions[msg.sender][doctor] = false;
    }
}

Flujo:
1. Doctor A (Hospital 1) crea registro médico
2. Datos sensibles encriptados y guardados en IPFS
3. Hash IPFS guardado en blockchain
4. Paciente otorga acceso a Doctor B (Hospital 2)
5. Doctor B lee registro completo
6. Paciente revoca acceso cuando desee

Ventajas:
- Paciente dueño de sus datos
- Interoperabilidad entre hospitales
- Historial inmutable (no puede ser alterado)
- Acceso granular y auditable
```

**Trazabilidad de Medicamentos:**
```
Problema:
- $200 billones en medicamentos falsificados/año
- 1 millón de muertes por medicamentos falsos

Solución (MediLedger):
1. Fabricante registra cada lote en blockchain
2. Número de serie único
3. Cada paso rastreado: fabricante → distribuidor → farmacia
4. Farmacia escanea antes de vender
5. Blockchain verifica autenticidad

Casos:
- Pfizer, Genentech usan para rastreo
- Reducción 95% falsificaciones en pilotos
```

---

### **4. Identidad Digital**

**Problema Tradicional:**
```
- Identidad controlada por gobiernos/corporaciones
- Sin control sobre datos personales
- Múltiples credenciales (email, redes sociales)
- Difícil verificar identidad remotamente
- Fraude de identidad (robo)
```

**Solución Blockchain:**
```
✅ Self-Sovereign Identity (SSI)
✅ Usuario controla su identidad
✅ Verificación sin revelar datos sensibles (ZK-proofs)
✅ Portabilidad entre servicios
✅ Resistencia a censura
```

**Ejemplo: Decentralized Identifiers (DIDs)**
```json
// DID Document
{
  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:example:123456789abcdefghi",
  "publicKey": [{
    "id": "did:example:123456789abcdefghi#keys-1",
    "type": "Ed25519VerificationKey2018",
    "owner": "did:example:123456789abcdefghi",
    "publicKeyBase58": "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
  }],
  "authentication": [{
    "type": "Ed25519SignatureAuthentication2018",
    "publicKey": "did:example:123456789abcdefghi#keys-1"
  }],
  "service": [{
    "type": "LinkedDomains",
    "serviceEndpoint": "https://example.com"
  }]
}
```

**Credenciales Verificables:**
```
Caso: Verificar edad para comprar alcohol

Tradicional:
- Mostrar ID físico (expone fecha nacimiento, dirección, etc.)
- Privacidad comprometida

Con Zero-Knowledge Proof:
1. Gobierno emite credencial digital: "Fecha Nacimiento: 1990-05-15"
2. Credencial firmada criptográficamente
3. Usuario genera proof: "Tengo >21 años" sin revelar fecha exacta
4. Tienda verifica proof (válido/inválido)
5. Sin revelar información adicional

Protocolo: zk-SNARK
Proyectos: Civic, uPort, SelfKey
```

---

### **5. Votación Electrónica**

**Problema Tradicional:**
```
- Fraude electoral (manipulación de votos)
- Falta de transparencia en conteo
- Costoso (logística, seguridad)
- Difícil para votantes remotos
- Recuentos controversiales
```

**Solución Blockchain:**
```
✅ Transparencia total (votos verificables)
✅ Inmutabilidad (no manipulación)
✅ Anonimato preservado (criptografía)
✅ Votación remota segura
✅ Resultados en tiempo real
```

**Ejemplo: Voatz (usado en West Virginia, USA)**
```
Proceso:
1. Registro biométrico (selfie + ID)
2. Verificación por autoridades electorales
3. Usuario recibe credencial blockchain
4. Vota desde smartphone
5. Voto encriptado y enviado a blockchain
6. Blockchain registra voto (anónimo)
7. Usuario recibe recibo encriptado (puede verificar)
8. Resultados calculados en blockchain
9. Auditoría pública posible

Características:
- Biometría previene duplicados
- Blockchain previene alteración
- Votos encriptados (privacidad)
- Trazabilidad sin comprometer anonimato

Desafíos:
- Seguridad dispositivos móviles
- Brecha digital (no todos con smartphone)
- Confianza en código (debe ser open source)
```

---

### **6. Propiedad Intelectual y NFTs**

**Problema Tradicional:**
```
- Piratería digital (música, arte, videos)
- Difícil demostrar propiedad original
- Artistas no reciben regalías de ventas secundarias
- Centralización en plataformas (Spotify, YouTube)
```

**Solución Blockchain:**
```
✅ NFTs como certificado de autenticidad
✅ Propiedad verificable on-chain
✅ Regalías automáticas en ventas secundarias
✅ Artistas venden directo a fans (sin intermediarios)
✅ Scarcity digital verificable
```

**Ejemplo: Royalties Automatizados**
```solidity
contract ArtNFT is ERC721 {
    address public artist;
    uint256 public royaltyPercentage = 10; // 10%
    
    constructor() ERC721("Art", "ART") {
        artist = msg.sender;
    }
    
    function transferWithRoyalty(
        address from,
        address to,
        uint256 tokenId
    ) external payable {
        uint256 royalty = (msg.value * royaltyPercentage) / 100;
        uint256 sellerAmount = msg.value - royalty;
        
        // Pagar regalía a artista
        payable(artist).transfer(royalty);
        
        // Pagar al vendedor
        payable(from).transfer(sellerAmount);
        
        // Transferir NFT
        _transfer(from, to, tokenId);
    }
}

Impacto:
- Artista gana en cada reventa (perpetuo)
- OpenSea, Rarible implementan royalties
- Beeple vendió NFT por $69M (primera venta)
- Gana 10% en cada reventa subsecuente

Casos de Uso:
- Arte digital (CryptoPunks, Bored Apes)
- Música (Kings of Leon lanzó álbum NFT)
- Tickets de eventos (GET Protocol)
- Bienes raíces virtuales (Decentraland)
- Gaming items (Axie Infinity)
```

---

### **7. Gaming y Metaverso**

**Problema Tradicional:**
```
- Ítems del juego no son del jugador (propiedad del estudio)
- No se pueden transferir entre juegos
- Cierre de juego = pérdida de inversión
- Economía centralizada controlada por empresa
```

**Solución Blockchain:**
```
✅ Play-to-Earn (ganar jugando)
✅ Propiedad real de ítems (NFTs)
✅ Interoperabilidad entre juegos
✅ Economía descentralizada
✅ Metaversos persistentes
```

**Ejemplo: Axie Infinity**
```
Mecánica:
1. Jugador compra 3 Axies (criaturas NFT)
2. Juega batallas PvP
3. Gana SLP tokens (Smooth Love Potion)
4. SLP usado para criar nuevos Axies
5. Vende Axies o SLP en mercado

Economía:
- Axies: $50 - $100,000+ (raros)
- SLP: Token ERC-20 tradeable
- AXS: Token de gobernanza

Impacto:
- Filipinos ganaron $400/mes (>salario mínimo)
- Becas: dueños de Axies prestan a jugadores
- $4 billones en volumen trading (2021)

Modelo Play-to-Earn:
Tiempo invertido → Habilidad → Earnings
```

**The Sandbox (Metaverso):**
```
Componentes:
- LAND: Parcelas de terreno (NFTs)
- ASSETS: Ítems 3D creados por usuarios (NFTs)
- SAND: Token de utilidad (ERC-20)

Economía:
- Comprar LAND (similar bienes raíces)
- Construir experiencias/juegos en LAND
- Vender/rentar LAND
- Monetizar creaciones

Casos:
- Snoop Dogg compró LAND virtual
- The Walking Dead lanzó experiencia
- Gucci, Adidas tienen presencia

Valor: Scarcity digital + ubicación + tráfico
```

---

### **8. Energía y Sostenibilidad**

**Problema Tradicional:**
```
- Grid eléctrico centralizado
- Difícil rastrear origen de energía renovable
- Certificados de carbono fraudulentos
- Sin incentivo para prosumidores (productores+consumidores)
```

**Solución Blockchain:**
```
✅ Peer-to-peer energy trading
✅ Trazabilidad de energía renovable
✅ Tokenización de créditos de carbono
✅ Microgrids descentralizados
```

**Ejemplo: Power Ledger (Australia)**
```
Caso: Energía Solar P2P

1. Casa A tiene paneles solares
2. Genera exceso de energía
3. Casa B necesita energía
4. Smart contract conecta A y B
5. Trading automático de energía
6. Blockchain registra transacción
7. Liquidación automática en tokens

Ventajas:
- Reducción 30% costo energía
- Incentivo para renovables
- Grid más resiliente
- Empoderamiento consumidores

Implementado en:
- Bangkok, Tailandia (comunidades)
- Fremantle, Australia (proyecto piloto)
```

---

**Potencialidades Clave de Blockchain:**

**1. Desintermediación**
```
Elimina middlemen:
- Bancos → DeFi
- Exchanges → DEX
- Notarios → Smart Contracts
- Plataformas → P2P directo

Resultado:
- Menores costos (no comisiones)
- Más rápido (sin aprobaciones)
- Mayor acceso (permissionless)
```

**2. Transparencia + Privacidad**
```
Paradoja aparente:
- Blockchain pública = transparente
- Pero con privacidad selectiva

Soluciones:
- ZK-proofs (privacidad con verificación)
- Encriptación (datos sensibles)
- Pseudonimidad (direcciones ≠ identidades)
```

**3. Programabilidad**
```
Money legos:
- Componible
- Interoperable
- Automatizable

Ejemplo:
Flash Loans (Aave):
- Préstamo sin colateral
- Condición: devolver en misma transacción
- Permite arbitraje instantáneo
- Imposible en finanzas tradicionales
```

**4. Tokenización de Assets**
```
Cualquier cosa → token:
- Bienes raíces → fracciones
- Arte → shares
- Carbono → credits
- Atención → BAT (Brave)

Beneficios:
- Liquidez mejorada
- Fraccionamiento
- Global trading
- Composabilidad
```

**Habilitación para Emprendedores:**
1. Identificar problema con intermediarios ineficientes
2. Evaluar si blockchain agrega valor real
3. Determinar tipo: pública, privada, consorcio
4. Diseñar tokenomics (si aplica)
5. Prototipar con herramientas dev
6. Validar con usuarios reales
7. Considerar regulación
8. Lanzar MVP en testnet

---

### Herramientas para el desarrollo de dApps (Truffle Suite, Ganache y Solidity)

**¿De qué trata?**
- Ecosistema de herramientas para desarrollar aplicaciones descentralizadas
- Frameworks, entornos de desarrollo y lenguajes de programación
- Ciclo completo: desarrollo, testing, deployment

**¿Por qué se utiliza?**
- Simplificar desarrollo de smart contracts
- Testing antes de deployment (evitar bugs costosos)
- Deployment automatizado
- Interacción con blockchain local y testnets

---

## **TRUFFLE SUITE**

**¿De qué trata?**
- Framework de desarrollo más popular para Ethereum
- Suite completa: Truffle, Ganache, Drizzle
- Ambiente de desarrollo, testing framework, deployment manager

**Componentes:**

**1. Truffle Framework**
```
Funcionalidades:
- Compilación de smart contracts
- Testing automatizado (JS/Solidity)
- Deployment a múltiples redes
- Gestión de artifacts
- Console interactivo
- Scriptable migrations
```

**Instalación:**
```bash
# Requisitos: Node.js v14+
npm install -g truffle

# Verificar instalación
truffle version
# Truffle v5.11.5
# Solidity v0.5.16
# Node v18.17.0
# Web3.js v1.10.0
```

**Estructura de Proyecto:**
```
my-dapp/
├── contracts/          # Smart contracts (.sol)
│   ├── Migrations.sol
│   └── MyContract.sol
├── migrations/         # Scripts de deployment
│   ├── 1_initial_migration.js
│   └── 2_deploy_contracts.js
├── test/               # Tests automatizados
│   └── myContract.test.js
├── truffle-config.js   # Configuración
└── build/              # Artefactos compilados (generado)
    └── contracts/
        └── MyContract.json
```

**truffle-config.js:**
```javascript
module.exports = {
  networks: {
    // Desarrollo local
    development: {
      host: "127.0.0.1",
      port: 7545,          // Ganache port
      network_id: "*",     // Cualquier network
    },
    
    // Goerli Testnet
    goerli: {
      provider: () => new HDWalletProvider(
        process.env.MNEMONIC,
        `https://goerli.infura.io/v3/${process.env.INFURA_KEY}`
      ),
      network_id: 5,
      gas: 5500000,
      confirmations: 2,
      timeoutBlocks: 200,
      skipDryRun: true
    },
    
    // Ethereum Mainnet
    mainnet: {
      provider: () => new HDWalletProvider(
        process.env.MNEMONIC,
        `https://mainnet.infura.io/v3/${process.env.INFURA_KEY}`
      ),
      network_id: 1,
      gas: 5500000,
      gasPrice: 20000000000, // 20 gwei
      confirmations: 2,
      timeoutBlocks: 200,
      skipDryRun: false
    }
  },
  
  compilers: {
    solc: {
      version: "0.8.19",
      settings: {
        optimizer: {
          enabled: true,
          runs: 200
        }
      }
    }
  },
  
  plugins: ["truffle-plugin-verify"],
  
  api_keys: {
    etherscan: process.env.ETHERSCAN_API_KEY
  }
};
```

**Comandos Principales:**

```bash
# Iniciar proyecto
truffle init

# Compilar contratos
truffle compile

# Migrar (deploy) a red
truffle migrate --network development
truffle migrate --network goerli --reset

# Testing
truffle test
truffle test test/specific_test.js

# Console interactivo
truffle console --network development

# Desarrollo continuo (recompila en cambios)
truffle develop
```

**Migration Script:**
```javascript
// migrations/2_deploy_contracts.js
const MyToken = artifacts.require("MyToken");

module.exports = async function(deployer, network, accounts) {
  const owner = accounts[0];
  const initialSupply = web3.utils.toWei('1000000', 'ether');
  
  // Deploy MyToken
  await deployer.deploy(MyToken, initialSupply, { from: owner });
  const token = await MyToken.deployed();
  
  console.log('MyToken deployed at:', token.address);
  console.log('Initial supply:', await token.totalSupply());
  
  // Configuración post-deployment
  if (network === 'mainnet') {
    await token.transferOwnership('0xNewOwner...', { from: owner });
  }
};
```

**Testing:**
```javascript
// test/MyToken.test.js
const MyToken = artifacts.require("MyToken");

contract("MyToken", (accounts) => {
  let token;
  const owner = accounts[0];
  const recipient = accounts[1];
  
  beforeEach(async () => {
    token = await MyToken.new(1000000);
  });
  
  it("should put 1000000 tokens in the owner account", async () => {
    const balance = await token.balanceOf(owner);
    assert.equal(balance.toNumber(), 1000000, "Initial balance incorrect");
  });
  
  it("should transfer tokens correctly", async () => {
    await token.transfer(recipient, 100, { from: owner });
    
    const balanceOwner = await token.balanceOf(owner);
    const balanceRecipient = await token.balanceOf(recipient);
    
    assert.equal(balanceOwner.toNumber(), 999900);
    assert.equal(balanceRecipient.toNumber(), 100);
  });
  
  it("should fail when trying to transfer more than balance", async () => {
    try {
      await token.transfer(recipient, 2000000, { from: owner });
      assert.fail("Expected revert");
    } catch (error) {
      assert(error.message.includes("revert"), "Expected 'revert'");
    }
  });
});
```

**Console Interactivo:**
```javascript
truffle(development)> let instance = await MyToken.deployed()
truffle(development)> let balance = await instance.balanceOf(accounts[0])
truffle(development)> balance.toString()
'1000000000000000000000000'  // Con 18 decimales

truffle(development)> await instance.transfer(accounts[1], 1000)
{
  tx: '0xabcd...',
  receipt: { ... },
  logs: [ ... ]
}

truffle(development)> let balanceAccount1 = await instance.balanceOf(accounts[1])
truffle(development)> balanceAccount1.toString()
'1000'
```

---

## **GANACHE**

**¿De qué trata?**
- Blockchain personal para desarrollo local
- Simula red Ethereum completa
- Accounts con ETH pre-financiados
- Mining instantáneo (no proof of work)

**Versiones:**
- **Ganache UI:** Interfaz gráfica (Windows, Mac, Linux)
- **ganache-cli:** Línea de comandos (deprecado, ahora Ganache)
- **Ganache (v7+):** CLI y programático

**Instalación:**
```bash
# Ganache CLI
npm install -g ganache

# Iniciar
ganache

# Con configuración
ganache --port 7545 --networkId 5777 --accounts 10 --defaultBalanceEther 100
```

**Características:**

```
Al iniciar Ganache muestra:

Ganache v7.7.3 (@ganache/cli: 0.8.3)

Available Accounts
==================
(0) 0x1234... (100 ETH)
(1) 0x5678... (100 ETH)
...
(9) 0xABCD... (100 ETH)

Private Keys
==================
(0) 0xprivatekey1...
(1) 0xprivatekey2...
...

HD Wallet
==================
Mnemonic:      candy maple cake sugar pudding cream honey rich smooth crumble sweet treat
Base HD Path:  m/44'/60'/0'/0/{account_index}

Gas Price
==================
20000000000

Gas Limit
==================
6721975

Call Gas Limit
==================
9007199254740991

Listening on 127.0.0.1:8545
```

**Opciones de Configuración:**
```bash
ganache \
  --port 7545 \
  --networkId 5777 \
  --accounts 20 \
  --defaultBalanceEther 1000 \
  --gasLimit 8000000 \
  --gasPrice 20000000000 \
  --mnemonic "your custom mnemonic phrase here" \
  --blockTime 3 \  # Minado cada 3 segundos
  --db ./ganache-db \  # Persistir estado
  --fork https://mainnet.infura.io/v3/YOUR_KEY \  # Fork de mainnet
  --fork https://mainnet.infura.io/v3/YOUR_KEY@15000000  # Fork en bloque específico
```

**Ganache UI Features:**
```
Tabs:
1. ACCOUNTS
   - Ver balances de cuentas
   - Copiar private keys
   
2. BLOCKS
   - Ver bloques minados
   - Transacciones en cada bloque
   - Gas usado
   
3. TRANSACTIONS
   - Lista de todas las transacciones
   - Detalle de cada tx
   - Logs de eventos
   
4. CONTRACTS
   - Smart contracts deployados
   - Ver storage
   - Llamar funciones
   
5. EVENTS
   - Logs de eventos emitidos
   - Filtros
   
6. LOGS
   - Logs de consola
   - Errores

Opciones:
- Guardar workspace
- Cargar workspace
- Fork de mainnet/testnet
- Configurar block time
```

**Uso Programático:**
```javascript
const ganache = require("ganache");

const options = {
  accounts: [
    {
      balance: web3.utils.toWei('1000', 'ether'),
      secretKey: '0x...'
    }
  ],
  gasLimit: 8000000,
  fork: {
    url: 'https://mainnet.infura.io/v3/YOUR_KEY'
  }
};

const server = ganache.server(options);
server.listen(8545, (err, blockchain) => {
  if (err) console.error(err);
  console.log('Ganache started on port 8545');
});
```

**Fork de Mainnet (Desarrollo):**
```bash
# Fork de Ethereum mainnet
ganache --fork https://mainnet.infura.io/v3/YOUR_INFURA_KEY

# Permite:
# - Interactuar con contratos reales (Uniswap, Aave, etc.)
# - Testing con estado real de mainnet
# - Sin gastar ETH real
# - Impersonar cualquier address

# Ejemplo: Impersonar Vitalik y transferir ETH
truffle console --network development

> await web3.eth.sendTransaction({
    from: '0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045',  // Vitalik
    to: accounts[0],
    value: web3.utils.toWei('100', 'ether')
  })
```

---

## **SOLIDITY**

**¿De qué trata?**
- Lenguaje de programación para smart contracts
- Sintaxis similar a JavaScript/C++
- Compilado a bytecode EVM (Ethereum Virtual Machine)
- Statically typed, supports inheritance

**Versión:**
```solidity
// Siempre especificar versión
pragma solidity ^0.8.0;  // Compatible con 0.8.x
pragma solidity >=0.8.0 <0.9.0;  // Rango específico
```

**Tipos de Datos:**

```solidity
contract DataTypes {
    // Booleanos
    bool public isActive = true;
    
    // Enteros
    uint256 public maxSupply = 1000000;  // uint = uint256
    uint8 public smallNumber = 255;
    int256 public temperature = -10;
    
    // Direcciones
    address public owner;
    address payable public recipient;
    
    // Bytes
    bytes32 public hash;
    bytes public data;
    
    // String
    string public name = "MyToken";
    
    // Enums
    enum State { Pending, Active, Cancelled }
    State public currentState;
    
    // Arrays
    uint[] public dynamicArray;
    uint[10] public fixedArray;
    
    // Mappings (hash table)
    mapping(address => uint) public balances;
    mapping(address => mapping(address => uint)) public allowances;
    
    // Structs
    struct User {
        string name;
        uint age;
        bool isActive;
    }
    User[] public users;
}
```

**Funciones:**

```solidity
contract Functions {
    uint public value;
    
    // Función básica
    function setValue(uint _value) public {
        value = _value;
    }
    
    // View: lee estado, no modifica
    function getValue() public view returns (uint) {
        return value;
    }
    
    // Pure: no lee ni modifica estado
    function add(uint a, uint b) public pure returns (uint) {
        return a + b;
    }
    
    // Payable: acepta ETH
    function deposit() public payable {
        // msg.value contiene ETH enviado
    }
    
    // Internal: solo dentro del contrato
    function _internal() internal {
        // ...
    }
    
    // Private: solo este contrato (no heredados)
    function _private() private {
        // ...
    }
    
    // External: solo desde fuera
    function external() external {
        // ...
    }
    
    // Múltiples returns
    function getMultiple() public pure returns (uint, string memory) {
        return (42, "Hello");
    }
    
    // Named returns
    function calculate(uint x) public pure returns (uint result) {
        result = x * 2;
        // return implícito
    }
}
```

**Modificadores:**

```solidity
contract Modifiers {
    address public owner;
    bool public paused;
    
    constructor() {
        owner = msg.sender;
    }
    
    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;  // Continúa con función
    }
    
    modifier whenNotPaused() {
        require(!paused, "Contract paused");
        _;
    }
    
    modifier validAddress(address _addr) {
        require(_addr != address(0), "Invalid address");
        _;
    }
    
    // Uso de modificadores
    function pause() public onlyOwner {
        paused = true;
    }
    
    function transfer(address to, uint amount) 
        public 
        whenNotPaused 
        validAddress(to) 
    {
        // Código de transferencia
    }
}
```

**Eventos:**

```solidity
contract Events {
    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);
    
    function transfer(address to, uint amount) public {
        // ... lógica de transferencia
        
        emit Transfer(msg.sender, to, amount);
    }
    
    // Escuchar eventos (JS)
    // contract.events.Transfer()
    //   .on('data', (event) => console.log(event))
}
```

**Herencia:**

```solidity
contract Base {
    uint public value;
    
    function setValue(uint _value) public virtual {
        value = _value;
    }
}

contract Derived is Base {
    // Override
    function setValue(uint _value) public override {
        value = _value * 2;
    }
}

// Herencia múltiple
contract A {
    function foo() public pure virtual returns (string memory) {
        return "A";
    }
}

contract B is A {
    function foo() public pure virtual override returns (string memory) {
        return "B";
    }
}

contract C is A, B {
    function foo() public pure override(A, B) returns (string memory) {
        return super.foo();  // Llama a B.foo()
    }
}
```

**Interfaces y Abstract:**

```solidity
// Interface
interface IERC20 {
    function transfer(address to, uint amount) external returns (bool);
    function balanceOf(address account) external view returns (uint);
}

// Abstract
abstract contract ERC20 {
    function transfer(address to, uint amount) public virtual returns (bool);
    
    function balanceOf(address account) public view returns (uint) {
        // Implementación
    }
}
```

**Ejemplo Completo: Token ERC20**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ERC20Token {
    string public name;
    string public symbol;
    uint8 public decimals = 18;
    uint256 public totalSupply;
    
    mapping(address => uint256) private balances;
    mapping(address => mapping(address => uint256)) private allowances;
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    constructor(string memory _name, string memory _symbol, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        totalSupply = _initialSupply * 10 ** uint256(decimals);
        balances[msg.sender] = totalSupply;
        
        emit Transfer(address(0), msg.sender, totalSupply);
    }
    
    function balanceOf(address account) public view returns (uint256) {
        return balances[account];
    }
    
    function transfer(address to, uint256 amount) public returns (bool) {
        require(to != address(0), "Transfer to zero address");
        require(balances[msg.sender] >= amount, "Insufficient balance");
        
        balances[msg.sender] -= amount;
        balances[to] += amount;
        
        emit Transfer(msg.sender, to, amount);
        return true;
    }
    
    function approve(address spender, uint256 amount) public returns (bool) {
        require(spender != address(0), "Approve to zero address");
        
        allowances[msg.sender][spender] = amount;
        
        emit Approval(msg.sender, spender, amount);
        return true;
    }
    
    function transferFrom(address from, address to, uint256 amount) public returns (bool) {
        require(from != address(0), "Transfer from zero address");
        require(to != address(0), "Transfer to zero address");
        require(balances[from] >= amount, "Insufficient balance");
        require(allowances[from][msg.sender] >= amount, "Allowance exceeded");
        
        balances[from] -= amount;
        balances[to] += amount;
        allowances[from][msg.sender] -= amount;
        
        emit Transfer(from, to, amount);
        return true;
    }
    
    function allowance(address owner, address spender) public view returns (uint256) {
        return allowances[owner][spender];
    }
}
```

**Mejores Prácticas Solidity:**

```solidity
// 1. Checks-Effects-Interactions Pattern
function withdraw(uint amount) public {
    // Checks
    require(balances[msg.sender] >= amount, "Insufficient balance");
    
    // Effects
    balances[msg.sender] -= amount;
    
    // Interactions (llamadas externas al final)
    payable(msg.sender).transfer(amount);
}

// 2. Protección contra Reentrancy
import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

contract Safe is ReentrancyGuard {
    function withdraw(uint amount) public nonReentrant {
        // ...
    }
}

// 3. Validaciones con require
function transfer(address to, uint amount) public {
    require(to != address(0), "Invalid address");
    require(amount > 0, "Amount must be > 0");
    require(balances[msg.sender] >= amount, "Insufficient balance");
    // ...
}

// 4. Uso de SafeMath (pre 0.8.0) o checked math (0.8.0+)
// 0.8.0+ tiene overflow protection por defecto
uint result = a + b;  // Revierte si overflow

// Para desactivar (unchecked, más gas eficiente)
unchecked {
    uint result = a + b;  // No revierte
}

// 5. Eventos para logging
emit Transfer(from, to, amount);

// 6. Funciones view/pure cuando posible (no gastan gas)
function calculateTotal() public pure returns (uint) {
    return price * quantity;
}
```

---

**Workflow Completo de Desarrollo:**

```bash
# 1. Crear proyecto
mkdir my-dapp && cd my-dapp
truffle init
npm init -y

# 2. Instalar dependencias
npm install @openzeppelin/contracts
npm install dotenv

# 3. Escribir smart contract
# contracts/MyContract.sol

# 4. Iniciar Ganache
ganache

# 5. Compilar
truffle compile

# 6. Escribir tests
# test/MyContract.test.js

# 7. Ejecutar tests
truffle test

# 8. Deploy a Ganache
truffle migrate --network development

# 9. Interactuar (console)
truffle console --network development
> let instance = await MyContract.deployed()
> await instance.myFunction()

# 10. Deploy a testnet (Goerli)
truffle migrate --network goerli

# 11. Verificar en Etherscan
truffle run verify MyContract --network goerli
```

**Habilitación:**
1. Instalar Node.js 14+
2. Instalar Truffle: `npm install -g truffle`
3. Instalar Ganache (UI o CLI)
4. Crear primer proyecto: `truffle init`
5. Seguir tutoriales oficiales: trufflesuite.com/tutorial
6. Leer documentación Solidity: docs.soliditylang.org
7. Explorar OpenZeppelin: contratos seguros y auditados
8. Practicar con CryptoZombies (tutorial interactivo)

---

### Definición de Smart Contracts y sus aplicaciones

**¿De qué trata?**
- Programas autoejecutables en blockchain
- Acuerdos digitales que se cumplen automáticamente
- Código = reglas, blockchain = ejecución imparcial

**¿Por qué se utiliza?**
- Eliminar intermediarios (abogados, notarios, agentes)
- Garantizar cumplimiento automático
- Reducir costos de transacciones
- Aumentar velocidad de ejecución
- Transparencia y verificabilidad

(Esta sección ya fue cubierta extensamente en "Smart Contracts, Oracle, IPFS y CBDCs", pero aquí va un resumen enfocado en aplicaciones)

---

**Aplicaciones de Smart Contracts por Industria:**

### **1. Finanzas Descentralizadas (DeFi)**

**Lending/Borrowing (Aave, Compound):**
```solidity
// Simplified lending pool
contract LendingPool {
    mapping(address => uint) public deposits;
    mapping(address => uint) public borrowed;
    
    function deposit() public payable {
        deposits[msg.sender] += msg.value;
    }
    
    function borrow(uint amount) public {
        uint maxBorrow = (deposits[msg.sender] * 75) / 100;  // 75% LTV
        require(borrowed[msg.sender] + amount <= maxBorrow, "Exceeds limit");
        
        borrowed[msg.sender] += amount;
        payable(msg.sender).transfer(amount);
    }
    
    function repay() public payable {
        require(borrowed[msg.sender] >= msg.value, "Overpayment");
        borrowed[msg.sender] -= msg.value;
    }
    
    function withdraw(uint amount) public {
        uint available = deposits[msg.sender] - (borrowed[msg.sender] * 100 / 75);
        require(amount <= available, "Insufficient collateral");
        
        deposits[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }
}
```

**Decentralized Exchange (Uniswap-like):**
```solidity
// Automated Market Maker (AMM)
contract SimpleDEX {
    uint public reserveA;
    uint public reserveB;
    
    function addLiquidity(uint amountA, uint amountB) public {
        // Transfer tokens from user
        // Update reserves
        reserveA += amountA;
        reserveB += amountB;
        // Mint LP tokens
    }
    
    function swap(uint amountAIn) public returns (uint amountBOut) {
        // Constant product formula: x * y = k
        uint k = reserveA * reserveB;
        uint newReserveA = reserveA + amountAIn;
        uint newReserveB = k / newReserveA;
        
        amountBOut = reserveB - newReserveB;
        
        reserveA = newReserveA;
        reserveB = newReserveB;
        
        // Transfer tokens
    }
}
```

---

### **2. NFTs y Marketplaces**

**NFT Marketplace:**
```solidity
contract NFTMarketplace {
    struct Listing {
        address seller;
        uint256 price;
        bool active;
    }
    
    mapping(address => mapping(uint256 => Listing)) public listings;
    
    function listNFT(address nftContract, uint256 tokenId, uint256 price) public {
        IERC721(nftContract).transferFrom(msg.sender, address(this), tokenId);
        
        listings[nftContract][tokenId] = Listing({
            seller: msg.sender,
            price: price,
            active: true
        });
        
        emit Listed(nftContract, tokenId, price);
    }
    
    function buyNFT(address nftContract, uint256 tokenId) public payable {
        Listing memory listing = listings[nftContract][tokenId];
        require(listing.active, "Not for sale");
        require(msg.value >= listing.price, "Insufficient payment");
        
        listings[nftContract][tokenId].active = false;
        
        // Transfer NFT to buyer
        IERC721(nftContract).transferFrom(address(this), msg.sender, tokenId);
        
        // Pay seller
        payable(listing.seller).transfer(listing.price);
        
        // Refund excess
        if (msg.value > listing.price) {
            payable(msg.sender).transfer(msg.value - listing.price);
        }
        
        emit Sold(nftContract, tokenId, msg.sender, listing.price);
    }
}
```

---

### **3. DAOs (Organizaciones Autónomas Descentralizadas)**

```solidity
contract SimpleDAO {
    struct Proposal {
        string description;
        uint256 amount;
        address payable recipient;
        uint256 votesFor;
        uint256 votesAgainst;
        uint256 deadline;
        bool executed;
        mapping(address => bool) hasVoted;
    }
    
    Proposal[] public proposals;
    mapping(address => uint256) public shares;
    uint256 public totalShares;
    
    function createProposal(
        string memory description,
        uint256 amount,
        address payable recipient
    ) public {
        require(shares[msg.sender] > 0, "No shares");
        
        Proposal storage newProposal = proposals.push();
        newProposal.description = description;
        newProposal.amount = amount;
        newProposal.recipient = recipient;
        newProposal.deadline = block.timestamp + 7 days;
    }
    
    function vote(uint256 proposalId, bool support) public {
        Proposal storage proposal = proposals[proposalId];
        require(block.timestamp < proposal.deadline, "Voting ended");
        require(!proposal.hasVoted[msg.sender], "Already voted");
        require(shares[msg.sender] > 0, "No shares");
        
        if (support) {
            proposal.votesFor += shares[msg.sender];
        } else {
            proposal.votesAgainst += shares[msg.sender];
        }
        
        proposal.hasVoted[msg.sender] = true;
    }
    
    function executeProposal(uint256 proposalId) public {
        Proposal storage proposal = proposals[proposalId];
        require(block.timestamp >= proposal.deadline, "Voting ongoing");
        require(!proposal.executed, "Already executed");
        require(proposal.votesFor > proposal.votesAgainst, "Proposal rejected");
        require(proposal.votesFor > totalShares / 2, "Not enough votes");
        
        proposal.executed = true;
        proposal.recipient.transfer(proposal.amount);
    }
}
```

---

### **4. Supply Chain**

```solidity
contract SupplyChain {
    enum Status { Created, InTransit, Delivered, Cancelled }
    
    struct Item {
        string name;
        address manufacturer;
        address currentOwner;
        Status status;
        uint256 createdAt;
        Location[] locations;
    }
    
    struct Location {
        string place;
        uint256 timestamp;
    }
    
    mapping(uint256 => Item) public items;
    uint256 public itemCount;
    
    event ItemCreated(uint256 indexed itemId, string name, address manufacturer);
    event ItemTransferred(uint256 indexed itemId, address from, address to);
    event LocationUpdated(uint256 indexed itemId, string location);
    
    function createItem(string memory name) public returns (uint256) {
        uint256 itemId = itemCount++;
        
        items[itemId].name = name;
        items[itemId].manufacturer = msg.sender;
        items[itemId].currentOwner = msg.sender;
        items[itemId].status = Status.Created;
        items[itemId].createdAt = block.timestamp;
        
        emit ItemCreated(itemId, name, msg.sender);
        return itemId;
    }
    
    function transferItem(uint256 itemId, address to) public {
        require(items[itemId].currentOwner == msg.sender, "Not owner");
        require(items[itemId].status != Status.Cancelled, "Item cancelled");
        
        items[itemId].currentOwner = to;
        
        emit ItemTransferred(itemId, msg.sender, to);
    }
    
    function updateLocation(uint256 itemId, string memory location) public {
        require(items[itemId].currentOwner == msg.sender, "Not owner");
        
        items[itemId].locations.push(Location({
            place: location,
            timestamp: block.timestamp
        }));
        
        emit LocationUpdated(itemId, location);
    }
    
    function markDelivered(uint256 itemId) public {
        require(items[itemId].currentOwner == msg.sender, "Not owner");
        items[itemId].status = Status.Delivered;
    }
    
    function getHistory(uint256 itemId) public view returns (Location[] memory) {
        return items[itemId].locations;
    }
}
```

---

### **5. Gaming**

```solidity
// Play-to-Earn Game
contract GameRewards {
    mapping(address => uint256) public playerScores;
    mapping(address => uint256) public rewards;
    
    IERC20 public rewardToken;
    uint256 public rewardRate = 1 ether; // 1 token per 100 points
    
    event ScoreUpdated(address indexed player, uint256 newScore);
    event RewardClaimed(address indexed player, uint256 amount);
    
    function updateScore(address player, uint256 points) external {
        // Solo el servidor del juego puede llamar (oracle)
        playerScores[player] += points;
        rewards[player] += (points * rewardRate) / 100;
        
        emit ScoreUpdated(player, playerScores[player]);
    }
    
    function claimReward() external {
        uint256 amount = rewards[msg.sender];
        require(amount > 0, "No rewards");
        
        rewards[msg.sender] = 0;
        rewardToken.transfer(msg.sender, amount);
        
        emit RewardClaimed(msg.sender, amount);
    }
}
```

---

### **6. Real Estate (Bienes Raíces)**

```solidity
contract RealEstateToken {
    struct Property {
        string address;
        uint256 totalShares;
        uint256 pricePerShare;
        address owner;
        mapping(address => uint256) shareholders;
        uint256 rentCollected;
    }
    
    mapping(uint256 => Property) public properties;
    uint256 public propertyCount;
    
    function tokenizeProperty(
        string memory propertyAddress,
        uint256 totalShares,
        uint256 pricePerShare
    ) public returns (uint256) {
        uint256 propertyId = propertyCount++;
        
        Property storage prop = properties[propertyId];
        prop.address = propertyAddress;
        prop.totalShares = totalShares;
        prop.pricePerShare = pricePerShare;
        prop.owner = msg.sender;
        prop.shareholders[msg.sender] = totalShares;
        
        return propertyId;
    }
    
    function buyShares(uint256 propertyId, uint256 shares) public payable {
        Property storage prop = properties[propertyId];
        require(msg.value >= shares * prop.pricePerShare, "Insufficient payment");
        require(prop.shareholders[prop.owner] >= shares, "Not enough shares");
        
        prop.shareholders[prop.owner] -= shares;
        prop.shareholders[msg.sender] += shares;
        
        payable(prop.owner).transfer(shares * prop.pricePerShare);
    }
    
    function distributeRent(uint256 propertyId) public payable {
        Property storage prop = properties[propertyId];
        prop.rentCollected += msg.value;
    }
    
    function claimRent(uint256 propertyId) public {
        Property storage prop = properties[propertyId];
        uint256 userShares = prop.shareholders[msg.sender];
        require(userShares > 0, "No shares");
        
        uint256 rentShare = (prop.rentCollected * userShares) / prop.totalShares;
        prop.rentCollected -= rentShare;
        
        payable(msg.sender).transfer(rentShare);
    }
}
```

---

**Habilitación para Desarrolladores:**
1. Aprender Solidity (docs.soliditylang.org)
2. Completar CryptoZombies (tutorial interactivo)
3. Estudiar ERC standards (ERC20, ERC721, ERC1155)
4. Usar OpenZeppelin Contracts (código auditado)
5. Practicar con Remix IDE (online)
6. Setup Truffle + Ganache (local)
7. Deploy a testnets (Goerli, Sepolia)
8. Auditar código (mythril, slither)
9. Leer casos de hacks (reentrancy, overflow)
10. Unirse a comunidad (Discord, Stack Exchange)