# Manual de Configuração de Ambiente de Desenvolvimento — GeoRural

> **Atenção:** este documento descreve como configurar o ambiente de **desenvolvimento** do projeto (backend + frontend rodando localmente). Não é um manual de deploy em produção.

## 1. Pré-requisitos

Antes de começar, tenha instalado/disponível:

- [Visual Studio Code](https://code.visualstudio.com/)
- Extensão [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) no VS Code
- [Docker](https://www.docker.com/) (necessário para o devcontainer)
- [Node.js 22 LTS](https://nodejs.org/)
- Acesso ao **wallet** do Oracle Autonomous Database (arquivo de credenciais fornecido pelo administrador do banco)
- Um cliente SQL de sua preferência (SQL Developer, DBeaver, etc.) para executar o script de schema

**OBS:** Java 21 e Maven **não precisam ser instalados manualmente** — são fornecidos pelo devcontainer (ver seção 2)

## 2. Configurando o ambiente Java/Maven

O projeto usa um **Dev Container** para padronizar o ambiente de backend.

1. Clone o repositório do backend.
2. Abra a pasta no VS Code.
3. Quando o VS Code detectar a configuração de devcontainer, clique em **"Reopen in Container"** (ou use a paleta de comandos: `Dev Containers: Reopen in Container`).
4. Aguarde a build da imagem. Ao final, o container já terá:
   - Java 21
   - Maven (instalado via SDKMAN)

Você pode confirmar as versões dentro do terminal do container:

```bash
java -version
mvn -version
```

## 3. Configurando o banco de dados (Oracle Autonomous Database)

### 3.1 Wallet de conexão

1. Obtenha o arquivo de wallet do Autonomous Database com o administrador do banco.
2. Extraia o wallet em uma pasta local e anote o caminho — ele será usado como `WALLET_DIR`.

### 3.2 Criando o schema

O schema do banco **não é criado automaticamente** pela aplicação, é necessário executá-lo manualmente:

1. Abra o script `.sql` disponível no repositório (pasta de scripts do projeto).
2. Conecte-se ao Autonomous Database usando seu cliente SQL de preferência (via wallet).
3. Execute o script para criar as tabelas necessárias.

### 3.3 Variáveis de ambiente

A aplicação lê os dados de conexão via variáveis de ambiente. **Elas precisam ser configuradas em toda nova sessão de terminal**, antes de rodar a aplicação:

```bash
export TNS_NAME="<nome_do_tns_no_wallet>"
export WALLET_DIR="<caminho_para_a_pasta_do_wallet>"
export DB_USERNAME="<usuario_do_banco>"
export DB_PASSWORD="<senha_do_banco>"
```

> ⚠️ Essas variáveis não persistem entre sessões de terminal ou reinicializações do container. Repita este passo sempre que abrir um novo terminal para rodar a aplicação.

## 4. Rodando o backend

Dentro do terminal do devcontainer, na raiz do projeto:

```bash
# build
./mvnw clean package

# executar
./mvnw spring-boot:run
```

Ou, alternativamente, execute a classe principal da aplicação diretamente pela interface do VS Code (com as variáveis de ambiente já exportadas no mesmo terminal/sessão).

## 5. Rodando o frontend

O frontend é um projeto separado (Vue 3).

1. Clone o repositório do frontend.
2. Instale as dependências:

```bash
npm install
```

3. Certifique-se de que a URL do backend local está configurada corretamente no projeto (arquivo de configuração/variáveis de ambiente do frontend).
4. Suba o servidor de desenvolvimento:

```bash
npm run dev
```

> Este comando inicia um servidor de desenvolvimento — ele não é adequado para produção e será encerrado ao fechar o terminal.

## 6. Checklist rápido (toda vez que for rodar o projeto)

- [ ] Container do devcontainer aberto (VS Code → Reopen in Container)
- [ ] Variáveis de ambiente do banco exportadas no terminal atual
- [ ] Backend rodando (`./mvnw spring-boot:run`)
- [ ] Frontend rodando (`npm run dev`)
- [ ] Frontend apontando para a URL correta do backend

---

**Nota:** este manual reflete o ambiente de desenvolvimento atual do projeto e não descreve um processo de deploy em produção.