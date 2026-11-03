# Especificação de Casos de Uso — ClinicABA (sugestão)

> **Versão de trabalho, não aprovada.** Esta proposta corrige a correspondência RF↔UC e padroniza atores, condições, fluxos principal/alternativo e critérios de aceite a partir do levantamento disponível. Preserva os comportamentos descritos pela equipe; decisões ausentes aparecem como `[a confirmar]`. Não altera `casos-de-uso-detalhado.md`.

- **Projeto:** Sistema AMDE — ClinicABA
- **Versão:** sugestão 1.0
- **Data:** 03/11/2026
- **Escopo:** requisitos RF01–RF24 propostos. RF25/UC21 permanece opcional e depende de decisão de escopo.
- **Prioridades:** a definir pela equipe e AMDE; nenhuma prioridade foi presumida.
- **Atores:** somente `Administrador` e `Profissional`, conforme o diagrama de casos de uso. “Autenticado” indica uma pré-condição do fluxo, não um terceiro ator. O diagrama também desenha a generalização `Profissional --> Administrador`; como a atribuição de permissões dos RFs não está totalmente uniforme, esta especificação mantém os atores associados diretamente a cada caso e deixa a abrangência da herança para confirmação da equipe/AMDE.

## Mapa de rastreabilidade

| Caso de uso | Requisito(s) | Nome / objetivo observável |
|---|---|---|
| UC01 | RF01 | Cadastrar profissional |
| UC02 | RF02 | Autenticar profissional |
| UC03 | RF03 | Visualizar Perfil de profissional |
| UC04 | RF04 | Editar profissional |
| UC05 | RF05 | Cadastrar assistidos |
| UC06 | RF06 | Editar assistidos |
| UC07 | RF07 | Visualizar assistidos |
| UC08 | RF08 | Visualizar Perfil de Assistido |
| UC09 | RF09 | Criar plano terapêutico |
| UC10 | RF10 | Alterar plano terapêutico |
| UC11 | RF11 | Visualizar Plano Terapêutico do Assistido |
| UC12 | RF12 | Desativação do plano terapêutico do assistido |
| UC13 | RF13 | Reativação do plano terapêutico do assistido |
| UC14 | RF14 | Cadastrar treino |
| UC15 | RF15 | Alterar treino |
| UC16 | RF16–RF20 | Configuração e Execução da Sessão |
| UC17 | RF21 | Histórico de sessões |
| UC18 | RF22 | Visualizar sessão |
| UC19 | RF23 | Editar sessão própria no prazo permitido |
| UC20 | RF24 | Exportar sessão em PDF |
| UC21 | RF25 (opcional) | Consulta e Análise de treinos |

RF16–RF20 compartilham UC16 porque descrevem etapas do mesmo objetivo de atendimento. UC21 foi incluído apenas como rastreio provisório do RF25; não significa que a função esteja aprovada.

## Casos de uso detalhados

### UC01 — Cadastrar profissional

| Campo | Especificação |
|---|---|
| Objetivo | Criar conta de profissional para acesso ao sistema. |
| Ator principal | Administrador. |
| Requisito relacionado | RF01. |
| Plataforma | Site. |
| Gatilho | Administrador solicita novo cadastro. |
| Pré-condições | Administrador autenticado e autorizado; campos obrigatórios definidos pela equipe. |
| Pós-condições | Conta é persistida e pode ser localizada para autenticação, conforme estado inicial acordado. |
| Dados | Campos de profissional definidos no formulário; CPF e e-mail aparecem únicos no modelo atual. Campos obrigatórios: a confirmar. |
| Prioridade / regra | A definir / regra de unicidade e gestão de conta a validar. |
| Critério de aceite | Cadastro válido e sem duplicidade cria uma conta; duplicidade ou dado inválido não cria outra conta e informa a correção necessária. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Abre o cadastro de profissional. | Apresenta os campos definidos para a conta. |
| 2 | Administrador | Preenche os campos e solicita salvar. | Valida campos e unicidade conforme regra aprovada. |
| 3 | Sistema | — | Persiste a conta e informa o resultado. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Há campo inválido ou obrigatório ausente. | Não persiste; identifica o campo e permite correção. Regras específicas: a confirmar. |
| A2 — passo 2 | CPF/e-mail ou identificador definido já está em uso. | Não cria duplicata; informa conflito sem revelar dados da conta existente. |

