# azure-essential-desafio-6
Dominando o Armazenamento na Azure
Aqui está um exemplo de um README detalhado para configurar recursos e dimensionar máquinas virtuais (VMs) no Microsoft Azure:

Aqui está um exemplo de um README detalhado para configurar e gerenciar armazenamento de dados no Azure:

---

# Configuração de Armazenamento de Dados no Azure

Este tutorial orienta você no processo de configuração e gerenciamento de serviços de armazenamento de dados no Microsoft Azure, cobrindo desde a criação de contas de armazenamento até a utilização de diferentes tipos de armazenamento.

## Pré-requisitos

- Uma conta ativa no [Azure](https://portal.azure.com).
- Permissões para criar e gerenciar recursos no Azure.
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) ou acesso ao portal Azure.

## Passo 1: Criando uma Conta de Armazenamento no Azure

A Conta de Armazenamento do Azure é a base para todos os serviços de armazenamento, como blobs, filas, tabelas e arquivos.

### Via Portal do Azure

1. Acesse o [Portal do Azure](https://portal.azure.com).
2. No painel à esquerda, clique em **Criar um recurso**.
3. Pesquise por **Conta de Armazenamento** e selecione **Criar**.
4. Preencha os detalhes:
   - **Assinatura**: Selecione sua assinatura.
   - **Grupo de Recursos**: Escolha um existente ou crie um novo.
   - **Nome da Conta de Armazenamento**: Insira um nome único.
   - **Região**: Escolha a localização geográfica onde os dados serão armazenados.
   - **Desempenho**: Selecione entre **Padrão** ou **Premium** (Premium é recomendado para cenários com alta demanda de IOPS).
   - **Replicação**: Escolha a opção de replicação adequada, como **LRS** (Local-Redundant Storage), **GRS** (Geo-Redundant Storage), etc.
   
5. Clique em **Revisar + Criar** e, em seguida, **Criar**.

### Via Azure CLI

```bash
# Exemplo de comando para criar uma conta de armazenamento
az storage account create \
  --name NomeDaContaDeArmazenamento \
  --resource-group NomeDoGrupoDeRecursos \
  --location eastus \
  --sku Standard_LRS
```

## Passo 2: Trabalhando com Armazenamento de Blobs

O armazenamento de blobs no Azure é utilizado para armazenar grandes quantidades de dados não estruturados, como imagens, vídeos e documentos.

### Criando um Contêiner de Blob

1. No portal do Azure, navegue até sua **Conta de Armazenamento**.
2. No menu à esquerda, selecione **Contêineres**.
3. Clique em **+ Contêiner** e defina:
   - **Nome**: Nome para o contêiner.
   - **Nível de Acesso Público**: Selecione se o contêiner será acessível publicamente ou privado.

4. Clique em **Criar**.

### Via Azure CLI

```bash
# Criar um contêiner de blob
az storage container create \
  --name NomeDoContainer \
  --account-name NomeDaContaDeArmazenamento \
  --public-access off
```

### Upload de Arquivos para o Contêiner de Blob

1. No portal do Azure, navegue até o contêiner criado.
2. Clique em **Carregar** e selecione o arquivo a ser carregado.

### Via Azure CLI

```bash
# Fazer upload de um arquivo para o contêiner
az storage blob upload \
  --container-name NomeDoContainer \
  --file CaminhoDoArquivo \
  --name NomeDoBlob \
  --account-name NomeDaContaDeArmazenamento
```

## Passo 3: Trabalhando com Tabelas de Armazenamento

O **Armazenamento de Tabelas** no Azure é uma solução NoSQL usada para armazenar grandes volumes de dados estruturados, como logs e metadados.

### Criando uma Tabela de Armazenamento

1. No portal do Azure, navegue até sua **Conta de Armazenamento**.
2. Selecione **Tabelas** no menu à esquerda.
3. Clique em **+ Tabela** e forneça um nome para a tabela.
4. Clique em **Criar**.

### Via Azure CLI

```bash
# Criar uma tabela de armazenamento
az storage table create \
  --name NomeDaTabela \
  --account-name NomeDaContaDeArmazenamento
```

### Inserindo e Consultando Dados em uma Tabela

```bash
# Inserir um item na tabela
az storage entity insert \
  --table-name NomeDaTabela \
  --entity PartitionKey=meuPK RowKey=meuRK Nome=Gabriel Sobrenome=Silva \
  --account-name NomeDaContaDeArmazenamento

# Consultar dados de uma tabela
az storage entity query \
  --table-name NomeDaTabela \
  --account-name NomeDaContaDeArmazenamento
```

## Passo 4: Trabalhando com o Armazenamento de Arquivos (File Share)

O **File Share** do Azure permite que você crie e use compartilhamentos de arquivos SMB para montar em VMs ou acessar diretamente.

### Criando um Compartilhamento de Arquivos

1. No portal do Azure, vá para sua **Conta de Armazenamento**.
2. Selecione **Compartilhamentos de Arquivos** no menu à esquerda.
3. Clique em **+ Compartilhamento de Arquivos**.
4. Defina um nome e o limite de cota para o compartilhamento.
5. Clique em **Criar**.

### Via Azure CLI

```bash
# Criar um compartilhamento de arquivos
az storage share create \
  --name NomeDoCompartilhamento \
  --account-name NomeDaContaDeArmazenamento
```

### Montando o Compartilhamento de Arquivos em uma VM

1. Navegue até o **Compartilhamento de Arquivos** criado.
2. Clique em **Conectar** para visualizar as instruções de montagem em sistemas Windows ou Linux.
3. Execute os comandos fornecidos na VM para montar o compartilhamento de arquivos.

## Passo 5: Configurando Regras de Acesso e Políticas

### Configurando Políticas de Acesso no Nível de Conta

1. Na **Conta de Armazenamento**, vá até **Configurações** > **Rede**.
2. Defina as regras de rede para permitir ou negar acesso a partir de IPs ou sub-redes específicas.

### Configurando SAS (Assinaturas de Acesso Compartilhado)

As SAS permitem o acesso temporário e seguro aos recursos de armazenamento.

1. No portal, vá até a **Conta de Armazenamento**.
2. Clique em **Assinatura de Acesso Compartilhado (SAS)** no menu à esquerda.
3. Defina as permissões, data de expiração e endereços IP permitidos.
4. Clique em **Gerar SAS** e copie a URL resultante.

## Conclusão

Agora você está pronto para criar e gerenciar contas de armazenamento, configurar blobs, tabelas, compartilhamentos de arquivos e aplicar políticas de segurança no Azure. Para mais informações e exemplos avançados, consulte a [documentação oficial do Azure](https://docs.microsoft.com/pt-br/azure/storage/).

---

Esse README fornece um guia completo para quem deseja começar a trabalhar com serviços de armazenamento no Azure.
