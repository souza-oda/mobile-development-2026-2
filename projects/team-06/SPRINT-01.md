# SPRINT 01 — Definição do Produto e Primeira Experiência

## Identificação da Equipe

- **Equipe:** Team-06
- **Projeto:** Caramelo — Plataforma de Mobilidade Urbana
- **Instituição:** UNEMAT
- **Integrante:** Odair Souza

---

## 1. Definição do Produto

### Nome do Produto

**Caramelo** — Mobilidade com calor humano.

### Problema

Usuários de serviços de mobilidade urbana precisam solicitar viagens com rapidez, entender o valor estimado da corrida e acompanhar o deslocamento com segurança. Apesar da existência de diferentes plataformas no mercado, a experiência ainda pode apresentar atritos importantes:

1. **Falta de Clareza na Solicitação:** Informações de origem, destino, tempo de espera, categoria do veículo e preço podem aparecer de forma dispersa, aumentando o esforço necessário para confirmar uma corrida.

2. **Baixa Previsibilidade:** A ausência de uma hierarquia visual clara dificulta a comparação entre modalidades de viagem, preços e quantidade de passageiros.

3. **Experiência Impessoal:** Muitas soluções priorizam somente a eficiência operacional e utilizam uma comunicação visual fria, com pouca proximidade cultural com o público brasileiro.

4. **Percepção de Insegurança:** Informações sobre proteção da viagem, localização do veículo e status da busca nem sempre são apresentadas de forma visível durante toda a jornada.

Dessa forma, existe a oportunidade de criar uma experiência de mobilidade simples, acolhedora e transparente, capaz de conectar passageiros e motoristas com menos atrito.

### Usuários-Alvo

Os usuários-alvo da plataforma Caramelo estão divididos nos seguintes perfis:

1. **Passageiros — Usuários Primários:**

   - **Perfil:** Pessoas que precisam realizar deslocamentos urbanos cotidianos, como viagens para casa, trabalho, estudo, compras e lazer.
   - **Necessidade:** Informar origem e destino rapidamente, comparar categorias, conhecer o preço estimado, selecionar o pagamento e acompanhar a busca por um motorista.

2. **Motoristas Parceiros — Usuários Primários:**

   - **Perfil:** Condutores que utilizam a plataforma para receber solicitações de viagem e gerar renda.
   - **Necessidade:** Visualizar pedidos próximos, conhecer os dados essenciais da corrida, aceitar viagens e acompanhar o trajeto.

3. **Equipe de Operação — Usuários Secundários:**

   - **Perfil:** Profissionais responsáveis por suporte, segurança, pagamentos e acompanhamento da operação.
   - **Necessidade:** Consultar corridas, acompanhar indicadores e prestar suporte a passageiros e motoristas.

4. **Parceiros Corporativos — Usuários Secundários:**

   - **Perfil:** Empresas e instituições que precisam organizar o transporte de colaboradores ou clientes.
   - **Necessidade:** Solicitar viagens, administrar formas de pagamento e consultar históricos.

### Objetivo do Produto

O objetivo principal do **Caramelo** é oferecer uma experiência de mobilidade urbana simples, segura e próxima, reduzindo as dúvidas entre a intenção de viajar e o embarque.

A aplicação busca alcançar os seguintes resultados:

- **Solicitação Ágil:** Permitir que o passageiro informe origem e destino em poucos passos.
- **Comparação Transparente:** Apresentar tempo estimado, capacidade, nível de conforto e preço de cada categoria.
- **Maior Previsibilidade:** Exibir motoristas próximos, rota, destino e previsão de embarque.
- **Sensação de Segurança:** Tornar visíveis os recursos de proteção durante toda a jornada.
- **Identidade Brasileira:** Utilizar linguagem acolhedora e uma identidade visual inspirada na paleta Caramelo.
- **Experiência Responsiva:** Funcionar adequadamente em computadores e dispositivos móveis.

### Funcionalidades Iniciais

- **Tela Principal de Solicitação:** Interface com mapa, origem, destino e categorias de viagem.
- **Origem e Destino:** Campos para indicar a localização atual e o local de chegada.
- **Locais Favoritos:** Atalhos para endereços como casa e trabalho.
- **Seleção de Categoria:** Opções Caramelo Leve, Caramelo Plus e Caramelo Grupo.
- **Estimativa da Viagem:** Exibição de preço, tempo de espera, conforto e capacidade.
- **Agendamento:** Alternância entre viagem imediata e horário programado.
- **Forma de Pagamento:** Resumo do cartão selecionado antes da confirmação.
- **Busca por Motorista:** Modal com progresso, previsão de embarque e opção de cancelamento.
- **Mapa Ilustrado:** Visualização da rota, do destino e de motoristas próximos.
- **Menu do Passageiro:** Acesso a viagens, pagamentos, segurança e indicações.
- **Pitch Comercial:** Apresentação interativa com sete capítulos sobre produto, marca e negócio.
- **Responsividade:** Experiências específicas para desktop e dispositivos móveis.

