# Requisitos e rastreabilidade

## Atores

- **Profissional:** pessoa autenticada que cadastra pacientes, organiza planos e registra atendimentos.
- **Paciente/assistido:** pessoa cujo acompanhamento é registrado. Não possui acesso próprio na versão atual.

## Requisitos funcionais

| ID | Requisito | Critério de aceite resumido |
|---|---|---|
| RF-01 | Autenticar e cadastrar profissionais. | Cadastro gera acesso e login válido retorna token JWT. |
| RF-02 | Consultar e atualizar o perfil profissional. | Usuário autenticado lê e altera seus próprios dados permitidos. |
| RF-03 | Cadastrar, consultar e editar pacientes. | CPF é único e os dados persistem no PostgreSQL. |
| RF-04 | Criar, consultar, editar, ativar e desativar planos. | Plano pertence a um paciente e registra seu profissional criador. |
| RF-05 | Criar e editar treinos por frequência ou duração. | Treino pertence a um plano e a uma categoria. |
| RF-06 | Iniciar e configurar uma sessão. | Sessão registra paciente, plano, profissional, data e horário inicial; treinos podem ser selecionados. |
| RF-07 | Registrar treino de frequência. | São persistidas as quantidades sem ajuda, com ajuda e não executado. |
| RF-08 | Registrar treino de duração. | A duração em segundos é persistida para o treino da sessão. |
| RF-09 | Encerrar treino com score e observação. | Score inteiro manual e observação ficam associados ao treino realizado. |
| RF-10 | Encerrar sessão com score final e observação. | Horário final é registrado; score final é informado manualmente e não deriva dos treinos. |
| RF-11 | Consultar histórico e detalhes das sessões. | Histórico por paciente e detalhes dos treinos são exibidos. |
| RF-12 | Exportar uma sessão em PDF. | API devolve um PDF identificado pela sessão. |
| RF-13 | Retomar sessão em aberto no mobile. | Sessão sem horário final e pertencente ao profissional pode ser reaberta pelo histórico. |

## Requisitos não funcionais

| ID | Requisito | Verificação esperada |
|---|---|---|
| RNF-01 | API protegida por autenticação stateless com JWT. | Apenas `/api/auth/**` é público. |
| RNF-02 | Senhas armazenadas com hash BCrypt. | Senha não é persistida em texto simples. |
| RNF-03 | Interfaces responsivas e acessíveis por teclado. | Portal se adapta a desktop e telas estreitas; controles têm foco visível. |
| RNF-04 | Formulários mobile utilizáveis com teclado aberto. | Campo focado e ação de salvar permanecem alcançáveis por rolagem. |
| RNF-05 | Persistência relacional em PostgreSQL. | Dados sobrevivem à recriação dos contêineres quando o volume é preservado. |
| RNF-06 | Builds reproduzíveis por Docker para API e web. | `docker compose build` conclui com as dependências declaradas. |
| RNF-07 | Falhas de rede não devem deixar carregamento indefinido. | Interfaces exibem erro e, nos fluxos principais, ação de nova tentativa. |

## Regras de negócio

| ID | Regra |
|---|---|
| RN-01 | CPF e e-mail do profissional são únicos; CPF do paciente também é único. |
| RN-02 | Apenas o criador pode alterar, ativar ou desativar um plano. |
| RN-03 | Apenas o profissional responsável pode modificar a sessão e seus registros. |
| RN-04 | Um plano novo inicia com status `ATIVO`. |
| RN-05 | Não é permitido adicionar treino a uma sessão encerrada. |
| RN-06 | O tipo do registro deve corresponder à medição do treino: `FREQUENCIA` ou `DURACAO`. |
| RN-07 | O score de treino é um número inteiro informado pela clínica; não representa porcentagem. |
| RN-08 | Os scores dos treinos atualizam a soma acumulada do paciente por categoria. Ao reeditar um treino, aplica-se apenas a diferença para evitar soma duplicada. |
| RN-09 | O score final da sessão é manual, separado e nunca calculado a partir dos scores dos treinos. |
| RN-10 | Score zero é um resultado concluído válido. |
| RN-11 | A API restringe a edição de sessão encerrada usando a data da sessão. A mensagem cita 24 horas, mas a implementação atual compara dias corridos; alinhar a regra é item de backlog. |

## Rastreabilidade

| Requisito | API | Web | Mobile | Evidência atual |
|---|---|---|---|---|
| RF-01/02 | `AuthController`, `ProfissionalController` | login, cadastro, perfil | login e perfil | Build web e typecheck mobile. |
| RF-03 | `AssistidoController` | cadastro, lista e detalhes | lista e detalhes | Busca mobile/web e carregamento da API. |
| RF-04/05 | controllers de plano e treino | formulários e detalhes | detalhes e criação integrada | Fluxos implementados; QA manual completa pendente. |
| RF-06 a RF-10 | `SessaoController` e `SessaoService` | edição e detalhes | fluxo de atendimento | Testes de regressão mobile para estados e scores. |
| RF-11 | endpoints por paciente e sessão | histórico e detalhes | histórico e detalhes | Implementado nas duas plataformas. |
| RF-12 | `/sessoes/{id}/exportar-pdf` | ação Exportar PDF | não exposto | Validação funcional do download pendente. |
| RF-13 | consulta de sessões abertas | não aplicável | histórico mobile | Implementado; QA em aparelho pendente. |

## Campos ainda não suportados

Nível de suporte, telefone do responsável, período do plano e objetivo livre da sessão apareceram nas referências visuais, mas não pertencem aos contratos atuais da API. Não devem ser exibidos como dados persistidos até que requisitos e modelo sejam aprovados.
