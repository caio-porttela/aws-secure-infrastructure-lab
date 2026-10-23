# Segurança — AWS Secure Infrastructure Lab

## 1. Objetivo

Documentar os controles de segurança estudados e testados durante a construção do laboratório AWS, com foco em identidade, permissões, acesso à rede e proteção de dados.

## 2. Gerenciamento de identidades e acessos (IAM)

Foi criado o usuário IAM `caio-admin`, associado ao grupo `AWS-Admins`.

Durante o laboratório, foi estudado o uso de políticas IAM para definir quais operações cada identidade pode executar.

Também foi utilizada a IAM Role `EC2-Private-SSM` para permitir que a instância EC2 execute operações autorizadas por meio da AWS CLI.

### Aprendizados

- Usuários representam identidades que podem acessar a AWS.
- Grupos facilitam o gerenciamento de permissões de usuários.
- Roles permitem conceder permissões temporárias a serviços e aplicações.
- O princípio do menor privilégio recomenda conceder somente as permissões necessárias.
- Erros `AccessDenied` ajudam a identificar operações não autorizadas.

**Observação:** o grupo `AWS-Admins` recebeu a política gerenciada `AdministratorAccess` durante o laboratório. Essa configuração concede permissões amplas e deve ser substituída por permissões mais restritas em um ambiente real.

## 3. Acesso à instância EC2

Foi utilizado o AWS Systems Manager Session Manager para acessar a instância EC2.

Esse método permitiu administrar a instância sem depender de uma conexão SSH aberta para acesso administrativo.

A instância utilizou uma IAM Role para acessar operações autorizadas da AWS.

## 4. Controle de tráfego com Security Groups

O banco de dados PostgreSQL utiliza a porta TCP 5432.

Durante os testes, foi observada a diferença de conectividade entre a EC2 e o RDS conforme a regra de entrada do Security Group era permitida ou removida.

O objetivo da configuração é permitir o acesso ao banco somente a partir dos recursos autorizados, preferencialmente usando o Security Group da EC2 como origem.

Antes de publicar, a configuração final das regras deve ser conferida para garantir que não exista uma regra de acesso público desnecessária.

## 5. Proteção do Amazon S3

O bucket `caio-aws-lab-2026-0905` foi criado para o laboratório.

O bloqueio de acesso público estava habilitado, reduzindo o risco de exposição acidental dos objetos armazenados.

O bloqueio de acesso público não substitui o controle de permissões IAM nem a revisão das políticas do bucket.

## 6. Proteção do banco de dados RDS

Durante o laboratório, foi verificado que a criptografia em repouso estava habilitada no RDS PostgreSQL.

O acesso ao banco foi testado a partir da instância EC2, utilizando a porta TCP 5432 e conexão TLS.

A instância não utilizava Multi-AZ, portanto não deve ser considerada uma arquitetura de alta disponibilidade.

## 7. Backup e recuperação

Foi criado o snapshot manual `aws-lab-rds-snapshot-01`.

A existência do snapshot foi verificada, mas a restauração não foi testada. Portanto, a capacidade de recuperação a partir desse snapshot ainda precisa ser validada.

A retenção de backup automático observada foi de um dia. Uma tentativa de aumentar esse período foi limitada pelas condições da conta AWS.

## 8. Melhorias recomendadas

- Aplicar o princípio do menor privilégio às permissões IAM.
- Revisar e remover regras de rede desnecessárias.
- Confirmar que o RDS não aceita conexões públicas desnecessárias.
- Nunca armazenar senhas, chaves de acesso ou outros segredos no repositório Git.
- Revisar os custos e remover recursos que não sejam mais necessários.
- Testar a restauração de backups antes de considerar a recuperação validada.

## 9. Conclusão

O laboratório demonstrou como IAM, Security Groups, Session Manager, criptografia e controles de acesso do S3 contribuem para a proteção de uma infraestrutura em nuvem.

A segurança depende da combinação de permissões adequadas, configuração de rede, proteção dos dados e validação contínua dos controles.
