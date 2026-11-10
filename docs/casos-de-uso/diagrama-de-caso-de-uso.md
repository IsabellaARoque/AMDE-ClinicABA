# Diagrama de Casos de Uso — Sistema AMDE

> O diagrama a seguir apresenta as principais funcionalidades do Sistema AMDE e as interações dos atores com a aplicação. São representados os dois perfis de acesso: Administrador e Profissional, considerando suas respectivas responsabilidades e permissões.

---

### Figura – Diagrama de Casos de Uso Geral do Sistema AMDE

```mermaid
flowchart LR
    subgraph Sistema ["Sistema AMDE"]
        direction TB

        subgraph Usuarios ["Usuários"]
            UC01(["UC01<br/>Cadastrar profissional"])
            UC02(["UC02<br/>Autenticar profissional"])
            UC03(["UC03<br/>Visualizar Perfil de profissional"])
            UC04(["UC04<br/>Editar profissional"])
        end

        subgraph Assistidos ["Assistidos"]
            UC05(["UC05<br/>Cadastrar assistidos"])
            UC06(["UC06<br/>Editar assistidos"])
            UC07(["UC07<br/>Visualizar assistidos"])
            UC08(["UC08<br/>Visualizar Perfil de Assistido"])
        end

        subgraph Planos ["Planos e Treinos"]
            UC09(["UC09<br/>Criar plano terapêutico"])
            UC10(["UC10<br/>Alterar plano terapêutico"])
            UC11(["UC11<br/>Visualizar Plano Terapêutico do Assistido"])
            UC12(["UC12<br/>Desativação do plano terapêutico do assistido"])
            UC13(["UC13<br/>Reativação do plano terapêutico do assistido"])
            UC14(["UC14<br/>Cadastrar treino"])
            UC15(["UC15<br/>Alterar treino"])
        end

        subgraph Sessoes ["Sessões"]
            UC16(["UC16<br/>Configuração e Execução da Sessão"])
            UC17(["UC17<br/>Histórico de sessões"])
            UC18(["UC18<br/>Visualizar sessão"])
            UC19(["UC19<br/>Editar sessão"])
            UC20(["UC20<br/>Exportar sessão"])
            UC21(["UC21<br/>Consulta e Análise de treinos"])
        end
    end

    Administrador["Administrador"]
    Profissional["Profissional"]

    %% Herança entre atores
    Profissional --> Administrador

    %% Administrador
    Administrador --> UC01
    Administrador --> UC02
    Administrador --> UC03
    Administrador --> UC04
    Administrador --> UC05
    Administrador --> UC06

    %% Profissional
    Profissional --> UC07
    Profissional --> UC08
    Profissional --> UC09
    Profissional --> UC10
    Profissional --> UC11
    Profissional --> UC12
    Profissional --> UC13
    Profissional --> UC14
    Profissional --> UC15
    Profissional --> UC16
    Profissional --> UC17
    Profissional --> UC18
    Profissional --> UC19
    Profissional --> UC20
    Profissional --> UC21

    %% Relacionamentos de extensão
    UC02 -.->|extend| UC03
    UC12 -.->|extend| UC13
    UC07 -.->|extend| UC08
    UC17 -.->|extend| UC18
    UC17 -.->|extend| UC20
    UC17 -.->|extend| UC21

    %% Cores
    classDef usuarios fill:#8dcc83,stroke:#548b50,color:#000
    classDef assistidos fill:#9bd5f0,stroke:#398bb5,color:#000
    classDef planos fill:#fff0a3,stroke:#d4b94b,color:#000
    classDef sessoes fill:#c5b4e5,stroke:#8064aa,color:#000

    class UC01,UC02,UC03,UC04 usuarios
    class UC05,UC06,UC07,UC08 assistidos
    class UC09,UC10,UC11,UC12,UC13,UC14,UC15 planos
    class UC16,UC17,UC18,UC19,UC20,UC21 sessoes
```

<div align="center">
<sub><b>Fonte:</b> Elaborado pelos autores.</sub>
</div>

### Descrição Sucinta das Funcionalidades do Diagrama

- **Cadastrar Profissional:** Permite ao administrador cadastrar profissionais para utilização do sistema.
- **Autenticar Profissional:** Permite que profissionais cadastrados realizem a autenticação e acessem as funcionalidades disponíveis conforme suas permissões.
- **Visualizar Perfil de Profissional:** Permite ao profissional consultar suas informações cadastrais.
- **Editar Profissional:** Permite ao profissional visualizar e alterar seus próprios dados cadastrais.
- **Cadastrar Assistido:** Permite ao administrador registrar novos assistidos, incluindo informações pessoais, dados de atendimento e informações do responsável.
- **Editar Assistido:** Permite ao administrador atualizar as informações cadastrais dos assistidos.
- **Visualizar Assistidos:** Permite ao profissional consultar a lista de assistidos disponíveis para acompanhamento.
- **Visualizar Perfil de Assistido:** Permite ao profissional consultar informações gerais, scores, planos terapêuticos e histórico de sessões de determinado assistido.
- **Criar Plano Terapêutico:** Permite ao profissional criar um plano de intervenção associado a um assistido, definindo seu nome e objetivo.
- **Alterar Plano Terapêutico:** Permite ao profissional responsável atualizar as informações de um plano terapêutico.
- **Visualizar Plano Terapêutico:** Permite consultar as informações de um plano e os treinos associados.
- **Desativar Plano Terapêutico:** Permite ao profissional responsável desativar um plano que não esteja mais em utilização.
- **Reativar Plano Terapêutico:** Permite ao profissional responsável reativar um plano anteriormente desativado.
- **Cadastrar Treino:** Permite cadastrar treinos associados a um plano terapêutico, definindo suas características e o tipo de medição.
- **Alterar Treino:** Permite atualizar as informações de um treino cadastrado.
- **Configurar e Executar Sessão:** Permite ao profissional iniciar uma sessão, selecionar o plano e os treinos que serão realizados e registrar os resultados das atividades.
- **Visualizar Histórico de Sessões:** Permite consultar as sessões realizadas com determinado assistido.
- **Visualizar Sessão:** Permite consultar os detalhes de uma sessão, incluindo treinos executados, resultados e scores.
- **Editar Sessão:** Permite ao profissional corrigir informações de sessões próprias dentro do período de edição estabelecido.
- **Exportar Sessão:** Permite gerar arquivos PDF contendo os registros de uma sessão.

> **Observação:** O Profissional também possui as funcionalidades administrativas atribuídas ao Administrador, conforme a definição dos atores do sistema.