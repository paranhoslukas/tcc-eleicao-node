# VoteChain — Nó Externo

Conecte sua máquina à rede blockchain do sistema de votação eletrônica auditável do TCC da Unianchieta.

Ao rodar este nó você ajuda a validar e auditar os votos registrados na rede GoQuorum IBFT2.

---

## Pré-requisitos

- Docker e Docker Compose instalados
- Porta `30303` TCP e UDP liberada no seu firewall/roteador

---

## Como rodar

```bash
# 1. Clone o repositório
git clone https://github.com/paranhoslukas/tcc-eleicao-node.git
cd tcc-eleicao-node

# 2. Suba o nó
docker compose up -d

# 3. Verifique se conectou à rede
docker logs tcc-no-externo -f
```

Você deve ver mensagens de sincronização de blocos em alguns segundos.

---

## Verificar conexão com a rede

```bash
# Número do bloco atual (deve aumentar a cada 2 segundos)
curl -s -X POST http://localhost:8545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'

# Peers conectados (deve ser >= 1)
curl -s -X POST http://localhost:8545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}'

# Validadores IBFT ativos
curl -s -X POST http://localhost:8545 \
  -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"istanbul_getValidators","params":["latest"],"id":1}'
```

---

## Rede

| Parâmetro     | Valor                        |
|---------------|------------------------------|
| Chain ID      | 1337                         |
| Consenso      | IBFT2                        |
| Validadores   | 4                            |
| Bloco         | a cada 2 segundos            |
| Host principal| auditvote.ddns.net       |
| Frontend      | auditvote.ddns.net:2001  |

---

## Sobre o projeto

TCC — Votação Eletrônica Auditável com Blockchain Permissiva  
Unianchieta · Jundiaí SP  
Autores: Lucas Paranhos · Matheus Barbosa · João Gabriel  
Orientador: Clayton Augusto Valdo