### UC02 — Autenticar profissional

| Campo | Especificação |
|---|---|
| Objetivo | Iniciar acesso autenticado para um profissional cadastrado. |
| Ator principal | Administrador ou Profissional, conforme os dois atores ligados à autenticação no diagrama. |
| Requisito relacionado | RF02. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional solicita entrar no sistema. |
| Pré-condições | Conta existente e sistema disponível. |
| Pós-condições | Identidade autenticada e permissões aplicadas; sessão/token conforme arquitetura aprovada. |
| Dados | Credenciais; não registrar valores reais em documentação/testes. |
| Prioridade / regra | A definir / política de tentativas, recuperação e expiração: a confirmar. |
| Critério de aceite | Credencial válida permite acesso autorizado; credencial inválida não cria sessão e não revela qual campo falhou. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador ou Profissional | Abre a tela de autenticação. | Solicita as credenciais previstas. |
| 2 | Administrador ou Profissional | Informa credenciais e confirma. | Valida credenciais no serviço de autenticação. |
| 3 | Sistema | — | Concede sessão/autorização e apresenta a área permitida ao perfil. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Credenciais inválidas ou conta não autenticável. | Nega acesso com mensagem genérica; permanece na tela de autenticação. |
| A2 — passo 2 | Serviço de autenticação indisponível. | Informa indisponibilidade sem conceder acesso; não registra autenticação bem-sucedida. |

### UC03 — Visualizar Perfil de profissional

| Campo | Especificação |
|---|---|
| Objetivo | Consultar os dados do perfil próprio do Administrador ou do Profissional autenticado. |
| Ator principal | Administrador ou Profissional, no próprio perfil. |
| Requisito relacionado | RF03. |
| Plataforma | Site e Mobile. |
| Gatilho | Administrador ou Profissional abre o próprio perfil. |
| Pré-condições | Administrador ou Profissional autenticado; perfil próprio existente. |
| Pós-condições | Nenhuma alteração; perfil correspondente à identidade autenticada é exibido. |
| Dados | Dados cadastrais autorizados; lista exata de campos: a confirmar. |
| Prioridade / regra | A definir / cada ator consulta somente o próprio perfil por esta função. |
| Critério de aceite | A resposta contém somente o perfil da identidade autenticada e campos autorizados. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador ou Profissional | Seleciona “Meu perfil”. | Consulta o perfil associado à identidade autenticada. |
| 2 | Sistema | — | Apresenta os campos permitidos do próprio perfil. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Sessão expirada ou ausente. | Nega a consulta protegida e solicita nova autenticação. |
| A2 — passo 1 | Perfil não localizado para a identidade. | Informa que não foi possível carregar o perfil; não apresenta dados de outra conta. |

### UC04 — Editar profissional

| Campo | Especificação |
|---|---|
| Objetivo | Atualizar os próprios dados cadastrais editáveis. |
| Ator principal | Administrador ou Profissional, no próprio perfil. |
| Requisito relacionado | RF04. |
| Plataforma | Site. |
| Gatilho | Administrador ou Profissional escolhe editar o próprio perfil. |
| Pré-condições | Administrador ou Profissional autenticado; perfil próprio existente. |
| Pós-condições | Campos válidos são atualizados no perfil próprio. |
| Dados | Campos editáveis/imutáveis: a confirmar; não presumir alteração de e-mail, CPF ou senha no mesmo fluxo. |
| Prioridade / regra | A definir / alteração limitada à identidade autenticada. |
| Critério de aceite | Dados válidos são persistidos e reaparecem em UC03; tentativa de editar outra conta é recusada. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador ou Profissional | Abre o perfil próprio e seleciona editar. | Apresenta os campos editáveis do próprio perfil. |
| 2 | Administrador ou Profissional | Altera os dados permitidos e confirma. | Valida os dados e autorização. |
| 3 | Sistema | — | Persiste alterações e apresenta confirmação. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Dados inválidos ou conflito de unicidade. | Não persiste; informa campos a corrigir. |
| A2 — passo 2 | Identidade não é proprietária do perfil-alvo. | Recusa a operação no backend; dados permanecem inalterados. |

