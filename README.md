<div align="center">
  <picture>
    <source
      media="(prefers-color-scheme: dark)"
      srcset="https://github.com/cumbucadev/design/raw/main/images/logo-dark-transparent.png"
    >
    <img
      alt="Logo do Cumbuca Dev"
      src="https://github.com/cumbucadev/design/raw/main/images/logo-light-transparent.png"
      width="20%"
    >
  </picture>
</div>

# Shared Workflows

[English Version](/README_EN.md)

Repositório central com **workflows reutilizáveis** do GitHub Actions para os repositórios da
organização.

- [Shared Workflows](#shared-workflows)
  - [O que tem aqui?](#o-que-tem-aqui)
  - [Como usar em outros repositórios](#como-usar-em-outros-repositórios)
  - [Catálogo](#catálogo)
    - [autoassign-issue](#autoassign-issue)
    - [close-stale-issues](#close-stale-issues)
    - [validate-pr-title](#validate-pr-title)
  - [💬 Novos Funcionalidades e Reportar Bugs](#-novos-funcionalidades-e-reportar-bugs)
  - [💡 Dúvidas? Ideias?](#-dúvidas-ideias)
  - [💻 Contribuindo com o Código do Projeto](#-contribuindo-com-o-código-do-projeto)
  - [❤️ Quem já Contribuiu](#-quem-já-contribuiu)

## O que tem aqui?

Este repositório armazena workflows padronizados que podem ser utilizados em outros repositórios da
organização por meio do recurso
[`workflow_call`](https://docs.github.com/pt/actions/using-workflows/reusing-workflows).

Aqui você encontra:

- Workflows de CI/CD padronizados
- Fluxos de automação para testes, build e deploy
- Convenções compartilhadas entre projetos

## Como usar em outros repositórios

Você pode reutilizar workflows deste repositório em outros projetos adicionando um trecho como o
exemplo abaixo no seu arquivo `.github/workflows/<nome>.yml`:

```yml
permissions: <permissões>

jobs:
  exemplo:
    uses: cumbucadev/shared-workflows/.github/workflows/<nome-do-workflow.yml>@main
```

Substituindo `<permissões>` pelas permissões necessárias e `<nome-do-workflow.yml>` pelo arquivo
desejado.

Exemplo real de uso:

```yml
permissions:
  pull-requests: write

jobs:
  exemplo:
    uses: cumbucadev/shared-workflows/.github/workflows/validate-pr-title-v1.yml@main
```

## Catálogo

Abaixo estão os workflows compartilhados atualmente usados na organização Cumbuca. Fazemos o
versionamento **pela major no nome do arquivo** (ex.: `-v1`, `-v2`). Veja o changelog para mudanças
quebráveis e notas de migração.

### autoassign-issue

#### Descrição

Este workflow atribui automaticamente uma issue a um usuário quando ele comenta uma **palavra-chave específica** na issue.
O comentário funciona como um gatilho de “quero assumir esta issue”, tornando o processo de autoatribuição simples, rápido e transparente.
Além disso, o workflow publica um comentário bilíngue (português + inglês) confirmando que a issue foi atribuída ao usuário.

#### Gatilhos

- `issue_comment` (created)

#### Palavras-chave (triggers)

- `"bora"`, `"bora!"`, `"dibs"`, `"dibs!"`
  _(case-insensitive — qualquer variação de maiúsculas/minúsculas é aceita)_

#### Resumo de comportamento

- Quando alguém comenta uma das palavras-chave em uma issue aberta:
  - A issue é automaticamente atribuída a esse usuário
  - Um comentário bilíngue é publicado confirmando a atribuição e incluindo link para o guia de contribuição
- Facilita o processo de contribuição, evitando trabalho manual de manutenção de assignees e melhorando a visibilidade de quem está trabalhando em cada issue

#### Changelog

- **v1** — Lançamento inicial
  - Implementa autoassign para comentários com palavras-chave específicas
  - Palavras-chave suportadas: `"bora"`, `"bora!"`, `"dibs"`, `"dibs!"`
  - Inclui comentário de confirmação bilíngue (PT-BR + EN)

### close-stale-issues

#### Descrição

Este workflow identifica automaticamente issues e pull requests inativos e os marca como “stale” após um período sem 
atividade. Caso não haja interação após a marcação, eles são fechados automaticamente. Todas as mensagens são bilíngues
(português + inglês) para facilitar a comunicação com colaboradores.

#### Gatilhos

- `schedule` (cron: `00 4 * * *`)
- `workflow_dispatch` (execução manual)

#### Mensagens

- Mensagem para issue marcada como stale:
  - Explica que a issue ficou 45 dias sem atividade e será fechada em 15 dias se não houver interação
  - Bilíngue (PT-BR + EN)

- Mensagem para PR marcado como stale:
  - Explica que o PR ficou 30 dias sem atividade e será fechado em 15 dias se não houver interação
  - Bilíngue (PT-BR + EN)

- Mensagem ao fechar issue:
  - Resume a linha do tempo: marcada como inativa após 45 dias, fechada após 15 dias adicionais
  - Fornece próximos passos (reabrir, atualizar contexto, criar nova issue se necessário)
  - Bilíngue (PT-BR + EN)

- Mensagem ao fechar PR:
  - Resume a linha do tempo: marcado como inativo após 30 dias, fechado após 15 dias adicionais
  - Fornece próximos passos (reabrir, resolver revisões, rebase/merge com a main)
  - Bilíngue (PT-BR + EN)

#### Resumo de comportamento

- A cada dia às 04:00 (UTC no cron `00 4 * * *`), o workflow avalia issues e PRs:
  - Issues: marcadas como stale após 45 dias sem atividade; fechadas após 15 dias adicionais (mensagens bilíngues)
  - PRs: marcados como stale após 30 dias sem atividade; fechados após 15 dias adicionais (mensagens bilíngues)
- Pode ser executado manualmente via `workflow_dispatch`
- Publica comentários claros com instruções do que fazer para manter aberto (remover label de stale ou comentar)

#### Changelog

- **v1** — Lançamento inicial
  - Implementa marcação automática de inatividade (stale) para issues (45 dias) e PRs (30 dias)
  - Fecha automaticamente após 15 dias adicionais sem resposta
  - Inclui mensagens bilíngues para marcação e fechamento de issues/PRs
  - Agendamento diário via cron e suporte a execução manual

### validate-pr-title

#### Descrição

Garante que os títulos dos pull requests sigam a especificação do
[Conventional Commits](https://www.conventionalcommits.org/pt-br/v1.0.0/).
Se o título não estiver no formato esperado, o workflow publica um comentário bilíngue (português +
inglês) explicando o problema, dando exemplos de prefixos válidos e incluindo links para a
documentação oficial. Assim que o título for corrigido, o comentário é removido automaticamente.

#### Gatilhos

- `workflow_call`
- `pull_request` (opened, edited, reopened)

#### Resumo de comportamento

- Valida os títulos de PRs contra uma lista permitida de tipos do Conventional Commits:
  - `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`, `revert`, `style`, `test`
- Se inválido:
  - Falha o check
  - Publica um comentário fixo com contexto, exemplos e links em PT-BR e EN
- Se válido:
  - Remove qualquer comentário de erro anterior
- Ajuda a manter o histórico do projeto limpo e padronizado, facilitando automações
  (ex.: changelogs, releases)

#### Changelog

- **v1** — Lançamento inicial.
  - Aplica os tipos permitidos do Conventional Commits (`chore`, `ci`, `docs`, `feat`, `fix`,
    `refactor`, `style`, `test`)
  - Inclui orientação bilíngue para contribuintes quando o título é inválido
  - Remove automaticamente comentários de orientação quando o título é corrigido

## 💬 Novos Funcionalidades e Reportar Bugs

Caso queira sugerir novas funcionalidades ou reportar bugs, basta criar
uma nova [issue][github-issues] e iremos lhe responder por lá!

(Para saber mais sobre github issues, confira a
[documentação oficial do GitHub][github-issues-doc]).

## 💡 Dúvidas? Ideias?

Dúvidas de como utilizar a biblioteca? Novas ideias para o projeto? Quer compartilhar algo com a
gente? Fique à vontade para criar um tópico no nosso [Discussions][github-discussions] que iremos
interagir por lá!

(Para saber mais sobre github discussions, confira a
[documentação oficial do GitHub][github-discussions-doc]).

## 💻 Contribuindo com o Código do Projeto

Sua colaboração é sempre muito bem-vinda! Para facilitar seus primeiros passos, preparamos os seguintes arquivos:

- [CONTRIBUTING.md](/CONTRIBUTING.md): Aqui você encontrará todas as instruções necessárias para contribuir com o projeto.
- [CONTRIBUTING_EN.md](/CONTRIBUTING_EN.md): Versão em inglês das diretrizes de contribuição.
- [CODE_OF_CONDUCT.md](/CODE_OF_CONDUCT.md): Nosso código de conduta, que define as expectativas para interações respeitosas e inclusivas dentro da comunidade.
- [CODE_OF_CONDUCT_EN.md](/CODE_OF_CONDUCT_EN.md): Versão em inglês do código de conduta.
- [CORE_TEAM.md](/CORE_TEAM.md): Lista e apresenta informações sobre as pessoas integrantes do time principal do projeto, incluindo suas funções e formas de contato.
- [CORE_TEAM_EN.md](CORE_TEAM_EN.md): Versão em inglês da lista e informações sobre o time principal do projeto.
- [LICENSE.md](/LICENSE.md): Detalhes sobre a licença do projeto. Ela define o que você pode e não pode fazer com o código. Em geral, a licença permite que você use, modifique e distribua o código, desde que siga os termos definidos. No entanto, é importante verificar se há restrições específicas, como atribuição de crédito ao autor original ou proibição de uso comercial.

Certifique-se de ler esses arquivos com atenção antes de contribuir. Se tiver qualquer dificuldade ou dúvida, não hesite em nos perguntar utilizando o [GitHub Discussions][github-discussions]. Toda ajuda conta!

## ❤️ Quem já Contribuiu

<a href="https://github.com/cumbucadev/shared-workflows/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=cumbucadev/shared-workflows" />
</a></br></br>

_Made with [contrib.rocks](https://contrib.rocks)._

[github-discussions-doc]: https://docs.github.com/pt/discussions
[github-discussions]: https://github.com/cumbucadev/shared-workflows/discussions
[github-issues-doc]: https://docs.github.com/pt/issues/tracking-your-work-with-issues/creating-an-issue
[github-issues]: https://github.com/cumbucadev/shared-workflows/issues
