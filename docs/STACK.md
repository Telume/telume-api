# TELUME Backend — Stack

Este documento registra as tecnologias e versões definidas para o backend do TELUME.

## Tecnologias

| Categoria              | Tecnologia  | Versão  |
| ---------------------- | ----------- | ------- |
| Runtime                | Node.js LTS | 24.21.0 |
| Gerenciador de pacotes | npm         | 11.19.0 |
| Linguagem              | TypeScript  | 5.9.3   |
| Banco de dados         | PostgreSQL  | 18.6    |
| ORM                    | Prisma ORM  | 7.10.0  |

## Estado atual

Neste bootstrap, apenas Node.js e npm estão configurados no repositório. TypeScript, PostgreSQL e Prisma serão adicionados quando a implementação começar, mantendo as versões registradas acima.

Nenhum framework HTTP, arquitetura, ponto de entrada ou estrutura de diretórios foi definido.

## Política de dependências

- Utilizar exclusivamente npm.
- Registrar dependências com versões exatas.
- Manter `package-lock.json` versionado.
- Utilizar `npm ci` para instalações reproduzíveis a partir do lockfile.
- Não depender de pacotes instalados globalmente.
- Alterações de versões devem atualizar, na mesma Pull Request, os arquivos de configuração e este documento.
