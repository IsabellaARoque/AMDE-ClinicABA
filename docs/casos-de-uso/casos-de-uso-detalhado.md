# Especificação de Casos de Uso — Sistema AMDE

> Este documento apresenta a especificação detalhada dos casos de uso do sistema AMDE, descrevendo os atores envolvidos, objetivos, requisitos relacionados, condições, fluxos principais, fluxos alternativos e regras aplicáveis. Os casos de uso representam as interações entre os usuários e o sistema, considerando as funcionalidades disponibilizadas nas plataformas web e mobile.

---

## Atores do Sistema

### Administrador

O Administrador é responsável pelas funções de gerenciamento dos usuários e dos assistidos no sistema. Pode cadastrar profissionais e assistidos, visualizar e editar seus próprios dados, além de realizar a autenticação e acessar as funcionalidades administrativas disponíveis no sistema.

### Profissional

O Profissional é responsável pelo acompanhamento dos assistidos e pelo gerenciamento de seus planos terapêuticos. Pode visualizar assistidos e seus perfis, criar, alterar, visualizar, desativar e reativar planos terapêuticos, além de cadastrar e alterar treinos.

Também é responsável pela realização e registro das sessões, podendo executar os treinos, registrar seus resultados e scores, consultar o histórico e os detalhes das sessões, realizar correções dentro das condições permitidas e exportar os registros das sessões.

Além dessas funções, o Profissional herda todas as funções do Administrador, podendo também realizar as operações administrativas atribuídas a esse ator.

---

# UC01 — Cadastrar Profissional

- **ID e nome:** UC01 — Cadastrar Profissional
- **Objetivo:** Permitir que um profissional autorizado realize o cadastro de um profissional para utilização do sistema.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF01.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita o cadastro de um novo profissional.
- **Pré-condições:**
  - O profissional não possui uma conta cadastrada.
  - O sistema está disponível.
- **Pós-condições:**
  - Uma nova conta de profissional é cadastrada no sistema.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a tela de cadastro. | Apresenta o formulário de cadastro. |
| 2 | Administrador | Informa os dados do profissional. | Recebe as informações fornecidas. |
| 3 | Administrador | Solicita o cadastro. | Valida as informações fornecidas. |
| 4 | — | — | Verifica se o profissional já possui cadastro. |
| 5 | — | — | Registra o profissional. |
| 6 | — | — | Informa que o cadastro foi realizado com sucesso. |

## Fluxos alternativos e exceções

