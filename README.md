# cursoMVC-DotNetCore
Básico da criação de um MVC Web .NetCore
# Criação Projeto MVC .Net Core Web Aplication

 1. Primeiro passo, criar o projeto: ASP.NET Core Web Application
 2. Criar uma classe no models chamada: Categoria
 3. Incluir como propriedades
		public int Id { get; set; }

Iremos seguir o code first (criaremos o código depois o banco de dados)
Todas as nossas classes terá um id inteiro, que será a chave primária das nossas tebelas

 4. Vamos instalar alguns pacotes seguindo os passos:
Tools -> Nuget Package Manager -> Package Manager Console
serão dois pacotes:
Entity Framework do sql server
Comando:
Install-Package Microsoft.EntityFrameworkCore.SqlServer

Ferramentas dos Entity Framework para podermos utilizar o Migration
Install-Package Microsoft.EntityFramework.Tools

 5. Criar uma nova classe na model chamada Context, essa Classe herda de uma interface do entity framework, chamada DbContext

colocar using 
using Microsoft.EntityFrameworkCore;

como herdamos, dentro da interface DbContext existe um método que iremos sobrescrever (override)
 OnConfiguring()
 ele é responsável por configurar nosso Entity Framework
 É dentro dele que vou falar qual banco de dados vou, utilizar
 E como instalei sqlServer, ele irá trazer o sqlServer e pede para colocarmos nossa string de conexão
 
 6. Preciso falar para o meu entity que eu vou ter uma classe categoria
 public DbSet<Categoria> categorias { get; set; }
 dentro do context
 
 7. no startup precisamos deixar a conexão com banco de dados visível utilizando
 services.AddDbContext<Context>();
 dentro do método ConfigureServices
 
 8. Agora vamos voltar pro Nuget rodar o Migration para criar a tabela no banco de dados o comando é:
 Add-Migration InitialCreate
 esse comando é porque temos o tools ele criará uma pasta Migrations
 
 9. Agora vamos digitar o 
 Update-Database
Ele é responsável por criar nosso banco de dados
 
 10. O Entity Framework tem um recurso que chama Scaffouded
 botão direito em Controllers --> Add --> new Scaffouded Item
Selecionar:
 MVC Controller with views, using Entity Framework
 Ele nos pede para selecionarmos duas opções:
No exemplo a classe de modelo será a Categoria
e a classe de contexto é a context

 11. Mandar compilar --> Build / Build Solution

 12. Vamos adicionar a Categoria no meu em
Views -> Shared -> _layout.cshtml

copia um nav item <li class="nav-link....
deixaremos dessa forma:
<li class="nav-item">
                            <a class="nav-link text-dark" asp-area="" asp-controller="Categorias" asp-action="Index">Categorias</a>
                        </li>

13. Apenas para conhecimento, ele apenas salva no banco após o await _context.SaveChangesAsync(); , ou seja é possível utilizar os dados antes disso.


14. Agora vamos criar a segunda model --> Produto
com essas propriedades
 public int Id { get; set; }

        public string Descricao { get; set; }

        public int Quantidade { get; set; }

        public int CategoriaId { get; set; }

        public Categoria Categoria { get; set; }
		
	15. e dentro da Classe Categoria, eu vou criar uma lista de produtos	
    16. depois vou no context e crio um DbSet e produtos
    17. depois dá o comando de migrate e update 

18. Agora vamos repetir o processo no Controller e criar um scafoud do produto
19. criar o link no layout - para o produto

20. Para exibir o nome da descrição e não o id da categoria, no produto,
basta ir no ProdutosController no Create na view, basta substituir id por descricao, sustituir em todos view data, no caso são 3

 21. dentro da view de produto é possível substituir a exibição do id para descrição

  22. Para exibir de forma amigável ou seja Descrição --> vamos na classe colocar um datanotation

23. using System.ComponentModel.DataAnnotations;
[Display(Name = "Descrição")]
24. Colocar o requerido
[Required(ErrorMessage ="O Campo descrição é obrigatório")]
25. valor mínimo e máximo utilizar o range
[Range(1,10,ErrorMessage ="Valor fora da faixa")]	
