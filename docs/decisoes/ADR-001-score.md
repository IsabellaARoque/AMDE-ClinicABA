# ADR-001 — Tratamento dos scores

**Estado:** aceita em 2026-11-03.

## Contexto

O domínio não define score como porcentagem e a clínica é responsável por avaliá-lo. Ao mesmo tempo, os resultados dos treinos precisam compor um acumulado por categoria.

## Decisão

- Score de treino é inteiro manual, inclusive zero e valores maiores que 100.
- Scores dos treinos são somados somente por categoria.
- Ao alterar um treino, a API aplica a diferença entre o valor novo e o anterior.
- Score final da sessão é inteiro manual e independente.
- Nenhuma interface calcula automaticamente uma avaliação clínica.

## Consequências

Interfaces não exibem `%` nem impõem faixa clínica arbitrária. `ScorePorCategoria.valor` permanece `Double` por compatibilidade com o modelo legado e deve ser revisto em uma migração futura.
