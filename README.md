<span href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=30&duration=1000&pause=1000&color=A5B4FC&vCenter=true&repeat=false&random=false&width=436&height=32&lines=Full-Stack+Developer" alt="Typing SVG" /></span>
<h2 style="margin-top: 0;">About me</h2>
<p>I'm Fullstack developer from  Peru, with a degree in <b>computer science</b>, very passionate about new technologies and learning them. I like challenges, <b>solving problems</b>, especially if it has to do with the client. That's why the <b>frontend</b> attracts my attention.<br/> I make sure my projects have a balance between <b>UI/UX</b> and performace, as well as following good coding practices. I am currently focusing on learning more about design patterns and software architecture.</p>
<h2>Skills</h2>
<h3>Things I code with</h3>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/JavaScript-0f172a?logo=javascript"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/TypeScript-0f172a?logo=typescript"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Python-0f172a?logo=python"></span>
<span href="#"><img alt="Java" src="https://custom-icon-badges.demolab.com/badge/Java-0f172a?logo=java&logoColor=white"></span>
<h3>Frontend Technologies</h3>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/HTML-0f172a?logo=html5"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/CSS-0f172a?logo=css3"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/React-0f172a?logo=react"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/React_Query-0f172a?logo=reactquery"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Zustand-0f172a"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Tailwind_CSS-0f172a?logo=tailwindcss"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Radix_UI-0f172a?logo=radixui"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Next_JS-0f172a?logo=nextdotjs"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Angular-0f172a?logo=angular"></span>
<h3>Backend Technologies</h3>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Node_JS-0f172a?logo=nodedotjs"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Express-0f172a?logo=express"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/MongoDB-0f172a?logo=mongodb"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Postgresql-0f172a?logo=postgresql"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Mysql-0f172a?logo=mysql"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/SQL_Server-0f172a?logo=microsoftsqlserver"></span>
<h3>Others</h3>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Git-0f172a?logo=git"></span>
<span href="#"><img alt="Static Badge" src="https://img.shields.io/badge/Postman-0f172a?logo=postman"></span>



<h3>Controller</h3>
<code>
using crud.Models;
using crud.Servicios;
using Microsoft.AspNetCore.Mvc;

namespace crud.Controllers
{
    public class VendedorController: Controller
    {
        private readonly IRepositorioVendedor repositorioVendedor;
        public VendedorController(IRepositorioVendedor repositorioVendedor) { 
            this.repositorioVendedor = repositorioVendedor;
        }

        public async Task<IActionResult> Index()
        {
            var vendedor = await repositorioVendedor.Obtener();
            return View(vendedor);

        }

        public IActionResult Crear()
        {
            return View();
        }


        [HttpPost]
        public async Task<IActionResult> Crear(Vendedor vendedor)
        {
            if (!ModelState.IsValid)
            {
                return View(vendedor);
            }

            vendedor.Id_Tipovendedor = 2;

            await repositorioVendedor.Crear(vendedor);

            return RedirectToAction("Index");
        
        }

        [HttpPost]
        public async Task<IActionResult> Editar(Vendedor vendedor)
        {

            var vendedorExiste = await repositorioVendedor.ObtenerId(vendedor.Id_Vendedor);

            await repositorioVendedor.Actualizar(vendedor);

            return RedirectToAction("Index");

        }

        [HttpGet]
        public async Task<IActionResult> Editar(int id)
        {
            var vendedor = await repositorioVendedor.ObtenerId(id);

            return View(vendedor);
        }


        public async Task<IActionResult> Borrar(int id)
        {
            var vendedor = await repositorioVendedor.ObtenerId(id);
            return View(vendedor);

        }

        [HttpPost]
        public async Task<IActionResult> BorrarVendedor(Vendedor vendedor)
        {

            await repositorioVendedor.Borrar(vendedor.Id_Vendedor);

            return RedirectToAction("Index");

        }


    }
}
</code>

<h3>Vista crear </h3>
<code>
@model Vendedor

@{
    ViewData["title"] = "Crear vendedor";

}

