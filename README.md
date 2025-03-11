public class Producto
{
    public int ProductoId { get; set; }
    public string ProductoNombre { get; set; }
    public decimal ProductoPrecio { get; set; }
    public int ProductoCantidad { get; set; }
    public decimal SubTotal => ProductoPrecio * ProductoCantidad;
}

using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;

public class ProductoController : Controller
{
    private static List<Producto> productos = new List<Producto>();

    public IActionResult Index()
    {
        return View(productos);
    }

    [HttpPost]
    public IActionResult AgregarProducto(Producto producto)
    {
        productos.Add(producto);
        return RedirectToAction("Index");
    }
}

@model List<Producto>

<div class="container mt-5">
    <h2>Ingreso de Productos</h2>
    <form method="post" asp-action="AgregarProducto">
        <div class="row">
            <div class="col-md-3">
                <input type="text" name="ProductoId" class="form-control" placeholder="ID">
            </div>
            <div class="col-md-3">
                <input type="text" name="ProductoNombre" class="form-control" placeholder="Nombre">
            </div>
            <div class="col-md-3">
                <input type="number" name="ProductoPrecio" class="form-control" placeholder="Precio">
            </div>
            <div class="col-md-3">
                <input type="number" name="ProductoCantidad" class="form-control" placeholder="Cantidad">
            </div>
        </div>
        <button type="submit" class="btn btn-primary mt-3">Agregar Producto</button>
    </form>

    <h3 class="mt-5">Lista de Productos</h3>
    <table class="table table-bordered">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Precio</th>
                <th>Cantidad</th>
                <th>SubTotal</th>
            </tr>
        </thead>
        <tbody>
            @foreach (var item in Model)
            {
                <tr>
                    <td>@item.ProductoId</td>
                    <td>@item.ProductoNombre</td>
                    <td>@item.ProductoPrecio</td>
                    <td>@item.ProductoCantidad</td>
                    <td>@item.SubTotal</td>
                </tr>
            }
        </tbody>
    </table>
</div>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/js/all.min.js"></script>

"ConnectionStrings": {
    "DefaultConnection": "Server=TU_SERVIDOR;Database=TuBaseDeDatos;Trusted_Connection=True;"
}

