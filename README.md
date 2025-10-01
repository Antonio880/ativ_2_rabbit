# Atividade 2 - RabbitMQ Work Queues

## O que foi feito

Implementação do tutorial "Work Queues" do RabbitMQ usando Node.js, criando um sistema de distribuição de tarefas entre múltiplos workers.

## Ferramentas necessárias

- **Node.js** (versão 14 ou superior)
- **Docker** (para rodar RabbitMQ)
- **npm** (gerenciador de pacotes do Node.js)

## Processo de execução

### 1. Instalar dependências
```bash
npm install
```

### 2. Iniciar RabbitMQ com Docker
```bash
# Rodar RabbitMQ com interface de gerenciamento
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4-management
```

### 3. Executar o sistema

**Passo 1:** Iniciar workers (consumidores)
```bash
# Terminal 1
node worker.js

# Terminal 2 (para testar múltiplos workers)
node worker.js
```

**Passo 2:** Enviar tarefas
```bash
# Em outro terminal
node new_task.js "Tarefa simples"
node new_task.js "Tarefa complexa..."
node new_task.js "Tarefa muito complexa....."
```

## Resultado esperado

- **Distribuição de tarefas**: As tarefas são distribuídas alternadamente entre os workers
- **Processamento sequencial**: Cada worker processa uma tarefa por vez
- **Simulação de trabalho**: Cada ponto (.) na mensagem = 1 segundo de processamento
- **Confiabilidade**: Mensagens não são perdidas mesmo se workers falharem

## Arquivos do projeto

- `new_task.js` - Produtor de tarefas
- `worker.js` - Consumidor de tarefas  
- `package.json` - Dependências
- `README.md` - Este arquivo

## Interface de gerenciamento

Após iniciar o RabbitMQ com Docker, acesse a interface web em:
- **URL**: http://localhost:15672
- **Usuário**: guest
- **Senha**: guest

## Funcionalidades implementadas

- Round-robin dispatching
- Message acknowledgment
- Message durability
- Fair dispatch com prefetch(1)
