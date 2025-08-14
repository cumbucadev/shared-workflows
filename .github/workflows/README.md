# Workflows

[English Version](/.github/workflows/README_EN.md)

Tabela de Conteúdos
- [Como funciona nosso versionamento de workflows](#como-funciona-nosso-versionamento-de-workflows)
  * [Ao adicionar ou atualizar um workflow](#ao-adicionar-ou-atualizar-um-workflow)
  * [Por que versionamos assim](#por-que-versionamos-assim)

## Como funciona nosso versionamento de workflows

Versionamos workflows compartilhados **incluindo a major no nome do arquivo**, por exemplo:

```yml
.github/workflows/semantic-pull-request-v1.yml
.github/workflows/python-lint-v1.yml
```

Trabalhamos **apenas com versões major** aqui:
- `-v1`, `-v2`… indicam a **major**.
- Criamos uma **nova major apenas para mudanças quebráveis** (alterações em inputs/secrets
  obrigatórios, triggers ou comportamento).
- Correções não quebráveis permanecem no mesmo arquivo/major — sem necessidade de renomear.
- Mantemos a major anterior por um **período de transição**, depois removemos quando todos os
  consumidores tiverem migrado.

### Ao adicionar ou atualizar um workflow

1. Se a mudança é **retrocompatível** → atualize o arquivo existente.
2. Se a mudança é **quebrável** → copie o arquivo, incremente o sufixo (`-v1` → `-v2`) e edite o novo.
3. Atualize a documentação e qualquer chamada de “reusable workflow” para apontar para a **nova major**.
4. Mantenha a major anterior até que todos os repositórios tenham migrado.

### Por que versionamos assim

1. **Workflows do GitHub não têm versionamento embutido**
Workflows são arquivos YAML no repositório. Não há forma nativa de fixar/controlar múltiplas
versões; incluir a **major no nome do arquivo** deixa o contrato explícito para todos os
repositórios.

2. **Pastas aninhadas não são permitidas para workflows**
O GitHub só reconhece arquivos diretamente em `.github/workflows`. Se você colocar um arquivo em
`./github/workflows/python-lint/v1/lint.yml`, ele não será executado. “Simulamos” uma estrutura
colocando a **versão no nome do arquivo**.

3. **Segurança durante migrações entre múltiplos repositórios**
Como esses workflows são compartilhados por **vários repositórios da organização Cumbuca**, a
coexistência de majors nos permite:
- Implementar atualizações gradualmente, repositório por repositório.
- Fazer rollback instantâneo se necessário.
- Ver facilmente (na interface do Actions e no nome do arquivo) qual major foi usada em uma
  execução.