### UC05 — Cadastrar assistidos

| Campo | Especificação |
|---|---|
| Objetivo | Registrar um assistido para acompanhamento. |
| Ator principal | Administrador. |
| Requisito relacionado | RF05. |
| Plataforma | Site. |
| Gatilho | Administrador solicita novo cadastro. |
| Pré-condições | Administrador autenticado/autorizado; campos obrigatórios e política de identificação definidos. |
| Pós-condições | Assistido é persistido e fica disponível conforme regra de acesso aprovada. |
| Dados | Nome, CPF, nascimento, sala, agente de sala, convênio, frequência/período, informações do responsável e observações constam no RF. Obrigatoriedade/necessidade de cada campo: validar. |
| Prioridade / regra | A definir / regra de duplicidade e uso de dados pessoais a aprovar. |
| Critério de aceite | Cadastro válido é criado uma vez; duplicidade ou dado inválido não gera segundo registro. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Abre o cadastro e informa os dados requeridos. | Valida formato e campos conforme regra aprovada. |
| 2 | Administrador | Confirma o cadastro. | Verifica duplicidade pelo identificador acordado. |
| 3 | Sistema | — | Persiste o assistido e confirma o cadastro. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Campo obrigatório ausente ou inválido. | Não persiste; informa o que precisa ser corrigido. |
| A2 — passo 2 | Identificador único já cadastrado. | Não cria duplicata; mantém o registro existente e informa o conflito sem expor dados indevidos. |

### UC06 — Editar assistidos

| Campo | Especificação |
|---|---|
| Objetivo | Atualizar campos permitidos de um assistido cadastrado. |
| Ator principal | Administrador. |
| Requisito relacionado | RF06. |
| Plataforma | Site. |
| Gatilho | Administrador seleciona “Editar” no assistido. |
| Pré-condições | Administrador autenticado/autorizado; assistido existente. |
| Pós-condições | Campos válidos são atualizados no mesmo registro. |
| Dados | Campos editáveis, histórico/auditoria e mudanças de identificador: a confirmar. |
| Prioridade / regra | A definir / autorização de edição conforme política aprovada. |
| Critério de aceite | Alteração válida é consultável depois de salvar; falha ou recusa não altera dados. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Administrador | Localiza e seleciona o assistido. | Apresenta o perfil correspondente. |
| 2 | Administrador | Seleciona editar, altera campos permitidos e confirma. | Valida dados e permissão. |
| 3 | Sistema | — | Persiste as alterações e apresenta o perfil atualizado. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Registro não existe ou não está acessível. | Informa que não foi localizado; não apresenta outro assistido. |
| A2 — passo 2 | Dados inválidos ou alteração de identificador conflitante. | Não persiste e identifica a correção necessária. |

### UC07 — Visualizar assistidos

| Campo | Especificação |
|---|---|
| Objetivo | Consultar assistidos disponíveis ao profissional. |
| Ator principal | Profissional autenticado. |
| Requisito relacionado | RF07. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional abre a lista de assistidos. |
| Pré-condições | Profissional autenticado; regra de alcance dos registros definida. |
| Pós-condições | Nenhuma alteração; lista ou estado vazio exibido. |
| Dados | Identificação mínima para seleção; campos visíveis: a confirmar. |
| Prioridade / regra | A definir / vínculo entre profissional e assistidos a confirmar. |
| Critério de aceite | Lista corresponde ao escopo autorizado; ausência de registros apresenta estado vazio. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Solicita a lista. | Consulta registros permitidos para a identidade. |
| 2 | Sistema | — | Apresenta a lista; permite selecionar um assistido. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Não há assistidos disponíveis. | Apresenta lista vazia e mensagem informativa, sem erro técnico. |
| A2 — passo 1 | Sessão expirada ou não autenticada. | Nega acesso e solicita autenticação. |

### UC08 — Visualizar Perfil de Assistido

