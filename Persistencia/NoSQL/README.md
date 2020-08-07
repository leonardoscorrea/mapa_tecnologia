# NoSQL
***
## Introdução

<p>
Quando falamos de persistência de dados, nem sempre bancos do tipo relacionais são as melhores opções, principalmente quando necessitamos de estruturas dinâmiâmicas(ou não convencionais, como grafos - por exemplo) ou tratar de grandes volumes de dados(principalmente quando falamos em CONSULTA). Aqui vale ressaltar que NÃO estou afirmando que NoSQL é melhor, ele possui suas particularidade para a finalidade que ele foi desenvolvido. 
</p>
<p>
A tecnologia não tem como objetivo substituir ou concorrer com bancos relacionais, muito pelo contrário, NoSQL é um complemento para lacunas arquiteturais para as quais os bancos relacionais não foram criados. Ambos possuem seus espaços dentro de um ecossistema empresarial, e juntos formam soluções mais robustas e eficientes. 
</p>

## Definições

<p>
A maior parte de nós fomos apresentado apenas a modelos relacionais compostos por colunas, linhas e tabelas, em previamente era estruturado e modelado para uso. No entanto, nem sempre isso atende nossas necessidade, e nesses casos que indica-se o uso de NoSQL, por exemplo, quando nossos dados estão organizados de forma de árvores ou suas estruturas são dinâmicas. Essas situações eram normalmente solucionadas com bancos relacionais criando-se colunas que eram preenchidas apenas em determinadas situações.
</p>
<p>
Por fim, vamos descrever 4 tipos de modelos de dados em que o NoSQL implementa:
</p>
#### Chave-valor
<p>
Lembrando a estrutura de Map do Java, os dados são armazenados apenas possuindo chave e valor, e toda a consulta é realizada exclusivamente pela chave. Essa característica dá a esse tipo de NoSQL a complexidade computacional O(1) para consulta, ou seja, a pesquisa é praticamente linear independente da volumetria que o banco possua.
Exemplos:
</p>
<ul>
<li>Redis</li>
<li>BerkeleyDB</li>
<li>Riak</li>
<li>Oracle NoSQL</li>
</ul>

#### Orientado a Documento
<p>
Como o próprio nome diz, esse modelo persiste um documento relacionado a uma chave criada na inserção do mesmo. Onde falamos em documento, podemos citar XML e JSON como exemplos claros e estruturados. Semelhante a chave-valor, no entanto, com uma diferença que sua chave é um identificador único dentro de uma coleção e sua pesquisa basea-se no documento, diferentemente do modelo anterior.  
Exemplos: 
</p>
<ul>
<li><a href="./MongoDB/README.md" >MongoDB</a></li>
<li>CouchBase</li>
</ul>

#### Colunar
<p>
Banco de dados colunar caracteriza-se por possuir três componentes bem definidos:
<ul>
<li>keyspace: que podemos vincular a um database de um banco relacional</li>
<li>Famílias de Colunas: que podemos vincular a uma estrutura de tabelas, por mais que não seja.</li>
<li>colunas: que diferentemente da estrutura de um banco relacional, as colunas são variáveis a cada linha, possuindo um identificador único</li>
</ul>
Exemplos:
<ul>
<li>Cassandra</li>
</ul>

Segue estrutura exemplo:
</p>

```
user = { // Família de Colunas
  leonardo: [ // leonardo é a chave dessa linha
    // colunas
    {coluna: "nome",    dados: [{timestamp: 123456789, valor: "Leonardo"}]},
    {coluna: "email",   dados: [{timestamp: 123456789, valor: "leonardo@exemplo.com.br"}]}
  ],
  joao : [ // joao é a chave desta linha
    // colunas
    {coluna: "user",  dados: [{timestamp: 123456789, valor: "joao"}]},
    {coluna: "idade", dados: [{timestamp: 123456789, valor: "22" }]},
    {coluna: "sexo",  dados: [{timestamp: 123456789, valor: "masculino"}]}
  ]
}
```

#### Grafos
<p>
Por fim, e não menos importante, NoSQL do tipo Grafos. Muito conhecido pela característica de redes sociais, o modelo autiliza 3 componentes básicos: o dado, as arestas(ou ligações entre grafos) e os atributos(ou propriedades). A principal vantagem desse modelo estão nas consultas complexas entre dados fotemente ligados entre si.
Exemplos:
</p>
</p>
<ul>
<li>Neo4J</li>
<li>OrientedDB</li>
<li>GraphBase</li>
<li>InfiniteGraph</li>
</ul>