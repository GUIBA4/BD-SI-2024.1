
# 🎲 Banco de Dados (IF976) 

O objetivo deste repositório é prover a documentação do projeto que será construída com a evolução da cadeira e aulas para que consigamos realizar a defesa do projeto ao final de cada módulo.


## 👤 Integrantes

- [Guilherme Vinicius - gvcc ](mailto:gvcc@cin.ufpe.br)
- [Lucas Tavora - lnt ](mailto:lnt@cin.ufpe.br) 
- [Isaque Diniz - itd ](mailto:itd@cin.ufpe.br) 
- [Gabriel Albertin - gav ](mailto:gav@cin.ufpe.br)
- [Maria Bezerra - mbma ](mailto:mbma@cin.ufpe.br)
- [Ícaro Amazonas - ias6 ](mailto:ias6@cin.ufpe.br)
- [Franklin Amaral - fansf ](mailto:fansf@cin.ufpe.br)


## 🔎 Visão geral e Contexto
O projeto tem o contexto de simular as principais operações de uma plataforma de apostas, similar à casas de apostas presentes na realidade. Nosso foco principal foi mapear as interações-chave de um usuário dentro da plataforma, seja realizando uma aposta em jogos ou realizando alguma transação para sua carteira. A construção desse projeto leva em consideração os conceitos aprendidos e requisitos para elaboração e entrega. 


## 🌎 Mini-mundo
Os usuários são a base do sistema de apostas, pois realizam apostas e movimentam transações em suas carteiras. Cada usuário possui informações básicas como nome, e-mail e CPF por onde são identificados. Adicionalmente, um usuário pode indicar novos usuários para a plataforma, tornando-se padrinho do novo usuário, que se torna seu afiliado.

Cada usuário possui uma carteira, que é identificada por um ID único. A carteira é onde o saldo do usuário é mantido e visualizado, e é através dela que as transações são realizadas. Assim que um usuário acessa nossa plataforma, ele recebe um bônus que a sua carteira possui. Esse bônus, identificado por um ID único, possui um valor específico e está disponível para ser utilizado em apostas.

Os usuários podem fazer apostas em rodadas dentro de um jogo. Cada jogo possui um nome, pode ser categorizado (por exemplo, cartas, azar, crash), tem uma data de criação na plataforma e é identificado por um ID único. As apostas só podem ser realizadas em rodadas pertencentes a um jogo. Quando uma aposta é feita em uma rodada que tem um resultado e um multiplicador, a data da aposta é registrada para marcar o momento exato da transação.

Todas as apostas feitas por um usuário resultam em uma transação interna na carteira desse usuário. Cada transação é identificada por um ID único. Além das apostas, os usuários podem adicionar ou retirar fundos de suas carteiras através de transações. Cada transação, seja interna ou externa, possui um ID, tipo (crédito ou débito) e valor. As transações externas são realizadas via banco e incluem informações detalhadas como código do banco, número da conta, agência e CPF.


## 🪢 Entidades, Atributos e Relacionamentos

#### 1. Entidades e Atributos
    1. Jogo (ID, Nome, Categorias, Data de Criação)
    2. Usuário (CPF, E-mail, Nome)
    3. Carteira (ID, Saldo)
    4. Bônus (ID, Valor)
    5. Transação (ID, Tipo, Valor), TransaçãoInterna (Internal_ID) e 
    TransaçãoExterna (External_ID, Dados bancários (Código do Banco, Conta, Agencia e CPF)
    6. Aposta (Valor, Data da Aposta)
    7. Rodada (Resultado, Data da Rodada, Multiplicador)

#### 2. Relacionamentos
    1. Indica (Usuário - Usuário): vários usuários (padrinho) podem indicar vários novos usuários (afiliados). 
    Um usuário pode não indicar ninguém, mas ao indicar pode ser indicado por um padrinho (N:N, parcial/parcial).

    2. Contém (Usuário - Bônus - Carteira): Todo carteira deve pertencer a um usuário. 
    Todo bônus deve pertencer a um usuário. Um usuário possui um bônus em uma carteira (1:1:1, parcial/total/total).

    3. Possui (Carteira - Transação): Uma carteira pode ter múltiplas transações. 
    Toda transação deve estar associada a uma carteira (1:N, parcial/total).

    4. Tem (Jogo - Rodada): Uma rodada pertence a um jogo. 
    Um jogo pode ter múltiplas rodadas. Toda rodada deve estar associada a um jogo (1:N, parcial/total).

    5. Cria (Aposta - TransaçãoInterna):  Quando uma aposta é realizada por um usuário, existe uma transação interna. 
    Quando uma rodada é positiva, existe uma transação interna (1:1,parcial/total).


## 📝 Requisitos da Modelagem

Os requisitos da modelagem foram atendidos da seguinte forma:

#### __Atributos__ (3)
- __Composto:__ Dados Bancários
- __Multivalorado:__ Categorias
- __Discriminador em Relacionamento:__ Data da Rodada

#### __Relacionamentos__ (11)
- __Relacionamento 1:1:__ Aposta - TransaçãoInterna
- __Relacionamento 1:N:__ Carteira - Transação
- __Relacionamento N:M:__ Usuário - Rodada
- __Relacionamento parcial-total:__ Carteira - Transação
- __Relacionamento parcial-parcial:__ Usuário - Rodada
- __Relacionamento Unário ou Auto Relacionamento:__ Usuário - Usuário (Indica)
- __Relacionamento Binário:__ Carteira - Transação
- __Relacionamento N-ário:__  Usuário - Carteira - Bônus
- __Entidade Fraca:__ Rodada
- __Entidade Associativa:__ Aposta
- __Herança:__ Transação Disjunta Total (Interna/Externa)

Totalizando 14 dos conceitos estudados na disciplina.


## 👍 Regras de Negócio

✅ A indicação de novos usuários registra a relação de padrinho e afiliado.

✅ A gestão da carteira permite que o usuário visualize o saldo da sua carteira.

✅ O bônus depende que o usuário entre na plataforma.

✅ A plataforma pode criar e gerir jogos por meio de nomes, categorias, data de criação e id.

✅ É possível realizar apostas em rodadas pertencentes a jogos e identifica-las por meio da data e hora da aposta, além dos resultados e multiplicadores das rodadas.

✅ Transações internas são criadas por meio de apostas, identificadas pelo ID, tipo (crédito ou débito) e valor.

✅ Transações externas envolvem contato apenas com banco, com detalhes como código do banco, conta, agencia, CPF e ID.


## 👎 Restrições
❌ Nenhum usuário deve possuir mais de uma carteira.

❌ Nenhum usuário deve ter mais de um CPF.

❌ O saldo da carteira nunca pode ser negativo.

❌ Não pode haver transações sem o tipo, sendo "crédito" e "débito" as únicas opções que podem ser registradas.

❌ O valor da aposta não pode exceder o saldo disponível na carteira do usuário no momento da aposta.

❌ As apostas não podem ser feitas em rodadas de jogos indisponíveis na plataforma.
