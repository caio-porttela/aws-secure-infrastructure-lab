# AWS Secure Infrastructure Lab

Laboratório prático de infraestrutura em nuvem com Amazon Web Services (AWS), desenvolvido para estudar fundamentos de Cloud Engineering, segurança, redes, banco de dados e troubleshooting.

O projeto documenta a construção e os testes de componentes AWS, com foco em compreender como os recursos se comunicam e como permissões e controles de rede influenciam a segurança da infraestrutura.

## Objetivos

- Estudar redes virtuais, sub-redes e conectividade na AWS.
- Utilizar uma instância EC2 para administrar e testar recursos.
- Conectar uma instância EC2 a um banco Amazon RDS for PostgreSQL.
- Trabalhar com IAM Users, Groups, Roles e Policies.
- Utilizar o AWS Systems Manager Session Manager para acessar a instância.
- Configurar armazenamento no Amazon S3 e bloquear acesso público.
- Investigar erros de autorização usando a AWS CLI.
- Compreender criptografia, backups e snapshots de banco de dados.

## Arquitetura e serviços

- **Amazon VPC:** rede virtual dos recursos.
- **Amazon EC2:** instância utilizada para executar comandos e acessar o banco.
- **Amazon RDS for PostgreSQL:** banco de dados relacional gerenciado.
- **Amazon S3:** armazenamento de objetos.
- **AWS IAM:** gerenciamento de identidades e permissões.
- **AWS Systems Manager Session Manager:** acesso administrativo à instância.
- **Security Groups:** controle de tráfego de rede.
- **AWS CLI:** consulta e administração de recursos por linha de comando.

## Testes e resultados

Durante o laboratório, foram realizados os seguintes testes:

- Conectividade TCP entre EC2 e RDS pela porta 5432.
- Bloqueio e restabelecimento da conectividade ao alterar temporariamente uma regra de Security Group.
- Conexão ao PostgreSQL usando `psql`.
- Criação, consulta e inspeção da estrutura da tabela `usuarios`.
- Validação da restrição de unicidade da coluna `email`.
- Consulta de informações do RDS com a AWS CLI após revisar permissões IAM.
- Investigação de erros `AccessDenied`.
- Criação e verificação de um snapshot manual do RDS.

## Segurança

O laboratório permitiu estudar e aplicar controles de segurança em diferentes camadas:

- IAM para controlar permissões de identidades e serviços.
- IAM Role associada à instância EC2.
- Security Groups para restringir a comunicação com o banco.
- Session Manager para acesso administrativo sem depender de SSH aberto.
- Criptografia em repouso do RDS.
- Bloqueio de acesso público no bucket S3.

A configuração do grupo administrativo e as regras de rede devem ser revisadas antes de reutilizar o ambiente em um cenário real.

## Documentação

- [Arquitetura](docs/arquitetura.md)
- [Segurança](docs/seguranca.md)
- [Testes e resultados](docs/testes.md)

## Limitações e próximos passos

O laboratório foi executado em uma conta AWS sujeita a limitações de créditos, recursos e permissões.

- A restauração do snapshot ainda não foi testada.
- O RDS estava configurado sem Multi-AZ; alta disponibilidade não foi validada.
- Algumas alterações de backup foram limitadas pelas condições da conta.
- O estado final das regras de rede e dos recursos deve ser revisado antes de considerar o ambiente encerrado.

Próximos passos: revisar os custos e recursos ativos, conferir a configuração final de segurança e evoluir os estudos para automação com Python, Git, Docker, CI/CD e infraestrutura como código.

## Tecnologias

`AWS` `VPC` `EC2` `RDS` `PostgreSQL` `S3` `IAM` `SSM` `AWS CLI` `Git`

---

Projeto de aprendizagem prática voltado ao desenvolvimento de competências em Cloud Engineering, DevOps e Cloud Security.
