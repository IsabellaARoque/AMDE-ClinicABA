# Requisitos Funcionais — Sistema AMDE (sugestão)

> **Documento de trabalho, não aprovado.** Esta revisão reorganiza os requisitos da versão 0.1 para melhorar identificação, testabilidade e rastreabilidade. A equipe deve validar atores, prioridades, critérios e escopo com a AMDE. Não altera o original `especificacao_requisitos_AMDE.md`.

- **Projeto:** ClinicABA — Sistema AMDE
- **Versão da sugestão:** 1.0
- **Data:** 03/11/2026
- **Base:** levantamento de requisitos versionado, diagramas/casos de uso versionados e entidades Java atualmente presentes no repositório.
- **Convenção:** `A definir` indica decisão não encontrada nas fontes. `Proposto` não significa aprovado nem implementado.

## Escopo e atores usados nesta versão

O levantamento descreve aplicação Site e Mobile. Mantive os termos **Administrador** e **Profissional** do material da equipe. A relação entre esses perfis precisa ser confirmada: a documentação atual diverge sobre se Profissional herda permissões administrativas. Até essa decisão, cada requisito abaixo identifica apenas o ator mencionado no levantamento, sem conceder permissões adicionais.

## Requisitos funcionais

| ID | Requisito e comportamento observável | Ator | Prioridade | Caso de uso | Critério de aceite proposto | Estado / origem |
|---|---|---|---|---|---|---|
| RF01 | Cadastrar um profissional com os dados obrigatórios definidos pela equipe. O cadastro não deve criar uma segunda conta para identificador já utilizado. | Administrador | A definir | UC01 | Com dados válidos e identificador livre, o cadastro fica disponível para autenticação; com duplicidade, não é criado novo registro e o sistema informa o motivo sem expor dados de outra conta. Campos obrigatórios e identificador único: a confirmar. | Proposto; levantamento AMDE |
| RF02 | Autenticar profissional cadastrado mediante credenciais válidas. | Profissional | A definir | UC02 | Credenciais válidas iniciam sessão/autorização conforme mecanismo adotado; inválidas não concedem acesso e exibem mensagem genérica. Política de bloqueio e recuperação: a confirmar. | Proposto; levantamento AMDE |
| RF03 | Consultar os dados do perfil do usuário autenticado. | Administrador ou Profissional autenticado | A definir | UC03 | O perfil retornado pertence à identidade autenticada e apresenta somente campos autorizados. Campos visíveis por perfil: a confirmar. | Proposto; levantamento AMDE |
| RF04 | Editar os próprios dados cadastrais permitidos. | Administrador ou Profissional autenticado | A definir | UC04 | Após confirmação de dados válidos, a consulta do perfil retorna os valores atualizados; campos que não podem ser editados devem ser identificados. | Proposto; levantamento AMDE |
| RF05 | Cadastrar um assistido com os dados de identificação e atendimento definidos no levantamento, incluindo campos atualmente listados: nome, CPF, nascimento, sala, agente da sala, convênio, frequência/período, dados do responsável e observações. | Administrador | A definir | UC05 | Com os campos obrigatórios confirmados preenchidos e sem duplicidade conforme regra de identificação aprovada, o registro é salvo; duplicidade/dado inválido impede gravação e informa correção necessária. Obrigatoriedade e uso de CPF: validar com a AMDE. | Proposto; levantamento AMDE |
| RF06 | Editar dados permitidos de um assistido cadastrado. | Administrador | A definir | UC06 | Usuário autorizado altera os campos editáveis; depois de salvar, uma nova consulta mostra os dados atualizados. Permissões por campo: a confirmar. | Proposto; levantamento AMDE |
| RF07 | Consultar a lista de assistidos disponíveis ao profissional autenticado. | Profissional | A definir | UC07 | A lista contém somente registros que a regra de acesso aprovada permite ao profissional consultar; a lista vazia é apresentada sem erro. Regra de vínculo/alcance: a confirmar. | Proposto; levantamento AMDE |
| RF08 | Consultar o perfil de um assistido e, conforme autorização, acessar informações gerais, scores, planos ativos/inativos e histórico de sessões. | Profissional | A definir | UC08 | O perfil corresponde ao assistido selecionado; cada seção mostra dados existentes, estado vazio quando não houver dados e links de ação autorizados para Site/Mobile. Campos e permissões: a confirmar. | Proposto; levantamento AMDE |
| RF09 | Criar plano terapêutico associado a um assistido, registrando nome, objetivo, profissional criador e data de criação; observação é opcional conforme o levantamento. | Profissional | A definir | UC09 | Após salvar dados válidos, o plano aparece no perfil correto, associado ao profissional autenticado e com data registrada pelo sistema. Obrigatoriedade dos campos: a confirmar. | Proposto; levantamento AMDE |
| RF10 | Alterar dados permitidos de plano criado pelo profissional responsável. | Profissional criador | A definir | UC10 | O responsável altera e consulta os valores atualizados; outro profissional não autorizado recebe recusa e os dados permanecem inalterados. Campos editáveis: a confirmar. | Proposto; RN01 |
| RF11 | Consultar um plano terapêutico e os treinos associados. | Profissional | A definir | UC11 | A consulta exibe o plano correto e seus treinos; sem treinos, apresenta estado vazio. Regra de acesso: a confirmar. | Proposto; levantamento AMDE |
| RF12 | Desativar plano terapêutico quando deixar de ser utilizado. | Profissional criador | A definir | UC12 | O responsável desativa o plano; ele deixa de aparecer como ativo e continua consultável como desativado. Outro usuário não autorizado não altera seu estado. | Proposto; RN02 |
| RF13 | Reativar plano terapêutico desativado. | Profissional criador | A definir | UC13 | O responsável reativa plano desativado e a consulta passa a identificá-lo como ativo; outros perfis não autorizados não alteram o estado. | Proposto; RN02 |
| RF14 | Cadastrar treino em um plano, com nome, categoria e tipo de medição entre frequência/repetição e duração. | Profissional | A definir | UC14 | Treino válido é associado ao plano selecionado e o tipo persistido corresponde à opção escolhida. Se categoria for obrigatória: a confirmar. | Proposto; levantamento AMDE |
| RF15 | Alterar dados permitidos de treino associado a plano sob responsabilidade do profissional. | Profissional responsável | A definir | UC15 | Após salvar, a consulta do plano apresenta o treino atualizado; outro profissional não autorizado não altera o registro. Definição de “responsável” para treino: confirmar se decorre do plano. | Proposto; levantamento AMDE |
| RF16 | Iniciar uma sessão para assistido e plano selecionados, registrando profissional autenticado, assistido e instante de início. | Profissional | A definir | UC16 | Uma sessão iniciada guarda os vínculos selecionados e instante de início gerado pelo sistema; não permite iniciar sem os vínculos obrigatórios confirmados. | Proposto; levantamento AMDE |
| RF17 | Configurar sessão com objetivo, plano de intervenção e treinos que serão realizados. | Profissional | A definir | UC16 | A sessão apresenta os dados selecionados antes da execução; os treinos escolhidos pertencem ao plano relacionado à sessão, se essa regra for confirmada. | Proposto; levantamento AMDE |
| RF18 | Selecionar e executar treinos da sessão, adicionar observações e avançar para outro treino ou encerrar a sessão. | Profissional | A definir | UC16 | O treino selecionado pertence à sessão; a observação salva é consultável; o usuário consegue retornar à lista de treinos da sessão. Fluxo de pausa/retomada: a confirmar. | Proposto; levantamento AMDE |
| RF19 | Registrar resultados por tipo de medição: contagens “sem ajuda”, “com ajuda” e “não executado” para frequência/repetição; cronômetro/medida de duração para tipo duração; score ao concluir o treino. | Profissional | A definir | UC16 | Os campos disponíveis correspondem ao tipo do treino; valores registrados são consultáveis na sessão. Unidade da duração, escala/cálculo do score e consistência entre score e contagens: a confirmar. | Proposto; levantamento AMDE |
| RF20 | Encerrar sessão, registrando instante de término, persistindo seus dados e calculando score da sessão a partir dos scores dos treinos. | Profissional | A definir | UC16 | Ao encerrar, a sessão recebe instante de término e seu score é igual à soma conforme regra RN04 aprovada; uma segunda finalização não duplica resultados. Escala, valores ausentes e arredondamento: a confirmar. | Proposto; levantamento AMDE / RN04 |
| RF21 | Consultar, a partir do perfil do assistido, o histórico de sessões realizadas com ele. | Profissional | A definir | UC17 | A lista contém sessões do assistido selecionado, com data e acesso aos detalhes; ordenação, filtros e alcance por profissional: a confirmar. | Proposto; levantamento AMDE |
| RF22 | Consultar os detalhes de sessão, incluindo profissional, assistido, treinos realizados, scores de treino/sessão e data. | Profissional | A definir | UC18 | A tela/documento identifica a sessão consultada e apresenta os dados persistidos disponíveis, sem substituir valores ausentes por zero. | Proposto; levantamento AMDE |
| RF23 | Corrigir sessão própria dentro de 24 horas após seu encerramento e recalcular score da sessão quando scores dos treinos mudarem. | Profissional autor da sessão | A definir | UC19 | Autor consegue salvar uma alteração válida antes do limite; outro profissional e o autor após o limite não alteram; score recalculado satisfaz RN04. O limite deve usar instante e fuso acordados. | Proposto; levantamento AMDE / RN03–RN04 |
| RF24 | Exportar em PDF os registros da sessão consultada. | Profissional autorizado | A definir | UC20 | PDF gerado corresponde à sessão selecionada, contém campos aprovados e não inclui dados de outras sessões; falha de geração deve ser informada sem perda do registro. Conteúdo/layout: a confirmar. | Proposto; levantamento AMDE |
| RF25 | **Opcional e pendente de decisão de escopo:** consultar registros anteriores de um treino para analisar sua evolução, possivelmente em tabela ou gráfico. | Profissional, se aprovado | A definir | UC21 (rascunho) | Somente após aprovação do escopo: selecionar assistido/treino e exibir registros existentes em ordem temporal; gráfico/tabela depende da decisão da equipe/AMDE. Métrica, filtros e interpretação: a confirmar. | Proposto opcional; não aprovado nem evidenciado como requisito fechado |

## Critérios para considerar a especificação consistente para a fase

1. Cada RF tem identificador estável, ator, comportamento observável, prioridade a definir, critério verificável, fonte e UC correspondente.
2. RF16–RF20 compõem o UC16 e continuam distinguíveis para teste e rastreabilidade.
3. RF25 fica explicitamente fora do escopo confirmado até que a equipe/AMDE decida mantê-lo; não deve ser apresentado como funcionalidade entregue.
4. A equipe valida em ata/registro os atores, permissões, prioridades e itens marcados “a confirmar”.
5. A rastreabilidade inversa verifica que toda função implementada relevante tem RF ou decisão de escopo registrada.

## Decisões que não devem ser preenchidas por suposição

- relação entre os perfis Administrador e Profissional e permissões de cada tela/rota;
- quais profissionais podem consultar quais assistidos;
- campos obrigatórios e política de identificação/duplicidade do assistido;
- escala do score, unidade de duração, cálculo para valores ausentes e arredondamento;
- fuso horário e instante inicial/final do prazo de 24 horas;
- conteúdo do PDF e adoção de gráficos/tabelas do RF25.

