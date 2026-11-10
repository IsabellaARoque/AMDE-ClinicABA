# Diagrama de Classes de Domínio — Sistema AMDE

> O diagrama de classes representa a estrutura estática do sistema ClinicABA, apresentando as principais entidades do domínio, seus atributos, operações, relacionamentos e multiplicidades. O modelo contempla o gerenciamento de profissionais, salas, assistidos, planos de intervenção, sessões e treinos, além das diferentes formas de registro de execução das atividades terapêuticas.

> **Referência no Template Fatec ADS:**
> Exigido no Capítulo 2.5 (*"Diagramas — Caso de Uso, DER, Diagramas de Classes"*). No texto acadêmico, o diagrama deve ser precedido por sua contextualização conceitual e seguido da explicação das principais classes de domínio e suas responsabilidades.


# Descrição das Classes e Responsabilidades
- **Classe `Sala`:** Representa as salas utilizadas nos atendimentos da AMDE. Armazena sua identificação e numeração, permitindo o cadastro e a alteração de informações. Relaciona-se aos profissionais e aos assistidos vinculados à respectiva sala.

- **Classe `Profissional`:** Representa os profissionais responsáveis pela utilização do sistema e pelo acompanhamento terapêutico dos assistidos. Armazena informações de identificação, credenciais de acesso e permissões. Disponibiliza operações de cadastro, autenticação e gerenciamento do próprio perfil, além de relacionar-se aos assistidos, sessões e planos de intervenção.

- **Classe `Assistido`:** Representa as pessoas atendidas pela AMDE. Armazena informações pessoais, dados de identificação, convênio, frequência de atendimento e informações do responsável. Permite o cadastro, a edição, a consulta e a visualização do perfil do assistido.

- **Classe `PlanoDeIntervencao`:** Representa o planejamento terapêutico associado a um assistido. Armazena nome, objetivo, data de criação e situação do plano, permitindo sua criação, alteração, visualização, desativação e reativação. Também estabelece a associação entre os planos e os treinos que serão realizados.

- **Classe `Sessao`:** Representa um atendimento realizado por um profissional com determinado assistido. Armazena informações como objetivo, data, horário de início e score. É responsável pelas operações de início, configuração, encerramento, edição, visualização e exportação dos registros em PDF.

- **Classe `Treino`:** Representa uma atividade terapêutica cadastrada em um plano de intervenção. Contém informações como nome, categoria, objetivo, tipo de medição e atividade. Permite o cadastro, a alteração e a consulta dos treinos disponíveis.

- **Classe `Categoria`:** Representa a classificação dos treinos cadastrados no sistema. Armazena a identificação e o nome da categoria, permitindo seu cadastro e sua edição. Cada treino está associado a uma categoria.

- **Classe `TreinoSessao`:** Representa a execução de um treino dentro de uma sessão específica. Armazena o score obtido e as observações referentes à execução, além de disponibilizar operações para iniciar, executar, registrar resultados e encerrar o treino. É uma classe especializada em registrar a ocorrência de um treino em determinada sessão.

- **Classe `RegTreinoFrequencia`:** Especialização da classe `TreinoSessao`, responsável pelo registro dos resultados de treinos cujo tipo de medição é frequência/repetição. Armazena a quantidade de execuções realizadas sem ajuda, com ajuda e não executadas.

- **Classe `RegTreinoDuracao`:** Especialização da classe `TreinoSessao`, responsável pelo registro dos resultados de treinos cujo tipo de medição é duração. Armazena o tempo registrado durante a execução da atividade.

---

### Figura – Diagrama de Classes de Domínio do Sistema ClinicABA

```mermaid
classDiagram
    class Sala {
        -Long id
        -int numero
        +criar() void
        +alterar() void
    }

    class Profissional {
        -Long id
        -string cpf
        -string nome
        -string email
        -string senha
        -string permissao
        +cadastrar() void
        +autenticar(string senha) boolean
        +visualizarPerfil() void
        +editarPerfil() void
    }

    class Assistido {
        -Long cpf
        -string nome
        -date dataNascimento
        -string convenio
        -string frequencia
        -string nomeResponsavel
        -string telResponsavel
        +cadastrar() void
        +editar() void
        +visualizarPerfil() Assistido
        +buscar() Assistido
    }

    class PlanoDeIntervencao {
        -Long id
        -string nome
        -string objetivo
        -date dataCriacao
        -boolean status
        +criar() void
        +alterar() void
        +desativar() void
        +reativar() void
        +visualizar() void
        +buscarPorId() void
    }

    class Sessao {
        -Long id
        -string objetivo
        -date data
        -time horarioInicio
        -int score
        +iniciar() void
        +configurar() void
        +encerrar() void
        +editar(string objetivo) void
        +exportarPDF() void
        +visualizar() void
    }

    class Treino {
        -Long id
        -string nome
        -string categoria
        -string objetivo
        -string tipoMedicao
        -string atividade
        +criar() void
        +alterar() void
        +visualizar() void
        +buscarPorId() void
    }

    class Categoria {
        -Long idCategoria
        -string nome
        +cadastrar() void
        +editar() void
    }

    class TreinoSessao {
        -Long id
        -int score
        -string observacao
        +executarTreino() void
        +registrarScore(int score) void
        +iniciarTreinoSessao() void
        +encerrarTreinoSessao() void
    }

    class RegTreinoFrequencia {
        -Long idExecFreq
        -int execucoesSemAjuda
        -int execucoesComAjuda
        -int naoExecutados
        +registrarFrequencia() void
    }

    class RegTreinoDuracao {
        -Long idExecDuracao
        -time duracao
        +registrarDuracao() void
    }

    Sala "1" -- "1" Profissional : vinculada
    Sala "1" -- "0..*" Assistido : organiza
    Profissional "1" -- "0..*" Assistido : acompanha
    Profissional "1" -- "0..*" Sessao : realiza
    Profissional "1" -- "0..*" PlanoDeIntervencao : cria
    PlanoDeIntervencao "1" -- "0..*" Sessao : vincula
    PlanoDeIntervencao "1" -- "0..*" Treino : contém
    Treino "0..*" -- "1" Categoria : pertence
    Sessao "1" -- "0..*" TreinoSessao : registra
    Treino "1" -- "0..*" TreinoSessao : executado em
    TreinoSessao <|-- RegTreinoFrequencia
    TreinoSessao <|-- RegTreinoDuracao

    