| Campo | Especificação |
|---|---|
| Objetivo | Consultar informações relacionadas a um assistido específico. |
| Ator principal | Profissional autenticado. |
| Requisito relacionado | RF08. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional seleciona assistido na lista ou abre seu perfil. |
| Pré-condições | Profissional autenticado; assistido existente e acessível. |
| Pós-condições | Nenhuma alteração; informações disponíveis são apresentadas. |
| Dados | Informações gerais, scores, planos ativos/inativos e histórico; campos autorizados por perfil: a confirmar. |
| Prioridade / regra | A definir / alcance dos dados a validar com AMDE. |
| Critério de aceite | Perfil é do assistido selecionado; cada seção mostra dados existentes ou estado vazio; ações são compatíveis com a plataforma e permissão. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona um assistido acessível. | Consulta e apresenta o perfil correspondente. |
| 2 | Sistema | — | Apresenta informações gerais, scores, planos e histórico disponíveis. |
| 3 | Profissional | Seleciona ação disponível no Site ou Mobile. | Abre o fluxo correspondente (UC09 ou UC16) após verificar autorização. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Assistido não existe ou não é acessível. | Nega consulta sem revelar dados; permanece na lista. |
| A2 — passo 2 | Uma seção não possui registros. | Apresenta estado vazio naquela seção, mantendo o restante do perfil. |

### UC09 — Criar plano terapêutico

| Campo | Especificação |
|---|---|
| Objetivo | Criar plano associado a um assistido. |
| Ator principal | Profissional autenticado. |
| Requisito relacionado | RF09. |
| Plataforma | Site. |
| Gatilho | Profissional escolhe criar plano no perfil do assistido. |
| Pré-condições | Profissional autenticado e autorizado; assistido acessível. |
| Pós-condições | Plano é criado e vinculado ao assistido e ao profissional criador. |
| Dados | Nome, objetivo, observação opcional conforme confirmação, data automática e estado inicial: a confirmar. |
| Prioridade / regra | A definir / criador do plano registrado. |
| Critério de aceite | Plano salvo aparece associado ao assistido e ao criador; data é gerada pelo sistema. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Abre o perfil e solicita criar plano. | Apresenta formulário de plano. |
| 2 | Profissional | Informa os campos e confirma. | Valida dados e autorização do assistido. |
| 3 | Sistema | — | Define criador/data conforme regra, persiste o plano e confirma. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Dados obrigatórios inválidos. | Não persiste; indica campos a corrigir. |
| A2 — passo 2 | Assistido deixou de estar acessível ou operação não autorizada. | Nega criação; nenhum plano é criado. |

### UC10 — Alterar plano terapêutico

| Campo | Especificação |
|---|---|
| Objetivo | Atualizar dados permitidos de plano existente. |
| Ator principal | Profissional criador/responsável. |
| Requisito relacionado | RF10. |
| Plataforma | Site. |
| Gatilho | Responsável abre o plano e solicita alteração. |
| Pré-condições | Plano existente; identidade corresponde ao profissional autorizado. |
| Pós-condições | Campos permitidos do plano são atualizados. |
| Dados | Campos editáveis e tratamento de plano desativado: a confirmar. |
| Prioridade / regra | A definir / RN01. |
| Critério de aceite | Criador altera e consulta valores atualizados; outro profissional não consegue alterar via interface nem API. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional responsável | Abre o plano e solicita editar. | Carrega o plano e verifica autoria/permissão. |
| 2 | Profissional responsável | Altera campos permitidos e confirma. | Valida dados e autorização novamente no servidor. |
| 3 | Sistema | — | Persiste alterações e confirma a atualização. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1/2 | Administrador ou Profissional não é o responsável autorizado. | Nega a operação e mantém o plano inalterado. |
| A2 — passo 2 | Dados inválidos ou plano não localizado. | Não persiste; informa a condição sem expor dados não autorizados. |

### UC11 — Visualizar Plano Terapêutico do Assistido

| Campo | Especificação |
|---|---|
| Objetivo | Consultar plano terapêutico e treinos vinculados. |
| Ator principal | Profissional autenticado e autorizado. |
| Requisito relacionado | RF11. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional seleciona um plano. |
| Pré-condições | Plano existe e é acessível ao profissional. |
| Pós-condições | Nenhuma alteração; plano e treinos disponíveis são apresentados. |
| Dados | Nome, objetivo, estado e treinos; campos expostos: a confirmar. |
| Prioridade / regra | A definir / acesso a planos de outros profissionais: confirmar. |
| Critério de aceite | Plano consultado é o selecionado; lista mostra apenas treinos relacionados e estado vazio quando não houver. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona plano acessível. | Consulta dados do plano e treinos associados. |
| 2 | Sistema | — | Apresenta plano e lista de treinos. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Plano não localizado, desativado sem permissão de consulta ou não autorizado. | Nega acesso ou informa indisponibilidade conforme política aprovada. |
| A2 — passo 2 | Plano não possui treinos. | Apresenta estado vazio; não cria treinos automaticamente. |

