# Arquitetura — AWS Secure Infrastructure Lab

## 1. Objetivo

Documentar a arquitetura de um laboratório de infraestrutura em nuvem criado para estudar os fundamentos de AWS, redes, computação, banco de dados e segurança.

## 2. Componentes utilizados

| Componente | Função |
|---|---|
| Amazon VPC | Rede virtual isolada para os recursos do laboratório |
| Sub-redes públicas e privadas | Organização dos recursos conforme sua necessidade de conectividade |
| Internet Gateway | Conectividade com a internet para recursos e rotas públicas, conforme configurado |
| NAT Gateway | Permite saída para a internet a partir de sub-redes privadas, conforme as rotas configuradas |
| Amazon EC2 | Instância de computação utilizada para executar comandos e acessar o banco |
| AWS Systems Manager Session Manager | Acesso administrativo à instância sem depender de SSH aberto |
| Amazon RDS for PostgreSQL | Banco de dados relacional gerenciado |
| Security Groups | Controle de tráfego de rede entre os recursos |
| AWS IAM | Controle de identidades e permissões |
| Amazon S3 | Armazenamento de objetos |

## 3. Fluxo de comunicação

O fluxo principal validado no laboratório foi:

1. O administrador acessa a instância EC2 por meio do Systems Manager Session Manager.
2. A instância EC2 utiliza o cliente PostgreSQL para se conectar ao RDS.
3. A conexão com o banco utiliza a porta TCP 5432.
4. As regras de Security Groups determinam se o tráfego de rede é permitido.
5. A instância utiliza uma IAM Role para acessar operações autorizadas da AWS por meio da AWS CLI.

## 4. Banco de dados

O banco de dados utilizado foi o Amazon RDS for PostgreSQL.

Configurações registradas durante o laboratório:

- Engine: PostgreSQL
- Versão observada: 18.3
- Armazenamento alocado: 20 GiB
- Porta: 5432
- Criptografia em repouso: habilitada
- Multi-AZ: desabilitado
- Retenção de backup automático observada: 1 dia

A tabela `usuarios` foi utilizada para testar criação, consulta e restrições de integridade dos dados.

## 5. Backup e recuperação

Foi criado um snapshot manual identificado como `aws-lab-rds-snapshot-01`.

A existência do snapshot foi verificada anteriormente no console. A restauração ainda precisa ser testada e documentada antes de ser considerada validada.

## 6. Limitações e considerações

- A configuração de rede deve ser confirmada pelas rotas e regras efetivamente existentes.
- A retenção de backup permaneceu em 1 dia devido às limitações informadas pela conta AWS.
- O ambiente não utiliza Multi-AZ.
- A disponibilidade contínua e a recuperação após desastre não foram validadas por um teste de restauração.

## 7. Aprendizados

O laboratório permitiu estudar a relação entre redes, controle de acesso, computação e banco de dados, além de demonstrar como permissões IAM e regras de rede atuam em camadas diferentes.