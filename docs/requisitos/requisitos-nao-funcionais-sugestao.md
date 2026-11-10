# Requisitos Não Funcionais — Sistema AMDE (sugestão)

> **Documento de trabalho, não aprovado.** As metas abaixo tornam verificáveis as necessidades descritas na especificação existente. Números e cenários marcados como propostos precisam ser confirmados pela equipe e pela AMDE antes de virarem critérios de aceite. Não altera `especificacao_requisitos_AMDE.md`.

- **Projeto:** ClinicABA — Sistema AMDE
- **Versão da sugestão:** 1.0
- **Data:** 03/11/2026
- **Base:** RNF01–RNF10 da especificação versionada e necessidades explícitas de proteção, integridade, usabilidade e desempenho.

## Requisitos

| ID | Atributo | Requisito mensurável proposto | Verificação reproduzível | Rastreio / prioridade / estado |
|---|---|---|---|---|
| RNF01 | Desempenho | Em ambiente de teste acordado, pelo menos 95% das operações representativas de consulta e gravação devem responder em até 4 s, excluindo indisponibilidade externa que seja registrada separadamente. | Registrar ambiente, versão, conexão, conjunto de operações, número de execuções e percentis medidos; comparar o percentil 95 com 4 s. O volume e o ambiente ainda precisam de validação. | RF01–RF24 conforme fluxo; prioridade a definir; meta inicial proposta |
| RNF02 | Usabilidade mobile | Em tarefas principais de sessão definidas com profissionais, cada participante deve conseguir localizar e iniciar a tarefa em até 3 interações a partir da tela inicial, sem ajuda do observador. | Roteiro de tarefas, perfil dos participantes, contagem de interações, erros e observações; a equipe/AMDE define tarefas e público antes do teste. | RF16–RF20 / UC16; prioridade a definir; meta proposta |
| RNF03 | Eficiência de interação | Para um cenário padrão de registro acordado, a quantidade de ações do profissional até salvar o resultado não deve exceder 5, sem contar o preenchimento de valores específicos da atividade. | Definir começo/fim e o que conta como ação; observar cenário com dados fictícios e registrar contagem por tarefa. Se houver conflito com RNF02, manter os dois critérios separados: facilidade de localizar versus quantidade de ações. | RF16–RF20 / UC16; prioridade a definir; meta proposta |
| RNF04 | Autenticação e autorização | Toda operação protegida deve exigir identidade autenticada e aplicar autorização no servidor/API, além de ocultar ações não permitidas na interface. Tentativas sem autenticação ou sem permissão não podem alterar nem consultar dado protegido. | Matriz de perfis/recursos aprovada; testar cada permissão permitida e negada pela interface e diretamente na API. A cobertura de cenários deve ser 100% da matriz acordada; não publicar credenciais reais nos registros. | RF01–RF24; RN01–RN03, RNF05 e RNF10; prioridade alta proposta, aprovar com a equipe |
| RNF05 | Integridade/autoria de sessão | Somente o profissional que criou/realizou a sessão pode alterá-la e somente até 24 horas após o encerramento, conforme a regra aprovada. A verificação deve ocorrer no servidor, usando instante inequívoco. | Testar autor antes do limite, autor no/ após o limite, outro profissional antes do limite e sessão ainda aberta. Usar fuso/relógio de teste controlado. Definir tratamento exato do instante-limite com a AMDE. | RF23 / UC19; RN03; prioridade alta proposta |
| RNF06 | Integridade e recuperação | Uma gravação confirmada deve permanecer consistente após nova consulta; repetição de uma solicitação por falha de rede não deve duplicar sessão/resultado. Falha parcial não deve deixar sessão com vínculos ou scores contraditórios. | Testes de gravação, consulta, falha/repetição e rollback em ambiente descartável com dados sintéticos. Definir backup, retenção e objetivos de recuperação (RPO/RTO) antes de alegar recuperação operacional. | RF16–RF20, RF23; RN04; prioridade alta proposta |
| RNF07 | Capacidade/desempenho | A meta inicial de capacidade é manter RNF01 com uma massa de referência de até 100 assistidos e 10.000 registros de sessão. Esses volumes são hipóteses e não representam demanda confirmada da AMDE. | Validar os volumes com a AMDE; gerar massa sintética; registrar configuração do ambiente, duração, concorrência, erros e tempos. Não executar carga em serviço ou base do cliente. | RF07–RF24; prioridade a definir; meta inicial proposta |
| RNF08 | Unicidade de cadastro | O sistema deve rejeitar duplicidade conforme identificador aprovado para cada entidade. Para assistido, CPF foi citado no levantamento, mas o uso e a regra de unicidade precisam de validação institucional e de privacidade. | Testar mesmo identificador, identificador formatado de formas equivalentes, dados incompletos e concorrência de dois cadastros. A regra de normalização e mensagens deve ser acordada. | RF01, RF05; prioridade alta proposta |
| RNF09 | Ciclo de vida e consistência de estado | Planos ativos e desativados devem ser distinguíveis; registros desativados permanecem consultáveis quando o fluxo prevê histórico e não devem aparecer como ativos em listas de seleção. | Verificar listagem ativa, consulta histórica e tentativa de uso de plano desativado; conferir estado persistido e resposta em cada fluxo. Confirmar se treino/assistido também possui ciclo de vida equivalente. | RF08, RF11–RF13; RN02; prioridade a definir |
| RNF10 | Autorização sobre plano terapêutico | Somente o profissional responsável pela criação do plano pode alterá-lo, desativá-lo ou reativá-lo, se essa regra for confirmada pela AMDE. A proteção deve ser aplicada no backend/API. | Criar plano com usuário A e testar operações de A e B via interface e chamadas à API; confirmar que recusas não alteram estado e deixam registro de auditoria conforme política aprovada. | RF10, RF12, RF13; RN01–RN02; prioridade alta proposta |

## Matriz de verificação sugerida

| ID RNF | Evidência necessária para aceite | Resultado na entrega atual |
|---|---|---|
| RNF01 | Relatório de medição com ambiente, massa, operações e percentis | Não evidenciado nesta revisão; meta aguarda validação |
| RNF02–RNF03 | Roteiro com profissionais, tarefas e contagem/observações | Não localizado como resultado executado; plano e participantes a definir |
| RNF04–RNF05, RNF10 | Matriz de permissões e testes negativos no backend/API | Não considerar concluído apenas pela existência de autenticação ou ocultação de botão; validar por rota e perfil |
| RNF06–RNF08 | Cenários de persistência, repetição, recuperação e unicidade | Não evidenciado como resultado executado; usar ambiente descartável e dados fictícios |
| RNF09 | Testes dos estados ativo/inativo e consulta de histórico | Regra descrita em requisitos; resultados de teste não evidenciados nesta sugestão |

## Critérios de conclusão do C3

- A AMDE/equipe valida metas, população, ambiente, volumes, perfis e exceções; alterações ficam registradas com versão e data.
- Cada RNF permanece independente, testável e ligado a RF/UC (ou possui justificativa de rastreio alternativo).
- O plano de testes identifica método, dados sintéticos, resultado esperado, resultado observado e commit testado.
- Metas ainda não validadas continuam rotuladas **propostas**, não sendo usadas como promessa contratual ou resultado alcançado.
- Requisitos de segurança e dados pessoais são avaliados apenas em ambiente autorizado; não usar informações reais nos testes ou exemplos.