### UC12 — Desativação do plano terapêutico do assistido

| Campo | Especificação |
|---|---|
| Objetivo | Alterar plano em uso para estado desativado. |
| Ator principal | Profissional criador/responsável. |
| Requisito relacionado | RF12. |
| Plataforma | Site. |
| Gatilho | Responsável solicita desativar plano. |
| Pré-condições | Plano ativo e identidade autorizada. |
| Pós-condições | Estado do plano fica desativado; histórico permanece consultável conforme regra aprovada. |
| Dados | Identificador, estado atual e estado solicitado. |
| Prioridade / regra | A definir / RN02. |
| Critério de aceite | Responsável desativa; operação repetida não corrompe estado; não responsável é recusado. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional responsável | Abre plano ativo e escolhe desativar. | Apresenta confirmação e estado atual. |
| 2 | Profissional responsável | Confirma a ação. | Verifica autorização e estado no servidor. |
| 3 | Sistema | — | Atualiza estado e confirma. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Solicitante não é responsável. | Recusa sem alterar estado. |
| A2 — passo 2 | Plano já desativado ou inexistente. | Informa estado/indisponibilidade; não cria novo registro. |

### UC13 — Reativação do plano terapêutico do assistido

| Campo | Especificação |
|---|---|
| Objetivo | Retornar plano desativado ao estado ativo. |
| Ator principal | Profissional criador/responsável. |
| Requisito relacionado | RF13. |
| Plataforma | Site. |
| Gatilho | Responsável solicita reativar plano desativado. |
| Pré-condições | Plano existente e desativado; solicitante autorizado. |
| Pós-condições | Estado fica ativo e plano volta a ser elegível nos fluxos que consideram planos ativos. |
| Dados | Identificador, estado atual e estado solicitado. |
| Prioridade / regra | A definir / RN02. |
| Critério de aceite | Profissional responsável reativa o plano; novo estado é consultável; Administrador ou Profissional sem autorização definida não altera o estado. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional responsável | Localiza plano desativado e solicita reativar. | Apresenta estado atual e confirmação. |
| 2 | Profissional responsável | Confirma a ação. | Verifica autorização e estado no servidor. |
| 3 | Sistema | — | Atualiza estado para ativo e confirma. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Solicitante não é responsável. | Recusa sem alterar estado. |
| A2 — passo 2 | Plano já ativo ou inexistente. | Informa estado/indisponibilidade; não duplica o plano. |

### UC14 — Cadastrar treino

| Campo | Especificação |
|---|---|
| Objetivo | Criar treino associado a plano terapêutico. |
| Ator principal | Profissional autorizado no plano. |
| Requisito relacionado | RF14. |
| Plataforma | Site. |
| Gatilho | Profissional escolhe cadastrar treino no plano. |
| Pré-condições | Plano existente e acessível; autorização definida. |
| Pós-condições | Treino é persistido e associado ao plano. |
| Dados | Nome, categoria e tipo de medição (frequência/repetição ou duração); campos adicionais: a confirmar. |
| Prioridade / regra | A definir / associação entre profissional e plano a confirmar. |
| Critério de aceite | Treino salvo pertence ao plano selecionado e possui tipo de medição válido. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Abre plano autorizado e escolhe cadastrar treino. | Apresenta formulário com tipos de medição previstos. |
| 2 | Profissional | Informa nome/categoria/tipo e confirma. | Valida dados e permissão no plano. |
| 3 | Sistema | — | Persiste treino associado ao plano e confirma. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Tipo ou dados inválidos. | Não persiste e informa correção necessária. |
| A2 — passo 2 | Plano não acessível ou profissional não autorizado. | Recusa a operação sem criar treino. |

### UC15 — Alterar treino