---

## 2. Especificação da Funcionalidade — SPEC-001

- **Título:** Solicitação inicial de viagem.
- **Componente principal:** `src/App.tsx`.
- **Estilos e tokens visuais:** `src/index.css`.

### Resumo da Especificação

A primeira especificação define a interface principal do passageiro. A tela deve apresentar a marca Caramelo, os campos de partida e destino, atalhos de localização, categorias de viagem, estimativas de preço, forma de pagamento e uma ação primária de confirmação.

Ao confirmar a viagem, o sistema deve abrir uma interface de busca por motorista com o destino informado, a categoria selecionada, o tempo estimado de embarque e o valor da corrida. O usuário deve conseguir cancelar a busca e retornar à tela principal.

### Requisitos Funcionais

- **FR-01:** Permitir visualizar e editar o destino da viagem.
- **FR-02:** Permitir selecionar uma das categorias de veículo disponíveis.
- **FR-03:** Atualizar a ação de confirmação conforme a categoria selecionada.
- **FR-04:** Permitir alternar entre viagem imediata e agendada.
- **FR-05:** Apresentar forma de pagamento antes da confirmação.
- **FR-06:** Abrir o estado de busca por motorista após a confirmação.
- **FR-07:** Permitir cancelar a busca e retornar à tela principal.
- **FR-08:** Permitir abrir e fechar o menu de navegação.
- **FR-09:** Permitir abrir e navegar pela apresentação comercial.
- **FR-10:** Adaptar o layout para dispositivos móveis e computadores.

---

## 3. Implementação da Primeira Experiência

- **Framework:** JetPackComposer;
- **Linguagem:** Java;
- **Build Tool:** Gradle / Maven2;
- **Estilização:** material3;
- **Módulo principal:** `src/App.tsx`;
- **Folha de estilos:** `src/index.css`.

### Componentes e Layout

- Estrutura principal responsiva com painel de solicitação e mapa ilustrado;
- Campos interativos de partida e destino;
- Lista de categorias com estado de seleção;
- Ilustrações vetoriais de veículos construídas em CSS;
- Ícones vetoriais em SVG;
- Mapa estilizado com ruas, áreas verdes, rota e marcadores;
- Modal de busca por motorista;
- Menu com perfil, viagens, pagamentos, segurança e indicação;
- Pitch deck comercial navegável por botões e teclado;
- Adaptação específica para telas com largura inferior a 780 pixels;
- Tokens de cor centralizados para preservar a paleta Caramelo.

### Paleta Visual

| Token | Cor | Uso principal |
| --- | --- | --- |
| Cacau | `#6A2D0E` | Marca, textos e elementos estruturais |
| Carinho | `#F6CAA6` | Superfícies acolhedoras e elementos secundários |
| Mel | `#FBB03B` | Destaques, veículos e seleção |
| Doçura | `#A62D0E` | Ações primárias e rota |

---

## 4. Escopo

### Incluído na Sprint

- Definição inicial do produto e de seus usuários;
- Criação da identidade visual baseada na paleta Caramelo;
- Implementação da experiência principal de solicitação;
- Categorias de corrida e estimativas simuladas;
- Estado visual de busca por motorista;
- Menu de navegação;
- Layout responsivo;
- Pitch deck comercial;
- Captura das evidências em desktop e mobile.

### Fora do Escopo desta Sprint

- Integração com mapas e rotas reais;
- Geolocalização por GPS;
- Cadastro e autenticação de usuários;
- Backend e banco de dados;
- Integração com motoristas reais;
- Processamento real de pagamentos;
- Notificações push;
- Histórico persistente de viagens;
- Publicação nas lojas Google Play e App Store;
- Projeto Android nativo ou configuração com Capacitor.

---

## 5. Critérios de Aceitação