<h1 class="text-primary">Formulario crear un nuevo vendedor</h1>

<div asp-validation-summary="All" class="text-danger"></div>

<form asp-controller="Vendedor" asp-action="Crear">

    <div class="mb-3">
        <label asp-for="Nombre" class="form-label">Nombre</label>
        <input type="text" asp-for="Nombre" class="form-control"/>

        <label asp-for="Apellido" class="form-label">Apellido</label>
        <input type="text" asp-for="Apellido" class="form-control" />

        <label asp-for="Email" class="form-label">Email</label>
        <input type="text" asp-for="Email" class="form-control" />

        <label asp-for="Edad" class="form-label">Edad</label>
        <input type="number" asp-for="Edad" class="form-control" />

    </div>
    <button type="submit" class="btn btn-primary">
        Crear vendedor
    </button>
    <button class="btn btn-outline-secondary" asp-action="Index">Cancelar</button>
</form>
</code>

<h3>Servicio RepositorioVendedor</h3>

<code>
using crud.Models;
using Dapper;
using Microsoft.Data.SqlClient;
using System.Data;

namespace crud.Servicios
{

    public interface IRepositorioVendedor
    {
        Task Actualizar(Vendedor vendedor);
        Task Borrar(int id);
        Task Crear(Vendedor vendedor);
        Task<IEnumerable<Vendedor>> Obtener();
        Task<Vendedor> ObtenerId(int id);
    }
    public class RepositorioVendedor: IRepositorioVendedor
    {

        private readonly string connectionString;

        public RepositorioVendedor(IConfiguration configuration)
        {
            connectionString = configuration.GetConnectionString("DefaultConnection");
        }

        public async Task Crear(Vendedor vendedor)
        {
            using var connection = new SqlConnection(connectionString);

            // Par谩metro de salida para capturar el Id_Vendedor
            var parameters = new DynamicParameters();
            parameters.Add("@Nombre", vendedor.Nombre);
            parameters.Add("@Apellido", vendedor.Apellido);
            parameters.Add("@Email", vendedor.Email);
            parameters.Add("@Edad", vendedor.Edad);
            parameters.Add("@Id_Tipovendedor", vendedor.Id_Tipovendedor);
            parameters.Add("@Id_Vendedor", dbType: DbType.Int32, direction: ParameterDirection.Output);

            // Llamada al procedimiento almacenado
            await connection.ExecuteAsync("spCrearVendedor", parameters, commandType: CommandType.StoredProcedure);

            // Obtener el valor del par谩metro de salida
            vendedor.Id_Vendedor = parameters.Get<int>("@Id_Vendedor");
        }


        public async Task<IEnumerable<Vendedor>> Obtener()
        {
            using var connection = new SqlConnection(connectionString);
            return await connection.QueryAsync<Vendedor>("SELECT * FROM vendedor");
        }

        public async Task Actualizar(Vendedor vendedor)
        {
            using var connection = new SqlConnection(connectionString);

            var parameters = new DynamicParameters();
            parameters.Add("@Id_Vendedor", vendedor.Id_Vendedor);
            parameters.Add("@Nombre", vendedor.Nombre);
            parameters.Add("@Apellido", vendedor.Apellido);
            parameters.Add("@Email", vendedor.Email);
            parameters.Add("@Edad", vendedor.Edad);

            await connection.ExecuteAsync("spActualizarVendedor", parameters, commandType: CommandType.StoredProcedure);
        }

        public async Task<Vendedor> ObtenerId(int id)
        {
            using var connection = new SqlConnection(connectionString);

            var parameters = new DynamicParameters();
            parameters.Add("@Id_Vendedor", id);

            return await connection.QueryFirstOrDefaultAsync<Vendedor>(
                "spObtenerVendedorPorId",
                parameters,
                commandType: CommandType.StoredProcedure
            );
        }


        public async Task Borrar(int id)
        {
            using var connection = new SqlConnection(connectionString);

            await connection.ExecuteAsync(@"DELETE vendedor WHERE Id_Vendedor = @id",new { id });
        }


    }

    
}
</code>






