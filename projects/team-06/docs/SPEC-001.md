# SPEC-001 — Definição do Produto Wi-Fi Mapper e Primeira Tela

> **Equipe:** Team 06  
> **Integrantes:** Odair Souza (@souza-oda)  
> **Sprint:** SPRINT 01  
> **Status:** Validado  
> **Documento da Sprint:** [`SPRINT-01.md`](../../SPRINT-01.md)

---

## 1. Contexto

**Problema:**  
Os transportes modernos possuem certa insegurança relativa ao motorista e as rotas de viagenns E também as viagens não apresentam certa experiencia de usuário causando assim um certo incomodo durante as viagens.

**Usuário / Ator:**  
QUalquer usuário de aplicativo de mobilidade que deseja uma boa experiência de viagem.

**Contexto de Uso:**  
O usuário poderar optar por diversas opções de viagem para se sentir acomodado, como um cafézinho ou um tipo de motorista de preferencia.
---

## 2. Objetivo

O objetivo será humanizar as viagens e deixa-las mais personalizadas. assim o passageiro se sente mais acomodado e confortado perante a certos tipos de transporte.

---

## 3. Cenário do Usuário (User Scenario)

**Dado** qO usuário deseja uma rota de transporte.  
**Quando** Deseja se locomover para outro lugar. 
**Então** O usuário espera por um transporte chegar e leva-lo a outro lugar de forma personalizada e humanizada.

---

## 4. Requisitos Funcionais

### RF-01 — Identidade Visual do Produto
A interface da primeira tela deve exibir o nome do aplicativo (**Caramelo Transportes**) com o tema de cores escolhido.

### RF-02 — Slogan e Proposta de Valor
A interface deve apresentar a mensagem os botoes de login, registro e recuperação de conta sem que haja conexão direta com outras telas.

### RF-03 — Elemento Visual de Sinal
A tela de mapa de ve estar apresentando um sistema de rastreio em tempo reale deve abrir na localização atual.

---

## 5. Restrições Técnicas

### Tecnologias Obrigatórias:
- **Linguagem:** Kotlin
- **UI Framework:** Jetpack Compose (Material Design 3)
- **IDE:** Android Studio (Ladybug 2024.2.1 ou superior)

### Restrições do Projeto:
- **SDK Mínimo:** API 24 (Android 7.0)
- **SDK Alvo:** API 34+
- **Layouts Legados:** Não utilizar XML layouts para telas de UI.
- **Escopo desta Sprint:** Não utilizar chamadas a APIs de rede externas ou banco de dados nesta etapa.

---

## 6. Fora do Escopo (Out of Scope)

Os seguintes itens não fazem parte do escopo da Sprint 01 e serão abordados em sprints posteriores:
- Não deve possuir nenhum requesito a partir da sprint 02.

---

## 7. Critérios de Aceitação

### AC-01 — Nome do Aplicativo Visível
**Requisito relacionado:** RF-01  
**Condição:** Ao abrir a tela, o título **Wi-Fi Mapper** deve estar visível, centralizado e legível com estilo tipográfico de destaque.

### AC-02 — Slogan e Proposta de Valor Acessíveis
**Requisito relacionado:** RF-02  
**Condição:** O texto descritivo do slogan deve estar posicionado abaixo do título, com contraste adequado e tipografia legível.

### AC-03 — Elemento Visual Central Apresentado
**Requisito relacionado:** RF-03  
**Condição:** A interface deve renderizar o container visual com cantos arredondados e as barras de intensidade de sinal.

### AC-04 — Botão de Ação Primária Funcional e Destacado
**Requisito relacionado:** RF-04  
**Condição:** O botão *"Iniciar Verificação de Sinal"* deve estar visível com largura proporcional, cores do tema e feedback visual de clique.

### AC-05 — Compilação e Execução Estável
**Requisitos relacionados:** RF-01, RF-02, RF-03, RF-04  
**Condição:** O aplicativo deve compilar com `./gradlew assembleDebug` e rodar em emuladores Android (API 24+) sem gerar falhas em tempo de execução (*no crash*).

---

## 8. Rastreabilidade dos Requisitos

| Requisito | Implementado Em | Critério de Aceitação | Evidência |
| :--- | :--- | :--- | :--- |
| **RF-01** | `MainActivity.kt` (`WifiMapperHomeScreen`) | AC-01 | `evidence/sprint-01/first-screen.png` |
| **RF-02** | `MainActivity.kt` (`WifiMapperHomeScreen`) | AC-02 | `evidence/sprint-01/first-screen.png` |
| **RF-03** | `MainActivity.kt` (`WifiMapperHomeScreen`) | AC-03 | `evidence/sprint-01/first-screen.png` |
| **RF-04** | `MainActivity.kt` (`WifiMapperHomeScreen`) | AC-04 | `evidence/sprint-01/first-screen.png` |

---

## 9. Plano de Implementação

### Componentes Criados/Modificados:
- `MainActivity.kt`: Implementação do Composable `LoginScreen` com `Scaffold`, `Column`, `Box`, `Row`, `Text`, `Button` e espaçamentos com `Arrangement.SpaceEvenly`.
- `Theme.kt`: Ajuste das cores e tipografia do Material Design 3.

### Fluxo de Interação Previsto:
```text
[Abertura do App]
      ↓
[Visualização do Nome, Slogan e Ilustração de Sinal]
      ↓
[Toque no Botão "Iniciar Verificação de Sinal"]
      ↓
[Feedback Visual de Toque (Ripple)]
```

---

## 10. Resultados da Validação

| Critério | Resultado | Observações |
| :--- | :--- | :--- |
| **AC-01** | **PASS** | Título "Wi-Fi Mapper" renderizado com destaque e alinhamento central. |
| **AC-02** | **PASS** | Slogan *"Encontre os pontos cegos do seu Wi-Fi..."* legível e centralizado. |
| **AC-03** | **PASS** | Container visual de intensidade de sinal com cantos arredondados renderizado. |
| **AC-04** | **PASS** | Botão primário *"Iniciar Verificação de Sinal"* estilizado e responsivo ao toque. |
| **AC-05** | **PASS** | Projeto compilando e executando sem crash no emulador Android. |

### Ambiente de Validação:
- **Dispositivo:** Emulador Android (Google Pixel 8)
- **Versão do Android:** API 34 (Android 14)
- **Resultado do Build:** PASS
- **Execução do App:** PASS

---

## 11. Evidência de Validação

- **Evidência Visual:** `projects/team-03/evidence/sprint-01/first-screen.png`
- **Referência no Documento da Sprint:** [`SPRINT-01.md`](../../SPRINT-01.md#4-validação-e-evidência)

---

## 12. Desenvolvimento com Apoio de IA

- **Ferramenta Utilizada:** Antigravity AI / Gemini 3.6 Flash
- **Uso:** Auxílio na estruturação dos requisitos funcionais, critérios de aceitação e arquitetura da interface com Jetpack Compose.
- **Revisão Humana:** Validação e adaptação de todos os textos para o contexto em português do **Cramelo Transportes** e verificação de compatibilidade com o Material Design 3.

---

## 13. Status da Especificação

- [x] Contexto e objetivo definidos com foco na dor real do usuário.
- [x] Requisitos funcionais completos e observáveis.
- [x] Restrições técnicas e fora de escopo explicitados.
- [x] Critérios de aceitação mensuráveis e testáveis.
- [x] Matriz de rastreabilidade de requisitos preenchida.
- [x] Validação executada e documentada.
- [x] Todas as integrantes compreendem a especificação e a implementação.
