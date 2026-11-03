# Especificação de Requisitos — Sistema AMDE

> Documento de especificação consolidado a partir do levantamento de requisitos do sistema AMDE. As métricas quantitativas indicadas nos requisitos não funcionais são propostas iniciais e devem ser validadas pela equipe e pela AMDE antes de serem consideradas critérios definitivos de aceite.

- **Projeto:** Sistema de acompanhamento terapêutico da AMDE: ClinicABA
- **Versão:** 0.1
- **Data:** 2026-11-03
- **Escopo/versão do produto:** Aplicação mobile para utilização durante as sessões e aplicação web/computador para gerenciamento, consulta e análise dos dados.
- **Origem e validação:** Levantamento de requisitos do projeto AMDE. Requisitos e métricas pendentes de validação com a equipe e, quando aplicável, com a AMDE.

---

## 1. Requisitos funcionais (RF)

| ID | Nome | Descrição | Prioridade | Caso de uso ou rastreio alternativo | Estado | Origem/evidência |
|---|---|---|---|---|---|---|
| RF01 | Cadastrar profissional (Site) | O sistema deve permitir que o Administrador cadastre profissionais para utilização da plataforma. | UC01 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF02 | Autenticar profissional (Site e Mobile) | O sistema deve permitir que profissionais cadastrados realizem login para acessar suas funcionalidades. | UC02 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF03 | Visualizar perfil de profissional (Site e Mobile) | O sistema deve apresentar as informações cadastradas sobre o usuário logado. | UC03 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF04 | Editar profissional (Site) | O sistema deve permitir que usuários cadastrados efetuem a edição dos dados do próprio perfil. | UC04 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF05 | Cadastrar assistido (Site) | O sistema deve permitir que o Administrador cadastre assistidos, incluindo CPF, nome, data de nascimento, sala, agente responsável da sala, convênio, frequência/período, informações do responsável e observações gerais. | UC05 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF06 | Editar assistido (Site) | O sistema deve permitir a edição dos dados cadastrados dos assistidos. | UC06 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF07 | Visualizar assistidos (Site e Mobile) | O sistema deve permitir que o profissional visualize os assistidos disponíveis para atendimento. | UC07 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF08 | Visualizar perfil de assistido (Site e Mobile) | O sistema deve permitir que o profissional visualize as informações do assistido, incluindo informações gerais, scores, planos terapêuticos ativos e desativados e histórico de sessões. A partir do perfil, poderá acessar funcionalidades relacionadas, como iniciar uma sessão no Mobile ou criar um plano terapêutico no Site. | UC08 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF09 | Criar plano terapêutico (Site) | O sistema deve permitir que o profissional crie planos terapêuticos para um assistido. O plano deve conter nome, profissional responsável, objetivo, data de criação automática e observação. O acesso deve ocorrer pelo perfil do assistido. | UC09 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF10 | Alterar plano terapêutico (Site) | O sistema deve permitir que o profissional responsável altere um plano terapêutico, a partir da página de visualização do plano. | UC10 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF11 | Visualizar plano terapêutico (Site e Mobile) | O sistema deve permitir que o profissional acesse um plano terapêutico cadastrado para o assistido e os treinos associados a esse plano. | UC11 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF12 | Desativar plano terapêutico (Site) | O sistema deve permitir que o profissional responsável pela criação do plano o desative quando não for mais utilizado. | UC12 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF13 | Reativar plano terapêutico (Site) | O sistema deve permitir que o profissional responsável pela criação do plano o reative, a partir do perfil do assistido. | UC13 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF14 | Cadastrar treino (Site) | O sistema deve permitir que o profissional cadastre treinos dentro de um plano terapêutico, informando nome, categoria e tipo de medição. Os tipos previstos são frequência/repetição e duração. | UC14| A definir | Proposto | Levantamento de requisitos AMDE |
| RF15 | Alterar treino (Site) | O sistema deve permitir que o profissional altere os treinos cadastrados em seus planos terapêuticos, a partir da visualização do plano. |UC15 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF16 | Iniciar sessão e registrar informações automaticamente (Mobile) | O sistema deve permitir que o profissional inicie uma sessão. O sistema deve registrar automaticamente o assistido, o profissional responsável, a data e o horário de início. | UC16 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF17 | Configurar sessão (Mobile) | O sistema deve permitir que o profissional registre informações básicas da sessão, como objetivo, plano de intervenção do assistido e treinos que serão realizados. | UC16 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF18 | Iniciar treinos dentro da sessão (Mobile) | O sistema deve permitir que o profissional acesse os treinos selecionados para a sessão e escolha qual deseja realizar. Após concluir um treino, poderá selecionar outro ou encerrar a sessão. Também poderá adicionar observações à sessão. | UC16 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF19 | Executar treino (Mobile) | O sistema deve permitir o registro dos resultados durante a execução dos treinos. Em treinos de frequência/repetição, deve apresentar as opções "Executado sem ajuda", "Executado com ajuda" e "Não executado", permitindo registros contínuos até o encerramento do treino. Em treinos de duração, deve apresentar um cronômetro. Após o encerramento do treino, deve permitir o registro do score e retornar à tela de treinos da sessão. | UC16 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF20 | Encerrar sessão (Mobile) | O sistema deve permitir que o profissional finalize a sessão após realizar os treinos desejados. Ao encerrar, deve registrar automaticamente o horário de término, armazenar as informações e calcular o score da sessão pela soma dos scores dos treinos realizados. | UC16 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF21 | Histórico de sessões (Mobile e Site) | O sistema deve permitir que o profissional visualize, a partir do perfil do assistido, a lista de sessões realizadas com ele. | UC17 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF22 | Visualizar sessão (Mobile e Site) | O sistema deve permitir que o profissional consulte os detalhes de uma sessão, incluindo profissional responsável, assistido, treinos realizados, scores dos treinos, score da sessão e data. O acesso deve ocorrer pelo histórico de sessões. | UC18 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF23 | Editar sessão (Site) | O sistema deve permitir que o profissional altere os dados de uma sessão realizada por ele, em até 24 horas após o encerramento. Não poderá alterar sessões de outros profissionais. Após a alteração dos scores dos treinos, o score da sessão deve ser recalculado pela soma dos scores dos treinos. | UC19 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF24 | Exportar sessão (Site) | O sistema deve permitir que o profissional exporte os registros de uma sessão realizada em formato PDF. | UC20 | A definir | Proposto | Levantamento de requisitos AMDE |
| RF25 | Consultar e analisar treinos | O sistema poderá permitir a consulta de registros anteriores de um treino para análise da evolução do assistido, podendo incluir gráficos e tabelas dos resultados. | A definir | -- | Proposto | Levantamento de requisitos AMDE |

