# Testes — AWS Secure Infrastructure Lab

## 1. Objetivo

Registrar os testes realizados durante o laboratório para validar a conectividade, o funcionamento do banco de dados, as permissões de acesso e os recursos de backup.

## 2. Conectividade entre EC2 e RDS

**Objetivo:** verificar se a instância EC2 consegue alcançar o banco PostgreSQL.

- Origem: instância EC2 acessada pelo Systems Manager Session Manager.
- Destino: instância Amazon RDS for PostgreSQL.
- Porta: TCP 5432.

### Procedimento

Foi executado um teste de conectividade TCP a partir da instância EC2.

```bash
timeout 5 bash -c '</dev/tcp/172.31.32.126/5432' \
  && echo "PORTA 5432 ABERTA" \
  || echo "PORTA 5432 FECHADA"
```

### Resultado observado

A conexão foi estabelecida quando a regra de rede permitia o tráfego. Ao remover temporariamente a regra correspondente durante o teste, a conexão deixou de funcionar. Após restaurar a regra, a conectividade voltou.

**Aprendizado:** os Security Groups controlam o tráfego permitido entre os recursos. A regra definitiva deve permitir somente as origens necessárias.

## 3. Conexão com PostgreSQL

**Objetivo:** validar o acesso ao banco de dados a partir da EC2.

A conexão foi realizada com o cliente `psql`, utilizando o banco `awslab`.

```sql
\conninfo
\dt
\d usuarios
SELECT * FROM usuarios;
```

### Resultado observado

- A conexão com o PostgreSQL foi estabelecida.
- A tabela `usuarios` foi identificada.
- A estrutura das colunas e as restrições da tabela foram consultadas.
- Os registros inseridos durante o laboratório puderam ser consultados.
- A conexão utilizou TLS.

**Aprendizado:** conectividade de rede e autenticação no banco são etapas distintas. Uma porta acessível, por si só, não garante que as credenciais ou permissões de banco sejam válidas.

## 4. Integridade dos dados

**Objetivo:** verificar se a restrição de unicidade do e-mail funciona.

A tabela `usuarios` possui uma restrição `UNIQUE` na coluna `email`.

Durante o teste, uma tentativa de inserir um registro com um e-mail já existente foi rejeitada pelo PostgreSQL.

### Resultado observado

O banco retornou um erro de violação da restrição de unicidade.

**Aprendizado:** restrições no banco ajudam a preservar a integridade dos dados, impedindo duplicações que não são permitidas pelo modelo.

## 5. Verificação de permissões com AWS CLI

**Objetivo:** compreender como as permissões IAM afetam as operações administrativas.

Foi utilizada a AWS CLI a partir da instância EC2 para consultar informações da infraestrutura.

Durante o laboratório, uma operação de consulta ao RDS inicialmente retornou `AccessDenied`. Após a revisão das permissões da IAM Role, a consulta autorizada passou a funcionar.

Uma tentativa de executar `rds:ModifyDBInstance` continuou sem autorização.

### Resultado observado

- A consulta de informações do RDS passou a funcionar após a correção das permissões necessárias.
- A operação de modificação permaneceu bloqueada.

**Aprendizado:** uma IAM Role deve receber apenas as permissões necessárias para sua finalidade. Permitir consultas não exige necessariamente permitir alterações nos recursos.

## 6. Snapshot manual do RDS

**Objetivo:** registrar um ponto de recuperação do banco de dados.

Foi criado o snapshot manual:

`aws-lab-rds-snapshot-01`

A existência do snapshot e seu estado concluído foram verificados durante o laboratório.

### Limitação

A restauração do snapshot não foi testada. Portanto, o procedimento de recuperação ainda não pode ser considerado validado.

## 7. Limitações encontradas

- A conta AWS informou uma limitação para aumentar a retenção de backups automáticos.
- O ambiente RDS estava configurado sem Multi-AZ.
- Uma consulta de listagem de bancos apresentou incompatibilidade entre o cliente `psql` versão 15 e os catálogos do servidor PostgreSQL 18. A conexão com o banco e outras consultas funcionaram.
- O console do RDS apresentou erros de carregamento em algumas tentativas.

Essas ocorrências foram registradas para distinguir limitações do ambiente de falhas na conectividade ou nos testes realizados.

## 8. Resumo dos resultados

| Teste | Resultado observado |
|---|---|
| Conectividade EC2 → RDS | Validada |
| Acesso ao PostgreSQL | Validado |
| Consulta à tabela `usuarios` | Validada |
| Restrição de e-mail único | Validada |
| Consulta ao RDS pela AWS CLI | Validada após ajuste de permissões |
| Bloqueio de operação sem permissão | Observado |
| Criação de snapshot manual | Validada |
| Restauração de snapshot | Não testada |

## 9. Conclusão

Os testes ajudaram a compreender a relação entre rede, identidade, permissões, banco de dados e recuperação de dados na AWS.

Além de validar funcionalidades, o laboratório permitiu investigar erros de autorização, observar o comportamento de regras de rede e registrar limitações do ambiente sem afirmar que testes não realizados foram concluídos.
