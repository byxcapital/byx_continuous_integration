# Executar Testes, Pre-Commit e SonarCloud

Esta ação customizada do GitHub executa testes do Django, hooks do pre-commit e uma análise do SonarCloud. Ela está configurada para ser usada como uma ação composta no GitHub Actions.

## Uso

Para utilizar esta ação em outro repositório, você precisará adicionar um arquivo de workflow no repositório de destino. Abaixo está um exemplo de como configurar isso.

### Exemplo de Uso

Crie um arquivo `.github/workflows/meu-action-exemplo.yml` no seu repositório de destino com o seguinte conteúdo:

```yaml
name: Meu Action Exemplo

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Set environment variables
        run: |
          echo "GITHUB_TOKEN=${{ secrets.GIT_TOKEN }}" >> $GITHUB_ENV
          echo "SONAR_TOKEN=${{ secrets.SONAR_TOKEN }}" >> $GITHUB_ENV
          echo "LANG=pt_BR.UTF-8" >> $GITHUB_ENV
          echo "LANGUAGE=pt_BR:pt" >> $GITHUB_ENV
          echo "LC_ALL=pt_BR.UTF-8" >> $GITHUB_ENV
          echo "ORGANIZATION_SONAR=karrary37" >> $GITHUB_ENV
          echo "PROJECT_KEY_SONAR=Karrary37_modelo_django" >> $GITHUB_ENV

      - name: Usar minha ação customizada
        uses: Karrary37/poc-github-action@VS-0.24
```

### Variáveis de Ambiente
Você precisa definir as seguintes variáveis de ambiente no seu repositório:

- GITHUB_TOKEN: Token do GitHub para autenticação.
- SONAR_TOKEN: Token do SonarCloud para autenticação.
- LANG: Definir a localidade como pt_BR.UTF-8.
- LANGUAGE: Definir a linguagem como pt_BR:pt.
- LC_ALL: Definir todas as categorias da localidade como pt_BR.UTF-8.
- ORGANIZATION_SONAR: Organização no SonarCloud.
- PROJECT_KEY_SONAR: Chave do projeto no SonarCloud.

### Detalhes da Ação
O arquivo action.yml está configurado para executar as seguintes etapas:

- Check out code: Faz o checkout do código do repositório.
- Set up Python: Configura a versão do Python.
- Install dependencies: Instala as dependências do projeto.
- Run pre-commit: Executa os hooks do pre-commit.
- Run Django tests: Executa os testes do Django.
- Start Redis and set locale: Inicia o Redis e configura a localidade.
- Load cached venv: Carrega o cache do ambiente virtual.
- Setup venv: Configura o ambiente virtual se o cache não estiver presente.
- Run Tests: Executa os testes com o ambiente virtual ativado.
- SonarCloud Scan: Executa a análise do SonarCloud.
- Run tests with coverage: Executa os testes com cobertura e gera o relatório XML.
- Upload coverage report to SonarCloud: Faz o upload do relatório de cobertura para o SonarCloud.