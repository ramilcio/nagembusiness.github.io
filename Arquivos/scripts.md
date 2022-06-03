# Scripts lógicos do componente Formulário - Nagem Expert

> <p> Aqui nessa área você irá compreender um pouco melhor sobre os scripts que são de certa forma padronizados e utilizados na construção dos formulários. </p>

## Informações de identificação
| Equipe   |      Cargo      |
|----------|:-------------:|
| Rodrigo Firmino |  Product Owner |
| Mateus Laranjeiras |    QA   |
| Francisco Gomes | Desenvolvedor |

|Data de Criação| Versão |
|----------|:-------------:|
|03-06-2022|1.0|

## Primeiros Scripts 🖥️

### Padrão de exibição dos respectivos scripts
- Formulário: [Nome do Formulário]
- Fieldset: [Nome do Fieldset]
- Botão   : [Nome do botão]
- descrição de comportamento: [Breve descrição sobre o comportamento do script]
> ---------------------------------------------------------------------------------------------------------------

- Formulário: [!! Procurar o nome ainda !!]
- Fieldset: Área do solicitante
- Botão: Carregar Área do Solicitante
- Descrição de comportamento: Sempre que for criado um novo formulário ou haja a necessidade de incluir tais informações em um formulário existente, primeiramente construir os respectivos campos e o botão que "chama" as informações do solicitante será preenchido automaticamente

```
x = QUERYEXECUTE('areasolicitante';'ImpAreaSoliciante=nmdepartment')
```
> ---------------------------------------------------------------------------------------------------------------

- Formulário: [Nome do Formulário]
- Fieldset: Área do solicitante
- Botão   : Cancelar Solicitação
- descrição de comportamento: Seguindo a mesma lógica do (Carregar área solicitante), esse script é referente para sempre que houver a necessidade de cancelar a solicitação, lembrando que por se tratar de uma plataforma low-code não se assuste caso fique confuso de como entender a lógica para escrever tal script, isso muitas vezes é gerado "automaticamente" após cliques de botão. 

```
x = ACAOGRUPO('DadosdoSolicitante';'Desabilitar,Não requerido,Ocultar';'')
x = ACAOITEMGRAFICO('DadosdoSolicitante';'Ocultar,Desabilitar';'')

x = ACAOGRUPO('Mecanica';'Desabilitar,Não requerido,Ocultar';'')
x = ACAOITEMGRAFICO('Mecanica';'Ocultar,Desabilitar';'')

x = ACAOGRUPO('Anexo';'Desabilitar,Não requerido,Ocultar';'')
x = ACAOITEMGRAFICO('Anexo';'Ocultar,Desabilitar';'')

x = ACAOGRUPO('TratativaInterna';'Desabilitar,Não requerido,Ocultar';'')
x = ACAOITEMGRAFICO('TratativaInterna';'Ocultar,Desabilitar';'')
```

> ---------------------------------------------------------------------------------------------------------------
> 