| Campo | Especificação |
|---|---|
| Objetivo | Alterar dados permitidos de treino existente. |
| Ator principal | Profissional responsável pelo plano, conforme regra a confirmar. |
| Requisito relacionado | RF15. |
| Plataforma | Site. |
| Gatilho | Profissional solicita editar treino na visualização do plano. |
| Pré-condições | Treino e plano existentes; autorização confirmada. |
| Pós-condições | Campos permitidos do treino são atualizados. |
| Dados | Campos editáveis e efeito de alteração do tipo de medição após haver registros: a confirmar. |
| Prioridade / regra | A definir / não há regra explícita de autoria de treino separada de RN01. |
| Critério de aceite | Treino atualizado aparece no plano correto; alteração não autorizada ou incompatível com dados existentes é recusada conforme regra definida. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional autorizado | Seleciona treino do plano e solicita editar. | Apresenta dados atuais e campos editáveis. |
| 2 | Profissional autorizado | Altera campos permitidos e confirma. | Valida dados e autorização. |
| 3 | Sistema | — | Persiste as alterações e apresenta confirmação. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Tipo de medição alterado com registros existentes. | Aplicar regra de compatibilidade/versionamento definida pela equipe; até a decisão, não converter ou apagar registros silenciosamente. |
| A2 — passo 1/2 | Treino não existe ou solicitante não tem permissão. | Recusa sem alteração. |

### UC16 — Configuração e Execução da Sessão

| Campo | Especificação |
|---|---|
| Objetivo | Registrar atendimento e resultados dos treinos realizados. |
| Ator principal | Profissional autenticado e autorizado para o assistido/plano. |
| Requisito relacionado | RF16, RF17, RF18, RF19 e RF20. |
| Plataforma | Mobile. |
| Gatilho | Profissional inicia atendimento para assistido selecionado. |
| Pré-condições | Profissional autenticado; assistido, plano e treinos acessíveis; regra de compatibilidade assistido/plano confirmada. |
| Pós-condições | Sessão contém vínculos e horários; treinos executados e registros persistidos; score da sessão calculado pela regra aprovada. |
| Dados | Assistido, profissional, plano, treinos, objetivo, horários, observações, tipo de medição, resultados e scores. Unidade/escala do score e duração: a confirmar. |
| Prioridade / regra | A definir / RN04; impedir vínculo contraditório entre sessão, plano e assistido. |
| Critério de aceite | Uma sessão completa pode ser consultada; seus resultados correspondem aos treinos registrados e o score segue RN04 validada. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona assistido e plano disponíveis. | Verifica acesso e apresenta treinos associados. |
| 2 | Profissional | Solicita iniciar sessão. | Cria sessão com profissional, assistido, plano e instante de início. |
| 3 | Profissional | Informa objetivo e seleciona treinos que realizará. | Guarda configuração e apresenta os treinos da sessão. |
| 4 | Profissional | Seleciona um treino e registra sua execução. | Para frequência, oferece as categorias previstas; para duração, disponibiliza medição temporal. |
| 5 | Profissional | Informa resultado/score e, se necessário, observação. | Valida tipo e persiste registro do treino na sessão. |
| 6 | Profissional | Seleciona outro treino ou solicita encerrar sessão. | Se houver outro treino, retorna à lista; se encerrar, segue ao passo 7. |
| 7 | Sistema | — | Registra horário de término, persiste a sessão e calcula score conforme RN04 aprovada. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Plano não pertence ao assistido selecionado ou não está disponível. | Bloqueia início e não cria sessão. Regra de elegibilidade precisa ser validada. |
| A2 — passo 4 | Tipo de medição ou conexão impede registrar resultado. | Mantém estado recuperável ou informa que não salvou; política de pausa/retomada e sincronização offline: a confirmar. |
| A3 — passo 7 | Não há treino registrado ou há campo de score ausente. | Regra para sessão vazia/score ausente: a confirmar. Não substituir ausência por zero sem decisão. |

### UC17 — Histórico de sessões

