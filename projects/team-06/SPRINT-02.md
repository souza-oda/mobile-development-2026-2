# SPRINT 02 — State & User Interaction

## Team Identification

- **Project:** Caramelo Transportes
- **Module:** Register Activity (`RegisterActivity.kt` / `RegisterScreen`)
- **Architecture:** Jetpack Compose (Declarative State Management)

---

## 1. Interaction Selection

### Selected Feature

**Formulário Dinâmico e Interativo de Cadastro de Usuários (`RegisterScreen`)**:
1. **Alternância Dinâmica de Tipo de Documento**: Seleção de perfil Nacional (CPF) vs. Internacional (Passaporte).
2. **Busca e Preenchimento Automático de CEP**: Integração assíncrona em corrotina com a API do ViaCEP ao digitar 8 dígitos de CEP, exibindo indicador visual de carregamento.
3. **Visibilidade de Senha Interativa**: Alternância entre senha oculta e visível para campos de senha e confirmação de senha.
4. **Validação de Formulário e Fluxo de Transição**: Verificação dos campos obrigatórios antes do avanço para o cadastro de veículos.

### Problem Solved

Preencher formulários extensos em telas mobile costuma ser burocrático e suscetível a erros de digitação (especialmente em endereços e senhas incorretas). Em `RegisterActivity.kt`, a interface reage dinamicamente aos inputs do usuário:
- Adapta os rótulos e tipo de teclado (numérico ou texto) conforme o tipo de documento (CPF ou Passaporte).
- Auto-completa rua, bairro, cidade e estado assim que o CEP é digitado, reduzindo o esforço do usuário.
- Garante o feedback visual em tempo real (loader no CEP, senhas visíveis/ocultas e validação de regras de cadastro).

### Meaningful Value for the Product

Esta funcionalidade estabelece o gerenciamento declarativo de estado (`remember` + `mutableStateOf` + Coroutines) no projeto Caramelo Transportes. O usuário vivencia uma experiência de cadastro fluida, inteligente e sem erros de preenchimento, permitindo uma transição perfeita para as próximas etapas do aplicativo (como o cadastro de veículos e navegação de rotas).

---

## 2. State & Compose Architecture

### State Definition

| Variável de Estado | Tipo de Dado | Valor Inicial | Mecanismo Compose | Descrição / Função na UI |
| --- | --- | --- | --- | --- |
| `isNational` | `Boolean` | `true` | `remember { mutableStateOf(true) }` | Alterna entre Cadastro Nacional (`true`, solicita CPF) e Internacional (`false`, solicita Passaporte). |
| `documentNumber` | `String` | `""` | `remember { mutableStateOf("") }` | Armazena o CPF ou número do Passaporte digitado. |
| `name` | `String` | `""` | `remember { mutableStateOf("") }` | Armazena o nome completo do usuário. |
| `email` | `String` | `""` | `remember { mutableStateOf("") }` | Armazena o e-mail do usuário. |
| `cep` | `String` | `""` | `remember { mutableStateOf("") }` | Armazena o CEP e dispara a busca automática ao atingir 8 dígitos. |
| `street`, `neighborhood`, `city`, `state` | `String` | `""` | `remember { mutableStateOf("") }` | Campos de endereço preenchidos automaticamente pela API ViaCEP ou manualmente. |
| `number`, `complement` | `String` | `""` | `remember { mutableStateOf("") }` | Número residencial e complemento. |
| `isLoadingCep` | `Boolean` | `false` | `remember { mutableStateOf(false) }` | Exibe o `CircularProgressIndicator` no ícone do campo de CEP durante a busca assíncrona. |
| `password`, `confirmPassword` | `String` | `""` | `remember { mutableStateOf("") }` | Campos para digitação e confirmação de senha. |
| `passwordVisible`, `confirmPasswordVisible` | `Boolean` | `false` | `remember { mutableStateOf(false) }` | Controla `PasswordVisualTransformation()` vs `VisualTransformation.None`. |

### Event -> State -> UI Flow

```text
1. ALTERNÂNCIA DE TIPO DE DOCUMENTO (Nacional vs. Internacional)
[Estado Inicial: isNational = true → Card "Nacional" selecionado com borda Cacau e fundo bege]
      ↓
[Ação do Usuário: Clica no Card "Internacional"]
      ↓
[Evento onClick → isNational = false, documentNumber = ""]
      ↓
[Recomposição: Card "Internacional" recebe borda destacada; Rótulo muda para "Passaporte / Doc. Internacional"]


2. BUSCA AUTOMÁTICA DE ENDEREÇO VIA CEP
[Ação do Usuário: Digita 8 dígitos no campo CEP (ex: 01001000)]
      ↓
[Evento onValueChange → cep = newCep → Dispara searchCep(newCep)]
      ↓
[Atualização de Estado: isLoadingCep = true → Recomposição exibe CircularProgressIndicator no trailingIcon]
      ↓
[Requisição Assíncrona (Corrotina Dispatchers.IO): fetchAddressViaCep("01001000")]
      ↓
[Sucesso na API → street = "Praça da Sé", neighborhood = "Sé", city = "São Paulo", state = "SP", isLoadingCep = false]
      ↓
[Recomposição UI: Preenche automaticamente os campos de Rua, Bairro, Cidade e UF no formulário]


3. VISIBILIDADE DE SENHA
[Ação do Usuário: Clica no IconButton de olho no campo de senha]
      ↓
[Evento onClick → passwordVisible = !passwordVisible]
      ↓
[Recomposição UI: Alterna o ícone entre Visibility / VisibilityOff e visualTransformation entre Password e None]
```

