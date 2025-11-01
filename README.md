#  Tarefa 05 – Transmissão de Dados via LoRa

##  Descrição do Projeto

Este projeto implementa um sistema de **comunicação sem fio via LoRa** entre uma **FPGA ColorLight i9** e uma **BitDogLab**, utilizando módulos **LoRa RFM96**.

O sistema é composto por dois nós:

- **Nó Transmissor (FPGA – ColorLight i9):**
  - Implementa um **SoC customizado** baseado no **LiteX**, com **core VexRiscv**.
  - Lê temperatura e umidade do sensor **AHT10** via barramento **I2C**.
  - Envia periodicamente (a cada 10 segundos) os dados coletados via **SPI** para o módulo **LoRa RFM96**.

- **Nó Receptor (BitDogLab):**
  - Recebe os pacotes LoRa transmitidos pela FPGA.
  - Decodifica e exibe os valores de **temperatura** e **umidade** em um **display OLED** via protocolo **I2C**.
  - Atualiza automaticamente a leitura a cada nova transmissão recebida.

---

##  Diagrama de Blocos do Sistema

    ┌─────────────────────────────┐
    │        FPGA ColorLight i9   │
    │ ┌─────────────────────────┐ │
    │ │       SoC LiteX         │ │
    │ │  Core: VexRiscv         │ │
    │ │                         │ │
    │ │ I2C  ───>  Sensor AHT10 │ │
    │ │ SPI  ───>  LoRa RFM96   │ │
    │ │Timer → Leitura periódica│ │
    │ └─────────────────────────┘ │
    └──────────────┬──────────────┘
                   │
              Comunicação LoRa
                   │
    ┌──────────────┴──────────────┐
    │         BitDogLab           │
    │ ┌─────────────────────────┐ │
    │ │  LoRa RFM96 (SPI)       │ │
    │ │  OLED SSD1306 (I2C)     │ │
    │ │                         │ │
    │ │ Exibe: Temp / Umid.     │ │
    │ └─────────────────────────┘ │
    └─────────────────────────────┘