---

## 2. Requisitos não funcionais (RNF)

> Os valores numéricos abaixo são metas iniciais para tornar os requisitos verificáveis. Devem ser confirmados com a equipe e com a AMDE, considerando o volume esperado de utilização, os dispositivos e as condições reais de atendimento.

| ID | Atributo/necessidade | Descrição | Critério de verificação acordado ou proposto | Prioridade/estado | Origem |
|---|---|---|---|---|---|
| RNF01 | Velocidade de registro | O sistema deve responder às ações do usuário em até 4 segundos em pelo menos 95% das operações, considerando condições normais de conexão e utilização. | Medir o tempo de resposta em uma amostra de operações representativas. A meta proposta é que pelo menos 95% delas sejam concluídas em até 4 segundos. Definir ambiente, conexão e conjunto de operações para o teste. | A definir / Proposto para validação | Necessidade de agilidade durante o uso; meta quantitativa a validar |
| RNF02 | Usabilidade / interface simplificada | A aplicação mobile deve possuir uma interface simples e intuitiva para utilização durante os atendimentos, permitindo que os profissionais identifiquem e acessem as principais funcionalidades em, no máximo, 3 interações a partir da tela inicial. | Realizar teste de usabilidade com profissionais e verificar se as principais funcionalidades podem ser localizadas e acessadas em até 3 interações, conforme tarefas previamente definidas. | A definir / Proposto para validação | Necessidade de uso durante os atendimentos |
| RNF03 | Eficiência de interação | O registro de informações de uma sessão deve exigir, preferencialmente, no máximo 5 ações do profissional para a conclusão de um registro padrão, desconsiderando o preenchimento dos dados específicos de cada atividade. | Contabilizar as ações necessárias para concluir um cenário padrão de registro. Validar com a equipe quais ações entram na contagem e quais etapas compõem o cenário. | A definir / Proposto para validação | Necessidade de reduzir ações durante o atendimento |
| RNF04 | Segurança / controle de acesso | O sistema deve proteger as informações contra acessos não autorizados, exigindo autenticação para acesso às funcionalidades internas e garantindo que as operações respeitem as permissões atribuídas ao usuário. | Testar os perfis e as operações de consulta, inclusão, alteração e exclusão. A meta proposta é bloquear 100% das tentativas não autorizadas nos cenários de teste definidos. | A definir / Proposto para validação | Necessidade de proteção das informações dos assistidos |
| RNF05 | Segurança / controle de edição de sessões | O sistema deve permitir apenas que o próprio profissional que realizou o registro edite a sessão. | Testar tentativas de edição pelo profissional autor e por outros profissionais, tanto pela interface quanto diretamente pela API, caso exista endpoint acessível. A meta proposta é bloquear 100% das tentativas feitas por usuários não autorizados. Considerar também a regra funcional de edição em até 24 horas após o encerramento (RF23). | A definir / Proposto para validação | Regra descrita no levantamento de requisitos |
| RNF06 | Integridade e confiabilidade dos registros | O sistema deve garantir que os dados coletados durante as sessões não sejam perdidos ou alterados incorretamente. | Executar testes de gravação, consulta e recuperação dos registros. A meta proposta é preservar integralmente 100% dos registros confirmados nos cenários de teste e evitar duplicações decorrentes de reenvio ou falha de processamento. Definir também estratégia de backup e recuperação. | A definir / Proposto para validação | Necessidade de preservar o histórico das sessões |
| RNF07 | Desempenho / capacidade | O sistema deve manter seu desempenho mesmo com o aumento da quantidade de assistidos, sessões e registros armazenados. | Realizar teste de carga com uma base de referência de, no mínimo, 100 assistidos e 10.000 registros de sessões. Verificar se o tempo de resposta permanece dentro da meta do RNF01. Os volumes são estimativas iniciais e precisam ser validados com a AMDE. | A definir / Proposto para validação | Expectativa de crescimento da base; volume a validar |
| RNF08 | Integridade / unicidade de cadastro | O sistema deve impedir que um mesmo assistido possua múltiplos cadastros, realizando a verificação de possíveis duplicidades com base nos dados de identificação disponíveis. | Testar tentativas de cadastrar novamente um assistido já existente. A meta proposta é verificar 100% das tentativas de cadastro. Validar com a AMDE quais campos serão usados na identificação; o CPF consta entre os dados previstos no RF05. | A definir / Proposto para validação | Necessidade de evitar cadastros duplicados; dados de identificação do RF05 |
| RNF09 | Gestão do ciclo de vida dos dados | O sistema deve diferenciar informações ativas e desativadas, permitindo consultar dados desativados quando necessário, sem apresentá-los como ativos nas listas e funcionalidades de utilização. | Verificar as listagens e funcionalidades que devem considerar somente dados ativos, bem como a possibilidade de consultar registros desativados em telas de histórico ou consulta. A meta proposta é aplicar corretamente o filtro em 100% dos cenários definidos. | A definir / Proposto para validação | Necessidade de distinguir informações ativas e desativadas |
| RNF10 | Autorização / gestão de plano terapêutico | O sistema deve permitir que apenas o profissional responsável pelo plano terapêutico do assistido realize sua desativação ou reativação. | Testar a desativação e a reativação por parte do profissional responsável e de outros profissionais. A meta proposta é bloquear 100% das tentativas realizadas por usuários não responsáveis. | A definir / Proposto para validação | Regra descrita nos requisitos de gerenciamento de planos terapêuticos |

