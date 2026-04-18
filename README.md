# 📡 iperf3 Network Benchmark Toolkit

> **Trabalho Final** da disciplina de **Redes de Computadores (REC)**.

Ferramenta em Python para automação de testes de desempenho de rede utilizando **iperf3**, com suporte a conexões **TCP** e **UDP** simultâneas, múltiplos algoritmos de congestionamento e geração automática de gráficos comparativos.

## 📋 Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Servidor multi-instância** | Inicia múltiplos servidores iperf3 em portas sequenciais |
| **Cliente TCP configurável** | Suporte a múltiplas conexões TCP simultâneas com escolha de algoritmo de congestionamento (`cubic` ou `reno`) e bitrate |
| **Cliente UDP** | Conexão UDP com bitrate configurável, iniciada com atraso programado em relação ao TCP |
| **Exportação JSON/TXT** | Resultados exportados automaticamente em formato JSON ou texto |
| **Geração de gráficos** | Visualização comparativa de métricas (throughput, retransmissões, jitter, pacotes perdidos, etc.) via Matplotlib |

## 🏗️ Estrutura do Projeto

```
.
├── scriptServer.py    # Inicia servidores iperf3 (1 ou mais instâncias)
├── scriptClient.py    # Executa clientes iperf3 TCP e UDP com threads
├── scriptPlot.py      # Gera gráficos comparativos a partir dos JSONs
├── TF.pdf             # Documento do trabalho final
└── Slides TF - Arthur e Carlos.pdf  # Slides da apresentação
```

## 🛠️ Tecnologias

- **Python 3.x**
- **iperf3** instalado e disponível no PATH
- **Matplotlib** (`pip install matplotlib`)

## 🚀 Como Executar

### 1. Iniciar o Servidor

```bash
python scriptServer.py
```

O script solicita:
- Número de servidores iperf3 a iniciar (padrão: 2)
- Formato de exportação (JSON ou TXT)

Os servidores são iniciados nas portas **5201, 5202, ...** sequencialmente.

### 2. Executar o Cliente

```bash
python scriptClient.py
```

O script solicita interativamente:
- **IP do servidor** alvo
- **Duração** dos testes (padrão: 10s)
- **Formato de saída** (JSON ou TXT)
- **Número de conexões TCP** e, para cada uma, o algoritmo de congestionamento (`cubic`/`reno`) e bitrate
- **Bitrate do UDP** (obrigatório)

> O cliente TCP inicia primeiro. Após um atraso de **5 segundos**, a conexão UDP é iniciada, permitindo observar o impacto da competição entre os protocolos.

### 3. Gerar Gráficos

```bash
python scriptPlot.py
```

Lê os arquivos JSON gerados e plota gráficos comparativos das seguintes métricas:

- `bits_per_second` (vazão)
- `bytes`
- `retransmits` (retransmissões TCP)
- `max_snd_cwnd` (janela de congestionamento)
- `jitter_ms` (jitter UDP)
- `lost_packets` / `packets` (perda UDP)

## 📊 Exemplo de Uso

```
# Terminal 1 (Servidor)
python scriptServer.py
→ 2 servidores, JSON

# Terminal 2 (Cliente)
python scriptClient.py
→ IP: 192.168.0.10
→ Duração: 30s
→ 2 conexões TCP (1x cubic, 1x reno)
→ UDP com 50 Mb

# Após os testes
python scriptPlot.py
→ Gráficos comparativos TCP cubic vs reno vs UDP
```

## 👥 Autores

- **Arthur**

## 📄 Licença

Projeto acadêmico — uso educacional.