**A1 — Dados inválidos (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a tela de cadastro. | Apresenta o formulário de cadastro. |
| 2 | Administrador | Informa os dados do profissional. | Recebe as informações fornecidas. |
| 3 | Administrador | Solicita o cadastro. | Identifica dados inválidos. |
| 4 | — | — | Informa quais dados precisam ser corrigidos. |
| 5 | Administrador | Corrige os dados. | Recebe as informações corrigidas. |
| 6 | — | — | Retorna ao passo 3 do fluxo principal. |

**A2 — Profissional já cadastrado (a partir do passo 4)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a tela de cadastro. | Apresenta o formulário de cadastro. |
| 2 | Administrador | Informa os dados do profissional. | Recebe as informações fornecidas. |
| 3 | Administrador | Solicita o cadastro. | Verifica os dados informados. |
| 4 | — | — | Identifica que já existe uma conta com os dados informados. |
| 5 | — | — | Informa que o cadastro já existe. |
| 6 | — | — | Encerra o fluxo sem realizar um novo cadastro. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF01.
- **Dados relevantes:** Dados cadastrais e informações de identificação do profissional.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O profissional deve ser cadastrado quando as informações forem válidas e não existir cadastro prévio.

---

# UC02 — Autenticar Profissional

- **ID e nome:** UC02 — Autenticar Profissional
- **Objetivo:** Permitir que profissionais cadastrados acessem o sistema.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF02.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita acesso ao sistema.
- **Pré-condições:**
  - O profissional possui cadastro.
  - O sistema está disponível.
- **Pós-condições:**
  - O profissional é autenticado.
  - O profissional tem acesso às funcionalidades permitidas.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a tela de login. | Solicita as credenciais de acesso. |
| 2 | Administrador | Informa suas credenciais corretas. | Recebe as credenciais fornecidas. |
| 3 | Administrador | Solicita o acesso. | Valida as informações. |
| 4 | — | — | Autentica o administrador. |
| 5 | — | — | Direciona o administrador para a página inicial. |

## Fluxos alternativos e exceções

**A1 — Credenciais inválidas (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a tela de login. | Solicita as credenciais. |
| 2 | Administrador | Informa suas credenciais incorretas. | Recebe as credenciais fornecidas. |
| 3 | Administrador | Solicita o acesso. | Identifica que as credenciais estão incorretas. |
| 4 | — | — | Informa que não foi possível realizar a autenticação. |
| 5 | Administrador | Pode tentar novamente. | Permite uma nova tentativa de autenticação. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF02.
- **Dados relevantes:** Credenciais de acesso do profissional.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve autenticar profissionais cadastrados mediante o fornecimento de credenciais corretas.

---

# UC03 — Visualizar Perfil de Profissional

- **ID e nome:** UC03 — Visualizar Perfil de Profissional
- **Objetivo:** Permitir que o usuário visualize suas informações cadastradas.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF03.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita a visualização do próprio perfil.
- **Pré-condições:**
  - O profissional está autenticado.
- **Pós-condições:**
  - As informações do profissional são apresentadas.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa seu perfil. | Identifica o administrador autenticado. |
| 2 | — | — | Busca os dados cadastrados do administrador. |
| 3 | — | — | Apresenta as informações do administrador. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF03.
- **Dados relevantes:** Informações cadastrais do profissional.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve apresentar as informações cadastradas do profissional autenticado.

---

# UC04 — Editar Profissional

- **ID e nome:** UC04 — Editar Profissional
- **Objetivo:** Permitir que o profissional altere seus dados cadastrais.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF04.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita a edição de seus dados cadastrais.
- **Pré-condições:**
  - O profissional está autenticado.
  - O profissional possui cadastro.
- **Pós-condições:**
  - Os dados alterados são armazenados no sistema.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa seu perfil. | Apresenta seus dados cadastrais. |
| 2 | Administrador | Seleciona a opção de edição. | Disponibiliza os campos para alteração. |
| 3 | Administrador | Altera os dados desejados. | Recebe as informações modificadas. |
| 4 | Administrador | Confirma as alterações. | Valida os dados. |
| 5 | — | — | Salva as alterações. |
| 6 | — | — | Informa que os dados foram atualizados. |

## Fluxos alternativos e exceções

**A1 — Dados inválidos (a partir do passo 4)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa seu perfil. | Apresenta seus dados. |
| 2 | Administrador | Seleciona a opção de edição. | Disponibiliza os campos para alteração. |
| 3 | Administrador | Altera os dados desejados. | Recebe as informações modificadas. |
| 4 | Administrador | Confirma as alterações. | Identifica informações inválidas. |
| 5 | — | — | Informa o problema identificado. |
| 6 | Administrador | Corrige os dados. | Recebe as informações corrigidas. |
| 7 | — | — | Retorna ao passo 4 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF04.
- **Dados relevantes:** Dados cadastrais do profissional.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve atualizar os dados cadastrais após a confirmação de informações válidas.

---

# UC05 — Cadastrar Assistido

- **ID e nome:** UC05 — Cadastrar Assistido
- **Objetivo:** Permitir o cadastro de um assistido no sistema.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF05.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita o cadastro de um novo assistido.
- **Pré-condições:**
  - O administrador está autenticado.
  - O assistido ainda não possui cadastro.
- **Pós-condições:**
  - O assistido é cadastrado no sistema.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a opção de cadastrar assistido. | Apresenta o formulário de cadastro. |
| 2 | Administrador | Informa os dados do assistido. | Recebe as informações fornecidas. |
| 3 | Administrador | Confirma o cadastro. | Valida os dados informados. |
| 4 | — | — | Verifica se já existe cadastro para o assistido. |
| 5 | — | — | Registra o assistido. |
| 6 | — | — | Informa que o cadastro foi realizado. |

**Dados do assistido:** CPF, nome, data de nascimento, sala, agente responsável da sala, convênio, frequência/período, informações do responsável e observações gerais.

## Fluxos alternativos e exceções

**A1 — Assistido já cadastrado (a partir do passo 4)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a opção de cadastrar assistido. | Apresenta o formulário. |
| 2 | Administrador | Informa os dados do assistido. | Recebe as informações fornecidas. |
| 3 | Administrador | Confirma o cadastro. | Verifica as informações. |
| 4 | — | — | Identifica que o assistido já possui cadastro. |
| 5 | — | — | Informa que não é possível realizar um novo cadastro. |
| 6 | — | — | Mantém o cadastro existente. |

**A2 — Dados inválidos (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a opção de cadastrar assistido. | Apresenta o formulário. |
| 2 | Administrador | Informa os dados do assistido. | Recebe as informações fornecidas. |
| 3 | Administrador | Confirma o cadastro. | Identifica dados inválidos. |
| 4 | — | — | Informa os campos que precisam ser corrigidos. |
| 5 | Administrador | Corrige as informações. | Recebe os dados corrigidos. |
| 6 | — | — | Retorna ao passo 3 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF05.
- **Dados relevantes:** CPF, nome, data de nascimento, sala, agente responsável da sala, convênio, frequência/período, informações do responsável e observações gerais.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O assistido deve ser cadastrado quando os dados forem válidos e não existir cadastro prévio.

---

# UC06 — Editar Assistido

- **ID e nome:** UC06 — Editar Assistido
- **Objetivo:** Permitir a alteração dos dados de um assistido.
- **Ator(es):** Administrador.
- **Requisito(s) relacionado(s):** RF06.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O administrador solicita a edição dos dados de um assistido.
- **Pré-condições:**
  - O administrador está autenticado.
  - O assistido está cadastrado.
- **Pós-condições:**
  - Os dados do assistido são atualizados.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a lista de assistidos. | Apresenta a lista de assistidos cadastrados. |
| 2 | Administrador | Seleciona um assistido. | Apresenta o perfil do assistido. |
| 3 | Administrador | Seleciona a opção de edição. | Apresenta os dados editáveis. |
| 4 | Administrador | Altera os dados. | Recebe as informações modificadas. |
| 5 | Administrador | Confirma as alterações. | Valida os dados. |
| 6 | — | — | Salva as alterações. |
| 7 | — | — | Apresenta os dados atualizados. |

## Fluxos alternativos e exceções

**A1 — Dados inválidos (a partir do passo 5)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Acessa a lista de assistidos. | Apresenta os assistidos cadastrados. |
| 2 | Administrador | Seleciona um assistido. | Apresenta o perfil do assistido. |
| 3 | Administrador | Seleciona a opção de edição. | Apresenta os dados editáveis. |
| 4 | Administrador | Altera os dados. | Recebe as informações modificadas. |
| 5 | Administrador | Confirma as alterações. | Identifica dados inválidos. |
| 6 | — | — | Informa o problema identificado. |
| 7 | Administrador | Corrige os dados. | Recebe as informações corrigidas. |
| 8 | — | — | Retorna ao passo 5 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF06.
- **Dados relevantes:** Informações cadastrais do assistido.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve atualizar os dados do assistido após a confirmação de informações válidas.

---

# UC07 — Visualizar Assistidos

- **ID e nome:** UC07 — Visualizar Assistidos
- **Objetivo:** Permitir que o profissional visualize os assistidos disponíveis para atendimento.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF07.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a visualização da lista de assistidos.
- **Pré-condições:**
  - O profissional está autenticado.
- **Pós-condições:**
  - O sistema apresenta os assistidos disponíveis.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa a opção de lista de assistidos. | Consulta os assistidos ativos. |
| 2 | — | — | Apresenta a lista de assistidos. |
| 3 | Profissional | Pode selecionar um assistido para visualizar seu perfil. | Disponibiliza o perfil do assistido selecionado. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF07.
- **Dados relevantes:** Informações dos assistidos ativos.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve apresentar a lista de assistidos disponíveis para consulta pelo profissional autenticado.

---

# UC08 — Visualizar Perfil de Assistido

- **ID e nome:** UC08 — Visualizar Perfil de Assistido
- **Objetivo:** Permitir que o profissional consulte as informações completas relacionadas ao assistido.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF08.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional seleciona um assistido para consultar seu perfil.
- **Pré-condições:**
  - O profissional está autenticado.
  - O assistido está cadastrado.
- **Pós-condições:**
  - As informações do assistido são apresentadas.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa a lista de assistidos. | Apresenta os assistidos disponíveis. |
| 2 | Profissional | Seleciona um assistido. | Apresenta o perfil do assistido. |
| 3 | — | — | Apresenta as informações gerais do assistido. |
| 4 | — | — | Apresenta os scores. |
| 5 | — | — | Apresenta os planos terapêuticos ativos. |
| 6 | — | — | Apresenta os planos desativados. |
| 7 | — | — | Disponibiliza o histórico de sessões. |
| 8 | Profissional | No Mobile, pode iniciar uma sessão de treino. | Disponibiliza a funcionalidade de início de sessão. |
| 9 | Profissional | No Site, pode criar outro plano terapêutico. | Disponibiliza a funcionalidade de criação de plano. |
| 10 | Profissional | No Site, pode editar informações de cadastro do assistido. | Disponibiliza a funcionalidade de edição do cadastro. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF08.
- **Dados relevantes:** Informações gerais do assistido, scores, planos terapêuticos ativos e desativados e histórico de sessões.
- **Variações web/mobile:**
  - **Site:** Permite criar planos terapêuticos e editar informações cadastrais do assistido.
  - **Mobile:** Permite iniciar uma sessão de treino.
- **Critério de aceite:** O sistema deve apresentar as informações do assistido e disponibilizar as funcionalidades correspondentes a cada plataforma.

---

# UC09 — Criar Plano Terapêutico

- **ID e nome:** UC09 — Criar Plano Terapêutico
- **Objetivo:** Permitir que o profissional crie um plano terapêutico para um assistido.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF09.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a criação de um plano terapêutico.
- **Pré-condições:**
  - O profissional está autenticado.
  - O assistido está cadastrado.
  - O profissional acessou o perfil do assistido.
- **Pós-condições:**
  - Um novo plano terapêutico é associado ao assistido.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta as informações do assistido. |
| 2 | Profissional | Seleciona a opção de criar plano terapêutico. | Apresenta o formulário de criação. |
| 3 | Profissional | Informa o nome do plano. | Recebe o nome informado. |
| 4 | — | — | Identifica o profissional responsável. |
| 5 | Profissional | Informa o objetivo do plano. | Recebe o objetivo informado. |
| 6 | — | — | Registra automaticamente a data de criação. |
| 7 | Profissional | Adiciona uma observação, se necessário. | Recebe a observação informada. |
| 8 | Profissional | Confirma a criação. | Valida os dados. |
| 9 | — | — | Registra o plano terapêutico. |
| 10 | — | — | Apresenta o plano criado. |

**Dados do plano:** Nome, profissional responsável, objetivo, data de criação automática e observação.

## Fluxos alternativos e exceções

**A1 — Informações inválidas (a partir do passo 8)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil. |
| 2 | Profissional | Seleciona a opção de criar plano terapêutico. | Apresenta o formulário. |
| 3 | Profissional | Informa o nome do plano. | Recebe o nome informado. |
| 4 | — | — | Identifica o profissional responsável. |
| 5 | Profissional | Informa o objetivo. | Recebe o objetivo informado. |
| 6 | — | — | Registra automaticamente a data de criação. |
| 7 | Profissional | Adiciona uma observação, se necessário. | Recebe a observação. |
| 8 | Profissional | Confirma a criação. | Identifica dados inválidos. |
| 9 | — | — | Informa quais dados precisam ser corrigidos. |
| 10 | Profissional | Corrige os dados. | Recebe as informações corrigidas. |
| 11 | — | — | Retorna ao passo 8 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF09.
- **Dados relevantes:** Nome, profissional responsável, objetivo, data de criação e observação.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve registrar o plano terapêutico e associá-lo ao assistido após a confirmação dos dados.

---

# UC10 — Alterar Plano Terapêutico

- **ID e nome:** UC10 — Alterar Plano Terapêutico
- **Objetivo:** Permitir que o profissional responsável altere um plano terapêutico.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF10.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a alteração de um plano terapêutico.
- **Pré-condições:**
  - O profissional está autenticado.
  - O plano está cadastrado.
  - O profissional é responsável pelo plano.
- **Pós-condições:**
  - O plano terapêutico é atualizado.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil do assistido. |
| 2 | Profissional | Acessa o plano terapêutico. | Apresenta as informações do plano. |
| 3 | — | — | Verifica o profissional responsável. |
| 4 | — | — | Permite a edição do plano. |
| 5 | Profissional | Altera as informações desejadas. | Recebe os dados modificados. |
| 6 | Profissional | Confirma as alterações. | Valida os dados. |
| 7 | — | — | Salva as alterações. |

## Fluxos alternativos e exceções

**A1 — Profissional não responsável (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil do assistido. |
| 2 | Profissional | Acessa o plano terapêutico. | Apresenta as informações do plano. |
| 3 | — | — | Verifica o profissional responsável. |
| 4 | — | — | Identifica que o profissional não é responsável pelo plano. |
| 5 | — | — | Impede a alteração. |
| 6 | — | — | Mantém o plano inalterado. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF10.
- **Dados relevantes:** Informações cadastrais e terapêuticas do plano.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** Somente o profissional responsável pelo plano pode realizar sua alteração.

---

# UC11 — Visualizar Plano Terapêutico

- **ID e nome:** UC11 — Visualizar Plano Terapêutico
- **Objetivo:** Permitir que o profissional consulte um plano terapêutico e seus treinos.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF11.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a visualização de um plano terapêutico.
- **Pré-condições:**
  - O profissional está autenticado.
  - O assistido possui plano terapêutico.
- **Pós-condições:**
  - O plano e seus treinos são apresentados.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta as informações do assistido. |
| 2 | Profissional | Seleciona um plano terapêutico. | Apresenta os dados do plano. |
| 3 | — | — | Apresenta os treinos associados ao plano. |
| 4 | — | — | Disponibiliza a opção de cadastrar treino. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF11.
- **Dados relevantes:** Informações do plano terapêutico e treinos associados.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve apresentar as informações do plano terapêutico e seus respectivos treinos.

---

# UC12 — Desativar Plano Terapêutico

- **ID e nome:** UC12 — Desativar Plano Terapêutico
- **Objetivo:** Permitir que o profissional responsável desative um plano que não seja mais utilizado.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF12.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a desativação de um plano terapêutico.
- **Pré-condições:**
  - O profissional está autenticado.
  - O plano está ativo.
  - O profissional é responsável pelo plano.
- **Pós-condições:**
  - O plano é marcado como desativado.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil do assistido. |
| 2 | Profissional | Acessa o plano terapêutico. | Apresenta os dados do plano. |
| 3 | Profissional | Seleciona a opção de desativar. | Verifica se o profissional é responsável pelo plano. |
| 4 | — | — | Solicita confirmação da desativação. |
| 5 | Profissional | Confirma a operação. | Recebe a confirmação. |
| 6 | — | — | Desativa o plano. |
| 7 | — | — | Informa que o plano foi desativado. |

## Fluxos alternativos e exceções

**A1 — Profissional não responsável (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil. |
| 2 | Profissional | Acessa o plano terapêutico. | Apresenta os dados do plano. |
| 3 | Profissional | Seleciona a opção de desativar. | Verifica o profissional responsável. |
| 4 | — | — | Identifica que o profissional não é responsável. |
| 5 | — | — | Impede a desativação. |
| 6 | — | — | Mantém o plano ativo. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF12.
- **Dados relevantes:** Identificação do plano, situação atual e profissional responsável.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O plano deve ser desativado mediante confirmação do profissional responsável.

---

# UC13 — Reativar Plano Terapêutico

- **ID e nome:** UC13 — Reativar Plano Terapêutico
- **Objetivo:** Permitir que o profissional responsável reative um plano terapêutico desativado.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF13.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a reativação de um plano terapêutico.
- **Pré-condições:**
  - O profissional está autenticado.
  - O plano está desativado.
  - O profissional é responsável pelo plano.
- **Pós-condições:**
  - O plano volta a ficar ativo.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil do assistido. |
| 2 | Profissional | Acessa a seção de planos desativados. | Apresenta os planos desativados. |
| 3 | Profissional | Seleciona o plano desejado. | Apresenta as informações do plano. |
| 4 | Profissional | Seleciona a opção de reativar. | Verifica se o profissional é responsável. |
| 5 | — | — | Solicita confirmação da operação. |
| 6 | Profissional | Confirma a operação. | Recebe a confirmação. |
| 7 | — | — | Reativa o plano. |
| 8 | — | — | Informa que o plano foi reativado. |

## Fluxos alternativos e exceções

**A1 — Profissional não responsável (a partir do passo 4)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta o perfil. |
| 2 | Profissional | Acessa a seção de planos desativados. | Apresenta os planos desativados. |
| 3 | Profissional | Seleciona o plano desejado. | Apresenta as informações do plano. |
| 4 | Profissional | Seleciona a opção de reativar. | Verifica o profissional responsável. |
| 5 | — | — | Identifica que o profissional não é responsável. |
| 6 | — | — | Impede a reativação. |
| 7 | — | — | Mantém o plano desativado. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF13.
- **Dados relevantes:** Identificação do plano, situação atual e profissional responsável.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O plano deve voltar à situação ativa após a confirmação do profissional responsável.

---

# UC14 — Cadastrar Treino

- **ID e nome:** UC14 — Cadastrar Treino
- **Objetivo:** Permitir que o profissional cadastre um treino dentro de um plano terapêutico.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF14.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita o cadastro de um novo treino.
- **Pré-condições:**
  - O profissional está autenticado.
  - Existe um plano terapêutico.
  - O profissional possui acesso ao plano.
- **Pós-condições:**
  - O treino é associado ao plano terapêutico.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa um plano terapêutico. | Apresenta as informações do plano. |
| 2 | Profissional | Seleciona a opção de cadastrar treino. | Apresenta o formulário de cadastro. |
| 3 | Profissional | Informa o nome do treino. | Recebe o nome informado. |
| 4 | Profissional | Informa a categoria do treino. | Recebe a categoria selecionada. |
| 5 | Profissional | Seleciona o tipo de medição. | Recebe o tipo de medição selecionado. |
| 6 | Profissional | Confirma o cadastro. | Valida as informações. |
| 7 | — | — | Associa o treino ao plano terapêutico. |
| 8 | — | — | Apresenta o treino cadastrado. |

**Tipos de medição previstos:** Frequência ou duração.

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF14.
- **Dados relevantes:** Nome, categoria e tipo de medição do treino.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O treino deve ser cadastrado e associado ao plano terapêutico após a confirmação das informações.

---

# UC15 — Alterar Treino

- **ID e nome:** UC15 — Alterar Treino
- **Objetivo:** Permitir que o profissional altere um treino cadastrado em seu plano terapêutico.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF15.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a alteração de um treino cadastrado.
- **Pré-condições:**
  - O profissional está autenticado.
  - O treino está cadastrado.
  - O treino pertence a um plano ao qual o profissional possui acesso.
- **Pós-condições:**
  - As informações do treino são atualizadas.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o plano terapêutico. | Apresenta os treinos associados. |
| 2 | Profissional | Seleciona um treino. | Apresenta as informações do treino. |
| 3 | Profissional | Seleciona a opção de editar. | Disponibiliza os campos para alteração. |
| 4 | Profissional | Altera as informações desejadas. | Recebe os dados modificados. |
| 5 | Profissional | Confirma as alterações. | Valida os dados. |
| 6 | — | — | Salva as alterações. |

## Fluxos alternativos e exceções

**A1 — Informações inválidas (a partir do passo 5)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o plano terapêutico. | Apresenta os treinos. |
| 2 | Profissional | Seleciona um treino. | Apresenta suas informações. |
| 3 | Profissional | Seleciona a opção de editar. | Disponibiliza os campos para alteração. |
| 4 | Profissional | Altera as informações. | Recebe os dados modificados. |
| 5 | Profissional | Confirma as alterações. | Identifica dados inválidos. |
| 6 | — | — | Informa quais dados precisam ser corrigidos. |
| 7 | Profissional | Corrige os dados. | Recebe as informações corrigidas. |
| 8 | — | — | Retorna ao passo 5 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF15.
- **Dados relevantes:** Nome, categoria, objetivo, tipo de medição e atividade do treino.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve atualizar as informações do treino após a confirmação de dados válidos.

---

# UC16 — Configuração e Execução de Sessão

- **ID e nome:** UC16 — Configuração e Execução de Sessão
- **Objetivo:** Permitir que o profissional inicie, configure e execute uma sessão de atendimento, selecionando o plano e os treinos que serão realizados, registrando os resultados de cada treino e finalizando a sessão.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF16, RF17, RF18, RF19 e RF20.
- **Interface/plataforma:** Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita o início de uma sessão de atendimento.
- **Pré-condições:**
  - O profissional está autenticado.
  - O assistido está cadastrado.
  - O assistido possui pelo menos um plano de intervenção cadastrado.
- **Pós-condições:**
  - A sessão é encerrada e armazenada no sistema.
  - O assistido, o profissional, a data e os horários de início e encerramento são registrados.
  - O objetivo, o plano e os treinos selecionados são registrados.
  - O score de cada treino realizado é armazenado.
  - O score da sessão é calculado pelo sistema a partir da soma dos scores dos treinos realizados.

## Fluxo principal — Configuração e andamento da sessão

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta as informações do assistido. |
| 2 | Profissional | Seleciona a opção de iniciar sessão. | Cria uma nova sessão. |
| 3 | — | — | Identifica automaticamente o assistido. |
| 4 | — | — | Identifica automaticamente o profissional. |
| 5 | — | — | Registra automaticamente a data e o horário de início. |
| 6 | — | — | Apresenta a tela de configuração da sessão. |
| 7 | Profissional | Informa o objetivo da sessão. | Recebe o objetivo informado. |
| 8 | Profissional | Seleciona o plano de intervenção. | Apresenta os treinos disponíveis no plano selecionado. |
| 9 | Profissional | Seleciona os treinos que serão realizados. | Registra os treinos selecionados. |
| 10 | Profissional | Confirma a configuração. | Registra as informações da sessão. |
| 11 | — | — | Apresenta os treinos selecionados. |
| 12 | Profissional | Seleciona um treino. | Identifica o tipo de medição definido para o treino. |
| 13 | — | — | Direciona o profissional para o fluxo de execução correspondente. |
| 14 | Profissional | Conclui a execução do treino. | Retorna ao fluxo principal. |
| 15 | Profissional | Pode selecionar outro treino e repetir os passos 12 a 14. | Apresenta os treinos selecionados disponíveis para execução. |
| 16 | Profissional | Pode adicionar observações à sessão. | Recebe as observações informadas. |
| 17 | Profissional | Seleciona a opção de encerrar a sessão após finalizar os treinos desejados. | Registra automaticamente o horário de encerramento. |
| 18 | — | — | Soma os scores dos treinos realizados. |
| 19 | — | — | Registra o resultado como score da sessão. |
| 20 | — | — | Grava as informações da sessão. |
| 21 | — | — | Disponibiliza os dados da sessão para consulta. |
| 22 | — | — | Informa que a sessão foi encerrada. |

## Fluxos alternativos e exceções

**A1 — Execução de treino de frequência/repetição (a partir do passo 13)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | — | — | Apresenta a tela de execução do treino de frequência/repetição. |
| 2 | Profissional | Realiza o treino e registra cada ocorrência utilizando os botões disponíveis. | Disponibiliza as opções de registro. |
| 3 | Profissional | Seleciona uma das opções: Executado sem ajuda, Executado com ajuda ou Não executado. | Registra cada clique realizado. |
| 4 | Profissional | Continua registrando as ocorrências conforme a execução do treino. | Armazena os registros realizados. |
| 5 | Profissional | Seleciona o botão "Encerrar", localizado no canto da tela. | Encerra o treino. |
| 6 | — | — | Apresenta um campo para adicionar o score do treino. |
| 7 | Profissional | Digita o score. | Recebe o valor informado. |
| 8 | — | — | Armazena o score do treino. |
| 9 | — | — | Retorna ao passo 15 do fluxo principal. |

**A2 — Execução de treino de duração (a partir do passo 13)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | — | — | Apresenta a tela de execução do treino de duração. |
| 2 | Profissional | Inicia a execução do treino. | Inicia o cronômetro. |
| 3 | Profissional | Realiza o treino. | Mantém a medição da duração. |
| 4 | Profissional | Encerra a medição. | Registra a duração obtida. |
| 5 | Profissional | Seleciona a opção de encerrar o treino. | Encerra o treino. |
| 6 | — | — | Apresenta um campo para adicionar o score do treino. |
| 7 | Profissional | Digita o score. | Recebe o valor informado. |
| 8 | — | — | Armazena o score do treino. |
| 9 | — | — | Retorna ao passo 15 do fluxo principal. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF16, RF17, RF18, RF19 e RF20.
- **Dados relevantes:** Assistido, profissional, objetivo, plano de intervenção, treinos selecionados, data, horários de início e encerramento, observações, frequência de execução, duração e scores.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Mobile.
- **Critério de aceite:** O sistema deve permitir a configuração e execução dos treinos, armazenar seus resultados e calcular o score da sessão pela soma dos scores dos treinos realizados.

---

# UC17 — Visualizar Histórico de Sessões

- **ID e nome:** UC17 — Visualizar Histórico de Sessões
- **Objetivo:** Permitir que o profissional consulte as sessões realizadas com um assistido.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF21.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a visualização do histórico de sessões de um assistido.
- **Pré-condições:**
  - O profissional está autenticado.
  - O assistido está cadastrado.
- **Pós-condições:**
  - O histórico de sessões é apresentado.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o perfil do assistido. | Apresenta as informações do assistido. |
| 2 | Profissional | Seleciona a opção de histórico de sessões. | Consulta as sessões realizadas. |
| 3 | — | — | Apresenta a lista de sessões. |
| 4 | Profissional | Seleciona uma sessão para visualizar seus detalhes. | Disponibiliza os detalhes da sessão selecionada. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF21.
- **Dados relevantes:** Registros das sessões realizadas com o assistido.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve apresentar o histórico de sessões do assistido e permitir a seleção de uma sessão para consulta dos detalhes.

---

# UC18 — Visualizar Sessão

- **ID e nome:** UC18 — Visualizar Sessão
- **Objetivo:** Permitir que o profissional consulte os detalhes de uma sessão realizada.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF22.
- **Interface/plataforma:** Site e Mobile.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional seleciona uma sessão no histórico para consultar seus detalhes.
- **Pré-condições:**
  - O profissional está autenticado.
  - Existe uma sessão registrada.
- **Pós-condições:**
  - Os detalhes da sessão são apresentados.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o histórico de sessões. | Apresenta a lista de sessões. |
| 2 | Profissional | Seleciona uma sessão. | Apresenta os detalhes da sessão. |
| 3 | — | — | Apresenta o profissional responsável. |
| 4 | — | — | Apresenta o assistido relacionado. |
| 5 | — | — | Apresenta os treinos realizados. |
| 6 | — | — | Apresenta os scores dos treinos. |
| 7 | — | — | Apresenta o score da sessão. |
| 8 | — | — | Apresenta a data da realização. |
| 9 | — | — | Verifica se a sessão pode ser editada. |
| 10 | — | — | Caso esteja dentro do período permitido, disponibiliza a opção de edição. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF22.
- **Dados relevantes:** Profissional responsável, assistido, treinos realizados, scores dos treinos, score da sessão e data da realização.
- **Variações web/mobile:** Disponível no Site e no Mobile.
- **Critério de aceite:** O sistema deve apresentar os detalhes da sessão, sendo o score da sessão correspondente à somatória dos scores dos treinos.

---

# UC19 — Editar Sessão

- **ID e nome:** UC19 — Editar Sessão
- **Objetivo:** Permitir que o profissional corrija ou altere informações registradas em uma sessão própria.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF23.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a edição de uma sessão registrada.
- **Pré-condições:**
  - O profissional está autenticado.
  - A sessão pertence ao profissional.
  - Não se passaram mais de 24 horas desde o encerramento da sessão.
- **Pós-condições:**
  - Os dados da sessão são atualizados.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o histórico de sessões. | Apresenta as sessões registradas. |
| 2 | Profissional | Seleciona uma sessão própria. | Apresenta os detalhes da sessão. |
| 3 | — | — | Verifica o profissional responsável. |
| 4 | — | — | Verifica o tempo decorrido desde o encerramento. |
| 5 | — | — | Identifica que a edição ainda é permitida. |
| 6 | — | — | Disponibiliza a opção de edição. |
| 7 | Profissional | Altera os dados desejados. | Recebe as informações modificadas. |
| 8 | Profissional | Confirma as alterações. | Valida os dados. |
| 9 | — | — | Salva as alterações. |
| 10 | — | — | Atualiza os dados da sessão. |

## Fluxos alternativos e exceções

**A1 — Sessão de outro profissional (a partir do passo 3)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona uma sessão no histórico. | Apresenta os detalhes da sessão. |
| 2 | — | — | Verifica o profissional responsável. |
| 3 | — | — | Identifica que a sessão pertence a outro profissional. |
| 4 | — | — | Bloqueia a edição. |
| 5 | — | — | Mantém os dados inalterados. |

**A2 — Prazo de 24 horas expirado (a partir do passo 4)**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona uma sessão no histórico. | Apresenta os detalhes da sessão. |
| 2 | — | — | Verifica o tempo decorrido desde o encerramento. |
| 3 | — | — | Identifica que passaram mais de 24 horas desde o encerramento. |
| 4 | — | — | Bloqueia a edição. |
| 5 | — | — | Mantém os dados inalterados. |

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF23. As restrições de edição também são relacionadas ao RF24 e ao RNF05, conforme especificado nos requisitos fornecidos.
- **Dados relevantes:** Identificação da sessão, profissional responsável, horário de encerramento e informações registradas na sessão.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve permitir a edição somente de sessões pertencentes ao profissional autenticado e dentro do período de até 24 horas após o encerramento.

---

# UC20 — Exportar Sessão

- **ID e nome:** UC20 — Exportar Sessão
- **Objetivo:** Permitir que o profissional exporte os registros de uma sessão em formato PDF.
- **Ator(es):** Profissional.
- **Requisito(s) relacionado(s):** RF24.
- **Interface/plataforma:** Site.
- **Versão e situação:** Não informado.

## Condições

- **Gatilho:** O profissional solicita a exportação dos registros de uma sessão.
- **Pré-condições:**
  - O profissional está autenticado.
  - Existe uma sessão registrada.
  - O profissional possui acesso à sessão.
- **Pós-condições:**
  - Um arquivo PDF contendo os registros da sessão é gerado.

## Fluxo principal

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Acessa o histórico de sessões. | Apresenta a lista de sessões. |
| 2 | Profissional | Seleciona uma sessão. | Apresenta os detalhes da sessão. |
| 3 | Profissional | Seleciona a opção de exportar. | Organiza os dados da sessão. |
| 4 | — | — | Gera o arquivo em formato PDF. |
| 5 | — | — | Disponibiliza o arquivo para o profissional. |

## Fluxos alternativos e exceções

Nenhum fluxo alternativo documentado nesta versão.

## Regras, dados e variações de plataforma

- **Regras relacionadas:** RF24.
- **Dados relevantes:** Registros e informações da sessão selecionada.
- **Variações web/mobile:** Funcionalidade disponível exclusivamente no Site.
- **Critério de aceite:** O sistema deve gerar e disponibilizar um arquivo PDF contendo os registros da sessão selecionada.

---