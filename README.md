# Padronizador de Commits · GitLab · Java 21

Ferramenta web simples para montar mensagens de commit e a resposta de protocolo no padrão da empresa, para os repositórios Java 21 no GitLab.

**Acesse:** https://mathhgs.github.io/padronizador-java21/

Não precisa instalar nada: é um único arquivo HTML que roda direto no navegador. Nenhum dado é enviado para servidor algum.

## Como usar

1. Informe o **número do processo** (formato `000000/0000`; a barra é inserida automaticamente).
2. Informe os **scripts**, se houver. Quando houver pelo menos um, o commit recebe `[SCRIPT]`.
3. Marque **Retrabalho**, se for o caso.
4. Para cada repositório alterado, escolha o **tipo do commit**, o **repositório** e escreva a **descrição**.
   - Abaixo de cada um aparece a mensagem montada e um contador de caracteres.
   - No repositório `relatorios`, aparecem campos para informar os relatórios alterados e se já foram atualizados em produção.
5. Preencha o **detalhamento da alteração**, se quiser.
6. Clique em **Finalizar** e copie as mensagens de commit e a resposta de protocolo.

## Padrão de commits

Máximo de **160 caracteres**:

```
prefixo(cpe): {número do processo} [SCRIPT] - {descrição}
```

Exemplo:

```
fix(cpe): 111111/2026 [SCRIPT] - Alteração no cálculo
```

| Prefixo    | Uso                               |
|------------|-----------------------------------|
| `feat`     | nova funcionalidade               |
| `fix`      | correção                          |
| `hotfix`   | correção urgente de produção      |
| `chore`    | manutenção                        |
| `docs`     | documentação                      |
| `refactor` | refatoração sem mudança funcional |
| `test`     | testes                            |
| `build`    | build/dependências                |
| `ci`       | pipeline                          |
| `revert`   | reversão                          |

O botão **Finalizar** não deixa gerar commits acima de 160 caracteres.

## Resposta de protocolo

A resposta sempre começa com a flag `[JAVA 21]`. Exemplo:

```
[JAVA 21]

[RETRABALHO]

Commits:
relatorios: fix(cpe): 111111/2026 [SCRIPT] - Alteração no cálculo

Scripts:
script_01.sql

Relatórios:
RelBalancete (Atualizado em produção)

Detalhamento da Alteração:
...
```

As seções `[RETRABALHO]`, Scripts, Relatórios e Detalhamento só aparecem quando preenchidas.

## Manutenção

Tudo fica no `index.html`. No início do `<script>` estão as listas que podem ser ajustadas:

- `REPOSITORIOS`: repositórios disponíveis para seleção.
- `PREFIXOS`: tipos de commit e suas descrições.
- `FLAG_JAVA`, `ESCOPO` e `LIMITE_COMMIT`: flag do protocolo, escopo do commit (`cpe`) e limite de caracteres.

Após o commit na branch `main`, o GitHub Pages publica a nova versão em alguns minutos (se a página antiga continuar aparecendo, use Ctrl+F5).
