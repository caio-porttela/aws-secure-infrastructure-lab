# AWS Secure Infrastructure Lab

## Sobre o projeto

Este projeto consiste em um laboratório prático de infraestrutura em nuvem utilizando Amazon Web Services (AWS), com foco em fundamentos de Cloud Engineering, segurança e administração de infraestrutura.

O objetivo foi compreender como os serviços de rede, computação, armazenamento, banco de dados e controle de acesso se integram em uma arquitetura AWS.

## Objetivos de aprendizagem

- Compreender os fundamentos de uma VPC e suas sub-redes.
- Utilizar uma instância EC2 para acessar e administrar recursos.
- Configurar acesso privado a um banco de dados RDS PostgreSQL.
- Aplicar conceitos de IAM, roles, policies e princípio do menor privilégio.
- Utilizar o AWS Systems Manager Session Manager para acessar uma instância sem depender de SSH aberto.
- Trabalhar com armazenamento S3 e bloqueio de acesso público.
- Testar conectividade de rede e permissões usando AWS CLI.
- Compreender backups automáticos e snapshots de banco de dados.
- Investigar erros de autorização e identificar suas causas.

## Serviços AWS utilizados

- Amazon VPC
- Amazon EC2
- Amazon RDS for PostgreSQL
- Amazon S3
- AWS IAM
- AWS Systems Manager Session Manager
- AWS CLI

## Testes realizados

- Conexão entre EC2 e RDS pela porta TCP 5432.
- Verificação do comportamento das regras de Security Groups.
- Conexão ao PostgreSQL por meio do cliente `psql`.
- Criação e consulta de registros em uma tabela.
- Validação de restrição de unicidade de e-mail.
- Consulta de informações do RDS usando AWS CLI.
- Investigação de erros `AccessDenied` relacionados a permissões IAM.
- Criação de snapshot manual do banco de dados.

## Segurança

Durante o laboratório foram estudados e aplicados conceitos como:

- Controle de acesso por IAM.
- Uso de IAM Roles para a instância EC2.
- Princípio do menor privilégio.
- Restrição de acesso ao banco de dados por Security Groups.
- Criptografia do RDS.
- Bloqueio de acesso público ao bucket S3.
- Acesso administrativo à instância por Session Manager.

## Limitações do laboratório

O ambiente foi desenvolvido em uma conta AWS sujeita a limitações de créditos e do plano gratuito. Algumas configurações de backup e alterações de recursos não puderam ser concluídas devido às restrições da conta e às permissões disponíveis.

Nenhum recurso deve ser considerado validado sem a respectiva evidência de teste.

## Próximos passos

- Finalizar a documentação da arquitetura.
- Registrar as configurações de segurança e os testes realizados.
- Revisar os custos e o estado dos recursos AWS.
- Evoluir para automação com Python, Git, Docker e CI/CD.

## Tecnologias

`AWS` `EC2` `RDS` `PostgreSQL` `S3` `IAM` `VPC` `SSM` `AWS CLI`

---

Projeto de aprendizagem prática desenvolvido para aprofundar conhecimentos em Cloud Engineering, DevOps e Cloud Security.