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
        u.nmuser as Nome,
        dp.nmdepartment,
        dp.CDDEPartment as CDDEPartment ,
        p.nmposition as Funcaao 
    from
        aduser u,
        ADUSERDEPTPOS d,
        adposition p ,
        addepartment dp 
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
- Descrição de funcionamento: A respectiva query é [continuar a descrição]

```
SELECT
    NMUSER
FROM
    ADUSER  
```