### Visual Feedback

1. **Seleção de Documento**: Borda de `2.dp` em tom `Cacau` (`#3B1705`) e fundo claro no Card do tipo selecionado ("Nacional" ou "Internacional").
2. **Indicador de CEP**: Substituição do ícone de localização por um `CircularProgressIndicator` animado durante a busca na API ViaCEP.
3. **Autocompletar de Endereço**: Preenchimento instantâneo e suave dos campos de logradouro, bairro, cidade e UF após o retorno da busca.
4. **Visibilidade da Senha**: Mudança instantânea do ícone e da revelação do texto digitado nos campos de senha.
5. **Validação ao Avançar**: Disparo de mensagens `Toast` explicativas caso falte preencher algum campo obrigatório ou se as senhas não coincidiram.

---

## 3. Scope & Requirements

### Functional Requirements

- **FR-01 — Alternância de Tipo de Registro**: Permite alternar entre "Nacional" e "Internacional", ajustando os rótulos e tipo de teclado do documento.
- **FR-02 — Preenchimento de Dados Pessoais**: Campos para nome completo e e-mail.
- **FR-03 — Busca Dinâmica por CEP**: Consulta à API pública do ViaCEP via corrotinas Kotlin quando o CEP possui 8 dígitos limpos.
- **FR-04 — Indicador Visual de Carregamento**: Exibição de spinner de carregamento no campo de CEP enquanto a consulta está em andamento.
- **FR-05 — Preenchimento Automático de Logradouro**: Atualização automática de Rua, Bairro, Cidade e Estado com os dados retornados pela API.
- **FR-06 — Campos Manuais de Endereço**: Campos editáveis para Número e Complemento.
- **FR-07 — Visibilidade de Senhas**: Botão para alternar a exibição/ocultação nos campos "Senha" e "Confirmar Senha".
- **FR-08 — Validação de Formulário**: Bloqueio de envio e exibição de alertas se houver campos em branco ou senhas divergentes.
- **FR-09 — Cadastro Rápido com Google**: Botão estilizado para fluxo de login/cadastro rápido.
- **FR-10 — Transição de Tela**: Redirecionamento para `VehicleRegisterActivity` ao cadastrar com sucesso, ou retorno para `LoginSideActivity`.

### Non-Functional Requirements

- **NFR-01 — Desempenho e Corrotinas**: A requisição de CEP roda em thread de I/O (`Dispatchers.IO`) sem bloquear a Thread Principal (UI Thread).
- **NFR-02 — Design System Material 3**: Utilização de `OutlinedTextField`, `Card`, `Button`, `Scaffold` e esquema de cores customizadas (`Cacau`, `Mel`).
- **NFR-03 — Feedback Acessível**: Ícones descritivos e mensagens em português claro para orientação do usuário.

---

## 4. Acceptance Criteria

- [x] **AC-01** — A tela de cadastro `RegisterActivity.kt` utiliza o ecossistema Jetpack Compose.
- [x] **AC-02** — Os estados do formulário são mantidos via `remember { mutableStateOf(...) }`.
- [x] **AC-03** — Disparo de eventos do usuário altera o estado (digitação, seleção de cards, botões de alternância).
- [x] **AC-04** — A UI recompõe corretamente apresentando feedback visual em tempo real.
- [x] **AC-05** — A busca de CEP assíncrona é executada sem travamentos na interface.
- [x] **AC-06** — As senhas possuem opção de serem exibidas ou ocultadas.
- [x] **AC-07** — Os erros de preenchimento são devidamente informados através de Toasts informativos.
- [x] **AC-08** — O aplicativo compila perfeitamente via Gradle sem erros de sintaxe ou execução.

---

## 5. Regression Validation

1. **Navegação de Retorno**: O link "Já tem uma conta? Faça Login" encerra a Activity e retorna corretamente para a tela de Login (`LoginSideActivity.kt`).
2. **Integração com Próxima Activity**: O cadastro com sucesso inicia a `VehicleRegisterActivity`.
3. **Temas e Estilos**: A paleta de cores (`Cacau`, `Mel`) e as tipografias mantêm a identidade do aplicativo Caramelo Transportes.

---

## 6. Deliverables

- `app/src/main/java/com/example/composeraraiser/RegisterActivity.kt` — Implementação completa com gerenciamento de estado e integração ViaCEP.
- `app/src/main/java/com/example/composeraraiser/LoginSideActivity.kt` — Tela de login integrada.
- `SPRINT-02.md` — Documento de especificação de estados e interações da `RegisterActivity`.
