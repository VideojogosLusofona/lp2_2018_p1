<!--
1º Projeto de Linguagens de Programação II 2018/2019 (c) by Nuno Fachada

1º Projeto de Linguagens de Programação II 2018/2019 is licensed under a
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.

You should have received a copy of the license along with this
work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
-->

# 1º Projeto de Linguagens de Programação II 2018/2019

## Descrição do problema

Os alunos devem implementar um programa em C# \[[1][ref1],[2][ref2]\] que
manipule e analise uma série de dados sobre jogos do Steam \[[3][ref3]\]. O
programa deve começar por ler um ficheiro [CSV][], disponibilizado no Moodle,
contendo os dados em questão. O utilizador do programa pode depois colocar
questões sobre os jogos, como por exemplo, quais os jogos lançados a partir de determinada data, que jogos suportam controlador, bem como efetuar algumas
ações sobre jogos específicos, tais como abrir a respetiva página do Steam no
*browser* ou descarregar a imagem de apresentação do jogo.

### Conteúdos do ficheiro CSV

Os ficheiros CSV (*comma-separated values*) contêm tabelas de dados, sendo que
os campos em cada linha estão separados por vírgulas. Este tipo de ficheiros
pode ou não ter uma linha de cabeçalho. Segue-se um exemplo:

```
Id,Type,Health,Mana,Shield
1,Elf,50,200,40
2,Dwarf,40,100,150
3,Troll,100,10,140
4,Wizard,25,300,30
```

No caso em questão, os ficheiros CSV têm uma série de campos com informação
sobre um videojogo disponível no Steam, nomedamente:

*   **ID** - ID do jogo
*   **Name** - Nome do jogo
*   **ReleaseDate** - Data de lançamento
*   **DLCCount** - Nº de DLCs lançados
*   **RequiredAge** - Idade mínima para jogar
*   **Metacritic** - Nota no Metacritic (0 a 100)
*   **MovieCount** - Nº de *trailers*
*   **RecommendationCount** - Nº de recomendações
*   **ScreenshotCount** - Nº de capturas de ecrã
*   **Owners** - Nº de pessoas que têm o jogo
*   **NumberOfPlayers** - Nº de pessoas que efetivamente jogaram o jogo
*   **AchievementCount** - Nº de *achievements*
*   **ControllerSupport** - Suporte para controlador (*True* ou *False*)
*   **PlatformWindows** - Suporte para Windows (*True* ou *False*)
*   **PlatformLinux** - Suporte para Linux (*True* ou *False*)
*   **PlatformMac** - Suporte para Mac (*True* ou *False*)
*   **CategorySinglePlayer** - Suporte para *singleplayer* (*True* ou *False*)
*   **CategoryMultiplayer** - Suporte para *multiplayer* (*True* ou *False*)
*   **CategoryCoop** - Suporte para *multiplayer* cooperativo (*True* ou *False*)
*   **CategoryIncludeLevelEditor** - Inclui editor de níveis (*True* ou *False*)
*   **CategoryVRSupport** - Suporte para VR (*True* ou *False*)
*   **SupportURL** - Website de suporte/ajuda do jogo
*   **AboutText** - Descrição do jogo
*   **HeaderImage** - URL da imagem do jogo
*   **Website** - Website do jogo

Cada linha do ficheiro corresponde a um jogo, e a primeira linha indica o nome
dos campos (cabeçalho).

### O programa a desenvolver

O programa pode ser desenvolvido de três formas distintas, no entanto será
apenas dado suporte à primeira forma:

1.  Solução Visual Studio 2017, Console App (.NET Framework ou .NET Core)
2.  Solução Visual Studio 2017, Desktop App (WPF ou Windows Forms)
3.  Unity 2018

