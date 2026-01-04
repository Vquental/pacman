# 👾 Pac-Man Clássico em Assembly

Este projeto é uma implementação em Assembly de um motor de jogo Pac-Man, criado para um ambiente de simulação ou hardware específico (microprocessador de 16 bits), focado em demonstrar a programação de baixo nível, manipulação direta de memória (ecrã) e lógica de jogo básica.

## 🎯 Objetivo do Projeto

O objetivo principal deste projeto é:

* **Dominar a Programação de Baixo Nível:** Entender como a lógica complexa de um jogo é construída usando apenas instruções básicas (registos, aritmética, saltos).
* **Controlo de Hardware:** Implementar rotinas de E/S para gestão de um teclado matricial e um display de matriz de 32x32 pixels, sem o uso de um sistema operativo ou bibliotecas.
* **Estruturas de Dados:** Implementar conceitos como **Pilha**, **Tabelas de Pesquisa (Lookup Tables)** e **Máscaras de Bit** para otimização.

## 🛠️ Requisitos e Configuração

### Requisitos de Hardware/Software

Este código foi desenvolvido para ser executado num **Simulador de Arquitetura de Microprocessador de 16-bits (Ex: Sim-16/Simulador de Eletrotécnico)**.

| Componente | Especificação |
| :--- | :--- |
| **Microprocessador** | 16-bit |
| **Ecrã** | Matriz de 32x32 pixels |
| **Memória de E/S** | Mapeamento de endereço de porta de E/S para teclado e displays. |

### Endereços de E/S Utilizados

As constantes de endereço são definidas no topo do ficheiro `pacman.asm`:

| Constante | Endereço | Descrição |
| :---: | :---: | :--- |
| `ECRA_INICIO` | `8000H` | Endereço de início da memória de vídeo (VRAM). |
| `PIN` | `0E000H` | Porta de entrada para leitura do teclado. |
| `POUT` | `0C000H` | Porta de saída para varredura do teclado. |
| `DISPLAYS` | `0A000H` | Porta de saída para o display de 7 segmentos (Tempo). |

## 🕹️ Funcionalidades e Gameplay

O jogo implementa as seguintes funcionalidades:

1.  **Menu Inicial:** Exibição da mensagem "PLAY" e espera pelo início do jogo.
2.  **Movimento:** Controlo do Pac-Man com deteção de colisão com a área central de confinamento dos fantasmas.
3.  **IA Simplificada do Fantasma:** Os fantasmas utilizam estados (Na Caixa, A Sair, Livre) e, no estado Livre, executam uma perseguição básica por coordenadas.
4.  **Coleta:** Rotina de coleta de 4 objetos (pontos) espalhados pelos cantos do ecrã.
5.  **Exibição de Tempo:** Contagem do tempo decorrido no display de 7 segmentos.
6.  **Condição de Fim:**
    * **Vitória:** Coletar todos os 4 pontos.
    * **Derrota:** Colisão com um fantasma no estado **Livre**.

## 💻 Estrutura do Código (`pacman.asm`)

O ficheiro está organizado em secções numeradas para facilitar a navegação e o entendimento da lógica de baixo nível:

| Secção | Descrição | Funções Chave |
| :---: | :---: | :--- |
| **1.** | Definições de Constantes | `EQU` |
| **2.** | Tabelas de Pixels (Sprites) | `tabela_pacman`, `tabela_fantasma` |
| **3.** | Tabelas de Lookup | `tabela_bits`, `tabela_7seg` |
| **4.** | Variáveis do Jogo | `estado_jogo`, `linha_pacman`, `fantasmas` |
| **6.** | Programa Principal | `inicio`, `loop_jogo` (Fluxo de Controlo) |
| **7.** | Rotinas de E/S | `ler_teclado_jogo`, `atualizar_displays` |
| **8.** | Lógica do Jogo | `mover_pacman`, `mover_fantasmas` |
| **9.** | Rotinas de Colisão | `verificar_coleta`, `verificar_colisoes` |
| **10.** | Rotinas de Desenho | `pixel_xy`, `desenhar_objeto`, `desenhar_caixa` |
| **11.** | Rotinas de Estado | `mostrar_menu`, `mostrar_tela_final` |

### Destaques da Implementação

* **Pixel Mapping (Rotina `pixel_xy`):** O cálculo do endereço de memória do ecrã é feito usando a fórmula: $Endereço = 8000H + (\text{Linha} \times 4) + (\text{Coluna} / 8)$.
* **Varredura do Teclado:** Implementação de um loop de varredura coluna por coluna, usando a porta de saída (`POUT`) e a porta de entrada (`PIN`) para detetar a linha e a coluna da tecla pressionada.

## 🤝 Contribuições

Sinta-se à vontade para sugerir melhorias, como:

* Melhoramento da IA dos fantasmas (Ex: Algoritmo Scatter/Chase).
* Adicionar mais níveis ou pontos.
* Otimização do uso de registos para ciclos de clock.

---
**Desenvolvido por:** [Valdemiro Quental/Arquitetura de computadores]
