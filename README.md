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

Para reutilizar um workflow deste repositório, adicione algo como o exemplo abaixo no repositório
desejado:

```yml
jobs:
  exemplo:
    uses: cumbucadev/shared-workflows/.github/workflows/<nome-do-workflow.yml>@main
```

Substituindo <nome-do-workflow.yml> pelo arquivo desejado.

Exemplo real de uso:

```yml
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
