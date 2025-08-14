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
    uses: cumbucadev/shared-workflows/.github/workflows/<workflow>/<version>/<nome-do-workflow.yml>@main
```

Substituindo <nome-do-workflow.yml> pelo arquivo desejado.

Exemplo real de uso:

```yml
jobs:
  exemplo:
    uses: cumbucadev/shared-workflows/.github/workflows/semantic-pull-request/v1/semantic-pull-request.yml@main
```

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