---

## 3. Regras de negócio (RN)

> Foram registradas somente regras de domínio explicitadas no levantamento. Regras adicionais devem ser confirmadas com a AMDE antes de serem incluídas.

| ID | Regra | Origem/validação | Requisitos relacionados | Estado |
|---|---|---|---|---|
| RN01 | Apenas o profissional responsável pela criação de um plano terapêutico pode alterá-lo. | Regra expressa no levantamento de requisitos; validar com a AMDE. | RF10 | Proposto |
| RN02 | Apenas o profissional responsável pela criação de um plano terapêutico pode desativá-lo ou reativá-lo. | Regra expressa nos requisitos de desativação e reativação; validar com a AMDE. | RF12, RF13, RNF10 | Proposto |
| RN03 | Um profissional pode editar somente sessões realizadas por ele, e a edição deve ocorrer em até 24 horas após o encerramento da sessão. | Regra expressa no levantamento de requisitos; validar com a AMDE. | RF23, RNF05 | Proposto |
| RN04 | O score de uma sessão corresponde à soma dos scores dos treinos realizados durante ela e deve ser atualizado quando os scores dos treinos forem alterados. | Regra expressa no levantamento de requisitos; validar com a AMDE. | RF20, RF22, RF23 | Proposto |
| RN05 | Os tipos de medição previstos para os treinos são frequência/repetição e duração. | Regra descrita no cadastro de treinos; validar com a AMDE. | RF14, RF19 | Proposto |