- [x] **AC-01** — A aplicação possui um nome claramente definido.
- [x] **AC-02** — O problema tratado pela aplicação está documentado.
- [x] **AC-03** — Os usuários-alvo estão identificados.
- [x] **AC-04** — O objetivo inicial do produto está documentado.
- [x] **AC-05** — A primeira experiência possui origem e destino.
- [x] **AC-06** — A aplicação apresenta pelo menos três categorias de viagem.
- [x] **AC-07** — Cada categoria informa preço e previsão de embarque.
- [x] **AC-08** — O usuário pode selecionar uma categoria.
- [x] **AC-09** — Existe uma ação primária para confirmar a viagem.
- [x] **AC-10** — A confirmação abre o estado de busca por motorista.
- [x] **AC-11** — O usuário pode cancelar a busca.
- [x] **AC-12** — O menu principal pode ser aberto e fechado.
- [x] **AC-13** — A interface se adapta a desktop e mobile.
- [x] **AC-14** — A paleta Caramelo é utilizada de forma consistente.
- [x] **AC-15** — O projeto gera uma compilação de produção sem erros.
- [x] **AC-16** — As principais telas possuem evidências visuais.
- [x] **AC-17** — A apresentação comercial pode ser acessada pelo aplicativo.

---

## 6. Validação

1. **Compilação de Produção:** O projeto foi compilado com sucesso por meio do comando `pnpm build`.

2. **Verificação do Código:** A verificação `git diff --check` foi executada sem erros de espaços ou formatação inválida.

3. **Teste da Tela Principal:** Foram validados visualmente os campos de origem e destino, as três categorias de veículo, os preços e a ação de confirmação.

4. **Teste de Seleção:** A categoria Caramelo Leve foi selecionada e exibida com destaque visual, preço, capacidade e previsão de embarque.

5. **Teste de Busca:** A ação “Confirmar Leve” abriu corretamente o modal de busca por motorista com destino, preço e tempo estimado.

6. **Teste do Menu:** O botão de menu abriu corretamente as opções de perfil, viagens, pagamentos, segurança e indicação.

7. **Teste do Pitch Comercial:** O botão “Pitch” abriu a apresentação comercial com navegação entre os sete capítulos.

8. **Teste Responsivo:** As telas foram renderizadas e capturadas nas resoluções de 1440 × 900 e 390 × 844.

9. **Captura de Evidências:** Os arquivos foram armazenados na pasta `screenshots/` e também disponibilizados no arquivo `Caramelo-Screenshots.zip`.

---

## 7. Evidências

### Tela Principal — Desktop

![Tela principal da corrida em desktop](../screenshots/01-corrida-desktop.png)

---

## 8. Uso de Inteligência Artificial

### Ferramenta

Figma Make, com assistência de inteligência artificial da OpenAI.

### Finalidade

A ferramenta foi utilizada para auxiliar na definição da experiência, implementação da interface em React e TypeScript, criação da identidade visual baseada na paleta fornecida, elaboração da apresentação comercial e organização da documentação da Sprint.

### Conteúdo Gerado

A IA auxiliou nas seguintes atividades:

- Estruturação inicial do produto e dos fluxos;
- Implementação dos componentes React;
- Criação dos estilos responsivos;
- Construção do mapa ilustrado;
- Desenvolvimento dos estados de interação;
- Criação do pitch deck comercial;
- Geração da apresentação em PowerPoint;
- Captura e organização das evidências;
- Adaptação deste relatório de Sprint.

### Alterações Humanas

O integrante da equipe definiu a proposta de um aplicativo de mobilidade, forneceu a paleta Caramelo como referência visual, escolheu o formato de pitch deck comercial e orientou os formatos de entrega.

### Validação

O resultado foi validado por compilação de produção, verificação do código, execução em navegador Chromium e captura das principais telas em resoluções desktop e mobile.

| Item | Resposta da equipe |
| --- | --- |
| LLM/ferramenta utilizada | Figma Make com assistência de IA da OpenAI |
| Tarefa apoiada pela IA | Definição do produto, implementação React, design responsivo, apresentação e documentação |
| Principal sugestão recebida | Organizar a experiência em solicitação, seleção de categoria, pagamento e busca por motorista |
| Alterações feitas pela equipe | Definição do tema de mobilidade, escolha da paleta, formato da apresentação e revisão das entregas |
| Como o resultado foi validado | Build de produção, testes de interação e capturas em desktop e mobile |

---

## 9. Entregáveis

- `src/App.tsx` — Componentes, conteúdo e interações do aplicativo;
- `src/index.css` — Identidade visual, mapa e responsividade;
- `docs/SPRINT-01.md` — Relatório preenchido da Sprint 01;
- `Caramelo-Pitch-Comercial.pptx` — Apresentação comercial editável;
- `screenshots/` — Evidências visuais do aplicativo;
- `Caramelo-Screenshots.zip` — Pacote compactado das evidências;
- `package.json` — Dependências e comandos do projeto.
