# Casos de uso

O ator principal é o **profissional autenticado**. Os fluxos abaixo representam o comportamento atualmente disponível.

## UC-01 — Autenticar profissional

- **Precondição:** profissional cadastrado.
- **Fluxo principal:** informa e-mail e senha; a API valida as credenciais; o cliente armazena o token e abre a área autenticada.
- **Exceções:** credenciais inválidas ou API indisponível geram mensagem de erro.
- **Pós-condição:** requisições protegidas passam a enviar o JWT.

## UC-02 — Gerenciar paciente

- **Precondição:** autenticação válida.
- **Fluxo principal:** profissional consulta a lista, pesquisa pelo nome, abre o perfil e cadastra ou edita informações.
- **Alternativas:** lista vazia e pesquisa sem resultado apresentam orientação.
- **Exceções:** CPF duplicado ou falha da API impedem a gravação.

## UC-03 — Gerenciar plano e treinos

- **Precondição:** paciente existente.
- **Fluxo principal:** profissional cria um plano, informa nome e objetivo, adiciona treinos, categoria e tipo de medição.
- **Alternativas:** o criador pode desativar e posteriormente reativar o plano.
- **Exceções:** outro profissional não pode modificar o plano.

## UC-04 — Iniciar e configurar sessão

- **Precondições:** paciente com plano ativo; profissional autenticado.
- **Fluxo principal:** seleciona o plano, inicia a sessão, escolhe os treinos e confirma a configuração.
- **Alternativas:** no mobile, pode criar um treino durante a seleção.
- **Pós-condição:** sessão permanece aberta até o encerramento e pode ser retomada pelo responsável.

## UC-05 — Executar treino de frequência

- **Fluxo principal:** registra tentativas sem ajuda, com ajuda ou não executadas; pode desfazer a última tentativa; informa score inteiro e observação; encerra o treino.
- **Pós-condição:** registro é persistido e o score atualiza a soma da categoria.
- **Exceção:** o tipo do treino deve ser `FREQUENCIA`.

## UC-06 — Executar treino de duração

- **Fluxo principal:** inicia, pausa e retoma o cronômetro; informa score inteiro e observação; encerra o treino.
- **Pós-condição:** duração em segundos e resultado são persistidos.
- **Exceção:** o tipo do treino deve ser `DURACAO`.

## UC-07 — Encerrar sessão

- **Precondição:** sessão pertencente ao profissional.
- **Fluxo principal:** profissional revisa o atendimento, informa observação geral e score final manual e confirma o encerramento.
- **Pós-condição:** horário final é registrado; a sessão passa a integrar o histórico.
- **Regra:** o score final não é calculado pelos scores dos treinos.

## UC-08 — Consultar, editar e exportar sessão

- **Fluxo principal:** abre o histórico do paciente, consulta uma sessão e seus treinos e, no portal, solicita o PDF.
- **Alternativa:** o responsável edita dados enquanto a API considerar a sessão dentro da janela permitida.
- **Exceção:** a verificação atual usa dias corridos, embora a mensagem da API informe 24 horas.