---

## 4. Critérios de aceite e validação

> Os cenários abaixo são propostas de verificação. A situação deve ser atualizada após a execução dos testes; não representa evidência de que o requisito já foi validado.

| Requisito | Cenário/condição | Resultado esperado | Método/evidência | Situação |
|---|---|---|---|---|
| RF01 | Administrador acessa o cadastro e informa os dados de um profissional. | O profissional é cadastrado e fica disponível para autenticação conforme as regras do sistema. | Teste funcional manual ou automatizado; registro do resultado. | Planejado |
| RF02 | Profissional cadastrado informa credenciais válidas e inválidas. | Credenciais válidas permitem acesso; inválidas não permitem acesso. | Teste funcional e evidência das respostas do sistema. | Planejado |
| RF03 | Usuário autenticado acessa a visualização do próprio perfil. | O sistema apresenta os dados cadastrados do usuário logado. | Inspeção da interface e teste funcional. | Planejado |
| RF04 | Usuário cadastrado altera dados do próprio perfil. | O sistema salva e apresenta os dados atualizados. | Teste funcional. | Planejado |
| RF05 | Administrador cadastra um assistido preenchendo os campos previstos. | O assistido é cadastrado com os dados informados. | Teste funcional e conferência dos dados persistidos. | Planejado |
| RF06 | Usuário autorizado altera dados de um assistido existente. | O sistema salva e apresenta os dados atualizados. | Teste funcional. | Planejado |
| RF07 | Profissional acessa a lista de assistidos. | O sistema apresenta os assistidos disponíveis para atendimento. | Teste funcional nos ambientes Site e Mobile. | Planejado |
| RF08 | Profissional abre o perfil de um assistido. | O sistema apresenta informações gerais, scores, planos ativos e desativados e histórico, além dos acessos previstos. | Inspeção da interface e teste funcional nos ambientes Site e Mobile. | Planejado |
| RF09 | Profissional cria um plano terapêutico a partir do perfil do assistido. | O plano é salvo com os campos previstos e data de criação automática. | Teste funcional e conferência do registro. | Planejado |
| RF10 | Profissional responsável tenta alterar um plano; outro profissional também tenta alterá-lo. | O responsável consegue alterar; usuário não responsável não consegue. | Teste de autorização com dois usuários. | Planejado |
| RF11 | Profissional acessa um plano terapêutico existente. | O sistema apresenta o plano e os treinos associados. | Teste funcional nos ambientes Site e Mobile. | Planejado |
| RF12 | Profissional responsável desativa um plano terapêutico. | O plano é desativado; usuário não responsável não consegue realizar a ação. | Teste funcional e teste de autorização. | Planejado |
| RF13 | Profissional responsável reativa um plano desativado. | O plano é reativado; usuário não responsável não consegue realizar a ação. | Teste funcional e teste de autorização. | Planejado |
| RF14 | Profissional cadastra treino com cada tipo de medição previsto. | O sistema salva nome, categoria e tipo de medição do treino. | Teste funcional para frequência/repetição e duração. | Planejado |
| RF15 | Profissional altera um treino de um plano sob sua responsabilidade. | O sistema salva e apresenta os dados atualizados do treino. | Teste funcional e verificação de autorização conforme regra definida para o plano. | Planejado |
| RF16 | Profissional inicia uma sessão para um assistido. | Assistido, profissional, data e horário de início são registrados automaticamente. | Teste funcional e conferência dos dados persistidos. | Planejado |
| RF17 | Profissional configura uma sessão preenchendo objetivo, plano de intervenção e treinos. | O sistema registra as informações selecionadas para a sessão. | Teste funcional. | Planejado |
| RF18 | Profissional seleciona e executa diferentes treinos dentro de uma sessão e adiciona observações. | O sistema permite alternar entre os treinos e registrar observações da sessão. | Teste funcional em dispositivo ou emulador mobile. | Planejado |
| RF19 | Profissional executa um treino de frequência/repetição e outro de duração. | O sistema registra as opções de execução ou o tempo medido e permite registrar o score após o encerramento. | Teste funcional dos dois tipos de medição. | Planejado |
| RF20 | Profissional encerra uma sessão com treinos e scores registrados. | O horário de encerramento é salvo e o score da sessão corresponde à soma dos scores dos treinos. | Teste funcional e conferência do cálculo. | Planejado |
| RF21 | Profissional acessa o histórico a partir do perfil do assistido. | O sistema apresenta a lista de sessões realizadas com o assistido. | Teste funcional nos ambientes Site e Mobile. | Planejado |
| RF22 | Profissional abre uma sessão pelo histórico. | O sistema apresenta os dados e scores previstos para a sessão. | Teste funcional e conferência dos dados. | Planejado |
| RF23 | Profissional autor tenta editar sessão dentro do prazo; outro profissional tenta editá-la; o autor tenta editar após 24 horas. | Somente o autor consegue editar dentro do prazo. O score da sessão é recalculado após alteração dos scores dos treinos. | Testes funcionais e de autorização, incluindo limites de tempo. | Planejado |
| RF24 | Profissional solicita a exportação de uma sessão. | O sistema gera um arquivo PDF com os registros da sessão. | Teste de exportação e inspeção do PDF gerado. | Planejado |
| RF25 | Profissional consulta registros anteriores de um treino. | Quando implementada, a funcionalidade apresenta os registros anteriores e os recursos de análise previstos no escopo. | Teste funcional; confirmar se o requisito fará parte da versão entregue. | A confirmar |
| RNF01 | Executar operações representativas em condições normais de conexão. | Pelo menos 95% das operações medidas respondem em até 4 segundos. | Teste de desempenho com registro dos tempos, ambiente e amostra. | Planejado; meta a validar |
| RNF02 | Profissional realiza tarefas comuns no aplicativo mobile. | As principais funcionalidades podem ser localizadas e acessadas em até 3 interações a partir da tela inicial. | Teste de usabilidade observado com profissionais. | Planejado; meta a validar |
| RNF03 | Profissional conclui um registro padrão de sessão. | O fluxo exige preferencialmente no máximo 5 ações, sem contar o preenchimento dos dados específicos da atividade. | Contagem de ações em roteiro de teste; validar a definição de "ação". | Planejado; meta a validar |
| RNF04 | Usuários com diferentes permissões tentam consultar, incluir, alterar e excluir informações. | Todas as tentativas não autorizadas são bloqueadas nos cenários definidos. | Testes de autenticação e autorização; matriz de permissões e evidências. | Planejado |
| RNF05 | Profissional autor e profissional não autor tentam editar uma sessão; testar também acesso direto à API, se aplicável. | Apenas o autor consegue editar a própria sessão, respeitando o prazo definido no RF23. | Testes de autorização na interface e na API, se houver. | Planejado |
| RNF06 | Salvar, consultar e recuperar registros; simular reenvio ou falha de processamento. | Registros confirmados permanecem íntegros e não são duplicados pelos cenários de falha testados. | Testes de integridade e recuperação; evidências de persistência. | Planejado; política de backup a definir |
| RNF07 | Executar testes com base contendo ao menos 100 assistidos e 10.000 registros de sessões. | O sistema mantém os tempos de resposta definidos no RNF01. | Teste de carga/desempenho; validar os volumes com a AMDE. | Planejado; volumes a validar |
| RNF08 | Tentar cadastrar novamente um assistido já existente, usando os dados de identificação definidos. | O sistema identifica a possível duplicidade e impede o cadastro duplicado conforme a regra acordada. | Testes de cadastro com dados repetidos e variações; validar campos identificadores. | Planejado; regra de identificação a validar |
| RNF09 | Consultar listas operacionais e registros desativados. | Dados desativados não aparecem como ativos nas funcionalidades operacionais, mas permanecem consultáveis onde previsto. | Testes de listagem, filtros e consulta de histórico. | Planejado |
| RNF10 | Profissional responsável e não responsável tentam desativar e reativar o mesmo plano. | Apenas o profissional responsável consegue realizar as operações. | Testes de autorização para as duas operações. | Planejado |

---

## 5. Pendências para validação

1. Confirmar com a AMDE as metas quantitativas dos RNFs, especialmente tempo de resposta, número de interações, quantidade de ações e volume de dados.
