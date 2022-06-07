# Scripts lógicos do componente Formulário - Nagem Expert 💻

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

## Primeiros Scripts 

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

- Formulário: [Nome do Formulário]
- Fieldset: Área do Solicitante
- Botão   : Carregar Área Superior
- descrição de comportamento: Tal script retorna e carrega todas as informações dos campos que vem na área superior, a diferença para o primeiro script é que esse script faz a chamada do banco referente a área o qual o usuário (solicitante) pertence, enquanto que o primeiro script só executa a query antes de fazer tal chamada no banco.

```    
// Cada usuário precisa pertencer a uma área, então aqui tal usuário será referenciado pela sua respectiva área.
vArea = VALORCAMPO('src';'area')

//Define consulta SQL
vSQL2 = "select dpp.nmdepartment from addepartment dp join addepartment dpp on dpp.iddepartment = left(dp.iddepartment,3) where dp.nmdepartment like '%" + vArea + "%'" 

//Define associação do campo SQL para Componente do Formulárrio
vArmazenar2 = 'inpAreaSuperiorSolicitante = nmdepartment'

//Executa o SQL
x = EXECUTESQL(vSQL2;vArmazenar2)
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: [Nome do Formulário]
- Fieldset: Área do Solicitante
- Botão   : Atualiza Dados do Solicitante
- descrição de comportamento: De forma auto explicativa, aqui serão carregados e atualizados os dados tanto do nome do solicitante quanto a área do solicitante, caso no meio dos processos seja necessário tal ação.

```
                                ...::: Nome Solicitante :::...

// INICIADOR('Nome')
vNomeSolicitante = FIGURASOLICITANTE('Usuário';'Nome') 
//Preenche o Nome do Solicitante no Formulário
X = ACAO('';'';'';'';'';'';'';'';'nmsolicitante';vNomeSolicitante)
          


                                ...::: Área do Solicitante :::...

//INICIADOR('Matrícula')
vLoginSolicitante = FIGURASOLICITANTE('Usuário';'Login') 

//Redefinir Login para o Solicitante
x = ACAO('';'';'';'';'';'';'';'';'logisolicitante';vLoginSolicitante)
x = QUERYEXECUTE('areasolicitante';'ImpAreaSoliciante=nmdepartment')



                  ...::: Área do Solicitante Superior (Área de Negócio) :::...
x = EXECUTESCRIPT('BTNCarregarAreaSuperior';'Clique')
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: CadastroMaterialConsumoRequisicao - Solicitação de Cadastro de Material para Consumo - Requisição
- Fieldset: Área do Solicitante
- Botão   : Solicitante - Ação: Cancelar Processo
- descrição de comportamento: De forma auto explicativa, aqui serão carregados e atualizados os dados tanto do nome do solicitante quanto a área do solicitante, caso no meio dos processos seja necessário tal ação.

```
// Método botão Solicitante - Ação: Cancelar Processo - btnAcaoCancelarProcesso

x=ACAOGRUPO('fsDadosGerais';'Desabilitar,Não requerido,Exibir';'')

x=ACAO('';'validgridempres';'';'validgridempres';'';'validgridempres';'';'';'')
```
> ---------------------------------------------------------------------------------------------------------------

- Formulário: CadastroMaterialConsumoRequisicao - Solicitação de Cadastro de Material para Consumo - Requisição
- Fieldset: Campos Ocultos
- Botão   : Verificar tipo de material 
- descrição de comportamento: A depender da flag, os respectivos campos receberão seus comportamento, se serão ativados ou não.

