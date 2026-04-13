# Sistema de Gestão de Contratos, Requisições e Catálogo

Este pacote contém uma versão pronta para implantação do sistema em ambiente local ou em nuvem, com interface em Streamlit, banco SQLite local e suporte a logo institucional.

## Estrutura do projeto

```text
deploy_pacote_sistema_contratos/
├── app.py
├── requirements.txt
├── README.md
├── .streamlit/
│   └── config.toml
├── runtime.txt
├── Procfile
└── start.sh
```

## Requisitos

- Python 3.11 ou superior
- Pip
- Ambiente virtual recomendado

## Instalação local

### 1. Criar e ativar ambiente virtual

No Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

No Linux ou macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Instalar dependências

```bash
pip install -r requirements.txt
```

### 3. Colocar a logo institucional

O sistema espera a logo no caminho:

```text
/mnt/data/logo-centra-de-compras.svg
```

Para uso local, ajuste a variável `LOGO_PATH` dentro do arquivo `app.py` para um caminho real da sua máquina, por exemplo:

```python
LOGO_PATH = "logo-centra-de-compras.svg"
```

Depois, coloque o arquivo SVG na mesma pasta do projeto.

### 4. Executar localmente

```bash
streamlit run app.py
```

O sistema abrirá normalmente no navegador.

## Banco de dados

Por padrão, o sistema usa SQLite com o arquivo:

```text
arp.db
```

Esse arquivo será criado automaticamente na primeira execução, na mesma pasta do projeto.

## Usuário administrador padrão

Se o banco estiver vazio, o sistema cria:

- Usuário: `AndersonMPMelo`
- Senha: `Tomatinho`

Altere isso depois da primeira execução.

## Implantação em nuvem

### Opção 1: Streamlit Community Cloud

1. Suba os arquivos para um repositório GitHub.
2. Garanta que o arquivo principal seja `app.py`.
3. Configure as dependências com `requirements.txt`.
4. No painel da plataforma, selecione o repositório e o arquivo principal.
5. Ajuste o `LOGO_PATH` para um caminho relativo, por exemplo:

```python
LOGO_PATH = "logo-centra-de-compras.svg"
```

### Opção 2: Render

Este pacote já inclui arquivos auxiliares para deploy simples:

- `Procfile`
- `runtime.txt`
- `start.sh`

Fluxo sugerido:

1. Criar um novo Web Service no Render.
2. Apontar para o repositório.
3. Usar o comando de build:

```bash
pip install -r requirements.txt
```

4. Usar o comando de start:

```bash
bash start.sh
```

### Opção 3: Railway ou servidor Linux próprio

No servidor:

```bash
pip install -r requirements.txt
streamlit run app.py --server.port 8501 --server.address 0.0.0.0
```

## Ajustes recomendados antes de produção

- trocar o SQLite por PostgreSQL
- mover credenciais padrão para variáveis de ambiente
- criar rotina de backup do banco
- definir política de alteração de senha
- ajustar o caminho da logo para produção
- revisar permissões por perfil
- publicar atrás de proxy reverso, se necessário

## Arquivos auxiliares

### `.streamlit/config.toml`
Define comportamento do servidor Streamlit e configurações básicas para deploy.

### `Procfile`
Facilita execução em plataformas compatíveis.

### `runtime.txt`
Ajuda plataformas que usam a versão de Python do arquivo.

### `start.sh`
Script de inicialização pronto para nuvem.

## Comandos rápidos

Instalar:

```bash
pip install -r requirements.txt
```

Executar:

```bash
streamlit run app.py
```

## Observações finais

Esta estrutura já é suficiente para:

- execução local imediata
- versionamento em GitHub
- deploy simples em nuvem
- testes de homologação

Para ambiente institucional definitivo, o próximo passo ideal é a migração para PostgreSQL e a externalização das configurações sensíveis.
