# Sql_Autorrelacionamento

# Banco de Dados de Funcionários com Autorrelacionamento

Este repositório contém o esquema e os dados de um banco de dados de funcionários, implementado com o conceito de autorrelacionamento. O banco de dados gerencia informações sobre funcionários e suas relações hierárquicas dentro da empresa.

## Conceito de Autorrelacionamento

O autorrelacionamento ocorre quando uma entidade em uma tabela está relacionada a ela mesma. No contexto deste banco de dados, a tabela `funcionario` utiliza um autorrelacionamento para representar a estrutura hierárquica da empresa. Cada funcionário pode ter um gerente direto, que também é um funcionário da mesma tabela.

### Estrutura da Tabela

A tabela `funcionario` inclui as seguintes colunas:

- **cpf**: O CPF do funcionário, que é a chave primária da tabela.
- **nome_completo**: O nome completo do funcionário.
- **departamento**: O departamento onde o funcionário trabalha.
- **email**: O e-mail do funcionário (deve ser único).
- **telefone**: O número de telefone do funcionário.
- **subordinado_fk**: O CPF do gerente direto do funcionário (chave estrangeira que referencia o próprio CPF da tabela). Se o funcionário não tem um gerente direto, este campo pode ser nulo.

### Esquema da Tabela

```sql
CREATE TABLE funcionario (
    cpf               VARCHAR(14) PRIMARY KEY,  
    nome_completo     VARCHAR(100) NOT NULL,
    departamento      VARCHAR(40) NOT NULL,
    email             VARCHAR(60) UNIQUE NOT NULL,
    telefone          VARCHAR(20),
    subordinado_fk    VARCHAR(14),
    FOREIGN KEY (subordinado_fk) REFERENCES funcionario(cpf) ON DELETE SET NULL
);