| Campo | Especificação |
|---|---|
| Objetivo | Consultar sessões associadas a um assistido. |
| Ator principal | Profissional autenticado. |
| Requisito relacionado | RF21. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional solicita histórico a partir do perfil do assistido. |
| Pré-condições | Assistido acessível e profissional autenticado. |
| Pós-condições | Nenhuma alteração; sessões disponíveis são listadas. |
| Dados | Data, resumo e identificador necessário para abrir sessão; filtros/ordem: a confirmar. |
| Prioridade / regra | A definir / alcance por profissional e retenção: a confirmar. |
| Critério de aceite | Histórico mostra somente sessões autorizadas do assistido selecionado e oferece acesso a UC18. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Abre o histórico no perfil do assistido. | Consulta sessões permitidas para o assistido. |
| 2 | Sistema | — | Apresenta a lista; permite selecionar uma sessão. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 2 | Não existem sessões. | Apresenta estado vazio, sem erro. |
| A2 — passo 1 | Assistido não existe ou não é acessível. | Nega consulta sem revelar informações. |

### UC18 — Visualizar sessão

| Campo | Especificação |
|---|---|
| Objetivo | Consultar os dados e os resultados de uma sessão selecionada. |
| Ator principal | Profissional autenticado e autorizado. |
| Requisito relacionado | RF22. |
| Plataforma | Site e Mobile. |
| Gatilho | Profissional seleciona sessão no histórico. |
| Pré-condições | Sessão existente e acessível. |
| Pós-condições | Nenhuma alteração; dados persistidos são apresentados. |
| Dados | Profissional, assistido, treinos, resultados, scores, data/horários e observações autorizadas. |
| Prioridade / regra | A definir / restrição de acesso a histórico a validar. |
| Critério de aceite | Detalhes correspondem ao ID selecionado e distinguem valores ausentes de zero. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Seleciona sessão do histórico. | Verifica acesso e recupera detalhes e registros de treino. |
| 2 | Sistema | — | Apresenta dados da sessão e resultados disponíveis. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Sessão não localizada ou não autorizada. | Nega acesso sem expor dados de sessão alheia. |
| A2 — passo 2 | Parte dos registros não existe. | Identifica informação ausente; não calcula ou exibe valor presumido. |

### UC19 — Editar sessão própria

| Campo | Especificação |
|---|---|
| Objetivo | Corrigir dados permitidos de sessão realizada pelo próprio profissional, dentro do prazo. |
| Ator principal | Profissional autor da sessão. |
| Requisito relacionado | RF23. |
| Plataforma | Site. |
| Gatilho | Autor solicita edição de sessão encerrada. |
| Pré-condições | Sessão encerrada; solicitante é seu autor; instante atual está dentro das 24 horas após o encerramento. |
| Pós-condições | Campos/resultados permitidos são atualizados e score recalculado conforme RN04. |
| Dados | Sessão, autoria, instante de encerramento, alterações e histórico/auditoria: política a confirmar. |
| Prioridade / regra | A definir / RN03–RN04; definir fuso e comportamento exato no limite. |
| Critério de aceite | O Profissional autor antes do limite consegue salvar; outro Profissional ou o autor fora do prazo não altera; score atualizado corresponde à regra aprovada. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional autor | Abre sessão encerrada e solicita editar. | Verifica autoria, estado e prazo no servidor. |
| 2 | Profissional autor | Altera dados permitidos e confirma. | Valida campos e recalcula o score quando scores de treino mudam. |
| 3 | Sistema | — | Persiste alterações e informa sucesso. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Solicitante não é o autor. | Recusa no backend e mantém dados inalterados. |
| A2 — passo 1 | Prazo expirou ou limite ainda não pode ser decidido por fuso ausente. | Recusa ou sinaliza a regra de limite definida; fuso e igualdade no instante-limite devem ser acordados antes da implementação. |
| A3 — passo 2 | Dados inválidos. | Não persiste parcialmente; apresenta correção necessária. |

### UC20 — Exportar sessão em PDF

| Campo | Especificação |
|---|---|
| Objetivo | Gerar arquivo PDF dos registros de uma sessão autorizada. |
| Ator principal | Profissional autenticado e autorizado. |
| Requisito relacionado | RF24. |
| Plataforma | Site. |
| Gatilho | Profissional solicita exportar sessão a partir dos detalhes/histórico. |
| Pré-condições | Sessão existe e é acessível; campos de exportação definidos. |
| Pós-condições | PDF é disponibilizado ao Profissional autorizado sem alterar a sessão. |
| Dados | Dados e identificação a incluir, política de retenção/armazenamento e nome do arquivo: a confirmar. |
| Prioridade / regra | A definir / proteger dados pessoais e impedir exportação de sessão alheia. |
| Critério de aceite | PDF corresponde à sessão selecionada, inclui somente campos autorizados e pode ser aberto; falha é informada sem alteração do registro. |

