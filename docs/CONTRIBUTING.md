# Contribuindo com o TELUME Backend

Este documento define o fluxo inicial de branches, commits e Pull Requests do repositório.

O projeto utiliza um fluxo simplificado baseado em `main`, `dev` e branches temporárias. Não adotamos, neste momento, o Git Flow completo com branches de release.

## Branches permanentes

### `main`

Contém somente versões estáveis do backend.

- Não recebe commits diretos.
- Recebe alterações por Pull Request.
- Normalmente recebe merges vindos de `dev`.
- Deve permanecer protegida contra exclusão e force push.

### `dev`

É a branch de integração do desenvolvimento.

- Não deve receber commits diretos após o bootstrap inicial.
- Recebe Pull Requests das branches temporárias.
- Deve conter as alterações que farão parte da próxima versão estável.

## Branches temporárias

Cada trabalho deve começar a partir da `dev`.

| Prefixo     | Uso                                      | Exemplo                     |
| ----------- | ---------------------------------------- | --------------------------- |
| `feature/`  | Nova funcionalidade                      | `feature/authentication`    |
| `fix/`      | Correção de defeito                      | `fix/invalid-email`         |
| `chore/`    | Configuração ou manutenção               | `chore/update-dependencies` |
| `docs/`     | Alterações de documentação               | `docs/setup-guide`          |
| `refactor/` | Refatoração sem mudança de comportamento | `refactor/user-service`     |
| `test/`     | Criação ou manutenção de testes          | `test/authentication`       |
| `ci/`       | Integração e automação                   | `ci/backend-validation`     |

Utilize nomes curtos, descritivos, em minúsculas e separados por hífen.

## Iniciando um trabalho

Atualize a `dev` local:

```bash
git switch dev
git pull --ff-only origin dev
```

Crie uma branch apropriada:

```bash
git switch -c feature/nome-da-feature
```

## Commits

Os commits devem ser pequenos, objetivos e relacionados a um único propósito.

Formato recomendado:

```text
tipo: descrição curta
```

Tipos utilizados:

- `feat`: nova funcionalidade;
- `fix`: correção;
- `docs`: documentação;
- `chore`: configuração ou manutenção;
- `refactor`: refatoração;
- `test`: testes;
- `ci`: integração contínua.

Exemplos:

```text
feat: add user registration
fix: validate duplicate email
docs: document local setup
chore: bootstrap repository
```

## Pull Requests

O destino normal das branches temporárias é a `dev`:

```text
feature/*  ─┐
fix/*      ─┤
chore/*    ─┼─> dev ─> main
docs/*     ─┤
refactor/* ─┘
```

Não abra uma Pull Request de uma branch temporária diretamente para `main`.

Uma Pull Request de `dev` para `main` representa a promoção de uma versão considerada estável.

## Antes de abrir uma Pull Request

- Atualize sua branch com a branch de destino.
- Verifique se a alteração possui um único objetivo.
- Execute os comandos de validação disponíveis no projeto.
- Atualize `package-lock.json` quando alterar dependências.
- Não inclua arquivos `.env`, credenciais ou outros dados sensíveis.
- Atualize a documentação quando necessário.
- Revise o próprio diff antes de solicitar revisão.

## Título da Pull Request

Utilize o mesmo padrão dos commits:

```text
tipo: descrição curta
```

Exemplo:

```text
feat: add user authentication
```

## Revisão e merge

- Toda Pull Request deve receber pelo menos uma aprovação.
- Todas as conversas da revisão devem ser resolvidas.
- Quando a integração contínua estiver configurada, suas verificações deverão passar.
- Branches temporárias devem utilizar **Squash and merge**.
- Pull Requests de `dev` para `main` devem utilizar **Create a merge commit**.
- A branch temporária deve ser excluída após o merge.
- Force push não deve ser utilizado em branches compartilhadas.

## Correções urgentes

Quando existir uma versão em produção, correções urgentes poderão utilizar branches `hotfix/*` criadas a partir de `main`.

Uma correção aplicada à `main` também deverá ser incorporada à `dev` imediatamente, evitando que ela seja perdida em versões futuras.

## Proteção das branches

Após o bootstrap inicial, `main` e `dev` deverão ser configuradas no GitHub para:

- exigir Pull Request antes do merge;
- exigir pelo menos uma aprovação;
- exigir resolução das conversas;
- bloquear force push;
- bloquear exclusão;
- exigir verificações automatizadas quando a CI estiver disponível.
