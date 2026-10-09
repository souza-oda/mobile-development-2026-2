# SPEC-002 — Formulário Dinâmico e Interativo de Cadastro (`RegisterActivity`)

> **Project:** Caramelo Transportes  
> **Module:** `RegisterActivity.kt` (`RegisterScreen`)  
> **Sprint:** Sprint 02 — State & User Interaction  
> **Status:** Completed  
> **Related Sprint:** `SPRINT-02.md`  

---

## 1. Context

**Problem:**

Formulários de cadastro mobile que dependem do preenchimento totalmente manual de dados de endereço e senhas sem validação em tempo real tendem a gerar alta taxa de abandono, erros de digitação (especialmente em CEPs, nomes de ruas e divergências de senhas) e insatisfação do usuário.

Em `RegisterActivity.kt`, foi desenvolvido um formulário dinâmico reativo em Jetpack Compose que:
- Adapta automaticamente o tipo de documento solicitado conforme a nacionalidade (CPF para brasileiros ou Passaporte para estrangeiros).
- Realiza a consulta assíncrona de CEP na API do ViaCEP assim que o usuário digita 8 dígitos, autocompletando rua, bairro, cidade e estado.
- Oferece controle interativo de visibilidade para os campos de senha.
- Valida os campos obrigatórios e direciona o usuário com fluidez para a próxima etapa (cadastro de veículos).

**User / Actor:**

- **Novos Usuários / Motoristas / Clientes** que desejam se cadastrar no aplicativo Caramelo Transportes.

**Usage Context:**

Iniciado a partir da tela de login (`LoginSideActivity.kt`) ao clicar em "Criar nova conta / Registrar".

---

## 2. Objective

Tornar a tela de cadastro **reativa, inteligente e segura** usando o gerenciamento declarativo de estado do Jetpack Compose (`remember`, `mutableStateOf` e Corrotinas). O objetivo principal é guiar o usuário com feedback visual em tempo real, preenchendo automaticamente o endereço via CEP, permitindo alternância de perfil de documento e garantindo a validação dos dados inseridos antes de prosseguir.

---

## 3. User Scenario

**Cenário A — Seleção do Tipo de Registro (Nacional vs. Internacional)**

**Given** que o usuário está na tela de cadastro (`RegisterScreen`),  
**When** ele clica no card "🌎 Internacional",  
**Then** a variável `isNational` torna-se `false`, o card "Internacional" ganha destaque visual e o campo de documento altera o rótulo para "Passaporte / Doc. Internacional".

**Cenário B — Autocompletar de Endereço via CEP**

**Given** que o usuário digita os 8 dígitos do CEP (ex: `01001000`),  
**When** a entrada atinge 8 caracteres numéricos,  
**Then** a corrotina aciona a API ViaCEP, exibe um spinner (`CircularProgressIndicator`) no campo de CEP e preenche automaticamente os campos de Rua, Bairro, Cidade e UF.

**Cenário C — Visibilidade de Senha**

**Given** que a senha foi digitada com máscara (`PasswordVisualTransformation`),  
**When** o usuário clica no ícone de olho (`IconButton`),  
**Then** a variável `passwordVisible` é alternada e o texto da senha é revelado.

---

## 4. Functional Requirements

### FR-01 — Alternância do Tipo de Documento
O aplicativo deve alternar entre perfil Nacional (CPF) e Internacional (Passaporte) através do estado `isNational`.

### FR-02 — Preenchimento de Identificação
O aplicativo deve disponibilizar campos para nome completo, e-mail e número do documento.

### FR-03 — Integração e Busca por CEP
O aplicativo deve consultar automaticamente a API pública do ViaCEP em segundo plano (`Dispatchers.IO`) quando um CEP com 8 dígitos for digitado.

### FR-04 — Feedback de Carregamento de CEP
O aplicativo deve exibir um indicador visual de progresso (`CircularProgressIndicator`) no campo de CEP enquanto a consulta HTTP estiver em andamento (`isLoadingCep = true`).

### FR-05 — Preenchimento Automático de Endereço
O aplicativo deve atualizar os estados `street`, `neighborhood`, `city` e `state` com a resposta da API do ViaCEP.

### FR-06 — Campos de Endereço Complementares
O aplicativo deve disponibilizar campos editáveis para Número e Complemento.

### FR-07 — Controle de Visibilidade das Senhas
O aplicativo deve permitir exibir ou ocultar os caracteres digitados nos campos "Senha" e "Confirmar Senha" individualmente via `passwordVisible` e `confirmPasswordVisible`.