Caso os alunos optem pela primeira forma, o nome do ficheiro CSV deve ser dado
como 1º argumento na linha de comandos. Na 2ª e 3ª formas o nome do ficheiro
deve ser solicitado numa caixa de diálogo da interface gráfica (Windows ou
Unity). Se o ficheiro for considerado válido, a análise dos jogos pode começar,
caso contrário o programa deve apresentar uma mensagem de erro apropriada. No
caso do programa ser uma aplicação de consola, deve terminar após o erro. Caso
o programa seja uma aplicação Windows Desktop ou Unity, deve voltar a pedir o
nome de ficheiro numa caixa de diálogo.

Durante a leitura do ficheiro, cada linha deve corresponder à instanciação de
um objeto do tipo `Game`, que deve ser guardado numa coleção contendo todos os
jogos listados. O tipo `Game` deve ter todos os campos presentes no ficheiro
CSV, e o tipo destes campos deve ser apropriado para o campo em questão. Por
exemplo:

*   Campos numéricos são essencialmente [`int`][]s.
*   Campos com valores *True* ou *False* devem ser representados com [`bool`][].
*   Campos de texto devem ser guardados como [`string`][].
*   Campos de data devem usar a `struct` [`DateTime`][].
*   Campos com endereços URL devem usar a classe [`Uri`][].

Jogos que apareçam repetidos devem ser ignorados ou descartados sem qualquer
aviso. Um jogo é considerado repetido se tiver o mesmo ID. Após leitura e
validação do ficheiro, o programa deve ter as seguintes opções:

1.  Mostrar informação de um jogo
2.  Efetuar uma pesquisa
3.  Sair

#### Mostrar informação de um jogo

