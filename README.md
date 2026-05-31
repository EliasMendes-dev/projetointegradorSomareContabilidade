# Somare Contabilidade — Projeto Integrador

## Visão geral

Aplicação desktop Windows Forms em C# para gerenciamento simples de contas (a pagar / a receber) e cadastro de usuários. Fornece telas para registro de usuário, login, cadastro/edição de contas e visualização de pagamentos, desenvolvido como Projeto Integrador do **Curso Técnico em Informática** do **Senac São Paulo**.

## Funcionalidades

- Cadastro de usuário (registro com perguntas de recuperação e login).
- Recuperação de senha por perguntas de segurança.
- CRUD de contas: criar, editar, excluir contas a pagar e a receber.
- Filtragem e busca nas listas de contas (por cliente, data, valor, tipo, categoria, situação).
- Marcar contas como pagas/pendentes/atrasadas e visualizar histórico de pagamentos.
- Exibição de valores agregados (soma de valores) e listagens separadas para contas pagas e não pagas.
- Interface Windows Forms intuitiva com painéis de navegação entre telas.

## Tecnologias

- **Linguagem:** C#
- **Plataforma:** .NET Framework 4.8
- **Banco de dados:** MySQL (script incluído)
- **Dependências chave:** `MySql.Data` (ver [packages.config](packages.config))

## Pré-requisitos

- Visual Studio (recomendado) com suporte a .NET Framework 4.8
- MySQL Server (ou MariaDB) acessível localmente

## Instalação e execução

1. Abra a solução `projetointegrador.sln` no Visual Studio.
2. Restaure os pacotes NuGet (se necessário): menu `Restore NuGet Packages`.
3. Buildar a solução (`Build -> Rebuild Solution`).
4. Execute o projeto (`F5` ou `Start`). O ponto de entrada é `Program.cs`.

## Configurar o banco de dados

1. No MySQL, execute o script SQL: [banco_de_dados_somare/somare.sql](banco_de_dados_somare/somare.sql). Isso cria a base `sistemasomare` e popula tabelas `cadastro` e `conta` com alguns registros.
2. O projeto usa uma string de conexão hardcoded em `Database.cs` apontando para `Server=localhost;Port=3306;User Id=root; database=sistemasomare;` — ajuste se necessário.

## Estrutura principal do projeto

- **Entrypoint:** [Program.cs](Program.cs)
- **Acesso a dados / conexões:** [Database.cs](Database.cs)
- **Formulários principais:**
  - Formulário de cadastro/login: [RegistroUsuario.cs](RegistroUsuario.cs)
  - Tela de pagamentos: [FormTelaPagamentos.cs](FormTelaPagamentos.cs)
  - Formulário de cadastro de conta: [FormCadastroConta.cs](FormCadastroConta.cs)
- **Modelos:** [Models/ContaModel.cs](Models/ContaModel.cs), [Models/UsuarioModel.cs](Models/UsuarioModel.cs), [Models/Sessao.cs](Models/Sessao.cs)
- **Script do banco:** [banco_de_dados_somare/somare.sql](banco_de_dados_somare/somare.sql)
- **Pacotes / target:** [packages.config](packages.config) (target framework: net48)

## Observações importantes

- A string de conexão está difundida no código (`Database.cs`). Recomenda-se mover para `App.config` ou um mecanismo seguro antes de produção.
- Senhas são armazenadas em texto simples no banco (script e código atual). Em produção, utilize hashing seguro (ex.: bcrypt) e práticas de segurança.
- O script SQL foi escrito para MySQL (uso de `AUTO_INCREMENT`, `DATE`, `DATETIME`, `CURRENT_TIMESTAMP`).

## Melhorias futuras

- Mover configuração de conexão para `App.config` e usar `ConfigurationManager`.
- Implementar hashing de senha e validação mais forte.
- Tratar exceções de banco de dados com logging.
- Parametrizar credenciais e porta do banco via variáveis de ambiente ou arquivo de configuração.

