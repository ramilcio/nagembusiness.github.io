# SQL mais utilizados no componente Formulário - Nagem Expert 💻

> <p> Aqui nessa área você irá compreender um pouco melhor sobre as queries que são de certa forma padronizados e utilizados na construção dos formulários. </p>

## Informações de identificação 
| Equipe   |      Cargo      |
|----------|:-------------:|
| Rodrigo Firmino |  Product Owner |
| Mateus Laranjeiras |    QA   |
| Francisco Gomes | Desenvolvedor |

|Data de Criação| Versão |
|----------|:-------------:|
|03-06-2022|1.0|

## Primeiras Queries 🎲

> ------------------------------------------------------------------------------------------


- Entidade: areasolicitante
- Descrição de funcionamento: A respectiva query é referente (com base nas tabelas pré moldadas da Soft Expert) retorna o nome do usuário, nome do departamento, Código Departamento e função

```
 select
        u.nmuser as Nome,                   -- Aqui o campo está sendo renomeado de "Nome"
        dp.nmdepartment,
        dp.CDDEPartment as CDDEPartment ,
        p.nmposition as Funcaao             -- Já aqui, o campo está sendo renomeado de Funcao
    from
        aduser u,                           -- A tabela "ADUSER" está sendo renomeada apenas como a letra "u", para melhor compreensão e manipulação 
        ADUSERDEPTPOS d,                    -- A mesma lógica usada na tabela acima, vale para a essa, tabela "ADUSERDEPTPOS" renomeada como letra "d"
        adposition p ,                      -- Também aqui, tabela "adposition" sendo renomeada para a letra "p"
        addepartment dp                     -- E por fim a respectiva tabela "addepartment" renomeada como "dp"
    where
        d.cduser = u.cduser 
        and d.fgdefaultdeptpos = 1 
        and u.fguserenabled = 1 
        and dp.cddepartment = d.cddepartment 
        and p.cdposition = d.cdposition 
        and u.idlogin = :loginUser
```
> ------------------------------------------------------------------------------------------

- Entidade: User
- Descrição de funcionamento: A respectiva query é uma consulta simples, que irá retornar o nome do usuário a partir da tabela "ADUSER"

```
SELECT
    NMUSER  -- Nome do campo que será retornado
FROM
    ADUSER  -- Nome da tabela que esses tais nomes estão sendo buscados.
```
> De forma resumida a query aqui está retornando a consulta do nome dos usuários que estão na tabela "ADUSER", lembrando que essas tabelas tem os nomes já pré-moldados na plataforma