Se o utilizador selecionar esta opção, o programa deve solicitar o ID do jogo
a mostrar. Se o ID for válido (i.e., se for um [`int`][] e se corresponder a um
jogo que exista na lista), o programa deve mostrar toda a informação sobre o
jogo, de forma bem formatada e agradável de visualizar. Se o programa for
desenvolvido em Unity, WPF ou Windows Forms, a informação sobre o jogo deve
também mostrar a imagem do jogo. Se for desenvolvido em consola, o programa
deve descarregar a imagem da Internet e indicar a pasta para a qual foi feita
a transferência. Seja qual for a opção escolhida pelos alunos, é possível
descarregar uma imagem da Internet usando a classe [`WebClient`][] (um bom
exemplo de utilização desta classe está disponível
[aqui](https://stackoverflow.com/questions/24797485/how-to-download-image-from-url)).

Os alunos podem implementar as seguintes extensões opcionais, que permitem
compensar eventuais problemas noutras partes do projeto, facilitando a obtenção
da nota máxima:

1.  Caso o programa tenha sido desenvolvido em consola, mostrar a imagem do
    jogo, ou [diretamente da consola](https://stackoverflow.com/questions/33538527/display-a-image-in-a-console-application/33604540),
    ou através do visualizador de imagens do Windows 10.
2.  Em qualquer tipo de implementação, dar a opção de abrir o *website* de
    suporte do jogo e *website* do jogo usando o *browser* por omissão do
    sistema.

A implementação destas extensões pode obrigar a lançar um programa externo, e a
forma de realizar essa ação é através da classe [`Process`][]. Vários exemplos
de como utilizar esta classe para esse efeito estão disponíveis
[aqui](https://stackoverflow.com/questions/181719/how-do-i-start-a-process-from-c),
[aqui](https://stackoverflow.com/questions/3173775/how-to-run-external-program-via-a-c-sharp-program)
e
[aqui](https://stackoverflow.com/questions/4580263/how-to-open-in-default-browser-in-c-sharp).

A implementação das extensões opcionais pode compensar eventuais problemas
noutras partes do projeto, facilitando a obtenção da nota máxima de 2 valores.

#### Efetuar uma pesquisa

<!--
https://stackoverflow.com/questions/3173775/how-to-run-external-program-via-a-c-sharp-program

https://stackoverflow.com/questions/33538527/display-a-image-in-a-console-application/33604540

https://stackoverflow.com/questions/24797485/how-to-download-image-from-url
-->

<!--
O jogo [Simplexity] é semelhante ao [4-em-linha], mas com uma variação: além de
**cor**, as peças têm também **forma**. O [Simplexity] é jogado em turnos, e em
cada turno o jogador coloca uma peça numa das 7 colunas do tabuleiro de jogo. A
peça cai na vertical até atingir a base da coluna ou uma peça já colocada na
coluna. Um jogador vence quando 4 peças da sua **cor** ou da sua **forma** são
colocadas em linha (na vertical, horizontal ou diagonal). Se ocorrer uma
situação em que existam 4 peças em linha da mesma cor e 4 peças em linha da
mesma forma, a forma sobrepõem-se à cor para efeitos de vitória. O jogo termina
num empate após todas as peças terem sido colocadas em jogo sem que exista uma
situação de vitória.

A [Tabela 1](#tab1) mostra as condições de vitória para cada jogador, bem como
as peças alocadas inicialmente a cada um. Em caso de dúvidas podes consultar as
[regras do Simplexity] ou entrar em contacto com o docente via Moodle.

<a name="tab1"></a>

**Tabela 1** - Condições de vitória (cor e forma) e peças alocadas inicialmente
a cada jogador.

| Jogador | Vitória de cor | Vitória de forma | Peças iniciais                             |
|---------|----------------|------------------|--------------------------------------------|
| 1       | Branco         | Cilindro         | 11 cubos brancos, 10 cilindros brancos     |
| 2       | Vermelho       | Cubo             | 11 cubos vermelhos, 10 cilindros vermelhos |

### Modo de funcionamento

O jogo começa automaticamente, entrando no seguinte ciclo (_game loop_):

1. Mostrar tabuleiro (ver secção <a href="#visualize">Visualização do jogo</a>)
2. Solicitar jogada ao jogador atual (jogador 1 é o primeiro a jogar)
3. Verificar se existe uma condição de vitória
   * Em caso afirmativo, terminar o jogo e indicar o vencedor
   * Em caso negativo:
      * Se ainda existirem peças para jogar, voltar ao ponto 1, alternando o
        jogador
      * Caso contrário, terminar jogo com empate

No ponto 2, é solicitado ao jogador: a) a peça a jogar (cubo ou cilindro); e,
b) a coluna onde colocar a peça. Antes de solicitar a jogada, deve ser dada
indicação de quantas peças de cada tipo o jogador ainda tem para jogar. Após o
jogador ter inserido uma jogada, o jogo deve verificar se: a) o jogador ainda
tem peças do tipo indicado; e, b) a coluna do tabuleiro ainda tem espaço para
mais peças (máximo de 7 peças por coluna). Se alguma destas verificações
falhar, o jogo deve solicitar ao jogador a repetição da jogada.

No ponto 3, o tabuleiro deve ser analisado de modo a determinar se existe uma
das condições de vitória descritas na secção anterior.-->

<!--<a name="visualize"></a>

### Visualização-->

<!--
A visualização do jogo deve feita em modo de texto. A [Figura 1](#fig1) mostra
uma possível implementação da visualização do jogo (lado esquerdo), com os
caracteres `R` e `r` indicando peças vermelhas cúbicas e cilíndricas,
respetivamente, e os caracteres `W` e `w` representando peças brancas cúbicas
e cilíndricas, respetivamente.

<a name="fig1"></a>

![visualize](https://user-images.githubusercontent.com/3018963/38045647-463cb488-32b5-11e8-9c98-70c6cc42a16f.png)

**Figura 1** - Possível implementação da visualização em modo de texto (lado
esquerdo) e situação de jogo equivalente (lado direito).-->


### Extensões opcionais

<!--
Os alunos podem opcionalmente desenvolver um modo _single-player_, onde o
jogador adversário é implementado com inteligência artificial. Para o efeito
podem usar o algoritmo [Minimax], com cortes [Alfa-Beta] para acelerar o
cálculo, além de ser uma excelente oportunidade para o uso de recursão.

Esta extensão permite melhorar, até ao máximo de 4 valores, a nota preliminar
do projeto. Atenção que esta extensão não é simples e os conceitos envolvidos
não fazem parte da matéria da disciplina. Só devem abordar este problema quando
o projeto base estiver devidamente concluído. Se abordarem o problema devem
fazê-lo num ramo Git separado, para poderem facilmente voltar à versão base
caso não tenham sucesso na implementação da extensão.
-->

<a name="orgclasses"></a>

### Organização do projeto e estrutura de classes

O projeto deve estar devidamente organizado, fazendo uso de classes, `struct`s
e/ou enumerações, consoante seja mais apropriado. Cada tipo (i.e., classe,
`struct` ou enumeração) deve ser colocado num ficheiro com o mesmo nome. Por
exemplo, uma classe chamada `Game` deve ser colocada no ficheiro `Game.cs`. Por
sua vez, a escolha da coleção ou coleções a usar também deve ser adequada ao
problema.

A estrutura de classes deve ser bem pensada e organizada de uma forma lógica.
Em particular, o projeto deve ser desenvolvido tendo em conta os seguintes
princípios (bem explicados na referência \[[4][ref4]\], que faz parte da
bibliografia da disciplina):

*   [Cada classe deve ter uma responsabilidade específica e bem definida][SRP].
    Em particular, deve haver uma clara separação de responsabilidades
    relativamente à visualização, controlo da aplicação, manipulação de dados e
    manipulação de ficheiros.
*   Programar para interfaces e não para implementações. Por outras palavras, o
    código deve depender o menos possível de outro código. Por exemplo, se
    usarmos uma [`List<T>`][] para guardar informação, e o restante código
    apenas necessitar de iterar sobre a informação lá contida, então esse
    restante código apenas precisa de saber que está a lidar com um
    [`IEnumerable<T>`][]. Desta forma é mais fácil no futuro mudar a coleção
    concreta usada, pois podemos chegar à conclusão que afinal um
    [`HashSet<T>`][] era muito mais eficiente para aquilo que pretendíamos
    fazer. Um princípio que vinca ainda mais esta ideia é o [princípio da
    inversão de dependências][DIP], que afirma que devemos depender apenas de
    abstrações (i.e. interfaces e classes abstratas) e não de classes
    concretas. Duas explicações interessantes sobre esta tema encontram-se
    [aqui](https://stackoverflow.com/questions/383947/what-does-it-mean-to-program-to-an-interface)
    e
    [aqui](https://pt.stackoverflow.com/questions/86484/programar-voltado-para-interface-e-n%C3%A3o-para-a-implementa%C3%A7%C3%A3o-por-qu%C3%AA).

Estes princípios devem ser balanceados com o princípio [KISS][], crucial no
desenvolvimento de qualquer sistema.

<a name="objetivos"></a>

## Objetivos e critério de avaliação

Este projeto tem os seguintes objetivos:

*   **O1** - Programa deve funcionar como especificado.
*   **O2** - Projeto e código bem organizados, nomeadamente:
    *   Estrutura de classes bem pensada (ver secção
        <a href="#orgclasses">Organização do projeto e estrutura de
        classes</a>).
    *   Código devidamente comentado e indentado.
    *   Inexistência de código "morto", que não faz nada, como por exemplo
        variáveis, propriedades ou métodos nunca usados.
    *   Soluções [simples][KISS] e eficientes.
    *   Projeto compila e executa sem erros e/ou *warnings*.
*   **O3** - Projeto adequadamente comentado e documentado. Documentação deve
    ser feita com [comentários de documentação XML][XML], e a documentação
    (gerada em formato HTML ou CHM com [Doxygen][], [Sandcastle][] ou
    ferramenta similar [\[5\]][ref5]) deve estar incluída no ZIP do projeto,
    mas **não** integrada no repositório Git.
*   **O4** - Repositório Git deve refletir boa utilização do mesmo, com
    *commits* de todos os elementos do grupo e mensagens de *commit* que sigam
    as melhores práticas para o efeito (como indicado
    [aqui](https://chris.beams.io/posts/git-commit/),
    [aqui](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53),
    [aqui](https://github.com/erlang/otp/wiki/writing-good-commit-messages) e
    [aqui](https://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)). Quaisquer *assets* binários, tais como imagens, devem ser integrados
    no repositório em modo Git LFS.
*   **O5** - Relatório em formato [Markdown][] (ficheiro `README.md`),
    organizado da seguinte forma:
    *   Título do projeto.
    *   Nome dos autores (primeiro e último) e respetivos números de aluno.
    *   Indicação do repositório público Git utilizado. Esta indicação é
        opcional, pois podem preferir desenvolver o projeto num repositório
        privado.
    *   Informação de quem fez o quê no projeto. Esta informação é
        **obrigatória** e deve refletir os *commits* feitos no Git.
    *   Descrição da solução:
        *   Arquitetura da solução, com breve explicação de como o programa foi
            organizado, indicação das coleções usadas e porquê, bem como
            algoritmos utilizados (e.g., para fazer *parsing* do ficheiro CSV,
            para conjugar as várias perguntas à base de dados, etc).
        *   Um diagrama UML de classes descrevendo a estrutura de classes.
        *   Um fluxograma mostrando o funcionamento do programa.
    *   Conclusões e matéria aprendida.
    *   Referências, incluindo trocas de ideias com colegas, código aberto
        reutilizado (e.g., do StackOverflow) e bibliotecas de terceiros
        utilizadas. Devem ser o mais detalhados possível.
    *   **Nota:** o relatório deve ser simples e breve, com informação mínima e
        suficiente para que seja possível ter uma boa ideia do que foi feito.
        Atenção aos erros ortográficos, pois serão tidos em conta na nota
        final.

O projeto tem um peso de 2 valores na nota final da disciplina e será avaliado
de forma qualitativa. Isto significa que todos os objetivos têm de ser
parcialmente ou totalmente cumpridos. A cada objetivo, O1 a O5, será atribuída
uma nota entre 0 e 1. A nota do projeto será dada pela seguinte fórmula:

*N = 2 x O1 x O2 x O3 x O4 x O5 x D*

Em que *D* corresponde à nota da discussão e percentagem equitativa de
realização do projeto, também entre 0 e 1. Isto significa que se os alunos
ignorarem completamente um dos objetivos, não tenham feito nada no projeto ou
não comparerecem na discussão, a nota final será zero.

## Entrega

O projeto deve ser entregue via Moodle até às 23h de 11 de novembro de 2018.
Deve ser submetido um ficheiro `zip` com os seguintes conteúdos:

*   Solução completa do projeto, contendo adicionalmente e obrigatoriamente:
    *   Pasta escondida `.git` com o repositório Git local do projeto.
    *   Documentação HTML ou CHM gerada com [Doxygen][], [Sandcastle][] ou
        ferramenta similar [\[5\]][ref5].
    *   Ficheiro `README.md` contendo o relatório do projeto em formato
        [Markdown][].
    *   Ficheiros de imagem contendo o fluxograma e o diagrama UML de classes.
        Estes ficheiros podem ser incluídos no repositório em modo Git LFS.

## Honestidade académica

Nesta disciplina, espera-se que cada aluno siga os mais altos padrões de
honestidade académica. Isto significa que cada ideia que não seja do
aluno deve ser claramente indicada, com devida referência ao respectivo
autor. O não cumprimento desta regra constitui plágio.

O plágio inclui a utilização de ideias, código ou conjuntos de soluções
de outros alunos ou indivíduos, ou quaisquer outras fontes para além
dos textos de apoio à disciplina, sem dar o respectivo crédito a essas
fontes. Os alunos são encorajados a discutir os problemas com outros
alunos e devem mencionar essa discussão quando submetem os projetos.
Essa menção **não** influenciará a nota. Os alunos não deverão, no
entanto, copiar códigos, documentação e relatórios de outros alunos, ou dar os
seus próprios códigos, documentação e relatórios a outros em qualquer
circunstância. De facto, não devem sequer deixar códigos, documentação e
relatórios em computadores de uso partilhado.

Nesta disciplina, a desonestidade académica é considerada fraude, com
todas as consequências legais que daí advêm. Qualquer fraude terá como
consequência imediata a anulação dos projetos de todos os alunos envolvidos
(incluindo os que possibilitaram a ocorrência). Qualquer suspeita de
desonestidade académica será relatada aos órgãos superiores da escola
para possível instauração de um processo disciplinar. Este poderá
resultar em reprovação à disciplina, reprovação de ano ou mesmo suspensão
temporária ou definitiva da ULHT.

*Texto adaptado da disciplina de [Algoritmos e
Estruturas de Dados][aed] do [Instituto Superior Técnico][ist]*

## Referências

*   <a name="ref1">\[1\]</a> Whitaker, R. B. (2016). **The C# Player's Guide**
    (3rd Edition). Starbound Software.
*   <a name="ref2">\[2\]</a> Albahari, J. (2017). **C# 7.0 in a Nutshell**.
    O’Reilly Media.
*   <a name="ref3">\[3\]</a> Kelly, C. (2016). **Steam Game Data**. Retrieved
    from <https://data.world/craigkelly/steam-game-data>.
*   <a name="ref4">\[4\]</a> Freeman, E., Robson, E., Bates, B., & Sierra, K.
    (2004). **Head First Design Patterns**. O'Reilly Media.
*   <a name="ref5">\[5\]</a> Dorsey, T. (2017). **Doing Visual Studio and .NET
    Code Documentation Right**. Visual Studio Magazine. Retrieved from
    <https://visualstudiomagazine.com/articles/2017/02/21/vs-dotnet-code-documentation-tools-roundup.aspx>.

## Licenças

Este enunciado é disponibilizados através da licença [CC BY-NC-SA 4.0][].

## Metadados

*   Autor: [Nuno Fachada][]
*   Curso:  [Licenciatura em Videojogos][lamv]
*   Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[ref1]:#ref1
[ref2]:#ref2
[ref3]:#ref3
[ref4]:#ref4
[ref5]:#ref5
[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[lamv]:https://www.ulusofona.pt/licenciatura/videojogos
[Nuno Fachada]:https://github.com/fakenmc
[ULHT]:https://www.ulusofona.pt/
[aed]:https://fenix.tecnico.ulisboa.pt/disciplinas/AED-2/2009-2010/2-semestre/honestidade-academica
[ist]:https://tecnico.ulisboa.pt/pt/
[Markdown]:https://guides.github.com/features/mastering-markdown/
[Doxygen]:https://www.stack.nl/~dimitri/doxygen/
[Sandcastle]:https://github.com/EWSoftware/SHFB
[SRP]:https://en.wikipedia.org/wiki/Single_responsibility_principle
[KISS]:https://en.wikipedia.org/wiki/KISS_principle
[CSV]:https://en.wikipedia.org/wiki/Comma-separated_values
[`DateTime`]:https://docs.microsoft.com/dotnet/api/system.datetime
[`int`]:https://docs.microsoft.com/dotnet/api/system.int32
[`Uri`]:https://docs.microsoft.com/dotnet/api/system.uri
[`bool`]:https://docs.microsoft.com/dotnet/api/system.boolean
[`string`]:https://docs.microsoft.com/dotnet/api/system.string
[`List<T>`]:https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1
[`IEnumerable<T>`]:https://docs.microsoft.com/dotnet/api/system.collections.generic.ienumerable-1
[`HashSet<T>`]:https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1
[DIP]:https://en.wikipedia.org/wiki/Dependency_inversion_principle
[XML]:https://docs.microsoft.com/dotnet/csharp/codedoc
[`WebClient`]:https://docs.microsoft.com/dotnet/api/system.net.webclient
[`Process`]:https://docs.microsoft.com/dotnet/api/system.diagnostics.process
