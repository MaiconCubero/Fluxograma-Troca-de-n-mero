```mermaid
flowchart TD


%% INÍCIO
A([Início do Atendimento]):::start --> B["Consultar histórico no sistema<br/>(CPF / Cadastro)"]:::process


%% HISTÓRICO
B -->|Histórico OK| C{Motivo da Solicitação?}:::decision
B -->|Excedeu limite / Flag anterior| Z["Negar troca<br/>Informar política de uso"]:::deny


%% RAMO BANIMENTO WHATSAPP
C -->|Banimento WhatsApp| D[Informar cliente sobre banimento]:::process


D --> D1["Orientar acesso ao suporte oficial da Meta:<br/>faq.whatsapp.com<br/>via link ou QR Code"]:::info
D1 --> D2["Esclarecer que a Meta pode vincular banimentos<br/>a IMEI, dispositivo ou comportamento"]:::info
D2 --> D3["Alertar: se banir novamente no novo número,<br/>a responsabilidade é da Meta"]:::warning


D3 --> E{"Já houve troca por banimento<br/>nos últimos 12 meses?"}:::decision


E -->|Sim| Z
E -->|Não| F["Aprovar 1 troca anual<br/>por banimento WhatsApp*"]:::approve


%% RAMO TROCA DDD
C -->|Troca de DDD| G[Solicitar documentos]:::process
G --> G1["Documento pessoal + comprovante de residência<br/>(ex: conta de luz, aluguel, contrato)"]:::info


G1 --> H{Documentação válida?}:::decision
H -->|Sim| F
H -->|Não| Z


%% DEMAIS MOTIVOS
C -->|Demais motivos| I[Analisar motivo informado]:::process


I --> J{Motivo comprovado?}:::decision


J -->|Documento válido| F
J -->|Suspeita de abuso| Z
J -->|Informação insuficiente| K["Solicitar mais informações<br/>ao cliente"]:::loop


K --> I


%% CASOS ESPECÍFICOS
I -->|Caso específico / exceção| L[Protocolar atendimento]:::process
L --> M[Encaminhar para Suporte Nível 2 – Redes]:::escalation


%% FINAL
F --> N([Executar troca de número]):::endNode
Z --> O([Encerrar atendimento]):::endNode


%% ESTILOS
classDef start fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px
classDef endNode fill:#E3F2FD,stroke:#1565C0,stroke-width:2px
classDef process fill:#F9F9F9,stroke:#555
classDef decision fill:#FFFDE7,stroke:#F9A825
classDef approve fill:#E8F5E9,stroke:#388E3C
classDef deny fill:#FDECEA,stroke:#C62828
classDef info fill:#E3F2FD,stroke:#1E88E5
classDef warning fill:#FFF3E0,stroke:#EF6C00
classDef loop fill:#F3E5F5,stroke:#6A1B9A
classDef escalation fill:#ECEFF1,stroke:#37474F