```
TpSolicitacao = VALORCAMPO('cadprodconsumo';'tpsolic')

SE (TpSolicitacao = 0)

X = ACAOGRUPO('InclusaoMaterial';'Habilitar,Requerido,Exibir';'')
X = ACAOITEMGRAFICO('InclusaoMaterial';'Exibir,Habilitar';'') 
X = ACAOGRUPO('ExpansaodeMaterial';'Desabilitar,Não requerido,Ocultar';'')
X = ACAOITEMGRAFICO('ExpansaodeMaterial';'Ocultar,Desabilitar';'')

SENAO
    SE(TpSolicitacao = 1)

    X = ACAOGRUPO('InclusaoMaterial';'Desabilitar,Não requerido,Ocultar';'')
    X = ACAOITEMGRAFICO('InclusaoMaterial';'Ocultar,Desabilitar';'') 
    X = ACAOGRUPO('ExpansaodeMaterial';'Habilitar,Requerido,Exibir';'')
    X = ACAOITEMGRAFICO('ExpansaodeMaterial';'Exibir,Habilitar';'')

   FIM
FIM
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: Importarclassavalia - Importar Classe de Avaliação - Cadastro de Material 
- Fieldset: Não possui
- Botão   : Importar
- descrição de comportamento: Script de importar uma planilha e "jogar" os resultados na Grid

```
x = IMPORTARPLANILHAPARAGRID('rlcimportclasse';'numavalia=A,nmclasse=B,contacontb=C';VERDADEIRO;'2';'';'')
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: GDC - Gerenciamento de Certificados Digitais
- Fieldset: Dados do Solicitante
- Campo   : Gestor Financeiro
- Botão   : Não possui
- Descrição de comportamento: O script retorna o nome dos gestores financeiros no respectivo campo (do tipo "valor fechado")

```
vlista = VALORCAMPO('gdc';'nmgestorfinan') 

vValidacao = 0

x = ACAO('';'';'';'';'';'';'';'';'validegestor';vValidacao)

SE(vlista = '') 

     x = ACAO('';'';'acionistas';'';'acionistas';'';'';'';'') 

SENAO 
     x = ACAO('';'';'gestorfinanceiro';'acionistas';'gestorfinanceiro';'';'acionistas';'';'')  
FIM  
RETORNO VERDADEIRO 
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: GDC - Gerenciamento de Certificados Digitais
- Fieldset: Dados do Solicitante
- Campo   : Acionista
- Botão   : Não possui
- Descrição de comportamento: O script retorna o nome dos acionistas no respectivo campo (do tipo "valor fechado")

```
vlista1 = VALORCAMPO('gdc';'nmacionista')

vValidacao = 1

x = ACAO('';'';'';'';'';'';'';'';'validegestor';vValidacao)

SE(vlista1 = '') 

     x = ACAO('';'';'gestorfinanceiro';'';'gestorfinanceiro';'';'';'';'') 

SENAO 
     x = ACAO('';'';'acionistas';'gestorfinanceiro';'acionistas';'';'gestorfinanceiro';'';'')  
FIM  
RETORNO VERDADEIRO 
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: GDC - Gerenciamento de Certificados Digitais
- Fieldset: Selecionar Tipo de Certificado
- Campo   : Radiobutton Pessoa Física
- Botão   : Radiobutton Pessoa Física (sim repetir apenas para separar a informação e enfatizar a diferença)
- Descrição de comportamento: Validar e atribuir os campos quando selecionado Pessoa Física

```
EXE = EXECUTESCRIPT('EXEVERPESSOA';'Clique')
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: GDC - Gerenciamento de Certificados Digitais
- Fieldset: Selecionar Tipo de Certificado
- Campo   : Radiobutton Pessoa Jurídica
- Botão   : Radiobutton Pessoa Jurídica (sim repetir apenas para separar a informação e enfatizar a diferença)
- Descrição de comportamento: Validar e atribuir os campos quando selecionado Pessoa Jurídica

```
EXE = EXECUTESCRIPT('EXEVERPESSOA';'Clique')
```

> ---------------------------------------------------------------------------------------------------------------

- Formulário: GDC - Gerenciamento de Certificados Digitais
- Fieldset: Pessoa Física/Jurídica 
- Campo   : Selecione o Certificado (tipo lista de valores fechados)
- Botão   : Selecione o Certificado (sim repetir apenas para separar a informação e enfatizar a diferença)
- Descrição de comportamento: Selecionar o certificado que não esteja previamente listado

```
vlista = VALORLISTA('gdc';'rlccertipj';'tipocertificpj') 

SE(vlista = '') 
     x = ACAO('outrocertpjurid';'';'';'outropjuridica';'outrocertpjurid';'outropjuridica';'outrocertpjurid,outropjuridica';'';'') 
SENAO 
     x = ACAO('outrocertpjurid';'';'rlccertipj';'outropjuridica';'outrocertpjurid';'outropjuridica';'outrocertpjurid';'';'') 
FIM  
RETORNO VERDADEIRO 
```

> ---------------------------------------------------------------------------------------------------------------


