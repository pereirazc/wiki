# Conexo XML (utField) API

##Metodos de utField
---
#####`addAttribute(name: string): utAttribute;`
> adiciona atributo C  tag

#####`addField(name: string): utField;`
> adds child field to tag

#####`findField(name: string): utField;`
> adds child field to tag

#####`getAttributeByName(name: string): utAttribute;`
> adds child field to tag

#####`getFieldByName(name: string): utField;`
> adds child field to tag




##Acessando Documento XML
---
utField unit utuMessage
Dada a classe Livro definida abaixo:

[gimmick:yuml]([Livro|-TC-tulo:acString;-Autor:acString;-Editora:acString;-AnoPublicacao:acInt|])

~~~
type
  Livro = class(acPersistentObject)
  private
    FTitulo: acString;
    FAutor: acString;
    FEditora: acString;
    fAnoPublicacao: acInt;
  published
    property Titulo: acString read FTitulo write FTitulo;
    property Autor: acString read FAutor write FAutor;
    property Editora: acString read FEditora write FEditora;
    property AnoPublicacao: acInt read FAnoPublicacao write FAnoPublicacao;
end;
~~~

~~~xml
<Livros>
    <Livro Autor="Antoine Saint-ExupC)ry" Editora="Agir" AnoPublicacao="1943">O Pequeno Principe</Livro>
    <Livro Autor="Thomas Piketty" Editora="IntrC-nseca" AnoPublicacao="2014">O Capital no SC)culo XXI</Livro>
    <Livro Autor="Johanna Basford" Editora="Sextante" AnoPublicacao="1911">Jardim Secreto</Livro>
</Livros>
~~~

~~~
var
    lEnum: acEnumerator;
    lXML: utField;
    lFieldLivro: utField;
begin
    lEnum := lXML.getFieldByName('Livros').getFieldEnumerator;
    try
        while not lEnum.EOL do
        begin
            lFieldLivro := lEnum.Current as utField;
            lLivro := Livro.CreateNew(Self.Session);
            lLivro.Titulo.Value         := lFieldLivro.asString;
            lLivro.Autor.Value          := lFieldLivro.AttributeByName('Autor').AsString;
            lLivro.Editora.Value        := lFieldLivro.AttributeByName('Editora').AsString;
            lLivro.AnoPublicacao.Value  := lFieldLivro.AttributeByName('AnoPublicacao').AsInt;
            lLivros.Add(lLivro);
            lEnum.MoveNext;
        end;
    finally
        lEnum.Free;
    end;
~~~

##Criando Documento XML
Supondo uma lista de objetos Livro como definida anteriormente
~~~
var
    lEnum: acEnumerator;
    lLivros: aPersistentcObjectList;
    lLivro: Livro;
    lFieldLivros,
    lFieldLivro: utField;
begin
    lEnum := lLivros.getEnumerator;
    try
        while not lEnum.EOL do
        begin
            lFieldLivro := lEnum.Current as utField;
            lLivro := Livro.CreateNew(Self.Session);
            lLivro.Titulo.Value         := lFieldLivro.asString;
            lLivro.Autor.Value          := lFieldLivro.AttributeByName('Autor').AsString;
            lLivro.Editora.Value        := lFieldLivro.AttributeByName('Editora').AsString;
            lLivro.AnoPublicacao.Value  := lFieldLivro.AttributeByName('AnoPublicacao').AsInt;
            lLivros.Add(lLivro);
            lEnum.MoveNext;
        end;
    finally
        lEnum.Free;
    end;
~~~