**Fluxo principal**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional | Solicita exportação da sessão selecionada. | Verifica autorização e recupera os dados da sessão. |
| 2 | Sistema | — | Gera PDF com o modelo/campos aprovados. |
| 3 | Sistema | — | Disponibiliza o arquivo ao profissional autorizado. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — passo 1 | Sessão não existe ou Profissional não está autorizado. | Nega exportação e não entrega dados. |
| A2 — passo 2 | Falha de geração/armazenamento do arquivo. | Informa falha e permite nova tentativa; sessão original permanece inalterada. Política de retenção: a confirmar. |

### UC21 — Consulta e Análise de treinos (rascunho opcional)

| Campo | Especificação |
|---|---|
| Objetivo | Permitir análise de registros anteriores de um treino para acompanhar evolução, **somente se RF25 for aprovado no escopo**. |
| Ator principal | Profissional, se autorizado pela AMDE. |
| Requisito relacionado | RF25 opcional. |
| Plataforma | Site/Mobile: a definir. |
| Gatilho | Profissional solicita histórico/análise de treino no perfil do assistido. |
| Pré-condições | RF25 aprovado; registros com período, métrica e autorização disponíveis. |
| Pós-condições | Nenhuma alteração; registros existentes são apresentados de forma interpretável. |
| Dados | Assistido, treino, datas, valores, unidade, escala e regra de agregação: todos a confirmar. O modelo atual de `ScorePorCategoria` não registra período. |
| Prioridade / regra | A definir / fora do escopo confirmado enquanto não houver decisão registrada. |
| Critério de aceite | Após aprovação, a equipe define cenário de análise e resultado esperado; tabela/gráfico só é aceito se representar dados e unidade identificados. |

**Fluxo principal proposto, condicionado à aprovação**

| Passo | Ator | Ação do ator | Resposta do sistema |
|---|---|---|---|
| 1 | Profissional autorizado | Seleciona assistido e treino. | Verifica acesso e existência de registros no período definido. |
| 2 | Profissional autorizado | Informa filtros/período, se adotados. | Valida filtros segundo decisões aprovadas. |
| 3 | Sistema | — | Apresenta registros ordenados com métrica/unidade e, se aprovado, representação gráfica. |

**Alternativas e exceções**

| ID / origem | Condição | Resposta e desfecho |
|---|---|---|
| A1 — decisão de escopo | RF25 ainda não aprovado. | Não tratar UC21 como função obrigatória nem como implementada; registrar decisão pendente. |
| A2 — passo 1/3 | Não há registros ou falta período/unidade necessário à interpretação. | Apresenta estado vazio/limitação; não fabrica série temporal nem score derivado. |

## Pendências para aprovação desta especificação

1. Registrar a decisão sobre hierarquia/permissões de Administrador e Profissional; atualizar UC01–UC08 e matriz de autorização.
2. Aprovar escopo de RF25/UC21 ou removê-lo do conjunto ativo; não contabilizar a proposta como funcionalidade entregue.
3. Confirmar campos obrigatórios, critérios de duplicidade e política de dados pessoais para profissional e assistido.
4. Definir escala/cálculo do score, unidade da duração, tratamento de campos ausentes, timezone do prazo de edição e regra de sessão sem treino.
5. Confirmar autorização e consistência entre profissional, assistido, plano e sessão em UI e backend/API.
6. Relacionar cada fluxo a tela/componente, implementação e caso de teste quando esses itens existirem; registrar o commit testado.

## Referência cruzada

As descrições preservam os nomes RF01–RF25 de `docs/requisitos/requisitos-funcionais-sugestao.md`. Os fluxos e critérios de aceite desta sugestão precisam ser revisados em conjunto com aquele arquivo, com o diagrama de casos de uso e com a implementação. O diagrama geral fornecido pela equipe não foi alterado nesta proposta; em especial, a relação de herança entre atores deve refletir a decisão de permissões depois de confirmada.