### FR-08 — Validação e Envio do Formulário
O aplicativo deve verificar se os campos obrigatórios foram preenchidos e se as senhas coincidem antes de chamar `onRegisterSuccess()`.

### FR-09 — Botão de Cadastro Rápido com Google
O aplicativo deve conter um botão customizado de cadastro com o Google.

### FR-10 — Navegação de Retorno
O aplicativo deve permitir que o usuário retorne à tela de Login através da callback `onBackToLogin`.

---

## 5. Constraints

### Required Technologies

- **Linguagem**: Kotlin
- **Framework UI**: Jetpack Compose (`Material 3`)
- **Assincronismo**: Kotlin Coroutines (`Dispatchers.IO` / `withContext`)
- **Rede / API**: `HttpURLConnection` + `org.json.JSONObject` (ViaCEP)

### Project Constraints

- Manutenção da paleta de cores institucional (`Cacau` - `#3B1705`, `Mel`).
- Uso de `remember { mutableStateOf(...) }` para gerenciamento local de estado.
- Interface responsiva com rolagem vertical (`verticalScroll(rememberScrollState())`).

---

## 6. Out of Scope

- Autenticação real no servidor backend Firebase / OAuth Google (simulado via `Toast` e navegação).
- Validação algorítmica de dígito verificador do CPF.
- Armazenamento persistente em banco de dados local (Room / SQLite).

---

## 7. Acceptance Criteria

### AC-01 — Alternância do Tipo de Documento
- [x] O clique no card "Internacional" altera a interface para solicitar Passaporte.
- [x] O clique no card "Nacional" restaura a solicitação de CPF.

### AC-02 — Busca por CEP e Autocompletar
- [x] Digitar um CEP válido (ex: 01001-000) dispara a requisição e exibe o indicador de carregamento.
- [x] Logradouro, Bairro, Cidade e UF são preenchidos automaticamente na tela.

### AC-03 — Alternância de Senha
- [x] O clique no ícone de olho alterna entre caracteres ocultos (`•••`) e texto visível.

### AC-04 — Validação de Formulário
- [x] Submeter o formulário com campos em branco gera um alerta de erro (`Toast`).
- [x] Submeter senhas divergentes exibe a mensagem "As senhas não coincidem".

### AC-05 — Navegação
- [x] Ao concluir com sucesso, o app direciona para o cadastro de veículos (`VehicleRegisterActivity`).
- [x] O botão "Já tem uma conta?" encerra a Activity e retorna ao Login.

---

## 8. Requirement Traceability

| Requisito | Componente / Função em `RegisterActivity.kt` | Critério de Aceite |
| --- | --- | --- |
| FR-01 | Estado `isNational` + Cards clicáveis | AC-01 |
| FR-02 | `OutlinedTextField` para Nome, E-mail e Documento | AC-04 |
| FR-03, FR-05 | `fetchAddressViaCep(cep)` + `searchCep()` em Corrotina | AC-02 |
| FR-04 | `isLoadingCep` + `CircularProgressIndicator` no `trailingIcon` | AC-02 |
| FR-06 | `OutlinedTextField` para Número e Complemento | AC-04 |
| FR-07 | `passwordVisible`, `confirmPasswordVisible` + `IconButton` | AC-03 |
| FR-08 | Validação no evento `onClick` do `Button` "Avançar" | AC-04 |
| FR-10 | `TextButton` com chamada para `onBackToLogin()` | AC-05 |

---

## 9. Implementation Plan

### Main Composable Architecture (`RegisterScreen`)

```text
RegisterScreen
├── Header (Título + Subtítulo)
├── Botão "Cadastrar com o Google"
├── Seleção de Perfil (Cards: Nacional vs Internacional)
├── Campos de Identificação (Documento, Nome Completo, E-mail)
├── Seção de Endereço (CEP com ViaCEP API + Logradouro, Número, Bairro, Cidade, UF)
├── Seção de Senha (Senha e Confirmação de Senha com alternância de visibilidade)
└── Botões de Ação ("Avançar: Cadastrar Veículo" e "Voltar para Login")
```

---

## 10. Validation Results

| Teste | Resultado | Observações |
| --- | --- | --- |
| Compilação e Preview | **PASS** | `RegisterScreenPreview` renderizado com sucesso. |
| Alternância Nacional/Internacional | **PASS** | Interface altera os rótulos e limpa o campo de documento corretamente. |
| Consulta de CEP | **PASS** | Conexão com a API ViaCEP em background preenche os campos com sucesso. |
| Visibilidade da Senha | **PASS** | O ícone de olho altera a visualização do texto da senha sem falhas. |
| Navegação entre Atividades | **PASS** | Sucesso no redirecionamento para `VehicleRegisterActivity`. |
